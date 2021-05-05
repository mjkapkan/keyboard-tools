## Author: M. Jaunius Kapkan
## Based on: https://github.com/moses-palmer/pynput/issues/170#issuecomment-602743287

from pynput import keyboard
import mouse

shift_off = True
 
def keyboard_listener():
    global listener
 
    def win32_event_filter(msg, data):
        global shift_off
        if msg == 256 and data.vkCode in [160,161]:
            shift_off = False
            listener._suppress = False
        elif msg == 257 and data.vkCode in [160,161]:
            shift_off = True
            listener._suppress = False
            
        elif msg == 256 and shift_off:
            if data.vkCode == 174:
                mouse.wheel(delta=-1)
                listener._suppress = True
            elif data.vkCode == 175:
                mouse.wheel(delta=1)
                listener._suppress = True
        else:
             listener._suppress = False
        return True
            
    return keyboard.Listener(
        win32_event_filter=win32_event_filter,
        suppress=False
    )

listener = keyboard_listener()

if __name__ == '__main__':
    with listener as ml:
        ml.join() 
