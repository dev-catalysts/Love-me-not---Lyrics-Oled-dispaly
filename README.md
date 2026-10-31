# ESP32 OLED Lyrics Visualizer

Two song projects for an ESP32 and a 0.96" SSD1306 OLED:

| Folder | What it does |
|--------|--------------|
| `love-me-not/` | Plays a pre-converted lyrics video (247 frames) on the OLED |
| `dracula-song/` | Draws synced lyrics live, with 9 animations, text effects and 4 reactive LEDs |

## Demo

Add your Instagram reel links, GIFs or photos of the build here.

## Hardware

| Part | Used in |
|------|---------|
| ESP32 Dev Module (38-pin) | both |
| 0.96" OLED, SSD1306, 128x64, I2C | both |
| 4x LEDs + 4x 220 ohm resistors | `dracula-song` only |
| Breadboard + jumper wires | both |

## Wiring

| OLED | ESP32 |
|------|-------|
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 19 |
| SCL | GPIO 18 |

`dracula-song` only: LED1-4 (anode via 220 ohm, cathode to GND) go to GPIO 25, 26, 32 and 33.

## Software setup

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Install the ESP32 board package **version 3.x** (Boards Manager, search "esp32" by Espressif).
3. Install these libraries (Library Manager): **Adafruit GFX Library** and **Adafruit SSD1306**.
4. Open the `.ino` of the project you want. Keep each folder intact: the folder name must match the `.ino` name, and the `.h` files must stay beside it.
5. Select **ESP32 Dev Module**, choose your port and upload.
6. Start the song and press the board's EN (reset) button at the same moment so it lines up.

## love-me-not

- `love-me-not.ino` - display code. Draws one frame every `FRAME_DELAY` ms and loops.
- `VideoFrame.h` - the video as 247 monochrome 128x64 bitmaps (1024 bytes each, stored in flash).

To use a different video, convert it to 128x64 1-bit frames, replace `VideoFrame.h`, and update `TOTAL_FRAMES` and `FRAME_DELAY` at the top of that file.

## dracula-song

- `dracula-song.ino` - animations, text effects and LED patterns.
- `lyrics.h` - the word-by-word timing. Each entry is `{ delayBeforeMs, durationMs, "word", EFFECT, textSize, 0 }`.

## Troubleshooting

- **"OLED not found" / blank screen:** check SDA/SCL wiring and that VCC is on 3.3V. If it still fails, lower `Wire.setClock(...)` (800000 is aggressive; try 400000).
- **Compile error about `analogWrite` (dracula-song):** your ESP32 core is older than 3.x. Update it.
- **Out of sync:** press reset exactly when the song starts. For `dracula-song` you can also tweak the timings in `lyrics.h`.

## Credits

- `dracula-song` is based on a sketch by **CircuitForge** and **@Afxlabz** ("GOD MODE" upgrade). Check their original licence before reusing the code.
- Songs belong to their artists and rights holders. This is a personal, non-commercial hobby project and is not affiliated with any artist or label.
- Hardware build and adaptation: *your name here*
