<img width="1918" height="872" alt="grafik" src="https://github.com/user-attachments/assets/5c39a0ac-52b1-445f-b248-2326d2e9b4ea" />

## Project Idea

This project is a simplified Chrome Dino runner clone using Lottie SVG animations as the visual system. The game combines animated character and UI assets with static SVG scenery to create a small playable runner.

## Technology Choices

The game uses one `game.html` file with inline CSS and JavaScript. This keeps the project easy to open, inspect, and explain. A larger framework would add structure, but it would not add much value for a compact runner prototype.

The implementation uses `lottie-web` because the animation files are already exported as Lottie JSON. The renderer is set to `svg`, matching the asset style and keeping the animations crisp at different screen sizes.

Plain DOM elements are used instead of canvas. This makes it simple to place Lottie animations, static SVG images, and UI text in the same layered scene.

## Screen Model

The game has three main screen states:

- `menu`: the start screen with the stone start button.
- `game`: the active runner screen.
- `highscore`: the game-over score screen shown after a cactus collision.

This state model keeps the flow clear. The player starts from the menu, plays until a collision, sees the highscore screen, then clicks that screen to return to the menu.

## Asset Strategy

Animated entities use files from `animations/`. The dino, cactus, haxen, sun, cloud, stone button, and highscore screen are all loaded through Lottie.

Static scenery uses files from `vectors/`. The ground and hills are normal SVG images because they do not need their own animation timelines. Instead, the game moves their containers horizontally.

## Game Loop And Motion

The game loop uses `requestAnimationFrame`, which is the browser-native way to update animation smoothly. Each frame calculates how much time has passed, then updates scrolling scenery, jump physics, spawned objects, collisions, and score.

Ground movement is created by placing two copies of `Ground.svg` next to each other and moving the track left. When one copy has moved offscreen, the track wraps back, creating the illusion of an endless seamless floor.

Hills use the same wrapping idea, but they move more slowly than the ground. This slower movement creates parallax, making the background feel farther away.

## Collision And Scoring

Collision is handled with DOM bounding boxes. This is accurate enough for a simple runner and avoids adding a physics engine.

When the dino overlaps a cactus, the game stops and moves to the highscore screen. When the dino overlaps a haxen, the haxen is collected, the score increases, and the collectible is removed.

The best score is stored in `localStorage`, so the highscore survives a page refresh in the same browser.
