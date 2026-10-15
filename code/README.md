# Прошивка

Плата: ESP32 DevKit. Среда: PlatformIO (Arduino framework).

## Структура

- `platformio.ini` — конфигурация сборки
- `src/main.ino` — точка входа, конечный автомат

## Модули (план)

| Модуль | Ответственность |
|--------|----------------|
| `audio_in` | захват речи с INMP441 (I2S), VAD |
| `audio_out` | воспроизведение через MAX98357 (I2S), I2S DAC / MP3 |
| `speech` | распознавание (wake-word + STT, напр. ESP-SR / облачный STT) |
| `ai_client` | запрос к LLM API по Wi-Fi (HTTP/WebSocket) |
| `display` | отрисовка глаз/эмоций на SSD1306 |
| `ears` | PWM-управление сервоприводами ушек |
| `touch` | обработка TTP223, долгое нажатие |
| `fsm` | конечный автомат (см. ../state-machine/) |

## Сборка

```bash
cd code
pio run -t upload
pio device monitor
```

## Статус

Заготовка. Пайплайн: wake-word → запись → STT → LLM → TTS → анимация.
