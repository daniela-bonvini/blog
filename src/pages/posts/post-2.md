---
layout: ../../layouts/MarkdownPostLayout.astro
title: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer - Part two"
pubDate: 09/09/2023
description: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer"
image: "/blog.png"
author: "Daniela"
tags: ["angular", "intersection observer", "sticky menu", "highlight"]
---

To achieve this scrolling functionality, we're primarily working with Angular's built-in event binding and a bit of DOM manipulation. Here's how it works:

In our HTML template, we have a menu constructed using an unordered list (<ul>) and Angular's \*ngFor directive to dynamically generate menu items based on an array of labels (labels in our TypeScript component). Each menu item is a clickable <span> element associated with a specific label.

### The HTML Structure

```html
<ul class="sticky">
  <li *ngFor="let label of labels">
    <span [ngClass]="{         active: label === intoViewLabel       }" (click)="scrollToLabel(label)"> {{ label }} </span>
  </li>
</ul>
```

In the code above, notice that we use Angular's event binding (click) to call the scrollToLabel(label) function when a menu item is clicked. This function takes the label of the clicked menu item as an argument.

Moving to the TypeScript component, the scrollToLabel(label) function updates the intoViewLabel property with the selected label and retrieves the corresponding section element using document.getElementById(). If the element is found, it smoothly scrolls to it using element.scrollIntoView({ behavior: 'smooth' }).

#### The TypeScript Logic

```typescript
scrollToLabel(label: string) {   this.intoViewLabel = label;   const elementToScroll = document.getElementById(`${label}`);   if (elementToScroll) {     elementToScroll.scrollIntoView({ behavior: 'smooth' });   } }
```

So, when you click on a menu item, it triggers this function, smoothly scrolling the page to the section associated with that label. As a result, you achieve the desired behavior of scrolling to the corresponding section's title when clicking on a menu button.

That's all for today, tune in for the final part!

As always documentation is our friend, so here's some useful links that explain in detail what I used here:
Intersection Observer: [https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API]
ScrollIntoView: [https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView]

And last but not least here's a working stackblitz with the completed project; I know it's pretty ugly, but it serves the purpose of explaining what I did, so don't come for me :D
[https://stackblitz-starters-31ugwg.stackblitz.io]
