### Overview

From an earlier email.

> Since my teachers neglected to assign any work this afternoon, I
> hacked out a simple implementation of something called a "particle
> filter" that is used in robotics to help localize (determine the
> position of) machines in an unpredictable environment. It's a very
> clever idea — I could never have done this on my own — that relies
> more on simulation than on functional inversion. It's a bit tricky to
> explain over email, but, for your enjoyment:
> 
> http://fatlotus.github.com/particle-filters
> 
> A note: the blue dot represents the actual position of the robot, and
> the little grey dots represent various hypotheses for where it is, and
> the red represents the average of those hypotheses. The big fort-like
> things are passive sonar beacons. Tomorrow I'll add in a bit of
> hyperbolic regression (more accurately representing sonar), but even
> for the moment it's fairly accurate. The robot is following a fairly
> basic protocol: "go as fast as possible unless I think I'm near a
> wall." Note that this behavior does not have access to the blue
> co-ordinates, only those of the red box, yet it is still adept at
> dealing with obstacles and uncertainty.
> 
> All the best,

#### Particle Filters Overview

Particle filters, as originally explained, are best described in lectures
[11-18][pf-intro] through [11-21][pf-outro] in the freely-available
[Stanford Online Artificial Inteligence][ai-course] course. These are
(unfortunately) only visible in video lecutre format, but the videos
are quite short and have captions available.

In essence, particle filters are incredibly simple, and they require little
difficult computation. The agent, keeping with my own (limited) understanding
of the human brain, keeps a list of tuples `{ x, y, theta, dx, dy, dtheta }`
of all the possible states that the boat can be in. At the start of the
simulation, any state is possible: the boat could be anywhere travelling at
any velocity. Every time the boat moves the ruddder position or spins the
propeller, every state, or particle, is updated according to a simple simulated
model. In this way, every particle is consistent with the moment-to-moment
adjustment of position and direction.

There is also another half to the algorithm, however. Since the boat is regularly
receiving sonar data, it must also remove those particles that aren't consistent
with it's external model of the world.

[pf-intro]: https://www.ai-class.com/course/video/videolecture/149
[pf-outro]: https://www.ai-class.com/course/video/videolecture/152
[ai-course]: https://www.ai-class.com

#### The Application

As stated above, the algorithm used is primarily one of dynamic
pathfinding in a stochastic environment. In essence, it simulates
all the relevant components of an aquatic vessel — a motor, rudder,
and sounding beacons — and includes a basic AI to direct the boat.

There are two samples available online, and there source is of course
available in this repository. [The first][first-sample] and most
simplistic simply localizes (determines the position of) the boat
given certain beacon locations and uncertain mechanics and sonar.

The [second][second-sample] is more complex. It simulates a
complete [SLAM][slam-article] ("simultaneous localization and
mapping") algorithm that dynamically attempts to localize and to
determine the position of the beacons. This algorithm knows with
certainty the shape of the basin but is uncertain about boat
position and momentum and the locations of the beacons. Naturally,
this second simulation is much more sophisticated and takes more
time to reach a solution.

[first-sample]: https://fatlotus.github.com/particle-filters/plain.html
[second-sample]: https://fatlotus.github.com/particle-filters/index.html
[slam-article]: https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping