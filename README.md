# pisugar-power-manager-rs

<img src="https://travis-ci.com/PiSugar/pisugar-power-manager-rs.svg?branch=master">

<p align="center">
  <img width="320" src="https://raw.githubusercontent.com/JdaieLin/PiSugar/master/logo.jpg">
</p>

## Management program for PiSugar 2

PiSugar power manager in rust language.

## Enable I2C interface

On raspberry pi

    sudo raspi-config

`Interfacing Options -> I2C -> Yes`

## Compilation

CPU architecture of raspberry pi is different from your linux/windows PC or macbook, there are two ways of compiling the code:

1. directly on raspberry pi
2. cross compilation

If you need more about rust cross compilation, please refer to https://dev.to/h_ajsf/cross-compiling-rust-for-raspberry-pi-4iai .

### On raspberry pi

Install rust

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    rustup update

Build

    cargo build --release

### Cross compilation - macos

Install cross compiler utils

    brew install FiloSottile/musl-cross/musl-cross --without-x86_64 --with-arm-hf

Install rust and armv6(zero/zerow) or armv7(3b/3b+) target

    brew install rustup-init
    rustup update
    rustup target add arm-unknown-linux-musleabihf      # armv6
    rustup target add armv7-unknown-linux-musleabihf    # armv7

Build

    cargo build --target arm-unknown-linux-musleabihf --release     # armv6
    cargo build --target armv7-unknown-linux-musleabihf --release   # armv7

### Cross compilation - linux/ubuntu

Install cross compiler utils

    sudo apt-get install gcc-arm-linux-gnueabihf

Install rust and arm/armv7 target

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    rustup update
    rustup target add arm-unknown-linux-gnueabihf       # armv6
    rustup target add armv7-unknown-linux-gnueabihf     # armv7

Build

    cargo build --target arm-unknown-linux-gnueabihf --release      # armv6
    cargo build --target armv7-unknown-linux-gnueabihf --release    # armv7

### Cross compilation - windows

Get cross toolchains from https://gnutoolchains.com/raspberry/

Install rust, please refer to https://forge.rust-lang.org/infra/other-installation-methods.html

### RLS

RLS configuration of vscode `.vscode/settings.json`

    {
        "rust.target": "arm-unknown-linux-gnueabihf"
    }

### Unix Domain Socket / Webscoket

| Command | Description | Response/Usage |
| :- | :-: | :-: |
| get battery             | battery level % | battery: [number] |
| get battery_i           | BAT current in A | battery_i: [number] |
| get battery_v           | BAT votage in V | battery_v: [number] |
| get battery_charging    | charging status  | battery_charging: [true\|false] |
| get model               | pisugar model | model: PiSugar 2 |
| get rtc_time            | rtc clock | rtc_time: [ISO8601 time string] |
| get rtc_alarm_enabled   | rtc wakeup alarm enable | rtc_alarm_enabled: [true\|false] |
| get rtc_alarm_time      | rtc wakeup alarm time | rtc_alarm_time: [ISO8601 time string] |
| get alarm_repeat        | rtc wakeup alarm repeat in weekdays (127=1111111) | alarm_repeat: [number] |
| get button_enable       | custom button enable status | button_enable: [single\|double\|long] [true\|false] |
| get button_shell        | shell script when button is clicked  | button_shell: [single\|double\|long] [shell] |
| get safe_shutdown_level | auto shutdown level | safe_shutdown_level: [number] |
| rtc_pi2rtc | sync time pi => rtc | |
| rtc_rtc2pi | sync time rtc => pi | |
| rtc_web | sync time web => rtc & pi | |
| rtc_alarm_set | set rtc wakeup alarm | rtc_alarm_set: [ISO8601 time string] [repeat] |
| rtc_alarm_disable | disable rtc wakeup alarm | |
| set_button_enable | auto shutdown level % | set_button_enable: [single\|double\|long] [0|1] |
| set_button_shell | auto shutdown level | safe_shutdown_level: [single\|double\|long] [shell] |
| set_safe_shutdown_level | set auto shutdown level % | safe_shutdown_level: 3 |

## LICENSE

GPL v3
