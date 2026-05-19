# AGENTS.md

## Project Context

This project is a Chrome Dino runner clone built with Lottie SVG animations. The goal is a small, readable arcade game rather than a framework-heavy application.

The playable entrypoint is `game.html`. Keep the game contained in this single HTML file with inline `<style>` and `<script>` unless the user explicitly asks for a different structure.

## Asset Rules

- Lottie animation JSON files live in `animations/`.
- Static SVG assets live in `vectors/`.
- Do not rename `vectors/` to `svg/` unless the user explicitly asks for a folder cleanup.
- The layered scene must use only existing project assets from `animations/` and `vectors/`.
- The only non-asset visual exception is the sky gradient behind the scene.
- Do not add custom illustrated shapes, external images, emoji, canvas art, or decorative graphics.
- Minimal UI text for labels, scores, and instructions is allowed.

## Screen Flow

The game has three screen states:

1. `menu`: shows the start button.
2. `game`: active runner gameplay.
3. `highscore`: shown after a cactus collision; clicking it returns to the menu.

Keep future changes aligned with this flow unless the user requests a new state.

## Gameplay Expectations

- Ground moves continuously left and wraps to create an infinite floor.
- Hills move left more slowly than the ground to create parallax depth.
- The dino uses the run animation while jumping; the jump is vertical movement of the dino container.
- Cactus obstacles spawn from the right and cause game over on collision.
- Haxen collectibles spawn from the right, can be collected, and update the score UI.
- Haxen are both a game object and the visual language for points.

## Technical Guidance

- Use plain HTML, CSS, and JavaScript.
- Use `lottie-web` with SVG rendering for animation playback.
- Use `requestAnimationFrame` for the game loop.
- Use DOM elements and bounding boxes for movement and collision.
- Avoid package managers, build tools, frameworks, and physics engines for this MVP.
- Keep changes small and readable so the project remains easy to explain and hand in.
