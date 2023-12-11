## Function: `get_resource_path`

### Purpose
The `get_resource_path` function is designed to reliably find and return the absolute path of resources (like data files, images, icons, etc.) used by a Python application. This is crucial for applications that are packaged into a single executable file using tools like PyInstaller, as the way these resources are accessed changes once the application is compiled.

### Explanation
- **Python Scripts vs Compiled Executables**:
  - When running a Python script directly (e.g., `python myapp.py`), resources like images or data files are typically accessed based on the script's current directory.
  - However, when a script is compiled into a single executable file, these resources are packaged inside the executable. The executable, when run, extracts these resources to a temporary directory.

- **Handling Different Running Contexts**:
  - The function checks if the application is "frozen" (i.e., compiled into an executable) using `getattr(sys, 'frozen', False)`.
  - If the application is frozen, it uses the `_MEIPASS` attribute of the `sys` module, which is set by PyInstaller and points to the temporary directory where resources are unpackaged.
  - If the application is not frozen (i.e., running as a regular Python script), it uses the script's directory to locate resources.

- **Joining Paths**:
  - The function takes a relative path (e.g., `'data/config.txt'`, `'images/icon.ico'`) as an argument.
  - It then combines this relative path with the base path determined based on the execution context (frozen or unfrozen) using `os.path.join`. This ensures the correct absolute path is generated regardless of how the application is run.

### Usage
This function is particularly useful when you need to access external resources in your application, both during development and after compiling it into an executable. Use this function to generate the correct path to your resources, ensuring they are loaded correctly in all scenarios.
