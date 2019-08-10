---
title: "Random Walker"
permalink: /NatureWithKivy/Random_Walker/
excerpt: "Simulate and visualize random walk in Python"
toc: True
---

## A Walker is born
Obviously, having a running app without displaying anything is extremely boring. Let's draw something inside.
{: .text-justify}

Imagine the window is now another 2D world we just created some mins ago, someone (or something) lives here. Hm, let's call it Walker. For now, it's just another class in the same file.
{: .text-justify}

```python
# main.py
class Walker(Widget):
    pass
```

Good, the Walker is now an invisible agent. However, I would like to visualize it. In Kivy, we can implement the visual representation with the *kv* language in **.kv** file, and the logic of app with python in the **.py** file. Let's just keep it simple and do everything in python for now.
{: .text-justify}

To start, we need the `__init__` function to define what we would like to see when the `Walker` is initialized. This is also for the visualization later.
{: .text-justify}
```python
class Walker(Widget):

    def __init__(self, *args, **kwargs):
        # Initialize the parent class
        super(Walker, self).__init__(*args, **kwargs)
```

Every Kivy widget comes with a *canvas* object, with which you can draw something. This is where you define how the Walker looks like e.g. the color, size, position...etc. For now, I would like the Walker to just be a point, a white point that appears in the center of the window.
{: .text-justify}

```python
# main.py
# import App and Widget class...
from kivy.core.window import Window
from kivy.graphics import Point, Color

class Walker(Widget):

    def __init__(self, *args, **kwargs):
        # Initialize the parent class
        super(Walker, self).__init__(*args, **kwargs)

        with self.canvas:
            # Value ranges from 0 to 1
            Color(1, 1, 1)
            # Initialize Walker's position in the center
            Point(points = Window.center)
```

Finally, modify the `build` method to return a `Walker` object instead of a `Widget` object.
{: .text-justify}
```python
class NatureApp(App):
    """A 2D world where the Walker lives"""

    def build(self):
        return Walker()    # A Walker object is returned

if __name__ == "__main__":
    NatureApp().run()
```

Run the `python main.py` in the terminal. You should see a white dot appears in the center of the window.
{: .text-justify}
![The Walker](/assets/images/Walker_in_center.png 'The Walker is in center of the window')

Fantastic.

## Locate the Walker
The Walker should be able to move, but not as free as we are in the real world. It can only go left, right, forward, backward, and maybe the combination of these. And that's just the most you can do in a 2D world. Anyway, I will be happy for now as long as the Walker moves!
{: .text-justify}

As you might have guessed, the position in this 2D world is represented in coordinates. Take the `Point(points = Window.center)` in the canvas for example, it's actually the coordinates `(x, y)` that defines the position of Walker. So, if we want the Walker to move, I think we need to play with the coordinates a bit.
{: .text-justify}

In fact, the `points` attribute is basically a *list* in the form of `(x1, y1, x2, y2, x3, y3,...)`. Therefore, it's a great way to represent the path that the Walker has been to. If we could update the list in some way, we could probably make the Walker behaves the way we want. In order to access and add new coordinates later, we make the `Point` as an attribute `path` of the Widget class. After all, the Walker should know where it is...[^1]
{: .text-justify}
```python
class Walker(Widget):

    def __init__(self, *args, **kwargs):
        # Initialize the parent class
        super(Walker, self).__init__(*args, **kwargs)

        with self.canvas:
            # Value ranges from 0 to 1
            Color(1, 1, 1)
            # Initialize Walker's position in the center
            self.path = Point(points = Window.center)
```
[^1]: If you add `print(self.path.points)` in the `__init__` function, you will see that there is only one pair of coordinates in the list. In my case, the coordinates are `[400.0, 300.0]`.

## The random Walker

Now, what pieces are missing? I imagine the Walker moves one second to the left, next second up, and maybe the next second left again. The direction of its movement should be *random*, and one step of a *time*. Yes, I think that's it.
{: .text-justify}

In order to make the Walker roam around in a random manner, I would like to add a second pair of coordinates to the list. The new coordinates should be not too far away from the old coordinates, maybe just `+1` or `-1` pixel away. To achieve this, the `random` python module is what we need.
{: .text-justify}
```python
from random import randint
```

How do we add a second pair of coordinates that are close to the first pair to the list? It turns out that we can do this through a `add_point` function. However, we also need to generate the random step in someway. Since the Walker knows where it is, let's wrap everything in one function to update its own position.
{: .text-justify}

```python
class Walker(widget):

    # def __init__(self):
    #     ...

    def update(self, *args):
        # Get current position
        last_x = self.path.points[-2]
        last_y = self.path.points[-1]

        # Generate random steps in 9 possible directions
        new_x = randint(-1,1)
        new_y = randint(-1,1)

        # Add the next step based on the previous position
        self.path.add_point(last_x + new_x, last_y + new_y)
```

Of course, we can use a `for` loop and call this update function as many time as we want, but let's do something fancier. To animate something, Kivy provides an easy way to do this, namely the function `schedule_interval(my_callback, t)` in the `Clock` module. Here, the `my_callback` is exactly the function we wrote before, while the `t` is the defined time interval. Because I want the random walking behavior to start as soon as the Walker appears, I would schedule the clock also in the `__init__`.
{: .text-justify}

```python
class Walker(Widget):

    def __init__(self, *args, **kwargs):
        # Initialize the parent class
        super(Walker, self).__init__(*args, **kwargs)

        with self.canvas:
            # RGB values range from 0 to 1
            Color(1, 1, 1)
            # Initialize Walker's position in the center
            self.path = Point(points = Window.center)

        # Update the its own position every 0.1 second
        Clock.schedule_interval(self.update, 0.1)
```

Put everything together:

{% highlight python linenos %}
#main.py

from kivy.app import App
from kivy.core.window import Window
from kivy.uix.widget import Widget
from kivy.graphics import Point, Color
from kivy.clock import Clock
from random import randint


class Walker(Widget):

    def __init__(self, *args, **kwargs):
        super(Walker, self).__init__(*args, **kwargs)

        # start walking
        with self.canvas:
            # Define the color of stroke
            Color(1, 1, 1)
            # Walker's initial position
            self.path = Point(points = Window.center)

        # Update the its own position every 0.1 second
        Clock.schedule_interval(self.update, 0.1)

    def update(self, *args):

        # Get current position
        last_x = self.path.points[-2]
        last_y = self.path.points[-1]

        # Generate random steps in 9 possible directions
        new_x = randint(-1,1)
        new_y = randint(-1,1)

        # Add the next step based on the previous position
        self.path.add_point(last_x + new_x, last_y + new_y)


class NatureApp(App):

    def build(self):
        return Walker()


if __name__ == "__main__":
    NatureApp().run()

{% endhighlight %}

Again, run `python main.py` in your terminal. After letting it run for 25 mins, I got something like this.
{: .text-justify}

![First Step](/assets/images/First_step.png 'The Walker takes his first step')

Great. Now I've got a random Walker.

**Warning Notice:**
There is currently a limit on the number of points you can add in the list. According to the docs, the list cannot contain more than 2^15-2 elements i.e. `x` or `y`. Based on the frequency (10Hz) we update the list, the app actually crashes less than half an hour.
{: .notice--warning}
