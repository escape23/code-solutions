#Tutorial for beginners
## Introduction
In this tutorial, we will create a simple calculator GUI using the Tkinter library in Python. Tkinter is a popular GUI toolkit for creating desktop applications.

The calculator will have the following features: - Display area to show the current input and result - Buttons for numbers (0-9), decimal point, and basic arithmetic operations (+, -, *, /) - Clear (C) button to clear the current input or result - Equal (=) button to calculate and display the result

Let's get started!

##How To Make a Python Calculator

## Step One
### Choose a text editor
1. I like to use visual studio code as my text editor. You can download it [here](https://code.visualstudio.com/download). you can also use other text editors, such as PyCharm or others.
2. if you are using visual studio code, you can install the python extension.
3. if you are using other text editors, make sure you have python installed. [install](https://www.python.org/downloads/).

## Step Two
### Create a file

1. Create a new file in the text editor and call it main.py.
### Libraries
2. write the code below in the file:
```python
import tkinter as tk
from tkinter import ttk
```
tkinter is the standard Python library for building GUIs. It is imported as tk.

ttk is a submodule of tkinter that provides themed widgets like buttons, labels, and entry fields, giving a modern look to the application.

### Functions

3. Lets define our first function: 
```python
    def handle_button_click(clicked_button_text):
        current_text = result_var.get()
```
this function is the core function that handles the logic of the calculator when a button is clicked. for example, if the user clicks the 7 button, the function will return the text 7.

```python
expression = current_text.replace("÷", "/").replace("x", "*")
result = eval(expression)
```

This code is used to convert the text to a mathematical expression.

The eval function is used to evaluate the mathematical expression.

```python
 if result.is_integer():
                result = int(result)
```
This code checks if the result is an integer. If it is, it is converted to an integer.

```python
result_var.set(result)
        except Exception as e:
            result_var.set("Error")
    elif clicked_button_text == "C":
        result_var.set("")
    elif clicked_button_text == "%":
        try:
            current_number = float(current_text)
            result_var.set(current_number / 100)
        except ValueError:
            result_var.set("Error")
```	

This portion of the code is part of the handle_button_click() function, and it handles specific actions for different calculator buttons: the =, C, and % buttons.

```python
elif clicked_button_text == "±":
        try:
            current_number = float(current_text)
            result_var.set(-current_number)
        except ValueError:
            result_var.set("Error")
    else:
        result_var.set(current_text + clicked_button_text)
```

This portion of the code is also part of the handle_button_click() function, and it handles the ± button.
### Main Window
```python	
root = tk.Tk()
root.title("Calculator")

root.configure(bg="Black")

result_var = tk.StringVar()
result_entry = ttk.Entry(root, textvariable=result_var, font=("Helvetica", 24), justify="right")
result_entry.grid(row=0, column=0, columnspan=4, sticky="nsew")
```	

`root = tk.Tk()`: Initializes the main application window for the calculator.

`root.title("Calculator")`: Sets the window's title to "Calculator".

`root.configure(bg="Black")`: Sets the background color of the window to black.

`result_var = tk.StringVar()`: Creates a string variable to store and update the text displayed in the calculator's result area.

`result_entry = ttk.Entry(root, textvariable=result_var, font=("Helvetica", 24), justify="right")`: Creates a text entry field (where results and expressions will be shown) with:
Large Helvetica font size (24) for better readability.
Right-aligned text, similar to typical calculator displays.

`result_entry.grid(row=0, column=0, columnspan=4, sticky="nsew")`: Positions the entry field at the top of the grid, spanning 4 columns and expanding to fit the available space. 

This section sets up the main window and the display area for the calculator.
### Buttons
```python
buttons = [
    ("C", 1, 0), ("±", 1, 1), ("%", 1, 2), ("÷", 1, 3),
    ("7", 2, 0), ("8", 2, 1), ("9", 2, 2), ("x", 2, 3),
    ("4", 3, 0), ("5", 3, 1), ("6", 3, 2), ("-", 3, 3),
    ("1", 4, 0), ("2", 4, 1), ("3", 4, 2), ("+", 4, 3),
    ("0", 5, 0, 2), (".", 5, 2), ("=", 5, 3)
]
```	
The `buttons` variable is a list that defines the layout and properties of the calculator buttons. Each group in the list represents a button and contains the following information:

1. Button text (e.g., "C", "7", "+")
2. Row position in the grid
3. Column position in the grid
4. (Optional) Column span for wider buttons

For example, `("C", 1, 0)` means:
- The button shows "C"
- It's in row 1
- It's in column 0

This list helps us create and position all the buttons in the calculator's layout, making it easy to change the design or add new buttons if needed.
## Step 3
### Visual Styling
```python
style = ttk.Style()

style.configure("TButton", font=("Helvetica", 16), background="Black", foreground="black", width=10, height=4)

style.configure("TEntry", fieldbackground="Black", foreground="black")
```	

These lines set up the visual style of the calculator:

`style = ttk.Style():` Creates a style object to customize the appearance of widgets.

`style.configure("TButton", ...):` Configures the style for buttons:
Sets the font to Helvetica with size 16
Sets the background and text color to black
Sets a default width and height for the buttons

`style.configure("TEntry", ...):` Configures the style for the entry field:
Sets the background and text color to black
    
```python
for button_info in buttons:
    button_text, row, col = button_info[:3]
    colspan = button_info[3] if len(button_info) > 3 else 1
    button = ttk.Button(root, text=button_text, command=lambda text=button_text: handle_button_click(text), style="TButton")
    button.grid(row=row, column=col, columnspan=colspan, sticky="nsew", ipadx=10, ipady=4, padx=5, pady=5)
```	
This code creates and positions all the calculator buttons:

It loops through each button's information in the buttons list.

For each button, it extracts the text, row, and column position.

It determines if the button should span multiple columns (for wider buttons like '0').

It creates a button widget with the appropriate text and assigns it the click handling function.

Finally, it places the button in the calculator's grid layout with specific positioning and spacing.

```python
for i in range(6):
    root.grid_rowconfigure(i, weight=1)
for i in range(4):
    root.grid_columnconfigure(i, weight=1)
```
The first loop sets up 6 rows in the grid:
It gives each row equal importance (weight=1)
This ensures that all rows will expand equally if the window is resized.

The second loop sets up 4 columns in the grid:
It gives each column equal importance (weight=1)
This ensures that all columns will expand equally if the window is resized.  
### Calculator Window Size
```python	
width = 500
height = 700
root.geometry(f"{width}x{height}")

root.resizable(False, False)
```	
`width = 500`and `height = 700`: 
Defines the initial dimensions of the calculator window in pixels.

`root.geometry(f"{width}x{height}")`: 
Sets the calculator window's size to 500 pixels wide and 700 pixels tall.

`root.resizable(False, False)`: 
Prevents the user from resizing the window.
The first False disables horizontal resizing, the second disables vertical resizing.
### Keyboard Shortcuts
```python
root.bind("<Return>", lambda event: handle_button_click("="))
root.bind("<BackSpace>", lambda event: handle_button_click("C"))
```
These lines add keyboard shortcuts to the calculator:

`root.bind("<Return>", lambda event: handle_button_click("="))`:
Binds the Enter key to act as if the "=" button was clicked.
When the user presses Enter, it calculates and displays the result.

`root.bind("<BackSpace>", lambda event: handle_button_click("C"))`:
Binds the Backspace key to act as if the "C" (Clear) button was clicked.
When the user presses Backspace, it clears the current input or result.
### Calculator Comes To Life!
```python
root.mainloop()
```	
This line makes your calculator come to life and stay active until you close the window.

## This is how the code should look like:
```python	
import tkinter as tk
from tkinter import ttk

def handle_button_click(clicked_button_text):
    current_text = result_var.get()

    if clicked_button_text == "=":
        try:

            expression = current_text.replace("÷", "/").replace("x", "*")
            result = eval(expression)

            if result.is_integer():
                result = int(result)

            result_var.set(result)
        except Exception as e:
            result_var.set("Error")
    elif clicked_button_text == "C":
        result_var.set("")
    elif clicked_button_text == "%":
        try:
            current_number = float(current_text)
            result_var.set(current_number / 100)
        except ValueError:
            result_var.set("Error")
    elif clicked_button_text == "±":
        try:
            current_number = float(current_text)
            result_var.set(-current_number)
        except ValueError:
            result_var.set("Error")
    else:
        result_var.set(current_text + clicked_button_text)


root = tk.Tk()
root.title("Calculator")


root.configure(bg="Black")

result_var = tk.StringVar()
result_entry = ttk.Entry(root, textvariable=result_var, font=("Helvetica", 24), justify="right")
result_entry.grid(row=0, column=0, columnspan=4, sticky="nsew")

buttons = [
    ("C", 1, 0), ("±", 1, 1), ("%", 1, 2), ("÷", 1, 3),
    ("7", 2, 0), ("8", 2, 1), ("9", 2, 2), ("x", 2, 3),
    ("4", 3, 0), ("5", 3, 1), ("6", 3, 2), ("-", 3, 3),
    ("1", 4, 0), ("2", 4, 1), ("3", 4, 2), ("+", 4, 3),
    ("0", 5, 0, 2), (".", 5, 2), ("=", 5, 3)
]


style = ttk.Style()


style.configure("TButton", font=("Helvetica", 16), background="Black", foreground="black", width=10, height=4)


style.configure("TEntry", fieldbackground="Black", foreground="black")

for button_info in buttons:
    button_text, row, col = button_info[:3]
    colspan = button_info[3] if len(button_info) > 3 else 1
    button = ttk.Button(root, text=button_text, command=lambda text=button_text: handle_button_click(text), style="TButton")
    button.grid(row=row, column=col, columnspan=colspan, sticky="nsew", ipadx=10, ipady=4, padx=5, pady=5)

for i in range(6):
    root.grid_rowconfigure(i, weight=1)
for i in range(4):
    root.grid_columnconfigure(i, weight=1)

width = 500
height = 700
root.geometry(f"{width}x{height}")

root.resizable(False, False)

root.bind("<Return>", lambda event: handle_button_click("="))
root.bind("<BackSpace>", lambda event: handle_button_click("C"))

root.mainloop()
```	
