# To-Do List

This Python script implements a simple web-based to-do list application. Users can add, complete/uncomplete, and delete tasks from the list. It uses the Microdot framework for web development.

## Prerequisites

- Python 3.x

## How to Run

1. Install the required dependencies by running the following command:
   ```
   pip install microdot
   ```

2. Run the script by executing the following command:
   ```
   python todo_list.py
   ```

3. Open a web browser and visit `http://localhost:8008` to access the to-do list application.

## Code Explanation

The code defines a web application that manages a to-do list.

```python
from microdot import Microdot, Response

app = Microdot()
Response.default_content_type = 'text/html'

todos = []
```

The script imports the `Microdot` module for web development and creates an instance of the `Microdot` application. It also sets the default content type of the responses to HTML. The `todos` variable is used to store the list of tasks.

```python
def htmldoc():
    todo_list = ''.join([f'<li>{todo[1]} - <a href="/toggle/{i}">{"Complete" if not todo[0] else "Uncomplete"}</a> - <a href="/delete/{i}">Delete</a></li>' for i, todo in enumerate(todos)])

    return f'''
        <html>
            <!-- HTML document structure -->
        </html>
    '''
```

The `htmldoc()` function generates an HTML document that represents the web page. It includes a form for adding new tasks, a list of existing tasks with options to complete/uncomplete and delete each task.

```python
@app.route('/', methods=['GET', 'POST'])
def home(request):
    if request.method == 'POST':
        todos.append([False, request.form.get('task')])
    return htmldoc()

@app.route('/add', methods=['POST'])
def add(request):
    todos.append([False, request.form.get('task')])
    return htmldoc()

@app.route('/toggle/<index>')
def toggle(request, index):
    todos[int(index)][0] = not todos[int(index)][0]
    return htmldoc()

@app.route('/delete/<index>')
def delete(request, index):
    todos.pop(int(index))
    return htmldoc()
```

The script defines several URL routes to handle different actions. The root route (`/`) handles both GET and POST requests. When a POST request is received, it adds a new task to the `todos` list. The `/add` route specifically handles the addition of tasks. The `/toggle/<index>` route toggles the completion status of a task based on the given index. The `/delete/<index>` route removes a task from the list based on the given index.

```python
app.run(debug=True, port=8008)
```

The script runs the Microdot application, enabling the web server to listen on port 8008 and handle incoming requests.

**Note:** Remember to update the port number and other details if necessary when running the application.
