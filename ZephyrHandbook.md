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
- When you build an application, Zephyr looks for a DeviceTree Source (DTS) source file that matches the specified board. 
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






<br>
<hr>

## DeviceTree
- DeviceTree is a tree data structure used to describe hardware.
- DeviceTree files use DeviceTree Source (DTS) format.
  - DeviceTree **bindings** for Zephyr replace the DTS format with `,yaml`.
- Zephyr uses CMake to process DeviceTree files and generate C macros for the application.

### Nodes
- Each node in a DeviceTree describes one device.
- Each node has exactly one parent node (except for the root node).
- Each node can be uniquely identified by specifying the full path (with `/`) from the root node, through all subnodes, to the desired node. 
```c
// Define an empty tree?
/dts-v1/;                  // required for Zephyr 
/ { };                     // root node is defined by forward slash /

// Define a general tree?
/dts-v1/;
/ {                        // root node
  NODE {
    NODE_PROPERTIES
    ...
    SUBNODE {
      SUBNODE_PROPERTIES
      ...
    };
  };
};

```

#### Properties
- Property names follow `kebab-case` and can contain alphanumeric characters and the special characters `.,_+?#-`.
```c
// Define different types of properties?
/dts-v1/;
/ {
  PROPERTIES {
    BOOLEAN;                                    // a property with no value is a boolean => true if it exists, false otherwise
    STRING = "STRING"                           // C-string literal => double-quoted, null-terminated
    INT = <INTEGER>                             // single 32-bit integer cell
    ARRAY = <ELEMENT1, ELEMENT2, ...>           // 32-bit integer cells, use the prefix 0x for hexadecimal values
    UINT8_ARRAY = [ ELEMENT1 ELEMENT2 ... ]      // 8-bit hexadecimal values (optionally) separated by spaces, use hexadecimal literals (DO NOT USE A PREFIX)
    STRING_ARRAY = "STRING1", "STRING2", ...    // comma-separated list of strings
  };
};

```
















