_This project has been created as part of the 42 curriculum by hamzarochd and Yahya Mouiguina._

# CUB3D - Raycasting Engine

![CUB3D Preview](textures/loading.png)

## Description

**CUB3D** is a 3D graphical representation project inspired by the classic Wolfenstein 3D game. This project implements a raycasting engine from scratch using the C programming language and the MLX42 graphics library.

### Goal

The primary objective of this project is to create a realistic 3D graphical representation of a maze from a first-person perspective using ray-casting principles. The project demonstrates: 

- Understanding of raycasting algorithms
- Efficient graphics rendering techniques
- Parsing and validation of scene configuration files
- Window management and event handling
- Mathematical concepts for 3D projection

### Features

**Mandatory Part:**
- Realistic 3D maze visualization using raycasting
- Textured walls with different textures for each cardinal direction (North, South, East, West)
- Configurable floor and ceiling colors
- Smooth player movement (W, A, S, D keys)
- Camera rotation (left/right arrow keys)
- Scene configuration parsing from `.cub` files
- Map validation and error handling

**Bonus Part:**
- Wall collisions
- Minimap system
- Doors that can open and close
- Animated sprites
- Mouse rotation
- Additional interactive features

## Dependencies

This project requires the following dependencies:

### Core Dependencies

| Dependency | Purpose | Required Version |
|------------|---------|------------------|
| **GCC/Clang** | C Compiler | Any recent version |
| **Make** | Build automation | GNU Make 3.81+ |
| **MLX42** | Graphics library | Included in repo |
| **GLFW** | Window & input handling | 3.3+ |
| **OpenGL** | Graphics rendering | 3.3+ |
| **pthread** | Threading support | POSIX standard |
| **libdl** | Dynamic linking | Standard |
| **libm** | Math library | Standard |

### System-Specific Installation

#### 🐧 Linux (Ubuntu/Debian)

```bash
# Update package list
sudo apt-get update

# Install compiler and build tools
sudo apt-get install build-essential

# Install GLFW and development libraries
sudo apt-get install libglfw3-dev

# Install X11 development libraries
sudo apt-get install xorg-dev

# Install OpenGL libraries
sudo apt-get install libgl1-mesa-dev

# Install additional dependencies
sudo apt-get install libc6-dev libpthread-stubs0-dev
```

#### 🐧 Linux (Fedora/RHEL/CentOS)

```bash
# Install development tools
sudo dnf groupinstall "Development Tools"

# Install GLFW
sudo dnf install glfw-devel

# Install Mesa OpenGL
sudo dnf install mesa-libGL-devel

# Install X11 libraries
sudo dnf install libX11-devel libXrandr-devel libXinerama-devel libXcursor-devel libXi-devel
```

#### 🐧 Linux (Arch)

```bash
# Install base development packages
sudo pacman -S base-devel

# Install GLFW and dependencies
sudo pacman -S glfw-x11

# Install Mesa
sudo pacman -S mesa
```

#### 🍎 macOS

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install GLFW
brew install glfw

# Install CMake (if needed)
brew install cmake

# Xcode Command Line Tools (if not installed)
xcode-select --install
```

**Note for macOS users:** Ensure you have Xcode Command Line Tools installed.  OpenGL comes pre-installed with macOS. 

### MLX42 Library

The **MLX42** library is already included in this repository as a static library (`libmlx42.a`). MLX42 is a modern, cross-platform graphics library that replaces the outdated MiniLibX. 

**MLX42 Features:**
- Cross-platform support (Linux, macOS)
- Built on top of OpenGL and GLFW
- Simple and intuitive API
- Better performance and stability

**MLX42 Repository:** [Codam-Coding-College/MLX42](https://github.com/Codam-Coding-College/MLX42)

### Verifying Installation

After installing dependencies, verify they are correctly installed: 

```bash
# Check GCC
gcc --version

# Check Make
make --version

# Check if GLFW is installed (Linux)
pkg-config --modversion glfw3

