---
title: "Random Walker"
permalink: /NatureWithKivy/Random_Walker/
excerpt: "Simulate and visualize random walk in Python"
toc: True
---

## A Walker Is Born
Obviously, having a running app without displaying anything is extremely boring. Let's draw something inside.
{: .text-justify}

Imagine the window is now another 2D world we just created 5 mins ago, someone (or something) lives here. Hm, let's call it Walker. For now, it's just another widget.
{: .text-justify}

```python
class Walker(Widget):
    pass
```

Good, the Walker is now an invisible agent. However, I would like to visualize it. In Kivy, we can implement the visual representation with the *kv* language in one file, and the logic of app with python in another file. Let's start with the **.kv** file. Create one file named `nature.kv` in the same folder where `main.py` is.
{: .text-justify}

Every Kivy widget comes with a *canvas*, on which you can draw something. This is where you define how the Walker looks like e.g. the color, size, position...etc. For now, I would like the Walker to just be a stroke, a white stroke that exists in the center of the window.
{: .text-justify}

```python
#nature.kv
<Walker>:

    canvas:
        Color:
            rgba:1,1,1,1          # range between 0 and 1
        Point:
            points: root.center   # root refers to the app itself
```

Back to the python file, modify the `build` method to return a `Walker` object instead of a `Widget` object.
{: .text-justify}
```python
#main.py
from kivy.app import App
from kivy.uix.widget import Widget

class Walker(Widget):
    pass

class NatureApp(App):
    """A 2D world where the Walker lives
    """
    def build(self):
        return Walker()    # A Walker object is returned

if __name__ == "__main__":
    NatureApp().run()
```

Run the `python main.py` in the terminal. You should see a white dot appears in the center of the window.
{: .text-justify}
![The Walker](/assets/images/Walker_in_center.png 'The Walker is in center of the window')

Fantastic.

## Locate The Walker
The Walker is able to move, but not as free as we are in the real world. It can only go left, right, forward, backward, and maybe the combination of all. That's just the most you can do in a 2D world. Anyway, I will be happy for now as long as the Walker moves!
{: .text-justify}
As you might have guessed, the position in this 2D world is represented in coordinates. Take the `root.center` in the .kv file as an example, it's actually the coordinates `(x, y)` that defines the position of Walker. So, if we want the Walker to move, I think we need to play with the coordinates a bit.
{: .text-justify}
In the .kv side, the way to draw path where the walker has been to is the `Point` property. It's basically a *list* of dots in the form of `(x1, y1, x2, y2, x3, y3,...)`. Therefore, if we could update the list in some way, we can probably make the Walker behaves the way we want.
{: .text-justify}
As I mentioned above, the .kv file is usually (not always) used for layout and other graphical arrangements, while .py file implements how the engine works. In order for two files being able to talk to each other, you need a Kivy property in the .py file. Since we are looking for a list, the `ListProperty` is what we need.
{: .text-justify}
```python
# main.py
from kivy.properties import ListProperty

# Imagine the ListProperty is a simple python list,
# but in a Kivy-compatible form.
```
I will make the `ListProperty` become an attribute of the Walker, and store the position of itself... Ok, consider it done. I also wish the Walker to start walking from the center of the window. With that in mind, I would program the .py file like this:
{: .text-justify}
```python
# main.py

from kivy.properties import ListProperty
from kivy.core.window import Window

class Walker(Widget):

    # A empty list for storing the position
    points = ListProperty([])

    def __init__(self, **kwargs):
        """ Overwrite the __init__ function,
        so that the Walker starts from the center.
        """
        super(Walker, self).__init__(**kwargs)

        # Let the first pair of coordinates to be the center of window
        self.points = Window.center
```
And in the .kv file:
```python
# nature.kv
<Walker>:

    canvas:
        Color:
            rgba:1,1,1,1
        Point:
            points: self.points
```
Nice, we are almost there.

## The Random Walker


{% highlight python linenos %}

class Walker(FloatLayout):

    points = ListProperty([])

    def __init__(self, **kwargs):
        super(Walker, self).__init__(**kwargs)

        # start random walk from the center
        self.points = Window.center
        # start walking
        Clock.schedule_interval(self.update, 0.1)

    def update(self, *args):

        # Get current position
        last_x = self.points[-2]
        last_y = self.points[-1]

        # 1.1 # Generate random steps in 9 possible directions
        new_x = randint(-1,1)
        new_y = randint(-1,1)

        # 1.2 # Or with a tendency moving down and right
        #new_x = choice([-1]*2 + [0]*2 + [1]*6)
        #new_y = choice([-1]*6 + [0]*2 + [1]*2)

        # 1.3 # 50% chance moving to where the mouse is
        #if random() <= 0.5:
        #    new_x = np.sign(Window.mouse_pos[0] - last_x)
        #    new_y = np.sign(Window.mouse_pos[1] - last_y)
        #else:
        #    new_x = randint(-1,1)
        #    new_y = randint(-1,1)

        # Add the next step based on the previous position
        self.points = self.points + [last_x + new_x, last_y + new_y]

class NatureApp(App):

    def build(self):

        return Walker()


if __name__ == "__main__":
    NatureApp().run()

{% endhighlight %}
