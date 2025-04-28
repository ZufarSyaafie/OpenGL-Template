# OpenGL Project Setup Guide

This README provides instructions for setting up and running the OpenGL project.

## Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [MinGW-w64](https://www.mingw-w64.org/) - Make sure it's installed at `C:/Program Files/mingw64/`
- Required libraries (already included in the project):
  - GLFW3
  - GLM
  - GLAD

## Project Structure

The project should have the following structure:

```
project/
├── include/
│   ├── glad/
│   ├── GLFW/
│   └── glm/
├── lib/
│   └── glfw3dll.lib
├── src/
│   ├── main.cpp
│   └── glad.c
├── .vscode/
│   └── tasks.json
└── README.md
```

## Building and Running

1. Open the project folder in Visual Studio Code
2. Press `Ctrl+Shift+B` to build the project
3. Run the generated `main.exe` file

## Modifying the Build Configuration

If you need to modify the build configuration in `tasks.json`, here's what each part does:

### Compiler Path

```json
"command": "C:/Program Files/mingw64/bin/g++.exe"
```

Change this if your g++ compiler is installed in a different location.

### Compiler Options

```json
"args": [
    "-g",                              // Enable debugging
    "-std=c++17",                      // Use C++17 standard
    "-mwindows",                       // Create Windows application (no console)
    "-I${workspaceFolder}/include",    // Include directory
    "-I${workspaceFolder}/include/glad",
    "-I${workspaceFolder}/include/GLFW",
    "-I${workspaceFolder}/include/glm",
    "-L${workspaceFolder}/lib",        // Library directory
    "${workspaceFolder}/src/main.cpp", // Source files
    "${workspaceFolder}/src/glad.c",
    "-lglfw3dll",                      // Link GLFW library
    "-lopengl32",                      // Link OpenGL library
    "-o",                              // Output file
    "${workspaceFolder}/main.exe"      // Output file path
]
```

### Common Modifications

1. **Adding source files**: Add more source files to the build by inserting additional paths after `"${workspaceFolder}/src/glad.c",`:

   ```json
   "${workspaceFolder}/src/main.cpp",
   "${workspaceFolder}/src/glad.c",
   "${workspaceFolder}/src/your_new_file.cpp",
   ```

2. **Adding libraries**: If you need to link additional libraries, add them with the `-l` prefix:

   ```json
   "-lglfw3dll",
   "-lopengl32",
   "-lyour_new_library",
   ```

3. **Adding include directories**: Add new include directories with the `-I` prefix:

   ```json
   "-I${workspaceFolder}/include/new_directory",
   ```

4. **Changing output file**: Modify the output executable name by changing:

   ```json
   "${workspaceFolder}/main.exe"
   ```

5. **Changing C++ standard**: If you need a different C++ standard, modify:
   ```json
   "-std=c++17"
   ```

## Runtime Requirements

Make sure the GLFW DLL file (`glfw3.dll`) is in the same directory as your executable or in your system PATH.

## Troubleshooting

1. **Compiler not found**: Ensure MinGW is installed at the specified path or update the path in `tasks.json`
2. **Missing libraries**: Verify that all required libraries are in the `lib` folder
3. **Missing includes**: Check that all header files are in the appropriate include directories
4. **Build fails**: Check the output console for specific error messages

For more help with OpenGL development, refer to resources like [LearnOpenGL](https://learnopengl.com/).
