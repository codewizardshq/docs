# Wizardlib

Here, you'll find the documentation for CodeWizardHQ's <em>Wizardlib</em> Python library. We use this library in the following courses:

|Elementary              | Middle School
|------------------------|--------------
|Python Game Development |Introduction to Programming with Python

<hr>





## add_audio()

<i>Adds an audio file.</i>

<hr>

Parameters:
- `add_audio(filename)`
- `filename` (`str`) : The filename.

Returns:

- The audio element.

Example usage:

```python
audio_element = add_audio("never-gonna-give-you-up.mp3")
```

<hr>





## add_background()

<i>Adds a background image.</i>

Parameters:
- `add_background(filename)`
- `filename` (`str`): The filename.

Example usage:

```python
add_background("flying-cats.png")
```

Example output:


<figure markdown>
![add_background() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/flying-cats.jpg?raw=true){ width="300" }
<figcaption></figcaption>
</figure>


<hr>





## add_background_audio()

<i>Adds background audio which plays when you click the *Start* button.</i>

Parameters:
- `add_background_audio(filename)`
- `filename` (`str`): The filename.

Example usage:

```python
add_background_audio("never-gonna-give-you-up.mp3")
```

<hr>




## add_button()

<i>Adds a button.</i>

Parameters:
- `add_button(text)`
- `text` (`str`): The text on the button.

Returns:

- The button element.

Example usage:

```python
button = add_button("Click Me")
```

Example output:

<figure markdown>
![add_button() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/button.png?raw=true){ width="200" }
<figcaption></figcaption>
</figure>

<hr>






## add_image()

<i>Adds an image to the page.</i>

Parameters:
- `add_image(filename, size)`
- `filename` (`str`): The filename.
- `size` (`int`): The size, in pixels (optional).

Returns:

- The image element.

Example usage:

```python
taco_image = add_image("taco.png")
```

Example output:

<figure markdown>
![add_image() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/taco.jpg?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## add_text()

<i>Adds text to the page.</i>

Parameters:
- `add_text(text, size)`
- `text` (`str`): The text to add to the page.
- `size` (`int`): The size, in pixels (optional, defaults to 18).

Returns:

- The text element.

Example usage:

```python
wizardlib_text = add_text("Wizardlib is cool!")
```

Example output:

<figure markdown>
![add_text() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/add-text-example.png?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>





## add_text_input()

<i>Adds a text input to the page.</i>

Parameters:
- `add_text_input(placeholder)`
- `placeholder` (`str`): The text to display in the input box.

Returns:

- The text input element.

Example usage:

```python
text_input = add_text_input("Enter your password:")
```

Example output:

<figure markdown>
![add_text_input() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/add-text-input-example.png?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## animate_down()

<i>Animates the `element` down by the given `distance`. Can optionally change the amount of time the animation takes and whether the `element` animates down and up repeatedly.</i>

Parameters:
- `animate_down(element, distance, time, loop)`
- `element` (`element`): An element to animate.
- `distance` (`int`): The distance the element should travel (in pixels).
- `time` (`int`): The amount of seconds the animation should take (optional, defaults to 8).
- `loop` (`bool`): Whether to repeatedly animate down and up (optional, defaults to `False`).


Example usage:

```python
taco_image = add_image("taco.jpg")
animate_down(taco_image, 100)
```

Example output:

<figure markdown>
![animate_down() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/animate-down.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## animate_left()

<i>Animates the `element` left by the given `distance`. Can optionally change the amount of time the animation takes and whether the `element` animates left and right repeatedly.</i>

Parameters:
- `animate_left(element, distance, time, loop)`
- `element` (`element`): An element to animate.
- `distance` (`int`): The distance the element should travel (in pixels).
- `time` (`int`): The amount of seconds the animation should take (optional, defaults to 8).
- `loop` (`bool`): Whether to repeatedly animate left and right (optional, defaults to `False`).


Example usage:

```python
taco_image = add_image("taco.jpg")
animate_left(taco_image, 100)
```

Example output:

<figure markdown>
![animate_left() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/animate-left.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## animate_right(element, distance, time, loop)

<i>Animates the `element` right by the given `distance`. Can optionally change the amount of time the animation takes and whether the `element` animates right and left repeatedly.</i>

Parameters:
- `animate_right(element, distance, time, loop)`
- `element` (`element`): An element to animate.
- `distance` (`int`): The distance the element should travel (in pixels).
- `time` (`int`): The amount of seconds the animation should take (optional, defaults to 8).
- `loop` (`bool`): Whether to repeatedly animate right and left (optional, defaults to `False`).

Example usage:

```python
taco_image = add_image("taco.jpg")
animate_right(taco_image, 100)
```

Example output:

<figure markdown>
![animate_right() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/animate-right.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>



## animate_up()

<i>Animates the `element` up by the given `distance`. Can optionally change the amount of time the animation takes and whether the `element` animates up and down repeatedly.</i>

Parameters:
- `animate_up(element, distance, time, loop)`
- `element` (`element`): An element to animate.
- `distance` (`int`): The distance the element should travel (in pixels).
- `time` (`int`): The amount of seconds the animation should take (optional, defaults to 8).
- `loop` (`bool`): Whether to repeatedly animate up and down (optional, defaults to `False`).


Example usage:

```python
taco_image = add_image("taco.jpg")
animate_up(taco_image, 100)
```

Example output:

<figure markdown>
![animate_up() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/animate-up.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## check_collision()

<i>If `element1` and `element2` collide, `function_to_run` is called.</i>

Parameters:
- `check_collision(element1, element2, function_to_run)`
- `element1` (`element`): An element to check for collisions with.
- `element2` (`element`): An element to check for collisions with.
- `function_to_run` (`function`): The function to run if `element1` hits `element2`.

Example usage:

```python
def cat_caught_taco():
    clear()
    text = add_text("The kitty caught the taco!")
    position_element(text, "center", "center")
    
    
def move(key):
    if key == "w":
        move_up(cat_image, 10)
    elif key == "a":
        move_left(cat_image, 10)
    elif key == "s":
        move_down(cat_image, 10)
    elif key == "d":
        move_right(cat_image, 10)
    
    
taco_image = add_image("taco.jpg", 100)
position_element(taco_image, "center", "center")

cat_image = add_image("flying-cats.jpg", 100)
position_element(cat_image, 700, 300)

keydown(move)

check_collision(taco_image, cat_image, cat_caught_taco)
```

Example output:

<figure markdown>
![check_collision() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/check-collision.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## clear()

<i>Clear the page of all elements.</i>

Example usage:

```python
def clear_page():
    clear()
    after_clear_text = add_text("Page was cleared", 32)
    position_element(after_clear_text, "center", "center")


before_clear_text = add_text("This is on the page before clearing", 32)
position_element(before_clear_text, "center", "center")

clear_page_button = add_button("Clear Page")
position_element(clear_page_button, "center", 400)

click(clear_page_button, clear_page)
```

Example output:

<figure markdown>
![clear() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/clear.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## click()

<i>Call `function_to_run` when `element` is clicked.</i>

Parameters:
- `click(element, function_to_run)`
- `element` (`element`): The element to click.
- `function_to_run` (`function`): The function to run if `element` is clicked.

Example usage:

```python
def show_text():
    text = add_text("Button was clicked!", 32)
    position_element(text, "center", "center")


button = add_button("Click Me")
position_element(button, "center", 400)

click(button, show_text)
```

Example output:

<figure markdown>
![click() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/click.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## fade_in()

<i>Fades the `element` from invisible to visible.</i>

Parameters:
- `fade_in(element)`
- `element` (`element`): The element to fade in.

Example usage:

```python
def fade_text_in():
    fade_in(hidden_text)


hidden_text = add_text("Hidden Text", 32)
position_element(hidden_text, "center", 400)
fade_out(hidden_text)

fade_in_button = add_button("Fade In")
position_element(fade_in_button, "center", "center")
click(fade_in_button, fade_text_in)
```

Example output:

<figure markdown>
![fade_in() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/fade-in.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## fade_out(element)

<i>Fades the `element` from visible to invisible.</i>

Parameters:
- `fade_out(element)`
- `element` (`element`): The element to fade out.

Example usage:

```python
def fade_text_out():
    fade_out(text_to_hide)


text_to_hide = add_text("Text To Hide", 32)
position_element(text_to_hide, "center", 400)

fade_out_button = add_button("Fade Out")
position_element(fade_out_button, "center", "center")
click(fade_out_button, fade_text_out)
```

Example output:

<figure markdown>
![fade_out() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/fade-out.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## get_input_value()

<i>Gets the value of the input `element`.</i>

Parameters:
- `get_input_value(element)`
- `element` (`element`): The element to get the value from.

Example usage:

```python
def login():
    password = get_input_value(password_input)
    clear()
    if password == "secretpassword":
        logged_in_text = add_text("You've logged in!", 32)
        position_element(logged_in_text, "center", 400)


password_input = add_text_input("Enter your password")
position_element(password_input, "center", 400)

login_button = add_button("Login")
position_element(login_button, "center", "center")
click(login_button, login)
```

Example output:

<figure markdown>
![get_input_value() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/get-input-value.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## keydown()

<i>Runs `function_to_run` when a key is pressed. The key that is pressed will be passed as the first argument to `function_to_run` and will always be lowercase.</i>

Parameters:
- `keydown(function_to_run)`
- `function_to_run` (`function`): The function to run when a key is pressed.

Example usage:

```python
def key_logger(pressed_key):
    update_text(last_key_pressed_text, f"Last key pressed: {pressed_key}")


last_key_pressed_text = add_text("Last key pressed: ", 32)
position_element(last_key_pressed_text, "center", 400)

keydown(key_logger)
```

Example output:

<figure markdown>
![keydown() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/keydown.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## move_down()

<i>Moves the `element` down by the given `distance`.</i>

Parameters:
- `move_down(element, distance)`
- `element` (`element`): The element to move down.
- `distance` (`int`): The distance the `element` should travel (in pixels).

Example usage:

```python
def move_taco(pressed_key):
    if pressed_key == "w":
        move_up(taco_image, 10)
    elif pressed_key == "a":
        move_left(taco_image, 10)
    elif pressed_key == "s":
        move_down(taco_image, 10)
    elif pressed_key == "d":
        move_right(taco_image, 10)


taco_image = add_image("taco.jpg", 100)
position_element(taco_image, "center", "center")

keydown(move_taco)
```

Example output:

<figure markdown>
![move_down() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/move-down.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## move_left()

<i>Moves the `element` left by the given `distance`.</i>

Parameters:
- `move_left(element, distance)`
- `element` (`element`): The element to move left.
- `distance` (`int`): The distance the `element` should travel (in pixels).

Example usage:

```python
def move_taco(pressed_key):
    if pressed_key == "w":
        move_up(taco_image, 10)
    elif pressed_key == "a":
        move_left(taco_image, 10)
    elif pressed_key == "s":
        move_down(taco_image, 10)
    elif pressed_key == "d":
        move_right(taco_image, 10)


taco_image = add_image("taco.jpg", 100)
position_element(taco_image, "center", "center")

keydown(move_taco)
```

Example output:

<figure markdown>
![move_left() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/move-left.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## move_right()

<i>Moves the `element` right by the given `distance`.</i>

Parameters:
- `move_right(element, distance)`
- `element` (`element`): The element to move right.
- `distance` (`int`): The distance the `element` should travel (in pixels).

Example usage:

```python
def move_taco(pressed_key):
    if pressed_key == "w":
        move_up(taco_image, 10)
    elif pressed_key == "a":
        move_left(taco_image, 10)
    elif pressed_key == "s":
        move_down(taco_image, 10)
    elif pressed_key == "d":
        move_right(taco_image, 10)


taco_image = add_image("taco.jpg", 100)
position_element(taco_image, "center", "center")

keydown(move_taco)
```

Example output:

<figure markdown>
![move_right() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/move-right.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## move_up()

<i>Moves the `element` up by the given `distance`.</i>

Parameters:
- `move_up(element, distance)`
- `element` (`element`): The element to move up.
- `distance` (`int`): The distance the `element` should travel (in pixels).

Example usage:

```python
def move_taco(pressed_key):
    if pressed_key == "w":
        move_up(taco_image, 10)
    elif pressed_key == "a":
        move_left(taco_image, 10)
    elif pressed_key == "s":
        move_down(taco_image, 10)
    elif pressed_key == "d":
        move_right(taco_image, 10)


taco_image = add_image("taco.jpg", 100)
position_element(taco_image, "center", "center")

keydown(move_taco)
```

Example output:

<figure markdown>
![move_up() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/move-up.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## play_audio()

<i>Plays the audio that `element` represents.</i>

Parameters:
- `play_audio(element)`
- `element` (`element`): The audio element to play.

Example usage:

```python
laugh_audio = add_audio("laugh.mp3")
play_audio(laugh_audio)
```

<hr>





## position_element()

<i>Position the `element` at the given `x` and `y` position. The `x` and `y` arguments can be any `int`, or one of the position helpers:</i>

|Position | Helper1  | Helper2    | Helper3    |
|---------|----------|------------|------------|
|`x`      | `"left"` | `"center"` | `"right"`  |
|`y`      | `"top"`  | `"center"` | `"bottom"` |

Parameters:
- `position_element(element, x, y)`
- `element` (`element`): The element to position.
- `x` (`int`|`str`): The desired x-position of the `element`.
- `y` (`int`|`str`): The desired y-position of the `element`.

Example usage:

```python
taco_image = add_image("taco.jpg")
position_element(taco_image, "center", 400)
```

<hr>




## set_background_color()

<i>Sets the background color of the page to `color`.</i>

Parameters:
- `set_background_color(color)`
- `color` (`str`): The desired background color.

Example usage:

```python
set_background_color("darksalmon")
```

Example output:

<figure markdown>
![set_background_color() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-background-color.png?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## set_element_width()

<i>Sets the `element` to the given `width`.</i>

Parameters:
- `set_element_width(element, width)`
- `element` (`element`): The element to adjust.
- `width` (`int`): The desired width of the `element`.

Example usage:

```python
def shrink_taco():
    set_element_width(taco_image, 100)


shrink_taco_button = add_button("Shrink Taco")
position_element(shrink_taco_button, "center", "center")

taco_image = add_image("taco.jpg", 300)
position_element(taco_image, "center", 200)

click(shrink_taco_button, shrink_taco)
```

Example output:

<figure markdown>
![set_element_width() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-element-width.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## set_font_size()

<i>Sets the font size of the `element` to the given `font_size`.</i>

Parameters:
- `set_font_size(element, font_size)`
- `element` (`element`): The element to adjust.
- `font_size` (`int`): The desired font_size of the `element`.

Example usage:

```python
def shrink_text():
    set_font_size(text_element, 25)


shrink_text_button = add_button("Shrink Font")
position_element(shrink_text_button, "center", "center")

text_element = add_text("Shrink this text!", 100)
position_element(text_element, "center", 300)

click(shrink_text_button, shrink_text)
```

Example output:

<figure markdown>
![set_font_size() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-font-size.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## set_text_color()

<i>Sets the `color` of the `text_element`.</i>

Parameters:
- `set_text_color(text_element, color)`
- `text_element` (`element`): The text element to adjust.
- `color` (`str`): The desired color of the `text_element`.

Example usage:

```python
red_text = add_text("This text is red", 32)
set_text_color(red_text, "red")
```

Example output:

<figure markdown>
![set_text_color() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-text-color.png?raw=true){ width="200" }
<figcaption></figcaption>
</figure>

<hr>




## set_text_decoration()

<i>Sets the text decoration of the given `text_element`.</i>

Parameters:
- `set_text_decoration(text_element, decoration_string)`
- `text_element` (`element`): The text element to adjust.
- `decoration_string` (`str`): The decoration string for the CSS property.

Example usage:

```python
text_element = add_text("Never Gonna Give You Up", 42)
set_text_decoration(text_element, "underline dotted blue")
```

Example output:

<figure markdown>
![set_text_decoration() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-text-decoration.png?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

Read about different options for the decoration_string [here](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration)

<hr>




## set_timeout()

<i>Runs `function_to_run` after `time` seconds.</i>

Parameters:
- `set_timeout(function_to_run, time)`
- `function_to_run` (`function`): The function to run.
- `time` (`int`): The time (in seconds) to wait before running the `function_to_run`.

Example usage:

```python
def show_boo_text():
    boo_text = add_text("BOO!!!", 100)
    position_element(boo_text, "center", 300)


set_timeout(show_boo_text, 3)
```

Example output:

<figure markdown>
![set_timeout() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/set-timeout.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## update_text()

<i>Changes the text in `text_element` to the `new_text`.</i>

Parameters:
- `update_text(text_element, new_text)`
- `text_element` (`element`): The element to adjust.
- `new_text` (`str`): The new text for the `text_element`.

Example usage:

```python
def update_text_element():
    update_text(text_element, "Updated text")


text_element = add_text("Original text", 32)
position_element(text_element, "center", 400)

update_text_button = add_button("Update Text")
position_element(update_text_button, "center", "center")

click(update_text_button, update_text_element)
```

Example output:

<figure markdown>
![update_text() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/update-text.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## remove_element()

<i>Removes the `element` from the page.</i>

Parameters:
- `remove_element(element)`
- `element` (`element`): The element to remove.

Example usage:

```python
def remove_taco():
    remove_element(taco_image)


taco_image = add_image("taco.jpg", 200)
position_element(taco_image, "center", 300)

remove_taco_button = add_button("Remove Taco")
position_element(remove_taco_button, "center", "center")

click(remove_taco_button, remove_taco)
```

Example output:

<figure markdown>
![remove_element() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/remove-element.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## rotate_element()

<i>Rotates the `element` by the given number of `degrees`.</i>

Parameters:
- `rotate_element(element, degrees)`
- `element` (`element`): The element to rotate.
- `degrees` (`int`): The number of degrees to rotate the `element`. 

Example usage:

```python
def rotate_taco():
    rotate_element(taco_image, 180)


taco_image = add_image("taco.jpg", 200)
position_element(taco_image, "center", 300)

rotate_taco_button = add_button("Rotate Taco")
position_element(rotate_taco_button, "center", "center")

click(rotate_taco_button, rotate_taco)
```

Example output:

<figure markdown>
![rotate_element() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/rotate-element.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>




## vanish()

<i>Removes the `element` from the page over a 1 second interval.</i>

Parameters:
- `vanish(element)`
- `element` (`element`): The element to remove.

Example usage:

```python
def vanish_taco():
    vanish(taco_image)


taco_image = add_image("taco.jpg", 200)
position_element(taco_image, "center", 300)

vanish_taco_button = add_button("Vanish Taco")
position_element(vanish_taco_button, "center", "center")

click(vanish_taco_button, vanish_taco)
```

Example output:

<figure markdown>
![vanish() example](https://github.com/codewizardshq/docs/blob/main/docs/assets/m11-wizardlib/vanish.gif?raw=true){ width="300" }
<figcaption></figcaption>
</figure>

<hr>
