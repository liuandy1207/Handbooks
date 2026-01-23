# <img src=https://www.zephyrproject.org/wp-content/uploads/2023/03/Zephyr_color-13.png width=75px> Zephyr Handbook

## Table of Contents
> ### [Basics](#basics) <br>

<br><br><br><br><br><br><br><br><br><br><br><br>
<hr>

## Basics
- Zephyr is a open-source real-time operating system (RTOS).
- Use Zephyr with 32-bit microcontrollers with at least 4kB of RAM. 
- Zephyr uses CMake to build projects and uses Kconfig to enable/disable software components.

### Set-Up
- Follow [this guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html) to install Zephyr locally. 
1. Run the following in the project directory:
```bash
west init -m https://github.com/zephyrproject-rtos/zephyr .
west update
```

### Activate a Python Virtual Environment
- Remember to re-activate the virtual environment when working on the Zephyr project. 
1. Run `python -m venv .venv`.
2. Run `source .venv/bin/activate`.
3. Run `pip install -r zephyr/scripts/requirements.txt`.

### Creating Application Directories
1. Run `west zephyr-export` to export Zephyr?
- Follow the following format for application directories:
  ```
  ZEPHYR_PROJECT/
  ├── app/
  │   ├── src/
  │   │   └── main.c          
  │   ├── prj.conf             
  │   └── CMakeLists.txt       
  └── ...                      
  ```

### Building Projects
- Zephyr projects must contain the following files:
  - `CMakeLists.txt`
  - `prj.conf`

1. Run `cd ./app` to change the working directory to the application directory.
2. Run `west build -p always -b BOARD_NAME` to build the project. <br>
   This should create a `build` directory.

### Boards
- `qemu_cortex_m3` is an emulated board (no hardware required). 

### Running a Built Project
1. Run `west build -t run` in the project directory. 

















