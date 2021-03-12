# Simple WS2812 LED library for the Raspberry Pi Pico in C++

After not finding any libraries to address my WS2812, I took the sample code from the documentation and wrote a simple library based on it.

## Getting started

- Copy over the `WS2812.cpp`, `WS2812.hpp` and `WS2812.pio` files into your project
- Add `pico_generate_pio_header(YourProject ${CMAKE_CURRENT_LIST_DIR}/WS2812.pio)` to your `CMakeLists.txt` (Replacing `YourProject` with the name of your project, duh :D)
- Add the `WS2812.cpp` to your `add_executable` instruction of your `CMakeLists.txt`
- Make sure `hardware_pio` is included within the `target_link_libraries` instruction of your `CMakeLists.txt`
- Initialize a `WS2812`-Object with the desired parameters (see below for more details)
- Set the pixels values using `setPixelColor` or `fill`
- Send the pixel data to the LED strip using `show`

### Initialization

```
WS2812(uint pin, uint length, PIO pio, uint sm);
WS2812(uint pin, uint length, PIO pio, uint sm, DataFormat format);
WS2812(uint pin, uint length, PIO pio, uint sm, DataByte b1, DataByte b2, DataByte b3);
WS2812(uint pin, uint length, PIO pio, uint sm, DataByte b1, DataByte b2, DataByte b3, DataByte b4);
```

** Required: **
- pin: The GPIO-pin of the pico that is connected to the data line of your LED strip
- length: The number of LEDs in your strip
- pio: Either `pio0` or `pio1` representing one of the two PIO-Blocks available in the pico
- sm: The index of the state machine for interfacing with the led strip (0-3) which can only be used once per PIO-Block

** Optional simple: **
- format: One of `FORMAT_RGB`, `FORMAT_GRB` or `FORMAT_WRGB` depending on your LED strip. Default is `FORMAT_GRB`. If in doubt just try it out.

** Optional flexible: **
If none of the predefined formats matches your strip, you can define the byte order manually
- b1-b4: One of `RED`, `GREEN`, `BLUE`, `WHITE`

For example (GBR-Format):
```
WS2812 ledStrip(0, 6, pio0, 0, WS2812.GREEN, WS2812.BLUE, WS2812.RED);
```

### Example

For a quick start you can simply use this repository as a starting point. The `example.cpp` contains the entry point and the `CMakeLists.txt` is already configured properly. All you have to do is compile it and upload it to your Raspberry Pi Pico.