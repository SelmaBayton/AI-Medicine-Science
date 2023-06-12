# Aquaponics System Control

This Python script implements a web-based control interface for an aquaponics system using the Microdot framework. The control interface allows users to toggle system components and set system parameters. The system state and parameters are stored in a CSV file for persistence.

## Prerequisites

- Python 3.x
- microdot
- pandas

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot pandas
   ```

2. Prepare the CSV file:
   - Create a CSV file named `state.csv` in the same directory as the script.
   - Ensure the CSV file has the following columns: 'water_pump', 'air_pump', 'light', 'water_level', 'temperature', 'pH_level'.
   - Add a row with initial values for the system state and parameters.

3. Run the script by executing the following command:
   ```
   python aquaponics_control.py
   ```

4. Open a web browser and visit `http://localhost:8008` to access the control interface.

## Code Explanation

The code implements a web-based control interface for an aquaponics system using the Microdot framework and pandas library for data management.

```python
from microdot import Microdot, Response
import pandas as pd

app = Microdot()
Response.default_content_type = 'text/html'

CSV_FILE = 'state.csv'

# Initialize the DataFrame
system_df = pd.DataFrame([{
    'water_pump': 'OFF',
    'air_pump': 'OFF',
    'light': 'OFF',
    'water_level': '0',
    'temperature': '0',
    'pH_level': '0',
}])
```

The script imports the necessary modules: `Microdot` and `Response` from Microdot, and `pandas`. It also sets the default content type to 'text/html' for the responses. A CSV file named `state.csv` is defined as the storage for system state and parameters. The system state is initialized using a pandas DataFrame with default values.

```python
def load_state_from_csv():
    global system_df
    system_df = pd.read_csv(CSV_FILE)


def save_state_to_csv():
    system_df.to_csv(CSV_FILE, index=False)

def htmldoc(water_pump_status, air_pump_status, light_status, water_level, temperature, pH_level):
    # HTML template for the control interface
    ...
    return html_template

def generate_html_doc():
    load_state_from_csv()
    data = system_df.iloc[0]
    return htmldoc(
        data['water_pump'],
        data['air_pump'],
        data['light'],
        data['water_level'],
        data['temperature'],
        data['pH_level'],
    )
```

The script defines helper functions. `load_state_from_csv()` loads the system state and parameters from the CSV file into the DataFrame. `save_state_to_csv()` saves the current system state and parameters to the CSV file. `htmldoc()` generates an HTML document with the control interface based on the provided system state and parameters.

```python
@app.route('/')
def control(request):
    return generate_html_doc()

@app.route('/toggle/<component>')
def toggle(request, component):
    system_df.at[0, component] = 'ON' if system_df.at[0, component] == 'OFF' else 'OFF'
    save_state_to_csv()
    return generate_html_doc()

@app.route('/set_parameter/<parameter>/<value>')
def set_parameter(request, parameter, value):
    system
