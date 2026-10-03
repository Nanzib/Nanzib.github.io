# HW 2 Reflection

1. flex-direction: row lays items out horizontally side by side (main axis is horizontal). flex-direction: column stacks items vertically on top of each other (main axis is vertical). It also changes how justify-content works, making it handle vertical spacing instead of horizontal.

2. Fixed pixels (px) don't scale when the viewport changes, which causes content to overflow and forces horizontal scrolling on smaller screens. Relative units like %, rem, and vh scale fluidly based on screen size or root font size, keeping the layout responsive and accessible.

3. AI Attribution
Prompt: "how to make a flexbox navbar with logo on left, links on right, and vertical stack on mobile"

Code provided:
@media (max-width: 768px) {
  .top-nav { position: sticky; top: 0; padding: 1.5rem 1rem; }
  .nav-links { flex-direction: column; gap: 1rem; }
}

Modification: The sticky positioning combined with the vertical stack and large padding took up nearly half the screen on mobile and blocked the content while scrolling. I changed .top-nav to position: static and reduced the padding and gap so the menu wouldn't take up too much screen space.
