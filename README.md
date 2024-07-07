Q1. How can you create a Bokeh plot using Python code?
Bokeh is a Python library that provides interactive plotting capabilities for web browsers. You can create Bokeh plots using Python code by following these steps:

Import necessary modules: Import the required functions and classes from the Bokeh library.

Prepare data: Define the data that you want to visualize in the plot.

Create a figure: Create a figure object using figure() function from bokeh.plotting.

Add glyphs: Add glyphs (markers or shapes) to the figure to represent the data points.

Customize: Customize the appearance of the plot, including axes, titles, legends, etc.

Show or save: Display the plot using show() function to open it in a browser, or save it using save() function.

Here's a basic example of creating a scatter plot using Bokeh:

python
Copy code
from bokeh.plotting import figure, show
from bokeh.io import output_notebook

# Sample data
x = [1, 2, 3, 4, 5]
y = [6, 7, 2, 4, 5]

# Output to notebook
output_notebook()

# Create a figure object
p = figure(title="Simple Scatter Plot", x_axis_label='X-axis', y_axis_label='Y-axis')

# Add glyphs (scatter markers)
p.circle(x, y, size=10, color='navy', alpha=0.5)

# Show the plot
show(p)
Q2. What are glyphs in Bokeh, and how can you add them to a Bokeh plot? Explain with an example.
Glyphs in Bokeh are visual markers or shapes that represent data points in a plot. They can be lines, markers, patches, or other geometric shapes. Glyphs are added to a Bokeh plot using specific methods provided by the figure object in Bokeh.

Here's an example of adding different glyphs to a Bokeh plot:

python
Copy code
from bokeh.plotting import figure, show
from bokeh.io import output_notebook

# Sample data
x = [1, 2, 3, 4, 5]
y = [6, 7, 2, 4, 5]

# Output to notebook
output_notebook()

# Create a figure object
p = figure(title="Example of Glyphs in Bokeh", x_axis_label='X-axis', y_axis_label='Y-axis')

# Add different glyphs
p.line(x, y, legend_label="Line", line_width=2)
p.circle(x, y, legend_label="Circle", size=10, color='navy', alpha=0.5)
p.square(x, y, legend_label="Square", size=8, color='green', alpha=0.5)

# Show the plot with legend
p.legend.location = "top_left"
show(p)
Q3. How can you customize the appearance of a Bokeh plot, including the axes, title, and legend?
You can customize various aspects of a Bokeh plot using attributes and methods provided by the figure object and other related objects. Here are some common customizations:

Title and Labels: Set title and axis labels using title, x_axis_label, and y_axis_label attributes of the figure object.

Axes: Customize axes appearance, ticks, and gridlines using attributes like xaxis, yaxis, xgrid, ygrid, etc.

Legend: Add legends to the plot using legend attribute, set its location and other properties.

Here’s an example of customizing a Bokeh plot:

python
Copy code
from bokeh.plotting import figure, show
from bokeh.io import output_notebook

# Sample data
x = [1, 2, 3, 4, 5]
y = [6, 7, 2, 4, 5]

# Output to notebook
output_notebook()

# Create a figure object
p = figure(title="Customized Bokeh Plot", x_axis_label='X-axis', y_axis_label='Y-axis',
           width=600, height=400)

# Add glyphs
p.circle(x, y, size=10, color='navy', alpha=0.5, legend_label='Data Points')

# Customize axes
p.xaxis.axis_label_text_color = "blue"
p.yaxis.axis_label_text_font_style = "italic"

# Customize title
p.title.text_color = "green"
p.title.text_font_size = "20px"

# Customize legend
p.legend.title = 'Legend'
p.legend.location = "top_right"
p.legend.label_text_font_style = "bold"

# Show the plot
show(p)
Q4. What is a Bokeh server, and how can you use it to create interactive plots that can be updated in real time?
A Bokeh server is a Python server that allows you to create interactive Bokeh plots that can be updated dynamically in response to user interactions or external inputs. It enables building sophisticated web applications with interactive visualizations.

To use Bokeh server:

Define your plot and interactions using Bokeh's plotting functions.

Write a Python script defining the server application logic and callbacks to update the plot based on user inputs.

Run the Bokeh server using bokeh serve command, specifying the Python script containing your application logic.

Here’s a basic example of using Bokeh server:

python
Copy code
# myapp.py
from bokeh.plotting import figure, curdoc
from bokeh.models import ColumnDataSource
from bokeh.layouts import column, row
import numpy as np

# Create initial data
x = np.linspace(0, 4*np.pi, 100)
y = np.sin(x)
source = ColumnDataSource(data=dict(x=x, y=y))

# Create a plot
plot = figure(title="Dynamic Sinusoidal Plot", plot_height=400, plot_width=600)
plot.line('x', 'y', source=source, line_width=3, line_alpha=0.6)

# Update callback function
def update_data(attrname, old, new):
    freq = freq_slider.value
    new_data = dict(x=x, y=np.sin(freq * x))
    source.data = new_data

# Create a slider widget
freq_slider = Slider(start=0.1, end=5, value=1, step=0.1, title="Frequency")
freq_slider.on_change('value', update_data)

# Layout setup
layout = column(freq_slider, plot)
curdoc().add_root(layout)
To run this script with Bokeh server:

css
Copy code
bokeh serve --show myapp.py
Q5. How can you embed a Bokeh plot into a web page or dashboard using Flask or Django?
To embed a Bokeh plot into a web page or dashboard using Flask or Django, follow these general steps:

Create a Bokeh plot: Create your Bokeh plot using Bokeh's plotting functions as usual.

Generate HTML: Use bokeh.embed module to generate HTML code that represents your Bokeh plot.

Integrate with Flask or Django: Incorporate the generated HTML code into your Flask or Django template.

Here’s a basic example of embedding a Bokeh plot into a Flask application:

python
Copy code
# Flask example

from flask import Flask, render_template
from bokeh.plotting import figure, output_file, save
from bokeh.embed import components

app = Flask(__name__)

@app.route('/')
def index():
    # Create Bokeh plot
    plot = figure()
    plot.circle([1, 2, 3], [4, 5, 6])

    # Generate components for embedding
    script, div = components(plot)

    # Render the HTML template with embedded Bokeh plot
    return render_template('index.html', script=script, div=div)

if __name__ == '__main__':
    app.run(debug=True)
In this example, components() function from Bokeh generates the JavaScript and HTML components needed to embed the plot into a Flask template (index.html). The script and div variables in the template are placeholders for the generated components.
