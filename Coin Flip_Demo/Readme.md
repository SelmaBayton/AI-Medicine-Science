# Coin Flip

This Python script demonstrates a simple web-based coin flip game. It uses the Microdot framework for web development.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python coin_flip.py
   ```

3. Open a web browser and visit `http://localhost:8008` to play the coin flip game.

## Code Explanation

The code consists of a simple web application that allows users to click a coin to flip it. The result of the coin flip (Heads or Tails) is displayed on the web page.

```python
from microdot import Microdot, Response
app = Microdot()
Response.default_content_type = 'text/html'
```

The script imports the `Microdot` module for web development and creates an instance of the `Microdot` application. It also sets the default content type of the responses to HTML.

```python
def htmldoc():
    coin_text = "Heads" if coin_state == 0 else "Tails"

    return f'''
        <html>
            <head>
                <title>Click to Flip Coin</title>
            </head>
            <body>
                <div>
                    <h1>Click the Coin to Flip</h1>
                    <svg width="200" height="200" viewBox="0 0 200 200">
                        <a href="/toggle">
                            <circle style="fill:#Dc5ccc" cx="100" cy="100" r="90"/>
                            <text x="50%" y="50%" font-size="24" text-anchor="middle" dy=".3em">{coin_text}</text>
                        </a>
                    </svg>
                </div>
            </body>
        </html>
        '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes an SVG element that displays a circle representing the coin and its current state (Heads or Tails). Clicking on the coin triggers a link that flips the coin when accessed.

```python
coin_state = 0
```

The `coin_state` variable represents the current state of the coin. It is initially set to 0, indicating Heads.

```python
@app.route('/')
def home(request):
    return htmldoc()

@app.route('/toggle')
def toggle_coin(request):
    global coin_state
    coin_state = 1 - coin_state
    return htmldoc()
```

The `@app.route()` decorators define the routes for the application. The `'/'` route is associated with the `home()` function, which returns the HTML document representing the initial state of the coin. The `'/toggle'` route is associated with the `toggle_coin()` function, which toggles the state of the coin and returns the updated HTML document.

```python
app.run(debug=True, port=8008)
```

The `app.run()` method starts the web application and listens on port 8008. Set the `debug` parameter to `True` for enabling debug mode.

## How to Play

1. Open a web browser and visit `http://localhost:8008`.

2. You will see a web page displaying a coin with the text "Click the Coin to Flip."

3. Click on the coin, and the state will toggle between Heads and Tails.

4. Each click on the coin will update the state accordingly.

Enjoy playing the coin flip
