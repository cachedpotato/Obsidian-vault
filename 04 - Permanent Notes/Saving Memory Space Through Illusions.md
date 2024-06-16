---
tags:
---
# Saving Memory Space Through Illusions
Games can get big. so big, in fact, we can't fit every aspect of the game onto our memory. This is highly costly with little to no benefits. However, we must make sure that the player _FEEL LIKE IT'S ALL THERE_, or else the gaming experience will be hindered. Therefore, game developers must master the art of _illusions_, where they make it _SEEM like it's there where it really isn't_.

A good example of this is terrain loading. Think of the Hyrule field, or even just the Death Mountain in Zelda OoT. The place is MASSIVE, but it sure as hell cannot fit in the puny NES64 hardware (though, it was cutting edge technology at that time). What did the developers do? They only rendered the parts that are visible.
![[화면 캡처 2024-06-14 092827.png]]
Here is the shopkeeper in OoT. This is the screen when we first enter the shop. Seems pretty innocuous, but there is some "hideous" rendering jargon going on at the back:
![[화면 캡처 2024-06-14 092912.png]]
NO LEGS????

Here we can see that the developers made a conscious decision to just, not create the leg portion of the body, because the shopkeeper will always be behind the counter and make the legs not visible. Why create something when you won't be able to see? It's just a waste of memory. 

Not just that, models we _thought_ were in 3D are just 2D images, just angled to give the sense of depth. These "illusions" are what makes games use less memory space, and be more performant.


---
Categories: [[020-Game Development]], [[CS50 - Game]]
References:
https://www.youtube.com/watch?v=HUgE9L7V4oY
Created: 2024-06-14
