---
title: "The First App"
permalink: /NatureWithKivy/Setup/
excerpt: "Set up a basic Kivy app so that it can display our simulation"
toc: false
---
<br>
OK. Before diving straight into the book, we need at least a window to display our simulation. This means that we need to setup a very basic running app in Kivy.

To start a basic Kivy application, there are two things you need:
- An `App` class
- A root `Widget`

```python
from kivy.app import App
from kivy.uix.widget import Widget
```

Then, you need to write a class which inherit from the `App` class. This will be your app window.

```python
class NatureApp(App):
    pass
```

Since every running Kivy application can have one and only one root widget, we need to add the widget to the window. Here, the root widget is returned by the `build` function when the `App` is instantiated.

```python
class NatureApp(App):
    def build(self):
        return Widget()
```

Finally, we just need to instantiate the `App` and run the application.

```python
if __name__ == "__main__":
    NatureApp().run()
```

Put all elements together:
{% highlight python linenos %}
# main.py

from kivy.app import App
from kivy.uix.widget import Widget

class NatureApp(App):
    def build(self):
        return Widget()


if __name__ == "__main__":
    NatureApp().run()
{% endhighlight %}


If you run the above code snippet with `python main.py` in you terminal, a basic window would appear with nothing inside.

![A running app](/assets/images/TheFirstApp.png 'A running app')

Nice.

For more details on how Kivy works under the hood, please refer to the official [docs](https://kivy.org/doc/stable/guide/basic.html#quickstart).
