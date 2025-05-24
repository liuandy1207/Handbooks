# <img src=https://www.zephyrproject.org/wp-content/uploads/2023/03/Zephyr_color-13.png width=75px> Zephyr Handbook

## Table of Contents
> ### [Basics](#basics) <br>
>> [Initialization](#initialization) <br>
>> [Building](#building) <br>
>>> [Boards](#boards) <br>
>> [Project Directory Structure](#project-directory-structure) <br>


<br><br><br><br><br><br><br><br><br><br><br><br>
<hr>

## Basics

### Initialization
1. Go to the project directory and open terminal.
2. Initialize Zephyr:
```bash
west init -m https://github.com/zephyrproject-rtos/zephyr .
west update
```
3. Initialize Python virtual environment:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r zephyr/scripts/requirements.txt
```
- Remember to re-activate the virtual environment when working on the project.
4. Export Zephyr
```bash
west zephyr-export
```
5. Create an application directory and main source code in the project directory as shown:
```
ZEPHYR_PROJECT/
├── app/
│   ├── src/
│   │   └── main.c          
│   ├── prj.conf             
│   └── CMakeLists.txt       
└── ...                      
```

### Building
1. Change directory to `app/`:
```bash
cd app/
```
2. Build the application using west:
```bash
west build -b BOARD_NAME .
```

#### Boards
- `qemu_cortex_m3` is an emulated board (no hardware required). 

### Running
```bash
west build -t run
```

### Project Directory Structure
```
ZEPHYR_PROJECT/
├── app/
│   ├── src/
│   │   └── main.c           
│   ├── prj.conf            
│   └── CMakeLists.txt      
├── .west/
├── zephyr/         
├── modules/          
├── tools/                
├── bootloader/   
├── scripts/           
├── .venv/      
├── build/          
├── west.yml         
└── CMakeLists.txt         
```









