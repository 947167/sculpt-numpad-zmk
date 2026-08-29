# Microsoft Sculpt Ergonomic Numpad - ZMK Bluetooth Firmware

把微软Sculpt人体工学小键盘改装成蓝牙键盘，使用nice!nano (nRF52840)主控。

## 硬件连接

### 矩阵引脚映射（10针FPC -> nRF52840）

| FPC引脚 | nRF52840引脚 | 矩阵角色 |
|---------|-------------|---------|
| FPC1 | P0.31 | 行2 (ROW2) |
| FPC2 | P0.29 | 行4 (ROW4) |
| FPC3 | P0.02 | 列2 (COL2) |
| FPC4 | P1.15 | 行5 (ROW5) |
| FPC5 | P1.13 | 列0 (COL0) |
| FPC6 | P0.17 | 列3 (COL3) |
| FPC7 | P0.20 | 列1 (COL1) |
| FPC8 | P0.22 | 行1 (ROW1) |
| FPC9 | P0.24 | 行3 (ROW3) |
| FPC10 | P1.00 | 行0 (ROW0) |

### 键位矩阵（6行 x 4列）

```
行0: [NumLock] [Calculator] [Backspace] [  空  ]
行1: [Clear(C)] [    /    ] [    *    ] [   -   ]
行2: [   7   ] [   9   ] [   8   ] [   +   ]
行3: [   4   ] [   6   ] [  空  ] [   5   ]
行4: [   1   ] [   3   ] [   2   ] [ Enter  ]
行5: [  空  ] [  空  ] [   0   ] [   .   ]
```

## 编译固件

### 方法一：GitHub Actions（推荐，无需本地环境）

1. Fork或创建GitHub仓库，上传本目录所有文件
2. 推送代码到`main`分支，GitHub Actions会自动编译
3. 在Actions页面下载编译好的`nice_nano_v2_shield_sculpt_numpad-zmk.uf2`

### 方法二：本地编译

```bash
west init -l config
west update
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=sculpt_numpad -DZMK_CONFIG=$PWD/config
```

## 刷入固件

1. 双击nice!nano上的RESET按钮，进入UF2 bootloader模式
2. 电脑会出现一个U盘（NICENANO）
3. 把编译好的`.uf2`文件复制到U盘根目录
4. 板子自动重启，固件刷入完成

## 蓝牙配对

1. 刷入固件后，键盘会自动进入蓝牙配对模式（蓝灯闪烁）
2. 在电脑/手机的蓝牙设置中搜索并连接"Sculpt Numpad"
3. 配对成功后即可使用

## 层说明

- **Base层**：默认小键盘功能
- **FN层**：按住NumLock键激活，可切换蓝牙设备、切换输出模式（蓝牙/USB）
