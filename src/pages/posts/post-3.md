---
layout: ../../layouts/MarkdownPostLayout.astro
title: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer - Part three"
pubDate: 10/09/2023
description: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer"
image: "/blog.png"
author: "Daniela"
tags: ["angular", "intersection observer", "sticky menu", "highlight"]
---

Let's delve into how to implement the second point, which is making the menu stick to the top of the page so users always know where they are on the page and can effortlessly click on section titles in the menu, using the provided code examples.

This effect is achieved through CSS styling and a dash of Angular magic. Here's how it works:

In our HTML template, the menu is wrapped in a <ul> element with the class sticky, which is essential for the sticky behavior. We use CSS properties to define its positioning:

### The HTML Structure

```html
<ul class="sticky">
  <!-- Menu items here -->
</ul>
```

In the associated CSS (app.component.css), the .sticky class is what brings the magic. It uses the position: sticky property, which allows the menu to stick to the top of the page when it reaches the specified position. In our case, top: 0 ensures it sticks to the very top of the viewport.

#### The Styling Magic

```css
.sticky {
  background-color: floralwhite;
  position: sticky;
  top: 0;
  z-index: 2;
}
```

The z-index property is also set to ensure the menu remains above other elements as it sticks to the top. This styling effectively achieves the goal of making the menu stay at the top of the page.

Now, let's bring Angular into the mix. In our TypeScript component (app.component.ts), we have an intoViewLabel property, which helps keep track of the currently visible section. We update this property in the onIntersection(label, isIntersecting) function, which is triggered by the Intersection Observer. When a section becomes visible, we set the intoViewLabel to the corresponding label.

#### The TypeScript Logic

```typescript
onIntersection(label: string, isIntersecting: boolean): void {   if (isIntersecting) {     this.intoViewLabel = label;   } }
```

This property is then used to highlight the active menu item, providing a visual cue to users about their current location on the page.

By combining these CSS styles with Angular's dynamic label tracking, we successfully make the menu stick to the top of the page and highlight the active section as users scroll, ensuring a smooth and user-friendly navigation experience.

And there you go, you have a nice dynamic navigation menu.

As always documentation is our friend, so here's some useful links that explain in detail what I used here:
Intersection Observer: [https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API]
ScrollIntoView: [https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView]

And last but not least here's a working stackblitz with the completed project; I know it's pretty ugly, but it serves the purpose of explaining what I did, so don't come for me :D
[https://stackblitz-starters-31ugwg.stackblitz.io]
