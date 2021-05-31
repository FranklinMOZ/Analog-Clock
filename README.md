# Analog-Clock
# This creates a window where the clock will be displayed
import tkinter as ui
import time
import math

window = ui.Tk()
window.geometry("1129x1122")
# The lines below tell the clock what time it is, the position of the hands, and rotation.
def update_clock():
    hours = int(time.strftime("%I"))
    minutes = int(time.strftime("%M"))
    seconds = int(time.strftime("%S"))
    # Below moves the hands and repositions following the formula for each hand. 360 degrees/60 secs = 6 radians
    seconds_x = seconds_hand_len * math.sin(math.radians(seconds * 6)) + center_x
    seconds_y = -1 * seconds_hand_len * math.cos(math.radians(seconds * 6)) + center_y
    canvas.coords(seconds_hand, center_x, center_y, seconds_x, seconds_y)

    minutes_x = minutes_hand_len * math.sin(math.radians(minutes * 6)) + center_x
    minutes_y = -1 * minutes_hand_len * math.cos(math.radians(minutes * 6)) + center_y
    canvas.coords(minutes_hand, center_x, center_y, minutes_x, minutes_y)

    hours_x = hours_hand_len * math.sin(math.radians(hours * 30)) + center_x
    hours_y = -1 * hours_hand_len * math.cos(math.radians(hours * 30)) + center_y
    canvas.coords(hours_hand, center_x, center_y, hours_x, hours_y)

    window.after(1000, update_clock)

canvas = ui.Canvas(window, width=1129, height=1122)
canvas.pack(expand=True, fill='both')

# This is the background or the numbers
bg = ui.PhotoImage(file='Clock - nohands.gray.PNG')
canvas.create_image(560, 550, image=bg)

# Below are the hands of the clock, the center position of all the hands, measurements of each hand.
center_x = 560
center_y = 550
seconds_hand_len = 300
minutes_hand_len = 260
hours_hand_len = 200

seconds_hand = canvas.create_line(560, 550,
                                   560 + seconds_hand_len, 550 + seconds_hand_len,
                                   width=1.8, fill='red')

minutes_hand = canvas.create_line(560, 550,
                                  560 + minutes_hand_len, 550 + minutes_hand_len,
                                  width=4, fill='white')

hours_hand = canvas.create_line(560, 550,
                                560 + hours_hand_len, 550 + hours_hand_len,
                                width=8, fill='white')


update_clock()
window.mainloop()
