import os
import random
import ctypes
import urllib.request
import tempfile
import tkinter as tk
from tkinter import messagebox, simpledialog, filedialog

# Default wallpaper folder - change this to your folder or keep empty to ask every time
LOCAL_WALLPAPER_FOLDER = r"C:\Users\YourUsername\Pictures\Wallpapers"

def set_wallpaper(image_path):
    SPI_SETDESKWALLPAPER = 20
    result = ctypes.windll.user32.SystemParametersInfoW(SPI_SETDESKWALLPAPER, 0, image_path, 3)
    if result:
        messagebox.showinfo("Success", f"Wallpaper set:\n{image_path}")
    else:
        messagebox.showerror("Error", "Failed to set wallpaper.")

def change_wallpaper_from_local():
    folder = filedialog.askdirectory(title="Select Wallpaper Folder", initialdir=LOCAL_WALLPAPER_FOLDER)
    if not folder:
        return
    images = [file for file in os.listdir(folder) if file.lower().endswith(('.jpg', '.jpeg', '.png', '.bmp'))]
    if not images:
        messagebox.showerror("Error", "No images found in the selected folder.")
        return
    chosen_image = random.choice(images)
    full_path = os.path.join(folder, chosen_image)
    set_wallpaper(full_path)

def change_wallpaper_from_web():
    url = simpledialog.askstring("Input", "Enter the full URL of the image (jpg, png, bmp):")
    if not url:
        return
    if not (url.lower().endswith('.jpg') or url.lower().endswith('.jpeg') or url.lower().endswith('.png') or url.lower().endswith('.bmp')):
        messagebox.showerror("Error", "URL must point to a JPG, PNG, or BMP image file.")
        return

    try:
        with urllib.request.urlopen(url) as response:
            img_data = response.read()

        # Save to temp file
        with tempfile.NamedTemporaryFile(delete=False, suffix=os.path.splitext(url)[1]) as tmp_file:
            tmp_file.write(img_data)
            tmp_path = tmp_file.name

        set_wallpaper(tmp_path)

    except Exception as e:
        messagebox.showerror("Error", f"Failed to download image:\n{e}")

def main():
    root = tk.Tk()
    root.title("Wallpaper Changer.exe")
    root.geometry("300x180")
    root.resizable(False, False)

    lbl = tk.Label(root, text="Choose wallpaper source:", font=("Arial", 14))
    lbl.pack(pady=10)

    btn_web = tk.Button(root, text="Choose from Web", width=20, command=change_wallpaper_from_web)
    btn_web.pack(pady=5)

    btn_local = tk.Button(root, text="Choose from Computer", width=20, command=change_wallpaper_from_local)
    btn_local.pack(pady=5)

    btn_exit = tk.Button(root, text="Exit", width=20, command=root.quit)
    btn_exit.pack(pady=10)

    root.mainloop()

if __name__ == "__main__":
    main()
