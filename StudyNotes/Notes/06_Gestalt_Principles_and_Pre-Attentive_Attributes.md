# Gestalt Principles and Pre-Attentive Attributes

Design principles help us in two ways:

- They generate design options.
- They help us choose among those options.

We can derive a few other useful design principles if we understand how our visual perception works. Let's take a look at the image below.

>  ![img](https://s3.amazonaws.com/dq-content/527/1.1-m527.svg)

If you see a square and a triangle, then you perceive a pattern. If we break down the image into individual components, however, we only have a bunch of small gray circles arbitrarily spaced and arranged. Then why do we see a pattern?

The pattern we see is a result of how our visual system processes the individual components. Our interest as data scientists is to predict what sort of patterns people see in our data visualizations. To predict that, we can use the **Gestalt principles**.

The idea behind Gestalt principles is that humans generally perceive patterns rather than individual objects. From a practical point of view, **Gestalt principles** tell us what sort of pattern we can expect people to see when we show them our data visualizations. 

Below, we see a data story from [FiveThirtyEight](https://fivethirtyeight.com/features/how-the-post-office-became-a-political-football/) showing how the coronavirus pandemic affected mail services compared to shipping and packaging.

>  ![img](https://s3.amazonaws.com/dq-content/527/fte_mail_shipping.png)

Generally, our perception groups together individual elements that are similar to one another. We call this the principle of **similarity**. Similarity can apply to color, shape, size, or other visual properties.

>  ![img](https://s3.amazonaws.com/dq-content/527/3.3-m527.svg)

Let's take a look at the image below:

>  ![img](https://s3.amazonaws.com/dq-content/527/4.1-m527.svg)

The circle and the square on the first row are both enclosed inside a rectangle. The enclosing leads us to perceive the circle and the square as belonging together.

When we see a set of distinct elements enclosed inside a visual form, we perceive them as part of the same group. We call this the principle of **enclosure**.

We can enclose objects using different visual forms, not just rectangles. Below, we create an enclosure using a shaded ellipse.

>  ![img](https://s3.amazonaws.com/dq-content/527/4.2-m527.svg)

In data visualization, enclosure comes in handy when we want to separate or draw attention to certain portions of a graph. Below, we highlight the third line plot using enclosure (let's say we want to draw attention to the third plot).

>  ![img](https://s3.amazonaws.com/dq-content/527/m3_10.png)

Let's take a look at the image below.

>  ![img](https://s3.amazonaws.com/dq-content/527/5.1-m527.svg)

The circle on the first row belongs with the triangle on the last row because of the line that connects them.

When we see distinct objects connected by some kind of a visual form (usually a line), we perceive them as part of the same group. We call this the principle of **connection**.

Below, we use this principle to show a connection between Mexico and Argentina (let's say we need to make a point about this connection).

>  ![img](https://s3.amazonaws.com/dq-content/527/m3_12.png)

So far, we've learned four Gestalt principles:

- Proximity
- Similarity
- Enclosure
- Connection

Connection is typically stronger than proximity and similarity. Let's take a look at the image below:

>  ![img](https://s3.amazonaws.com/dq-content/527/6.1-m527.svg)

We perceive the first two squares as belonging together because of the line that connects them. Connection cancels out the space between them — in other words, connection is stronger than proximity.

Below, we see an interaction between connection and similarity:

>  ![img](https://s3.amazonaws.com/dq-content/527/6.2-m527.svg)

On each row, we perceive the square and the circle as belonging together because of the line that connects them. We don't see two groups (three squares and three circles) because connection is stronger than similarity.

Connection and enclosure typically have similar strengths. What makes the difference is the properties of the visual objects we use to create the enclosure and the connection. Thicker lines and stronger color can mean a stronger connection. Dotted lines along with a strong-colored enclosing form can mean stronger enclosure and weaker connection.

>  ![img](https://s3.amazonaws.com/dq-content/527/6.3-m527.svg)

Because some of the principles are stronger than others, a **visual hierarchy** develops. When we create data visualizations, we need to create with visual hierarchy in mind. If connection cancels out similarity without us realizing, we can communicate incorrect information.

**Gestalt principles** describe how we can visually perceive distinct elements as a group. These principles indirectly show us that visual perception isn't random. We perceive visual stimuli according to certain rules, and the output is typically predictable.

The way we direct our attention on an image is also non-random. Let's start by examining the image below:

>  ![img](https://s3.amazonaws.com/dq-content/527/7.1-m527.svg)

We see a few parallel horizontal lines, and except for their position in space, they are identical. Nothing really stands out. Let's now look at this image:

>  ![img](https://s3.amazonaws.com/dq-content/527/7.2-m527.svg)

The thicker green line instantly draws our attention because it's different from the rest. It signals where to look. We see a similar visual effect in the horizontal bar plot below:

>  ![img](https://s3.amazonaws.com/dq-content/527/m3_18.png)

We focus our attention on Brazil because the color of its corresponding bar is different.

A visual object that is different from the rest stands out and signals where to look. We can use this visual effect to guide our audience's attention. If people look where we want them to, we can present information more efficiently.

Our brains typically become aware of these different objects before we consciously direct our attention toward them. Because they come before conscious attention, we call them **pre-attentive** ("pre" means "before"). Below, we see some of the pre-attentive attributes we can use in our data visualizations.

>  ![img](https://s3.amazonaws.com/dq-content/527/7.4-m527.png)

You can explore more principles [here](https://en.wikipedia.org/wiki/Gestalt_psychology)

