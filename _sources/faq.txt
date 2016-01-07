Frequently Asked Questions
======================================================

What are the potential applications of this work?
-------------------------------------------------
The most important application of these findings is to have robots that can be useful for long periods of time without requiring humans to perform constant maintenance. For example, if we send robots in to find survivors after an earthquake, or to put out forest fires, or to shut down a nuclear plant in crisis like Fukushima, we need them to be able to keep working if they become damaged. In such situations, every second counts, and robots are likely to become damaged, because these environments are very unpredictable and hostile. Even in less extreme cases, such as in-home robot assistants that help the elderly or sick, we want robots to keep performing their important tasks even if some of their parts break. Overall, quick, effective, damage-recovery algorithms like Intelligent Trial & Error will make robots more effective and reliable, potentially changing them from things we only see in the movies, to things that help us every day.

What is the main difference between this work and previous approaches? Why does it work so well?
---------------------------------------------------------------------------------------

Compared to traditional reinforcement learning (RL) approaches, our techniques are much faster. That is because it was designed from the ground up to work with real robots (instead of only in simulation). It requires only a few minutes and a few physical trials on the robot, whereas RL algorithms typically have to conduct, hundreds, if not thousands, of tests to learn what to do. That is why most videos of RL on robots are sped up between 5 and 50 fold (ours is in real time). In our approach, the robot has a "simulated childhood" in which it learns different ways it can move its body, and those intuitions allow it to adapt after only a few tests and about two minutes. How does this simulated childhood help? Previous algorithms were searching for something very rare (a behavior that works given the damage) amongst a huge space of all possible behaviors. In our case, the size of this "search space" is 10^47, which is roughly the number of water molecules on earth! Very few of these possibilities are good, so previous algorithms had to search in this space to find the few, rare, good behaviors. Our algorithm searches ahead of time to collect all of the good behaviors, so instead of searching through all of the water molecules on earth, it is searching in a neatly sorted array of about 13,000 high-quality behaviors, which is much faster. We still need an intelligent learning algorithm to find the best of these 13,000 behaviors in only 10 trials, which is why we call it "intelligent" trial and error, but we already have made solving the problem much faster. In short, whereas previous algorithms searched for needles in fields of haystacks, we gather the needles ahead of time, so we are searching through a pile of needles to find the right one.

Compared to traditional "diagnose and respond" (aka fault-tolerance) approaches, there are two main differences: (1) our robot does not need to know what the damage is, it simply needs a way to measure its performance; (2) we do not have a large library that specifies what to do for each type of damage. Instead, our robot learns how to cope with whatever damage comes its way.

What are typical ways people misunderstand this work? Can you tell us things about your algorithm that are not obvious?
---------------------------------

**The robot never understands the damage.** It does not do any diagnosis. It just finds a behavior that works in spite of the damage. The difference is the same as between finding a way to limp with an extremely painful knee, but not knowing exactly what is wrong, and visiting a doctor to get an MRI and learn precisely what happened to your knee. Diagnosis requires more skill and equipment than simply finding a limp that minimizes pain. This is why our method is fast and cheap.

**The robot is not simply picking a working gait from a small library of options.** The map (or library) has over 13,000 behaviors. Yet the robot finds one that works after trying around 8 of them. Clearly, it is not testing them all. It is able to do this because the robot, like a scientist, carefully chooses which experiments to conduct to find an answer as quickly as possible (here, the answer the robot seeks is how to keep functioning despite its damage).

**The map of behaviors is not hand-designed: it is learned by the robot.** The robot uses a computer simulation of itself to create this map ahead of time. These maps can be quite large. In our experiments with the six-legged robot, the map contained over 13,000 gaits. While generating that map is computationally intensive, it only has to be done once per robot design before the robots are deployed. Importantly, this map does not represent all possible behaviors the robot can make. The space of all possible behaviors that is searched to find these 13,000 high-performing behaviors is unimaginably vast. In fact, it contains 10^47 possible behaviors, which is about how many water molecules on the planet Earth! That would be too many for our robot scientist to search through once damaged. Instead, we search through this vast space ahead of time to find 13,000 high-performing gaits (via a new algorithm we invented called "MAP-Elites"). In short, whereas previous algorithms searched for needles in fields of haystacks, we gather the needles ahead of time, so we are searching through a pile of needles to find the right one.

**The robot does not try to anticipate the damage conditions.** We do not pre-compute anything like "find a gait that works if leg 3 is missing". What we do with the simulator is simply to say "find as many different ways to walk as you can". That gives the robot intuitions about different ways that it can walk that work well. It then uses these intuitions to adapt once damaged.

**The robot does not "repair" itself.** Instead, it searches for an alternative way to work despite the damage. This is similar to what a human with an extremely painful knee would do: he will quickly find a way to limp so that the knee hurts less. But that does not mean he has adapted via healing: instead, he has adapted to deal with the damage that exists, yet still walk. Healing is something that would happen over a longer timeframe. For example, our algorithm could cause the robot to keep functioning until it is possible for it to take itself in for repair.

