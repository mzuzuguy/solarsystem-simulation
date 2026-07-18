# Solar System Simulation

A simple n-body gravity simulation built with C++ and SFML 3. The Sun and planets
attract each other using Newtonian gravity, and each body's orbit emerges from
real physics rather than a scripted animation.

## Features

- Real pairwise gravitational forces (`F = G·m₁·m₂ / d²`) applied to every body each frame
- Velocity/position integration via simple Euler stepping
- Starting velocities computed for roughly circular orbits (`v = √(GM/r)`)
- The Moon orbits the Earth (inheriting Earth's velocity plus its own orbital velocity), while the planets orbit the Sun
- Rendered in real time with SFML's 2D graphics API

## Requirements

- C++17 (or newer) compiler
- [SFML 3.x](https://www.sfml-dev.org/) (Graphics, Window, and System modules)
- CMake (recommended) or your preferred build setup

## Building

### Using g++ directly

```bash
g++ -std=c++17 solar_system.cpp -o solar_system \
    -lsfml-graphics -lsfml-window -lsfml-system
```

### Using CMake

```cmake
cmake_minimum_required(VERSION 3.16)
project(SolarSystem)

set(CMAKE_CXX_STANDARD 17)
find_package(SFML 3 COMPONENTS Graphics Window System REQUIRED)

add_executable(solar_system solar_system.cpp)
target_link_libraries(solar_system PRIVATE SFML::Graphics SFML::Window SFML::System)
```

```bash
mkdir build && cd build
cmake ..
cmake --build .
```

## Running

```bash
./solar_system
```

A window opens showing the Sun and planets orbiting under gravity. Close the
window to exit.

## Project Structure

```
.
├── solar_system.cpp   # Main simulation source
└── README.md
```

## Physics Notes

- `G` and `DT` (the gravitational constant and timestep) are tuned for visual
  clarity, not real-world units — the simulation is scaled to fit an 800×600
  window.
- Because forces are computed pairwise, orbits are **not** perfectly stable
  circles; you'll see gradual perturbation from other bodies' gravity, which
  is expected n-body behavior.

## Possible Improvements

- Spread initial planet angles around the Sun instead of stacking them vertically
- Add a fixed/variable timestep toggle for numerical stability at higher speeds
- Add trails to visualize orbital paths
- Add UI controls to adjust `G`, speed, or add/remove bodies at runtime
