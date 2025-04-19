There's a pipeline that is usually applied to every object before it appears on a user's screen.
It is not as straightforward as it might seem, but after understanding how it is derived, it becomes much easier.
The purpose of the following text is to finally figure out how all these things work under the hood.

General view of the process
<img src="3d-rendering/general_view.jpg">
As you can see, there are 5 spaces in which an object may exist:

Local space — in its own coordinate system.

World space — in the world coordinate system.

View space — in the camera's coordinate system.

Clip space — TODO

Screen space — TODO

There is nothing particularly interesting to say about the first two spaces,
so let's just skip them.

The fun begins with the third one. What is the view space?

Let's say we have a camera wandering around in world space. The camera's coordinate system forms the view space.

What parameters does the camera have?

Position in world space

Direction

Up vector

Position $$\vec{P}$$ is a vector starting from the world space origin and pointing to the camera position.

Direction $$\vec{D}$$ is a vector starting from the camera position and pointing to a certain point in world space (already normalized for convenience).

Up vector $$\vec{U}$$ is a vector pointing upward relative to the camera. It is not necessarily perpendicular to $$\vec{D}$$ and is always adjusted (we will discuss this later).

The first thing to do is calculate the basis vectors of the view space coordinate system.

Let's say $$\vec{f}$$ (front), $$\vec{r}$$ (right), and $$\vec{u}$$ (true up) are the basis vectors of this system. The first step is to calculate $$\vec{r}$$:
$$
\vec{r} = \vec{D} \times \vec{U}
$$

The second step is to get the true (adjusted) up vector:
$$
\vec{u} = \frac{\vec{D} \times \vec{r}}{|\vec{D} \times \vec{r}|}
$$

Now we have a basis coordinate system.
