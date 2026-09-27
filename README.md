# Bouncy Ball
A launch-and-bounce physics puzzle: pull back on the ball, let it fly, and bounce it off trampolines, shapes and fans until it lands in the cup. Comes with a level editor for building your own.

**[▶ Open the live app](https://timothyhadfield.github.io/bouncy-ball/)** · best on a laptop (aiming and the editor use a mouse)

<p align="center">
  <img src="docs/screenshots/level.png" alt="Aiming a shot: a dotted trajectory preview and power meter over a level with a fan, wall, spike, trampoline and cup" width="49%">
  &nbsp;
  <img src="docs/screenshots/editor.png" alt="The level editor with a toolbar of pieces and a selected block showing resize and rotate handles" width="49%">
</p>

<p align="center">
  <img src="docs/screenshots/menu.png" alt="Level menu with a thumbnail for each saved level and a + tile to create a new one" width="49%">
</p>

## Features
- **Slingshot launch**: drag back from the ball to aim; a dotted line previews the arc and shows your power.
- **Physics pieces**: trampolines, fans that blow the ball upward, spikes that pop it, circles, blocks and walls.
- **Level editor**: place pieces from a toolbar, drag to move, scroll to resize, drag a handle to rotate, and set the ball's start point.
- **Per-level physics**: gravity, bounciness and friction sliders for each level.
- **Your levels are saved**: the menu shows a thumbnail of every level, and everything is kept in your browser.
- **Camera**: the view frames the ball and the cup, zooms out as you pull back, and can be panned (right-drag) and zoomed (scroll).

## Built with
One HTML file: plain JavaScript and Canvas, with a hand-written physics loop. No build step, no server.
