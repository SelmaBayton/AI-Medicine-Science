# High Low Guessing Game

This Python script implements a simple web-based high-low number guessing game. It uses the Microdot framework for web development and the random module for generating random numbers.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python high_low_game.py
   ```

3. Open a web browser and visit `http://localhost:8008` to play the high-low number guessing game.

## Code Explanation

The code consists of a web application that allows users to guess a number between 1 and 100. The application provides feedback on each guess (whether it is too high, too low, or correct) and keeps track of the number of guesses.

```python
from microdot import Microdot, Response
import random

app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports the `Microdot` module for web development and the `random` module for generating random numbers. It creates an instance of the `Microdot` application and sets the default content type of the responses to HTML.

```python
def htmldoc(guesses, message, color):
    return f'''
        <html>
            <head>
                <title>High Low Guessing Game</title>
            </head>
            <body>
                <div>
                    <h1>High Low Guessing Game</h1>
                    <p>{message}</p>
                    <form method="post" action="/">
                        <label for="guess">Guess a number between 1 and 100:</label>
                        <input type="number" name="guess" id="guess" min="1" max="100" required>
                        <button type="submit">Submit</button>
                    </form>
                    <p>Guesses: {guesses}</p>
                    <svg width="100" height="100" viewBox="0 0 512 512">
                        <circle style="fill:#{color}" cx="255.995" cy="255.995" r="200"/>
                    </svg>
                    <form method="post" action="/new_game">
                        <button type="submit">New Game</button>
                    </form>
                </div>
            </body>
        </html>
        '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes a form for users to submit their guesses, a feedback message, the number of guesses made, and a colored circle visual representation based on the guess result.

```python
random_number = random.randint(1, 100)
guesses = 0
```

The `random_number` variable stores the randomly generated number between 1 and 100 that the user needs to guess. The `guesses` variable keeps track of the number of guesses made.

```python
@app.route('/', methods=['GET', 'POST'])
def home(request):
    global random_number, guesses

    if request.method == 'POST':
        guess = int(request.form.get('guess'))

        if guess < random_number:
            message = 'Too low!'
            color = '853737' # Red
        elif guess > random_number:
            message = 'Too high!'
            color = '907A4A' # Yellow
        else:
            message = 'Correct!'
            color = '4E7039' # Green

        guesses += 1

    else:
        message = '
