# Pymakr Handbook

1. In file explorer, make a project folder for the micropython code.
2. In the Pymaker panel, click Create Project and select that folder.
3. Connect your device.
4. In the Pymaker panel, click your project and select your device.
5. Connect to the device by selecting the lightning bolt icon.
6. Open device terminal by selecting the box with an arrow in it.
7. Open device file explorer by selecting the file icon.

When the ESP32 is reset, it looks for `boot.py` and then `main.py`

Right click files in File Explorer and go to pymakr > Upload to device to upload files.
do `machine.reset()` to get boot.py and main.py to run again
