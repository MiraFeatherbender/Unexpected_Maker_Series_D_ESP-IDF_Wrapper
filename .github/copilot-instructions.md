
# Copilot Instructions for UMSeriesD ESP-IDF Wrapper Project

## Project Overview
- ESP-IDF project for ESP32-family chips, porting the Unexpected Maker Series D Arduino Helper library to ESP-IDF.
- Provides a C++ wrapper class (`UMSeriesD`) for board features, with a C core for low-level hardware access.
- Supports multiple UM Series D boards (EdgeS3[D], TinyS3[D], FeatherS3[D], ProS3[D]).
- Demonstrates blinking built-in RGB, blue, and external GPIO LEDs, and supports addressable LEDs (WS2812) via the [led_strip](https://components.espressif.com/component/espressif/led_strip) library.

## Key Files & Structure
- `main/examples/blink_example_main.cpp`: Main C++ example, demonstrates blinking various LEDs using the C++ wrapper.
- `main/examples/colorwheel.cpp`: C++ example, cycles the RGB LED through the color wheel.
- `main/src/UMSeriesD.hpp`: C++ wrapper class header (modernized from .h to .hpp).
- `main/src/UMSeriesD.cpp`: C++ wrapper class implementation, exposes a class interface matching the original Arduino library.
- `main/src/UMSeriesD_idf.h`: C helper header, provides low-level ESP-IDF functions.
- `main/src/UMSeriesD_idf.c`: C helper implementation, contains all hardware logic and board-specific code.
- `main/Kconfig.projbuild`: Project-specific Kconfig options (board type, LED type, GPIO, etc.).
- `Kconfig`: Root Kconfig, includes project configuration.
- `CMakeLists.txt` and `main/CMakeLists.txt`: ESP-IDF build setup.
- `main/idf_component.yml`: ESP-IDF component manager dependencies (e.g., led_strip).
- `sdkconfig*`: Project configuration files, generated/used by ESP-IDF.

## Usage Pattern
- Instantiate the C++ wrapper: `UMSeriesD ums3;`
- Initialize hardware: `ums3.begin();`
- Use wrapper methods to control LEDs, read sensors, etc. (e.g., `ums3.setPixelColor(r, g, b);`)
- All board-specific logic is handled in the C layer, with the C++ class providing a user-friendly interface.

## Build & Flash Workflow
- Set target chip: `idf.py set-target <chip_name>`
- Configure: `idf.py menuconfig` (choose board, LED type, GPIO, etc.)
- Build, flash, and monitor: `idf.py -p PORT flash monitor`
- Exit monitor: `Ctrl-]`

## Project Conventions & Patterns
- C++ wrapper (`UMSeriesD`) delegates to C functions for all hardware access.
- C++ header uses `.hpp` extension to distinguish from C headers.
- C and C++ code are kept in separate files for clarity and maintainability.
- Project uses ESP-IDF component manager for dependencies.
- Board, LED type, and example selection are configurable at build time via Kconfig.
- Logging via ESP-IDF's `ESP_LOG*` macros.
- Follows ESP-IDF minimal build pattern (`idf_build_set_property(MINIMAL_BUILD ON)`).

## Integration Points
- External: [led_strip](https://components.espressif.com/component/espressif/led_strip) library for addressable LEDs.
- Kconfig and CMake integration for flexible configuration and build.

## Examples
- To blink a regular LED: select `GPIO` in menuconfig, set `External GPIO number to blink`.
- To use an addressable LED strip: select `RBG LED` in menuconfig (TinyS3[D], FeatherS3[D], ProS3[D]).
- To use the blue LED: select `Blue LED` (FeatherS3[D] only).
- To run the color wheel demo: select `Color Wheel Example` in menuconfig.

## References
- See `README.md` for hardware requirements, usage details, and troubleshooting.
- For new features or components, follow the pattern in `main/src/` and update Kconfig/CMake as needed.

---

*Edit this file to update project-specific AI agent instructions. See https://aka.ms/vscode-instructions-docs for more info.*
