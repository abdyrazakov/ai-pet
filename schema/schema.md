# Схема подключения

## Таблица распиновки ESP32

| ESP32 | Устройство | Протокол |
|-------|-----------|----------|
| GPIO 32 | INMP441 WS | I2S (mic) |
| GPIO 33 | INMP441 SCK | I2S (mic) |
| GPIO 35 | INMP441 SD | I2S (mic) |
| GPIO 25 | MAX98357 BCLK | I2S (out) |
| GPIO 26 | MAX98357 LRC | I2S (out) |
| GPIO 27 | MAX98357 DIN | I2S (out) |
| GPIO 21 | OLED SDA | I2C |
| GPIO 22 | OLED SCL | I2C |
| GPIO 13 | Серво ухо L | PWM |
| GPIO 14 | Серво ухо R | PWM |
| GPIO 4 | TTP223 (касание) | digital in |
| 3V3 | VCC всех модулей | питание |
| GND | GND всех модулей | питание |

## Блок-схема

```mermaid
flowchart LR
    MIC[INMP441] -- I2S --> ESP[ESP32]
    ESP -- I2S --> AMP[MAX98357] --> SPK[Динамик]
    ESP -- I2C --> OLED[OLED 0.91"]
    ESP -- PWM --> S1[Серво L]
    ESP -- PWM --> S2[Серво R]
    TOUCH[TTP223] -- GPIO4 --> ESP
    ESP -- Wi-Fi --> CLOUD[AI-сервис / LLM API]
```

## Заметки

- INMP441: L/R pin → GND (левый канал), питание 3.3В.
- MAX98357: SD pin → GND (канал L), громкость = Vout по формуле даташита; можно добавить потенциометр.
- Серво: отдельное питание 5В (не с ESP32!), общий GND.
- OLED SSD1306 адрес I2C: 0x3C.
