# Aquaponics System Control

This Python script implements a basic web-based control interface for an aquaponics system. It allows the user to toggle the status of the water pump and air pump of the system. The Microdot framework is used for web development.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python aquaponics_control.py
   ```

3. Open a web browser and visit `http://localhost:8008` to access the aquaponics system control interface.

## Code Explanation

The code defines a web application that controls the aquaponics system.

```python
from microdot import Microdot, Response

app = Microdot()
Response.default_content_type = 'text/html'

system_state = {
    'water_pump': False,
    'air_pump': False,
}
```

The script imports the `Microdot` module for web development and creates an instance of the `Microdot` application. It also sets the default content type of the responses to HTML. The `system_state` variable is a dictionary that stores the current status (ON/OFF) of the water pump and air pump.

```python
def htmldoc(water_pump_status, air_pump_status):
    return f'''
        <html>
            <!-- HTML document structure -->
        </html>
    '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes buttons for toggling the status of the water pump and air pump. The status is determined by the `water_pump_status` and `air_pump_status` parameters.

```python
@app.route('/')
def control(request):
    return htmldoc(
        'ON' if system_state['water_pump'] else 'OFF',
        'ON' if system_state['air_pump'] else 'OFF'
    )

@app.route('/toggle/<component>')
def toggle(request, component):
    system_state[component] = not system_state[component]
    return htmldoc(
        'ON' if system_state['water_pump'] else 'OFF',
        'ON' if system_state['air_pump'] else 'OFF'
    )
```

The script defines two URL routes. The root route (`/`) displays the control interface. It calls the `htmldoc()` function, passing the current status of the water pump and air pump. The `/toggle/<component>` route is used to toggle the status of a component (water pump or air pump). It updates the corresponding value in the `system_state` dictionary and then calls `htmldoc()` to refresh the control interface.

```python
app.run(debug=True, port=8008)
```

The script runs the Microdot application, enabling the web server to listen on port 8008 and handle incoming requests.

**Note:** Remember to update the port number and other details if necessary when running the application.
