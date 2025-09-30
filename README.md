# FT6X36 Touch Controller Library

Single-file C library for FT6X36 capacitive touch controllers.

## Setup

Copy `ft6x36.h` and `ft6x36.c` into your project.

Include the driver:
```c
#include "ft6x36.h"
```

Implement the necessary platform-specific functions:
```c
bool read_int_pin(void) {
    // Return INT pin state (active low)
}

void reset_chip(void) {
    // Reset the FT6X36 chip
}

void i2c_read(uint32_t addr, uint32_t reg, void *data, int len) {
    // I2C read implementation
}

void i2c_write(uint32_t addr, uint32_t reg, void *data, int len) {
    // I2C write implementation
}
```

Initialize the driver:
```c
// Initialize
FT6X36Config_t config = {
    .fnReadIntPin = read_int_pin,
    .fnResetChip = reset_chip,
    .fnSerialRead = i2c_read,
    .fnSerialWrite = i2c_write
};
ft6326_init(&config);
```

## Example Usage

You're now ready to start using the device:
```c
// Check for touches
if (ft6x36_touched()) {
    FT6X36Touchpoint_t touches[FT6X36_MAX_TOUCH_POINTS];
    int count = ft6x36_get_touches(touches);

    for (int i = 0; i < count; i++) {
        printf("Touch %d: x=%d, y=%d\n", i, touches[i].x, touches[i].y);
    }
}
```

## API

- `ft6326_init(config)` - Initialize the driver with platform callbacks
- `ft6x36_touched()` - Check if screen is touched
- `ft6x36_get_touches(array)` - Get touch coordinates and details
