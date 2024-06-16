---
tags:
---
# Delta Time
Games are rendered in terms of frames. every frame, functions are called, states are changed, etc. It goes without saying that frames are extremely important, whether it be the perspective of the player, or the perspective of the developer.

Let's focus on the developer side for a minute. Developers have to deal with player (the human player not the in-game character)'s difference in specs. Some computers are just complete potatoes, and can only crank up to 30 FPS, whereas other near-supercomputer like builds can make frame skyrocket through the hundreds. What does this mean?

Going back to basics, FPS is short for "Frames Per Second". 30 FPS means 30 frames will be rendered every second, and for 60 FPS, 60 frames, etc. etc. Each frame will get a fraction of a second, and the higher the framerate, the thinner this fraction gets. Meaning, if we just render the frames in strictly frame basis, faster computers will run the game faster than the slower ones, even if they're the same game, because they simply render more frames in the same amount of time.

This may be a slight inconvenience for some, and complete deal-breaker for others. How should we solve this problem? Why, by updating based on the _TIME_ passed, of course.

If we update the game based on time instead of frames, it does not matter what FPS the games run at, because all will move the same distance in the same amount of time. Take a simple position update for example:

```GDScript
func _process(delta):
	position += velocity * speed * delta
```
Here, the `delta` argument is the delta time. If we run the game at 30 FPS, the `delta` value will be twice as big as the `delta` value when the game runs at `60 FPS`. Even if 60 FPS will render the game twice as many times as 30 FPS, the distance travelled will be the same:
$$
\begin{flalign}
position(x_{i+1})@30FPS & = position(x_{i}) + velocity * \Delta t_{30} \\
position(x_{i+2})@60FPS& = position(x_{i}) + velocity * 2\Delta t_{60} \\
\Delta t_{30} & = \frac{1}{30} = 2*\frac{1}{60} = 2\Delta t_{60} \\
\therefore position(x_{i+1})@30FPS &= position(x_{i+2})@60FPS
\end{flalign}
$$

---
Categories: [[020-Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-14
