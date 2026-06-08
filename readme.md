# HAL_10_ADCMultiChannel

## 简介

本项目基于 STM32F103 系列 MCU 和 STM32 HAL 库，演示了 ADC1 的多通道扫描采样，并将多个通道的结果通过 OLED 屏幕显示。
项目采用 STM32CubeMX 生成的 CMake 构建配置，结合自定义 OLED 显示模块实现实时数据显示。

## 主要功能

- 初始化 STM32F103 HAL 外设、时钟和 GPIO
- 配置 ADC1 多通道扫描转换，支持 4 个模拟输入通道
- 启动 ADC 校准并使用软件触发进行多通道采样
- 依次读取 ADC1_IN0、ADC1_IN1、ADC1_IN3、ADC1_IN6
- 将每个通道的采样结果显示在 OLED 屏幕上

## 关键文件

- `CMakeLists.txt`：项目根 CMake 构建脚本
- `CMakePresets.json`：配置和构建预设，支持 `Debug` 和 `Release`
- `config.ioc`：STM32CubeMX 项目配置
- `Core/Src/main.c`：主程序入口，包含 ADC 启动、轮询读取与 OLED 显示逻辑
- `Core/Src/adc.c`：ADC1 初始化与多通道配置
- `Core/Inc/adc.h`：ADC 模块接口声明
- `Core/Src/OLED.c`：OLED 控制逻辑与软件 I2C 实现
- `Core/Inc/OLED.h`：OLED 功能接口声明
- `Core/Inc/OLED_Font.h`：OLED 字库数据
- `cmake/user_sources.cmake`：自定义源文件和 include 路径注册
- `Drivers/`：STM32 HAL 库源文件和 CMSIS 头文件

## 构建环境与依赖

- CMake 3.22 及以上
- Ninja 构建器
- ARM GCC 交叉编译器（例如 `arm-none-eabi-gcc`）
- STM32 HAL 库（包含在 `Drivers/` 目录中）

## 构建步骤

推荐使用 VS Code 的 CMake 工具或命令行：

```bash
cd d:/Electronics/HAL_Projects/HAL_10_ADCMultiChannel
cmake --preset Debug
cmake --build --preset Debug
```

## 运行与下载

1. 生成固件之后，使用 ST-Link 或其他支持的下载工具烧录生成的 ELF/HEX/BIN 文件到目标板。
2. 重新上电后，OLED 屏幕会显示各 ADC 通道的采样值。

## 硬件说明

- 目标 MCU：STM32F103 系列
- ADC1 多通道输入：
  - `ADC1_IN0`：PA0
  - `ADC1_IN1`：PA1
  - `ADC1_IN3`：PA3
  - `ADC1_IN6`：PA6
- OLED 软件 I2C 默认引脚：
  - `PB8`：SCL
  - `PB9`：SDA

## 许可

MIT License
