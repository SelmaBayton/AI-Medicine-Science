# SVG Dice Roll

This Python script implements a web-based dice rolling game using SVG (Scalable Vector Graphics). It uses the Microdot framework for web development and the random module for generating random numbers and colors.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python dice_roll.py
   ```

3. Open a web browser and visit `http://localhost:8008` to play the dice rolling game.

## Code Explanation

The code consists of a web application that allows users to roll dice and view the results using SVG graphics.

```python
from microdot import Microdot, Response
import random

app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports the `Microdot` module for web development and the `random` module for generating random numbers and colors. It creates an instance of the `Microdot` application and sets the default content type of the responses to HTML.

```python
def random_color():
    return ''.join([random.choice('0123456789ABCDEF') for _ in range(6)])
```

The `random_color()` function generates a random hexadecimal color code.

```python
def htmldoc(dice_faces, background_colors):
    dice_faces_svg = {
        # SVG representations of dice faces
    }

    dice_svgs = ''
    for i in range(len(dice_faces)):
        x_offset = 220 * i
        dice_svgs += f'''
            <svg x="{x_offset}" width="200" height="200" viewBox="0 0 200 200">
                <rect x="10" y="10" width="180" height="180" rx="20" ry="20" fill="#{background_colors[i]}" />
                {dice_faces_svg[dice_faces[i]]}
            </svg>
        '''

    return f'''
        <html>
            <!-- HTML document structure -->
        </html>
    '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes SVG graphics for displaying dice faces and buttons for rolling different numbers of dice. The SVG graphics are created based on the provided dice faces and background colors.

```python
@app.route('/')
def home(request):
    return htmldoc([1], ['F0E68C'])
```

The root URL route displays the initial web page with one dice face and a specific background color.

```python
@app.route('/roll/<num_dice>')
def roll_dice(request, num_dice):
    num_dice = int(num_dice)
    dice_faces = [random.randint(1, 6) for _ in range(num_dice)]
    background_colors = [random_color() for _ in range(num_dice)]
    return htmldoc(dice_faces, background_colors)
```

The `/roll/<num_dice>` URL route handles the dice rolling functionality. It generates a specified number of dice faces and background colors using random numbers and the `random_color()` function. It then returns the updated web page with the new dice results.

```python
app.run(debug=True, port=8008)
```

The script runs the Microdot application, enabling the web server to listen on port 8008 and handle incoming requests.

Feel free to customize and enhance the code according to your needs!
