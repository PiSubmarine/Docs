# WSL2 Windows Cross-Compilation

This setup uses WSL2 as the build environment while still producing `x64` Windows binaries.

## Why

Native Windows configure/build paths become very long in PiSubmarine because module names, dependency names and FetchContent directories are all descriptive. The new WSL2 preset keeps the source checkout where it is, but moves build and install directories into a short WSL path:

- `~/.cache/pisubmarine/build/<repo>/wsl2-windows-x64-debug`
- `~/.cache/pisubmarine/install/<repo>/wsl2-windows-x64-debug`

That removes the usual Windows path-length pressure during configure and build.

## Preset

Host-side modules now expose this configure preset:

- `wsl2-windows-x64-debug`

It uses:

- `x86_64-w64-mingw32-gcc`
- `x86_64-w64-mingw32-g++`
- `x86_64-w64-mingw32-windres`
- `VCPKG_TARGET_TRIPLET=x64-mingw-static`
- `VCPKG_HOST_TRIPLET=x64-linux`

## WSL2 setup

Run these commands inside your Ubuntu WSL2 distribution:

```bash
sudo apt update
sudo apt install -y build-essential cmake ninja-build pkg-config mingw-w64 zip unzip tar curl git

git clone https://github.com/microsoft/vcpkg.git "$HOME/vcpkg"
"$HOME/vcpkg/bootstrap-vcpkg.sh" -disableMetrics

echo 'export VCPKG_ROOT="$HOME/vcpkg"' >> "$HOME/.bashrc"
source "$HOME/.bashrc"
```

If `~/vcpkg` already exists, skip the clone and bootstrap steps.

Sanity-check the cross toolchain after installation:

```bash
which x86_64-w64-mingw32-gcc
which x86_64-w64-mingw32-g++
which x86_64-w64-mingw32-windres
```

All three commands should print paths under `/usr/bin/`.

## Using the preset

### CLion

Use a WSL toolchain, then select the `wsl2-windows-x64-debug` CMake preset.

### Visual Studio

Open the project through the WSL2 workflow and select the `wsl2-windows-x64-debug` preset.

### Command line inside WSL2

From a module repository:

```bash
cmake --preset wsl2-windows-x64-debug
cmake --build ~/.cache/pisubmarine/build/$(basename "$PWD")/wsl2-windows-x64-debug
```

## Tests

Cross-compiled Windows test executables cannot run directly inside Linux.

To avoid build failures during test discovery, module tests now use `gtest_add_tests(...)` when `CMAKE_CROSSCOMPILING` is enabled. That allows the build to finish, but actually running the tests still requires one of these:

- a native Windows build
- Wine
- another Windows-side execution step

## Notes

- This setup targets Windows through MinGW, not MSVC.
- If you need ABI compatibility with MSVC-built libraries or Windows-only vendor SDKs, keep using the native Windows presets for those modules.
- If `vcpkg` reports `/usr/bin/cc` or `/usr/bin/c++` while configuring an `x64-mingw-static` port, the MinGW cross-compiler is not installed or not visible in `PATH` inside WSL.