What kinds of damage can the robots recover from?
--------------------------------------------------
With our approach, a robot can adapt to any damage provided that there exists a way to achieve the mission in spite of the damage. So far, we did not encounter any damage for which our algorithm did not help! With the legged robot, we tried 6 different damage conditions, including cutting off two of its legs, and it figured out a way to keep going in every case. With the robotic arm we tried 14 different damage conditions, including two of its eight motors malfunctioning, and it always figured out a way to perform its task despite so much damage.

Does this work for any robot?
------------------------------
Yes. We cannot think of any reason it would not. In the paper, we tested with two very different robots (a 6-legged robot and a robotic arm) and it worked well on both.

Is this technique expensive?
-----------------------------
Our approach is actually very cost effective, because it does not require complex internal sensors. The robot only needs to measure how well it performs. It does not need to know the precise reason why it cannot perform the task. That allows tremendous cost savings, because a robot does not need to have a suite of expensive self-diagnosing sensors woven throughout its body.

Did the algorithm ever learn to do anything that surprised you? Any fun anecdote?
----------------------------------------------------------------------------------

Two years ago, we had a scheduled visit from high-profile scientists. Because our university wanted everything to look great for these important visitors, the university applied wax to the floor the day before. The floor was clean and shiny, which looked nice, but it was also much more slippery! We tried the gait our algorithm had previously learned, which we had tested many times to make sure it would work for these visitors, but it did not work at all. Fortunately, however, our robot can adapt! We launched our adaption algorithm, and a few minutes later, our robot was walking again on the newly waxed floor. As you can imagine, our visitors loved our work.
Another surprise was the following: To create a diversity of behaviors, we used evolution to produce a variety of different ways to walk. We did that by selecting for many different types of walking, measured as robots that have their feet touching the ground different percentages of the time (100%, 75%, ..., 25%, 0%). We thought evolution of course would not be able to solve the 0% case, but it surprised us! It flipped over on it's back and crawled on its elbows with its feet in the air.


What did we find most surprising?
----------------------------------
One thing we were surprised by was the extent of damage to which the robot could quickly adapt to. We subjected these robots to all sorts of abuse, and they always found a way to keep walking. With the legged robot, we tried 6 different damage conditions, including cutting off two of its legs, and it figured out a way to keep going in every case. With the robotic arm we tried 14 different damage conditions, including two of its eight motors malfunctioning, and it always figured out a way to perform its task despite so much damage.

What are the most exciting implications?
-----------------------------------------
We find it exciting that the techniques in this paper have implications far beyond damage recovery. They could in principle be applied to having robots learn almost anything. Because our approach works in just a few minutes, it brings closer the day in which robots will quickly learn a variety of different tasks.

Until now, nearly all approaches for having robots learn took many hours, which is why videos of robots doing anything are often extremely sped up. Watching them learn in real time was excruciating, much like watching grass grow. Now we can see robots learning in real time, much like you would watch a dog or child learn a new skill. Thus, for the first time, we have robots that learn something useful after trying a few different things, just like animals and humans. Actually, the first time Antoine Cully (the lead author of this paper) tested the algorithm, it worked so well that one of us (JBM) did not believe him!

What specific directions do you think your research might or should go from here? What are the next steps?
--------------------------------------------------------------------------------------
We will test our algorithm on more advanced robots in more real-world situations, for example with robots for disaster-response operations like those of the DARPA Robotics Challenge (http://www.theroboticschallenge.org/). One of the main challenges will be to take into account the complex environments the robots must operate in.

What is the biggest challenge towards achieving robots with such damage recovery capabilities?
---------------------------------------------------------------------------------
The biggest challenge is to make robots that are both creative problem solvers and fast thinkers: these two concepts are usually antagonistic! Here we overcome this challenge by allowing for a long, creative, exploratory period during the “simulated childhood” that happens before the robot is sent out into the field, and then, once the robot is damaged, having very efficient, modern machine learning algorithms incorporate the knowledge the robot learns in simulation to make very intelligent decisions about which behaviors to try to find one that works.

Why are legged robots useful?
------------------------------
For the same reason they are the predominant solution for land animals: because they can navigate and adapt to rugged terrain.

How does the robot know it is broken?
--------------------------------------
The robot does not know exactly that it is broken. It only knows that its performance has suddenly dropped. It has no internal sensors to detect whether any of its components are damaged.

Does the robot really learn?
---------------------------
According to the common definition, learning is "gaining knowledge or skill by studying, practicing, being taught, or experiencing something" (Merriam-Webster). Here, the robot uses a simulation of itself to autonomously find thousands of different good ways to walk: it is gaining knowledge by practicing in its ``head''. Since we did not explain to it how to walk, it is already learning autonomously. Once damaged, the robot conducts experiences and update its knowledge about the performance of each possible behavior (the update is done with a machine learning algorithm: a Gaussian process regression). It cannot try all the 13,000 behaviors that it stored before, therefore it has to leverage its knowledge to conduct the most informative and the most useful tests: in most cases, it tests less than 10 behaviors to find one that works in spite of the damage. Therefore, we can say that the robot learns how to walk for the same reason that we say that a child learns to shoot a ball in a ring: the robot practices, updates its knowledge, and try again until it has acquired the skill it needs.


Where can I learn more about all of this?
-----------------------------------------
Read our articles! They are freely accessible on our :doc:`publications` page, and they contain a lot of references to other work.
