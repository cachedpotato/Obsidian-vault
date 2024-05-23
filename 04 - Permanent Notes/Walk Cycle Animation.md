---
tags:
---
# Walk Cycle Animation
Walk cycle consists of mainly 5 key frames, repeated 2 times.
![[스크린샷 2024-05-23 121322.png|600]]

## Contact 1
Think of it as the starting frame of your walking animation. However the walk cycle ends, it must loop naturally back to contact 1. The head is at a neutral height.

## Down
When the first leg/foot hits the ground. For the sake of explanation let this be the right leg. as we are hitting the ground the leg will bend a bit, causing the head to go down as well.
The arm swing will be at its widest here.

## Passing
A transition period where the legs cross. Because we're starting to go back up, the head will be at roughly the same position as contact 1.
The arm will be alongside the body.

## Up
When the right leg is fully extended. The left leg will now be more at the front than the right leg. Because one leg is fully extended, the head will be at its peak height.

## Contact 2
Same as contact 1, but with leg position now switched. Now the left leg is at the front. Because of our body's symmetry, we can just copy past all the frames drawn before, just switch legs, and voila, we have a super basic walking cycle! Make sure to add secondary animation for a more natural look.


---
Categories: [[Animation]]
References: 
https://www.youtube.com/watch?v=7T6yOk5n-zk
-TOREAD: the Animator's Survival Kit

Created: 2024-05-14
