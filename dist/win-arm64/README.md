# UPX for Windows 11 on Arm64 (win-arm64)

This folder has a native **Windows Arm64 (AArch64)** build of UPX.
It runs on Windows 11 on Arm (Snapdragon X and other Arm64 PCs) with
no x64 emulation.

本目录提供 **原生 Windows Arm64 (AArch64)** 版 UPX 可执行文件，
可直接在 Windows 11 Arm64 设备上运行（无需 x64 模拟）。

| Item | Value |
|------|-------|
| File | `upx.exe` |
| UPX version | 5.3.1 (git `0d3ea26`) |
| Machine | `IMAGE_FILE_MACHINE_ARM64` (0xaa64), PE32+ console |
| Toolchain | llvm-mingw 20261104 (clang 23.1.5), UCRT, static C++ runtime |
| Runtime dependencies | only `KERNEL32.dll` + Universal CRT (`api-ms-win-crt-*`), both built into Windows 10/11 |
| SHA-256 | `0f768e22b26851b8deed88916aec5f1f0dae80c8f9bc802d8053210517a267e0` |

## Usage / 使用方法

```bat
upx.exe --version
upx.exe --best your-program.exe
upx.exe -t your-program.exe
upx.exe -d your-program.exe
```

The Arm64 build of UPX can pack all formats that UPX supports, including
`win64/arm64` (Arm64 PE), `win64/pe` (x64 PE) and `win32/pe` (x86 PE).

UPX 在 Arm64 上同样支持压缩 `win64/arm64`（Arm64 PE）、`win64/pe`（x64）、
`win32/pe`（x86）等所有 UPX 支持的格式。

## Rebuilding / 重新编译

This binary was cross-compiled on Linux. Run these commands from the
repository root:

```bash
git submodule update --init
# download llvm-mingw from https://github.com/mstorsjo/llvm-mingw/releases
export PATH=/path/to/llvm-mingw/bin:$PATH
make build/extra/cross-windows-arm64/release
# result: build/extra/cross-windows-arm64/release/upx.exe
llvm-strip build/extra/cross-windows-arm64/release/upx.exe
```

You can also build on the Windows Arm64 machine itself with Visual Studio 2022
(ARM64 tools) or llvm-mingw `aarch64`, using CMake:

```bat
cmake -S . -B build\release -A ARM64
cmake --build build\release --config Release
```

## License

UPX is distributed under the GNU GPL v2+ with a special exception.
See `COPYING` and `LICENSE`.
