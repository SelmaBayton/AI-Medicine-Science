# Counter Demo

This Python script demonstrates a simple web-based counter application and a scatter plot visualization. It uses the Microdot framework for web development.

## Prerequisites

- Python 3.x
- NumPy
- Matplotlib

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot numpy matplotlib
   ```

2. Run the script by executing the following command:
   ```
   python counter_demo.py
   ```

3. Open a web browser and visit `http://localhost:8008` to view the counter demo or `http://localhost:5000` to view the scatter plot visualization.

## Code Explanation

### Counter Demo

The code defines a web application that implements a counter. Users can increment or decrement the counter by clicking the corresponding buttons.

```python
from microdot import Microdot, Response

app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports the `Microdot` module for web development and sets the default content type of the responses to HTML. It also creates an instance of the `Microdot` application.

```python
def htmldoc(counter):
    return f'''
        <html>
            <!-- HTML document structure -->
        </html>
    '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes a counter value and two buttons for incrementing and decrementing the counter.

```python
@app.route('/')
def home(request):
    return htmldoc(0)

@app.route('/change/<current_counter>/<step>')
def change(request, current_counter, step):
    counter = int(current_counter) + int(step)
    return htmldoc(counter)
```

The script defines two URL routes: `/` and `/change/<current_counter>/<step>`. The root route (`/`) displays the initial web page with the counter set to 0. The `/change/<current_counter>/<step>` route handles the incrementing or decrementing of the counter based on the given step value.

```python
app.run(debug=True, port=8008)
```

The script runs the Microdot application, enabling the web server to listen on port 8008 and handle incoming requests.

### Scatter Plot Visualization

The code also includes a scatter plot visualization that generates a random scatter plot with a specified number of data points.

```python
import base64
import io
from io import BytesIO
import numpy as np
from matplotlib.figure import Figure
from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas

app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports necessary modules for generating the scatter plot using NumPy and Matplotlib. It creates an instance of the `Microdot` application and sets the default content type of the responses to HTML.

```python
@app.route("/")
@app.route("/<points>")
def hello(request, points="10"):
    points = int(points)

    # Generate random data points
    data = np.random.rand(points, 2)

    fig = Figure()
    FigureCanvas(fig)

    ax = fig.add_subplot(111)

    ax.scatter(data[:, 0], data[:, 1])

    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title(f'There are {points} data points!')
    ax.grid(True)

    img = io.StringIO()
    fig.savefig(img, format='svg')
    # Clip off the XML headers from the image
    svg_img = '<svg' + img.getvalue().split('<svg')[1]

    return
