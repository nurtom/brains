---
title: "Everything about Google Translate crashing React (and other web apps) by Martijn Hols"
source: "https://martijnhols.nl/blog/everything-about-google-translate-crashing-react"
author:
  - "[[Martijn Hols]]"
published: 2024-05-29
created: 2025-02-14
description: "A deep dive into Google Translate (and other browser extensions) interference breaking React and other web apps."
tags:
  - "clippings"
---
Google Translate, the built-in extension of Google Chrome, is a *machine translator* that provides users with an easy way of translating webpages from within their browser tab. This allows webpages to be used by users from all over the world, regardless of their native language.

![](https://martijnhols.nl/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fgoogle-translate-react-clashing.fedd8c6b.png&w=640&q=75)

But this convenience comes at a cost, as it interferes with the workings of many modern sites. This is because **Google Translate manipulates the DOM in such a way that it breaks the base apps.** This interference often manifest as crashes caused by the DOM element's native `removeChild` method, resulting in errors like `NotFoundError: Failed to execute 'removeChild' on 'Node': The node to be removed is not a child of this node.`, but it affects a lot more. **Not all issues are as obvious as a crash.**

The focus of this article will be on Google Translate's interference of React, but it's important to note that these issues are not unique to React; they affect most machine translators and can disrupt any large and complex web app.

In this article, we will explore:

- How Google Translate works
- Google Translate's interference
- The interference of browser extensions in general
- The impact on regular JavaScript code
- Possible workarounds and alternatives

Additionally, at the end of the article you will find an [addendum](https://martijnhols.nl/blog/everything-about-google-translate-crashing-react#addendum) in which I share my views on whether web apps should even claim full and exclusive control of the DOM.

But first, let's take a look at how Google Translate works.

## How Google Translate works

To understand what Google Translate does, we need to take a close look at the DOM structure before and after translation.

All HTML that is rendered in the browser is represented by the DOM in JavaScript. This is a tree-like structure where each element is a node. HTML elements are represented by `Element`\-nodes and text is represented by a `TextNode`.

Let's take a simple piece of HTML:

```prism
<p>There are 4 lights!</p>
```

In JavaScript, this is represented in the DOM by a structure like this:

Mounted DOM (English)

Hover or tap the TextNode to see its contents.

When Google Translate activates, it looks for `TextNode`s to translate. These nodes are then replaced with `FontElement` elements with the new, translated, strings inside. This results in the following HTML (assuming we're translating to Dutch):

```prism
<p><font>Er zijn 4 lampen!</font></p>
```

More importantly, the DOM structure becomes this:

Mounted DOM (now translated)

Unmounted (the original English node)

Hover or tap the TextNode to see its contents.

What this shows is that **the original `TextNode` is unmounted and replaced with a new `FontElement`** with the translated text inside.

This is the gist of how Google Translate impacts the DOM and an important piece of why Google Translate causes problems (i.e. interferes) with JavaScript apps doing DOM manipulation.

### Simulating Google Translate

Now that we know how Google Translate works, we can simulate it being applied to a part of a page. This will allow us to reproduce the issues caused by Google Translate more easily.

The snippet below will search for an element with the id "translateme" and replace all direct `TextNode` children with `FontElement`s similar to how Google Translate operates. To make it more obvious which text has the Google Translate simulation applied, any text affected is surrounded with square brackets (“There are 4 lights!” becomes “\[There are 4 lights!\]”).

```prism
useEffect(() => {
  document.getElementById('translateme').childNodes.forEach((child) => {
    if (child.nodeType === Node.TEXT_NODE) {
      const fontElem = document.createElement('font')
      fontElem.textContent = \`[${child.textContent}]\`
      child.parentElement.insertBefore(fontElem, child)
      child.parentElement.removeChild(child)
    }
  })
})
```

The reproduction examples below all use this method to simulate Google Translate.

### Manually testing Google Translate

If you want to validate the issues caused by Google Translate yourself, you can do so by manually testing it. This will help you understand the impact of Google Translate on your app.

The easiest way I found to test Google Translate, is to translate English to some other language. To get Google Chrome to do this, you will need to change your *Preferred languages* in the settings like so:

![An animated GIF showing Chrome "Preferred language" settings. The Dutch language is added, and all other languages are removed afterwards.](https://martijnhols.nl/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fgoogle-translate-language-setup.746e5db3.gif&w=3840&q=75)

[Replace all preferred languages in the settings](https://martijnhols.nl/_next/static/media/google-translate-language-setup.746e5db3.gif)

Next, go to the webpage you want to test. If the webpage is set up correctly (and it's in English), it should have `lang="en"` in its `html` tag. This allows Google Translate to reliably detect its language and translate it. If it doesn't suggest it by itself, click the translation icon in the address bar.

![An animated GIF showing how Google Translate activation in Chrome.](https://martijnhols.nl/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fgoogle-translate-activate.09bbe59f.gif&w=3840&q=75)

[Google Translate will immediately translate the page](https://martijnhols.nl/_next/static/media/google-translate-activate.09bbe59f.gif)

## The interference issues

Now that we know how Google Translate manipulates the DOM, we can explore the interference issues it causes. The most common issues are:

### Issue: Translated text not updating

When Google Translate unmounts DOM nodes and places its own new ones in their place, the original DOM nodes will continue to exist in-memory. Any changes then made to the original DOM nodes will not show up in the user's browser in any way. The changes will remain in-memory.

This is an issue for systems like React that work with a Virtual DOM. One of the main reasons behind using the Virtual DOM is performance, and a key part of that is, whenever possible, updating the values of DOM nodes instead of replacing them. Replacing DOM nodes is more computationally expensive.

The consequence of this is that, in React, any text or number that might change alongside another string is affected. **When Google Translate is applied, values shown on your page may never update again.**

This is a big problem for any app that shows users important data, which probably means every big React app. Showing the wrong data could be misleading and even dangerous. A dashboard showing the wrong number could lead to users making the wrong decisions, your app showing invalid prices could be a legal issue, while showing a user the wrong dosage of medicine could have much more dire consequences. How big of a risk this is, depends on your app and your business.

This issue is hard to discover since it doesn't lead to a crash or any error.

#### Reproduction

In the below reproduction, we have a simple counter tracking the number of lights (a number in a `useState`). The button increments the number of lights by one every time it's pressed. The marked label directly next to it is no more than `There are {lights} lights!` - no conditions or anything.

We simulate Google Translate using the method [described above](https://martijnhols.nl/blog/everything-about-google-translate-crashing-react#simulating-google-translate). The Google Translate simulation adds square brackets around the text to indicate it's active. The value shown in green underneath the button is the actual value, which is unaffected by Google Translate.

Reproduction

Simulate Google Translate

\[There are \]

\[4\]

\[ lights!\]

When you click the button a few times, you will see the state is updating and the component is rerendering, but the translated text is never updated to reflect the new value.

![An animated GIF of Jean-Luc Picard (Star Trek) yelling "There are four lights!".](https://martijnhols.nl/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fgoogle-translate-lights-meme.bc1b3c90.gif&w=3840&q=75)

[There are 4 lights!](https://martijnhols.nl/_next/static/media/google-translate-lights-meme.bc1b3c90.gif)

Aside

The reproduction shows three sets of brackets around the text. This is because React makes a separate `TextNode` for each variable in a string. The real Google Translate would [normalize](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize) the text nodes, merging them together, but our simulation doesn't do this to keep it simpler. This makes the reproduction slightly different from Google Translate, but the result is the same.

### Issue: Crashes

If you're running an error monitoring tool like Sentry or tried manually testing Google Translate, you've probably seen these before. In React, the following errors are common due to interference from Google Translate:

- `NotFoundError: Failed to execute 'removeChild' on 'Node': The node to be removed is not a child of this node.`
- `Failed to execute 'insertBefore' on 'Node': The node before which the new node is to be inserted is not a child of this node.`

When one of those errors occurs, React will unmount your tree to the closest error boundary. But if you have no error boundary (which is common on websites), **your entire app will crash**.

The `removeChild` error usually happens because your app was trying to remove a conditionally rendered `TextNode` from the DOM that Google Translate unmounted. The `insertBefore` error is less common; this usually occurs because something conditionally rendered is trying to appear *before* a `TextNode` that was unmounted by Google Translate.

I think in many cases these crashes might be less important than the [translated text not updating](https://martijnhols.nl/blog/everything-about-google-translate-crashing-react#issue-translated-text-not-updating). Text not updating is less predictable than not showing anything at all. It may mislead users, which would be a worse outcome than not showing anything at all.

#### Reproduction

The button below toggles whether the lights are on by simply flipping a boolean in a `useState`. When the lights are turned off, the “There are 4 lights!” text will no longer be rendered through the conditional expression `{lightsOn && 'There are 4 lights!'}`. React tries to reconsolidate this render by removing the `TextNode` from the parent that it added it to. When it does this with Google Translate active, the `TextNode` is no longer a child of the parent, which results in a crash.

Reproduction

Simulate Google Translate

\[There are 4 lights!\]

To reproduce it, the conditional `TextNode` needs to have a sibling of any kind. In React nearly every node that's conditionally rendered will have a sibling, so this is a common situation.

Another way of reproducing this crash is by rendering a different amount of `TextNode`s within a ternary. The reproduction below also toggles the lights, but instead of rendering nothing when the lights are off, it tries to render the text "The lights are off" through a ternary: `{lightsOn ? <>There are {lights} lights!</> : <>The lights are off</>}`.

Reproduction

Simulate Google Translate

\[There are \]

\[4\]

\[ lights!\]

The important part of this reproduction is that the sides of the ternary have a different amount of `TextNode`s. While it might not be obvious, this is the case here, as React produces three `TextNode`s for the `<>There are {lights} lights!</>` expression.

This reproduction is a simplified version of what you might have in your app. In the example code, we could have used a single template string for both sides of the ternary. In the real world, these expressions tend to be more complex, making it hard to turn it into a template string.

As there are more ways to vary the amount of `TextNode`s rendered, I'm sure there are more ways of reproducing this crash. This makes it hard to find a workaround that solves all cases.

#### Workarounds

React's crashes have been reported in [this issue](https://github.com/facebook/react/issues/11538) on GitHub. Several workarounds have been posted, but unfortunately, none of the workarounds provide a quick fix. Some just make things worse.

The below workarounds only focus on the crashes and have absolutely no impact on translated text not updating.

##### 1\. Monkey patching removeChild and insertBefore

*Gaearon*, a member of the React Core team, posted [a workaround](https://github.com/facebook/react/issues/11538#issuecomment-417504600) that monkey patches `removeChild` and `insertBefore` to fail silently when they're called with invalid arguments.

While this monkey patch succeeds at preventing the crashes, it doesn't solve the underlying issue at all. Instead of React crashing when it tries to remove a `TextNode` through `removeChild`, it does nothing and **the translated text will remain in the DOM** until its parent is removed. And when the `insertBefore` error is triggered, the **newly rendered text won't appear** for your user.

Unless the user is aware of the behavior, both issues make an app almost as unusable as when it would crash.

Watch this monkey patch in action:

Reproduction

Simulate Google Translate

\[There are 4 lights!\]

You can toggle the Google Translate simulation to see how the component behaves with and without its interference. It also serves as a great way of resetting the component to its initial state.

##### 2\. Surrounding TextNodes with spans

GitHub user *Shuhei* proposed [a workaround](https://github.com/facebook/react/issues/11538#issuecomment-390386520) of surrounding all conditionally rendered and adjacent text in `span` elements. This avoids the crashes by ensuring React doesn't try to remove or insert a `TextNode` directly.

**This fixes some of the most common crashes, but not all of them.** The crashes caused by conditionally rendered `TextNode`s like the `{lightsOn && 'There are 4 lights!'}` expression in the first reproduction above, can be fixed by this workaround. But crashes caused by other conditionally rendered `TextNode`s, like those in the ternary expression reproduction, are not.

Implementing this workaround does require mangling a lot of existing, regular, code. Without an ESLint rule to enforce this, it is going take a lot of pleading in PRs to get your entire team to consistently apply this workaround. And for many the honest truth is that it's not worth the effort and code quality sacrifice for them.

Aside

The ESLint plugin [eslint-plugin-sayari](https://github.com/sayari-analytics/eslint-plugin-sayari) has a rule that *requires `TextNode`s that share a common parent with other elements to be wrapped in a `<span>` tag*. While this probably catches the problematic expressions, this rule has an extremely high false-positive rate and will require you to wrap nearly all `TextNode`s in your app. The ternary crashes are also not solved by this rule.

##### 3\. Self re-rendering error boundaries

An error boundary that just renders the same children again when it runs into an error is [a good idea by GitHub user Sorahn](https://github.com/facebook/react/issues/11538#issuecomment-2052692225), but unfortunately, any components in the subtree will lose their state in the process. While this could work for some of the instances, it's not a general solution and if you're going to be adapting your code anyway, you're probably better off surrounding your `TextNode`s with spans.

### Issue: Inconsistent `event.target`

When Google Translate is active, the value of `event.target` becomes unpredictable, as users are likely to click on one of Google Translate's `font` elements instead of the underlying element that you, as the developer, created and could reasonably expect. In some instances, such as inside overlays, this could lead to click events not working correctly.

While this issue is very specific and can be worked around with relative ease, very few developers will even be aware of the issue or think to test it.

#### Reproduction

In the reproduction below, the text of the button gets translated by the Google Translate simulator. When you click anywhere within the reproduction, the element type of the `event.target` (the element you clicked on) will appear in the text underneath the button. Normally when you click the button, `event.target` would refer to the `button`, but with Google Translate, it will be a `font` element instead.

Click the button. Toggle Google Translate simulation. Click again. Compare results.

Reproduction

Simulate Google Translate

## Not just React

**Google Translate's interference affects not just React apps.**

Any JavaScript code that manipulates the DOM in a similar fasion is affected. This includes operations such as updating a value of a `TextNode`, adding or removing children, or using `event.target`. These operations are not specific to React.

However, these issues are more commonly observed in React applications since React is a prominent user of the “[Virtual DOM](https://reactjs.org/docs/faq-internals.html)”. The Virtual DOM keeps references to all DOM nodes so it only has to update parts of the DOM that are actually changed (through a process called [reconciliation](https://reactjs.org/docs/reconciliation.html)). This allows for high-performance apps, as it's more efficient than replacing DOM nodes. Because of this, React's use of a Virtual DOM to reuse and update nodes rather than constantly replacing them is a natural evolution for frameworks.

## Not just Google Translate

Most machine translators work pretty much the same way as Google Translate, so the issue is not just limited to it. But the issue is even bigger than that: **any browser extensions that manipulate the DOM can interfere**. Some other examples are:

- Password managers manipulating forms to show prefill dropdowns
- Extensions that inject alternative prices on competing webshops (\*)
- An adblocker removing an element
- [AutocardAnywhere](https://chromewebstore.google.com/detail/eobkhgkgoejnjaiofdmphhkemmomfabg): Displays card image popups for collectible card games (\*)

![A screenshot of WoWAnalyzer, showing a Magic: the Gathering card popup added by AutocardAnywhere for a random, but matching piece of text.](https://martijnhols.nl/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fgoogle-translate-autocardanywhere.fe3d11d2.png&w=3840&q=75)

[AutocardAnywhere showing a Magic: the Gathering card for a random piece of text on WoWAnalyzer](https://martijnhols.nl/_next/static/media/google-translate-autocardanywhere.fe3d11d2.png)

I want to stress that I do not think the team behind Google Translate deserves any blame for the issues. It's a great tool that helps people worldwide and makes the web usable for many more people. Google Translate was originally architected at a time when the web was very different from what it is today. The issues are a result of the web evolving; websites aren't almost exclusively static websites anymore as many of the popular websites today are actually large and complex web apps.

Fixing the issues is also not trivial. For many translations, Google Translate needs to be able to restructure sentences to make them work in the target language. That's nearly impossible to do without interfering with the DOM.

## There is no real solution (yet)

At the time of writing, there is, unfortunately, no solution yet that can make Google Translate work well enough with React for a large React app. As mentioned above, the workarounds for the crashes introduce a new set of issues, and they still leave any complex app barely usable after translation by Google Translate.

There are a couple of things you *can* do, but I don't think you're gonna like them.

### The regrettable “fix”

When I first ran into this issue back in 2017, I posted in the React issue tracker that I had [”fixed” my app by blocking translation entirely](https://github.com/facebook/react/issues/11538#issuecomment-350110297). Now, 7 years later, I am sad to have to report that this still appears to be the only quick way of avoiding all of the issues caused by Google Translate.

I don't like solving it this way. It makes apps less accessible to people worldwide. But for some complex apps, it beats serving Google Translate users a broken app that barely works.

If you're willing to put in the time and effort, [wrapping](https://martijnhols.nl/blog/everything-about-google-translate-crashing-react#surrounding-textnodes-with-spans) conditional `TextNode`s in `span`s will solve a large chunk of the crashes (but not the other issues). This will usually be good enough for a simple website like this as a typical website isn't very reactive, has a small codebase, has few developers working on it, and doesn't show any computed numbers that are critical.

You will have to carefully consider which of these solutions is the right fit for your app. Leaving Google Translate available will be a big help for some of your users, but it will take some debugging to get it to work well enough and ensure you're not showing users incorrect data.

### Alternatives

The only alternative solution that I can think of, is to **implement your own localization within your app** (i.e. internationalization). This makes machine translation unnecessary and provides international users with the best possible experience. But this has a couple of downsides:

- It takes a lot of effort to do at all
- It's hard to get right
- It slows down development
- Good translators are expensive
- It's infeasible to cover as many languages as Google Translate covers

All things considered, this isn't the most practical solution for most apps. Do you know of any other alternatives?

Aside

There might be a possible (external) workaround in React that uses a similar mechanic to React Dev Tools's “render highlighting” to trigger remounting (by React) of the entire parent of `TextNode`s that are changed. However, I looked into the feature's code and that is part of a >4500 LOC file so it seemed more involved than I bargained for. Maybe someone else can take a look at it.

## Conclusion

That's everything about Google Translate crashing React apps (and other web apps). Or, as we've discovered, everything about third-party browser extension DOM manipulation interfering with complex JavaScript app reactivity, often leading to crashes and other issues.

I hope this article will help you understand the issues and help you choose the right way to deal with them in your app.

Please help bring attention to this issue by upvoting its bug report on the Chromium project: [https://issues.chromium.org/issues/41407169](https://issues.chromium.org/issues/41407169). The increased attention can help the chances of the issues being addressed.

So what do you think? Can you think of any other workarounds? Or do you know a machine translator that doesn't have these issues? Please share your insights through the links below.

ps. In the [addendum](https://martijnhols.nl/blog/everything-about-google-translate-crashing-react#addendum) below, I discuss whether it is reasonable for an app to claim full and exclusive control of the DOM, as React does with its Virtual DOM.