# Check OpenGL (Linux)
glxinfo | grep "OpenGL version"
```

## Instructions

### Compilation

To compile the **mandatory** part: 
```bash
make
```

To compile the **bonus** part:
```bash
make bonus
```

To clean object files:
```bash
make clean
```

To clean everything (object files and executables):
```bash
make fclean
```

To recompile: 
```bash
make re
```

### Compilation Flags

The project uses the following optimization and security flags:

```makefile
-funroll-loops          # Loop optimization
-O3                     # Maximum optimization
-ffast-math            # Fast math operations
-mavx2                 # AVX2 CPU instructions
-flto                  # Link-time optimization
-Wall -Wextra -Werror  # All warnings as errors
-fsanitize=address     # Memory leak detection
-g                     # Debug symbols
```

**Note:** If you encounter compilation issues, you can remove `-fsanitize=address` from the Makefile.

### Execution

Run the program with a valid `.cub` map file:

**Mandatory:**
```bash
./cub3D [path_to_map.cub]
```

**Bonus:**
```bash
./cub3D_bonus [path_to_map. cub]
```

**Example:**
```bash
./cub3D good/subject_map.cub
```

### Map Configuration

The `.cub` file defines the scene configuration with the following format:

```
NO [path_to_north_texture]
SO [path_to_south_texture]
WE [path_to_west_texture]
EA [path_to_east_texture]

F [R,G,B]  (Floor color)
C [R,G,B]  (Ceiling color)

[Map layout using characters]
```

**Map Characters:**
- `0` - Empty space
- `1` - Wall
- `N/S/E/W` - Player starting position and orientation
- `D` - Door (bonus only)

**Example maps are provided in:**
- `good/` - Valid map examples
- `bad/` - Invalid map examples (for testing error handling)

### Controls

**Movement:**
- `W` - Move forward
- `S` - Move backward
- `A` - Strafe left
- `D` - Strafe right

**Camera:**
- `←` (Left arrow) - Rotate camera left
- `→` (Right arrow) - Rotate camera right
- `Mouse` (bonus) - Rotate camera

**Actions (Bonus):**
- `Left Click` - Fire/Interact
- `R` - Reload (if applicable)
- `E` - Open/Close doors

**Exit:**
- `ESC` - Close the game
- Click the window close button

### Project Structure

```
CUB3D_RaycastingEngine/
├── mandatory/          # Mandatory part source files
│   ├── cub3d.h        # Main header file
│   ├── main.c         # Entry point
│   ├── parsing*. c     # Map and config parsing
│   ├── raycasting*.c  # Raycasting algorithms
│   ├── render. c       # Rendering engine
│   ├── hooks_setter.c # Event handlers
│   ├── collisions.c   # Collision detection
│   └── ...             # Other source files
├── bonus/             # Bonus part source files
│   ├── cub3d_bonus.h  # Bonus header file
│   ├── minimap_bonus.c # Minimap rendering
│   ├── door_handler_bonus.c # Door mechanics
│   ├── firing_bonus.c # Weapon mechanics
│   └── ...            # Other bonus features
├── textures/          # Wall texture files (. xpm, .png)
├── good/              # Valid test maps
├── bad/               # Invalid test maps
├── Makefile           # Build configuration
├── MLX42.h            # MLX42 library header
├── libmlx42.a         # MLX42 static library
└── README.md          # This file
```

## Troubleshooting

### Common Issues

**1. "GLFW not found" error**
```bash
# Linux
sudo apt-get install libglfw3-dev

# macOS
brew install glfw
```

**2. "undefined reference to `dlopen`"**
- Make sure `-ldl` is in your linker flags
- Already included in the Makefile

**3. "X11 libraries not found" (Linux)**
```bash
sudo apt-get install xorg-dev
```

**4.  Slow performance**
- Remove `-fsanitize=address` from CFLAGS in Makefile
- Ensure your graphics drivers are up to date

**5. Segmentation fault**
- Check your map file format
- Ensure all textures exist in the specified paths
- Run with address sanitizer enabled for debugging

## Resources

To learn more about raycasting and the concepts used in this project:

- [Lode's Computer Graphics Tutorial - Raycasting](https://lodev.org/cgtutor/raycasting.html)
- [Ray-Casting Tutorial For Game Development](https://permadi.com/1996/05/ray-casting-tutorial-table-of-contents/)
- [Wolfenstein 3D Wikipedia](https://en.wikipedia.org/wiki/Wolfenstein_3D)
- [MLX42 Documentation](https://github.com/codam-coding-college/MLX42)
- [GLFW Documentation](https://www.glfw.org/documentation.html)

## Author

**hamzarochd** - [GitHub Profile](https://github.com/hamzarochd)

---

_Project completed as part of the 42 School curriculum._
---

_Project completed as part of the 42 School curriculum._
