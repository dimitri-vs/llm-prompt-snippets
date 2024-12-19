<!-- Original FlashPaste name: Writing Better Userscripts / Chrome Ext. -->
<!-- FlashPaste ID: 122 -->

SOURCE: https://news.ycombinator.com/item?id=40215507

> The main issue I've run into is that I have no idea how to hook into and modify the behavior of fancy modern web sites with all of their React and Angular and Snorfleflox. I was kind of hoping this was for that. Is there some sort of framework that makes that stuff easier, or failing that, a really good tutorial for an experienced but a little out of date web developer to get up to speed?

I've written extensions (L I N K S I N B I O) which significantly modify Twitter.com (which uses React Native for Web) and YouTube (which uses web components), which are both SPAs - the main tips I'd give are:

1. Which page am I on?

In an MPA extension or userscript, you just check the current URL and go. In an SPA, you could go as far as patching the pushState() method on History (although you can't do this from an extension's content script - you would need to inject a page script) and watching for popstate events to detect URL changes, but I've found using a MutationObserver [1] to observe the contents of <title> to be a simpler proxy for the current page changing.

When the <title> changes, check the current URL to see if it's one you've already handled, and if not, start making your modifications. This also gives you a natural place to put any teardown logic, such as disconnecting active observers and cancelling any async actions which may be in progress for the previous page, such as waiting for elements to appear.

The target app may even have custom events you can hook into. YouTube has these, for example, but I found they were being fired at the same time the <title> was being changed whenever the user was navigating to a different page, so I stuck with the implementation-independent approach.

2. When are the main elements I care about available?

You'll need some utility functions which allow you to wait for specific elements to be available in the current page, either as an indicator the page is ready to modify, or because you need to do something with their contents.

This could be as un-smart as writing a function which returns a Promise wrapping document.querySelector() calls at regular intervals, or uses a MutationObserver to wait for a specific element to appear, then resolves with it, but there should be lots of existing open source utilities like these available out there (some have already been linked to in this thread).

I ended up writing my own version of these so I could specifically control stopping waiting for an element based on a timeout and/or other conditions, e.g. immediately resolving the Promise with `null` if the current URL has changed at the next available interval.

3. When do the elements I care about change?

Use the MutationObserver API [1] to watch for child elements being added/removed, or for specific attributes being changed.

It's kind of clunky, so you may want to write your own convenience wrapper - this is also a natural place to facilitate storing active observers for a later teardown. I've found I usually end up with at least a pageObservers collection, which makes it easy to disconnect everything which is currently being observed when the page changes.

e.g. I use a MutationObserver on the element which contains Twitter timeline contents to watch for the current window of visible tweets being changed so I can do things like hide quotes of specific tweets or hide Retweets from the Following timeline.

4. Hiding things in an SPA-friendly way

Removing elements which UI libraries such as React expect to be under their control when some state changes at a later time can lead to errors, so I've found it best to use CSS where possible to hide things, and even adding your own class names to use as styling hooks. It can also just be more convenient than writing code to manually remove things from the DOM.

e.g. Twitter uses React Native for Web's styling system, which takes CSS-like style objects and generates utility-like style rules from them (it's like Tailwind in reverse) - this means there aren't any developer-friendly class names to use as styling hooks, so on some pages I add my own. If I open my own user profile, <body> will have 'Profile' and 'OwnProfile' classes on it, which I can use to hide the "Articles" and "Highlights" tabs, which are there purely as Premium upsells.

[1] https://developer.mozilla.org/en-US/docs/Web/API/MutationObs...

---

I haven't done a lot of userscript dev, but based on my experience so far, all of this advice is spot-on.
I found it useful to create a `waitForElement(query)` helper function that takes a CSS selector path and returns a Promise that resolves when the query starts finding a match in the DOM. (Internally, it's just populating a table that is iterated over in the MutationObserver callback.)

As for SPA "navigation", I had trouble with popstate events. I hadn't considered your <title> trick; I'll bet that would have worked for me! Right now, I'm polling window.location.href every half second, which sucks.