---
layout: ../../layouts/MarkdownPostLayout.astro
title: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer - Part one"
pubDate: 03/09/2023
description: "Sticky menu highlighting active section when scrolling, using Angular framework and Intersection Observer"
image: "/blog.png"
author: "Daniela"
tags: ["angular", "intersection observer", "sticky menu", "highlight"]
---

Hey there, fellow developers! Today, we're about to embark on a journey to enhance user experience on your Angular websites. We'll tackle a scenario I recently encountered, where I needed to implement a sticky menu that highlights the active section when scrolling. Trust me, this little feature can go a long way in improving your website's navigation and aesthetics.

In this blog post, we'll take a simplified approach to solving this problem using Angular and the Intersection Observer API. So, if you've got an intermediate level of knowledge in web development and Angular, you're in the right place!

## The Challenge

Picture this: You have an Angular app with a menu containing various sections. Each section has a title and a table full of data. Your mission, should you choose to accept it, is to:

1. Scroll to the corresponding section's title when clicking on a menu button.
2. Make the menu stick to the top of the page so users always know where they are on the page and can easily click on section titles in the menu.

Seems straightforward, right? But here's the twist—I couldn't use the good old href property for various reasons, which meant I had to come up with an alternative solution. And that's what we'll explore today.

Let's dive into some code snippets to see how to make this magic happen!

### The HTML Structure

```html
<ul class="sticky">
  <li *ngFor="let label of labels">
    <span [ngClass]="{         active: label === intoViewLabel       }" (click)="scrollToLabel(label)"> {{ label }} </span>
  </li>
</ul>
<div *ngFor="let label of labels" [attr.id]="label" class="section" (intersection)="onIntersection(label, $event)">
  <h2 class="section-title">{{ label }}</h2>
</div>
```

#### The TypeScript Logic

```typescript
const labels = ['one', 'two', 'three']; intoViewLabel: string = this.labels[0]; scrollToLabel(label: string)
{   this.intoViewLabel = label;   const elementToScroll = document.getElementById(`${label}`);
if (elementToScroll) {     elementToScroll.scrollIntoView({ behavior: 'smooth' });   } }
onIntersection(label: string, isIntersecting: boolean): void {   if (isIntersecting) {     this.intoViewLabel = label;   } }
```

#### The Styling Magic

```css
.active {
  color: #1890ff;
  text-shadow: 0 0 0.25px currentcolor;
}
.active::after {
  border-bottom: #1890ff solid 3px;
  content: "";
  display: block;
}
.sticky {
  background-color: floralwhite;
  position: sticky;
  top: 0;
  z-index: 2;
}
ul {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  list-style-type: none;
  margin: 0;
  padding: 0;
}
ul > li {
  cursor: pointer;
}
.section {
  height: 600px;
  background-color: cornflowerblue;
}
.section-title {
  color: floralwhite;
  padding-left: 10px;
  padding-top: 20px;
}
```

#### The Intersection Observer Directive

```typescript
import { Directive, ElementRef, EventEmitter, Output } from "@angular/core";
@Directive({ selector: "[intersection]" })
export class IntersectionDirective {
  @Output() intersection = new EventEmitter<boolean>();
  constructor(private elementRef: ElementRef) {
    const options = { root: null, rootMargin: "0px", threshold: 0.5 };
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          this.intersection.emit(true);
        } else {
          this.intersection.emit(false);
        }
      });
    }, options);
    observer.observe(this.elementRef.nativeElement);
  }
}
```

Now that we've set the stage, let's dive into the nitty-gritty details of how this code works and how you can implement it in your own Angular projects. Stay tuned for the next parts of this blog, where we'll break down each component and its role in creating our sticky menu with active section highlighting. Happy coding!

As always documentation is our friend, so here's some useful links that explain in detail what I used here:
Intersection Observer: [https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API]
ScrollIntoView: [https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView]

And last but not least here's a working stackblitz with the completed project; I know it's pretty ugly, but it serves the purpose of explaining what I did, so don't come for me :D
[https://stackblitz-starters-31ugwg.stackblitz.io]
