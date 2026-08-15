# Fibonacci Tree

An interactive 3D tree grown by the rules of the Fibonacci sequence, rendered in real time using Three.js. No npm, no bundler, open [Fibonacci Tree](https://tengyanhaiin-star.github.io/Fibonacci-Tree/) directly in any modern browser.

---

## How It Works

The branching structure is built directly from the biological model behind the Fibonacci sequence — the same model Fibonacci himself used to describe rabbit population growth.

Every branch is in one of two states:

| State | Behaviour |
|-------|-----------|
| **Young** | Extends into a single Mature branch — not yet ready to split |
| **Mature** | Splits into one Mature branch and one Young branch |

Starting from a single Young trunk, the number of branch tips at each generation follows the Fibonacci sequence exactly:

```
Generation:   1   2   3   4   5   6   7   8   9  10 ...
Tips:         1   1   2   3   5   8  13  21  34  55 ...
```

Each fork is coplanar — the parent branch and its two children always lie in the same plane, keeping the structure geometrically clean. The orientation of that plane rotates freely in 3D space at every node, giving the tree a natural, non-flat appearance.

Branch thickness tapers with depth using Fibonacci ratios, and color transitions smoothly from trunk to twig via vertex-colored geometry.

---

## Parameters

| Parameter | Description |
|-----------|-------------|
| **Depth** | Number of recursive generations (reflecting the two seed generations of the Fibonacci sequence) |
| **Trunk Length** | Length of the root branch in world units |
| **Decay Ratio** | Controls how quickly branches shorten with depth. Applied as `ratio^(depth/maxDepth)` for a natural taper |
| **Fork Angle** | Angle between the two child branches at each split |
| **Trunk Width** | Radius of the root cylinder; thins toward tips following Fibonacci ratios |

---

## Interaction

### Desktop
- **Drag** to rotate the tree
- **Scroll** to zoom in and out
- Adjust parameters via the sidebar; the tree rebuilds instantly

### Mobile
- **Single finger drag** to rotate
- **Pinch** to zoom
- Tap **Grow** to watch the tree animate from depth 4 to 16, then loop
- Tap **Random** to generate a new tree shape
- Tap the panel handle to expand or collapse the parameter controls
- Changing the Depth slider while Grow is playing stops the animation

---

## Grow Animation

The **Grow** mode animates the tree's development in real time:

1. Starting at depth 4, the tree adds one generation every 1.8 seconds
2. At depth 16, it pauses for 6 seconds — a full rotation to appreciate the complete tree
3. The cycle then restarts from depth 4

The key property: **every seed produces a consistent tree shape across all depths**. Increasing the depth adds new branches at the tips without altering any existing structure, so the growth feels genuinely additive rather than a redraw.

This is achieved by assigning random values through a path-keyed hash rather than a sequential random stream — each node in the tree always receives the same random values regardless of how deep the recursion goes.

---

## Ornaments

- **Leaves** appear at the tips of Young branches — flat pointed ellipses oriented along the branch direction, with a random axial roll for variety
- **Flowers** appear at the tips of Mature branches — five elliptical petals arranged in a plane perpendicular to the branch, around a central sphere

---

## Technical Notes

- Built with **Three.js r128**
- Branch cylinders use **vertex colors** for smooth trunk-to-twig color gradients
- **MeshLambertMaterial** throughout for efficient diffuse shading
- Lighting: ambient warm light + directional sun + cool fill light + shadow mapping
- Rendering is **on-demand** when idle (no continuous RAF loop), switching to continuous only during rotation or Grow playback — keeping CPU usage low
- Font: **Roboto**

---

## Dependencies

| Library | Version | Source |
|---------|---------|--------|
| [Three.js](https://threejs.org/) | r128 | cdnjs |
| [Roboto](https://fonts.google.com/specimen/Roboto) | — | Google Fonts |

## License
 
MIT — see [LICENSE](LICENSE) for details.
