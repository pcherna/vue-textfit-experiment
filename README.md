# vue-textfit-experiment

This is a Vue 3 project that is an experiment to build a \<TextFit\> component using <https://github.com/STRML/textFit>

## The Problem

The basic problem is that if the \<TextFit\> component is placed inside an element that uses `v-show`, it doesn't work. I basically understand the cause of the problem, that the elements are mounted into a div with `display:none` so the required geometry information is not available at `mounted()` time. I just wish I could figure out how to catch the "right" time to evaluate the text-fitting.

Read on for fuller details.

## Setup

Nothing fancy here:

```bash
npm install
```

*Note that I am including a lightly modified version of textFit, to facilitate experiments.*

## Run the Example

```bash
npm run serve
```

## What You See

There are a total of five samples of using my \<TextFit\> component, each of which is trying to fit some sample text into a 1024x200 box. The first two samples are displayed immediately, and essentially work fine:

* Sample 1: This fits the text in single-line mode, and works fine.
* Sample 2: This fits the text in multi-line mode, and works fine.

The remaining three samples use delayed rendering, by being inside of

```html
<div v-show="ready">
...
</div>
```

Where `ready` is triggered one second after App's `mounted()`.

*In a realistic example the delay could because some content is designed to come into view later, or perhaps we're waiting for some assets or data to load.*

In the deferred case, the component's `mounted()` is called when the elements are added to the DOM (which is the correct time according to Vue). But because the containing div is still `display:none` then it lacks the geometry needed to solve the text fit. I understand that part.

* Sample 3: This example is in the delayed div, and it just fails
* Sample 4: This example puts an explicit `v-show` ***also on the \<TextFit\> component***, which causes the component's `updated` hook to fire at a suitable time, which is great, but structurally it's very painful to repeat `v-show` deeply nested inside the div it belongs on.
* Sample 5: In this experiment I'm trying to supply the explicit width/height to `textfit`, but whatever is still missing from the geometry leads `textfit` to decide that the width and height needed for the text remains zero, so it ends up choosing the `maxFontSize`.
