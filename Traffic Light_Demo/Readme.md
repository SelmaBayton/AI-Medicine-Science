# Traffic Light

This Python script implements a web-based traffic light simulation using SVG (Scalable Vector Graphics). It uses the Microdot framework for web development.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python traffic_light.py
   ```

3. Open a web browser and visit `http://localhost:8008` to view the traffic light simulation.

## Code Explanation

The code defines a web application that simulates a traffic light. It uses SVG graphics to represent the traffic light and allows users to toggle the lights by clicking on them.

```python
from microdot import Microdot, Response

app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports the `Microdot` module for web development and sets the default content type of the responses to HTML. It also creates an instance of the `Microdot` application.

```python
def htmldoc():
    # Define colors for the lights
    reds     = ["853737","ff6465"]
    yellows  = ["907A4A","ffd782"]
    greens   = ["4E7039","a5eb78"]

    # Determine the color for each light based on the current state
    red     =     reds[lights[0]]
    yellow  =  yellows[lights[1]]
    green   =   greens[lights[2]]

    return f'''
        <html>
            <!-- HTML document structure -->
        </html>
    '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes an SVG graphic of a traffic light and defines the colors for each light (red, yellow, and green) based on the current state of the lights.

```python
lights = [0,0,1]

@app.route('/')
def hello(request):
    return htmldoc()

@app.route('/toggle/<light_index>')
def toggle_light(request, light_index):
    light_index = int(light_index)
    lights[light_index] = 1 - lights[light_index]
    return htmldoc()
```

The script defines two URL routes: `/` and `/toggle/<light_index>`. The root route (`/`) displays the initial web page with the traffic light. The `/toggle/<light_index>` route handles the toggling of the lights. When a light is clicked, its state is changed by toggling between 0 and 1.

```python
app.run(debug=True, port=8008)
```

The script runs the Microdot application, enabling the web server to listen on port 8008 and handle incoming requests.

Feel free to customize and enhance the code according to your needs!
