# 📡 SIM800Plus

**SIM800Plus** is a lightweight Arduino library designed for managing GSM/GPRS connections using the SIMCom SIM800L module.  
This version extends the original library to add additional methods, including sending raw byte arrays in POST requests, improving data transmission flexibility.

Originally based on [Olivier Staquet's SIM800L driver](https://github.com/ostaquet/Arduino-SIM800L-driver).

---

## ✨ Features

- GSM/GPRS connectivity management.
- HTTP and HTTPS connections (GET and POST methods).
- **Supports POST with raw byte arrays** (send integer arrays instead of only strings).
- Signal strength and network registration checks.
- Power management features.
- Supports both SoftwareSerial and HardwareSerial.

---

## 📦 Installation

1. Download or clone this repository.
2. Move the `SIM800Plus` folder into your Arduino `libraries` directory.
3. Restart Arduino IDE.

Or, if using PlatformIO:

```ini
lib_deps =
  MesutEmpire/SIM800Plus
```

---

## 🛠️ Basic Usage

```cpp
#include <SIM800Plus.h>
#include <SoftwareSerial.h>

SoftwareSerial simSerial(10, 11); // RX, TX
SIM800Plus modem(simSerial);

void setup() {
  Serial.begin(9600);
  simSerial.begin(9600);

  if (modem.connectGPRS("your_apn", "your_user", "your_pass")) {
    Serial.println("GPRS Connected!");
  } else {
    Serial.println("GPRS Connection Failed.");
  }

  String response;
  if (modem.doGet("http://example.com", response)) {
    Serial.println("Server Response:");
    Serial.println(response);
  } else {
    Serial.println("GET request failed.");
  }
}

void loop() {
  // Nothing here
}
```

---

## 🧩 New Extended Methods

**➔ New feature added:**

- `doPost()` can now accept **raw byte arrays** (integers) as the body,  
  allowing you to send binary or structured data more efficiently over HTTP/S connections.

Example sending raw data:

```cpp
uint8_t rawData[] = {0x01, 0x02, 0x03, 0x04}; // Your raw data
String response;

if (modem.doPost("http://example.com/endpoint", rawData, sizeof(rawData), response)) {
  Serial.println("POST request successful.");
  Serial.println(response);
} else {
  Serial.println("POST request failed.");
}
```

---

## 📚 Documentation

- [`SIM800Plus.h`](src/SIM800Plus.h) and [`SIM800Plus.cpp`](src/SIM800Plus.cpp) contain full API documentation via comments.
- Basic examples are available inside the `examples/` directory.

---

## 🖇️ Compatibility

- Arduino Uno, Mega, Nano, Leonardo
- ESP8266, ESP32 (using HardwareSerial or SoftwareSerial)
- STM32, RP2040 boards
- Any board supporting SoftwareSerial or equivalent.

---

## 📜 License

This library is licensed under the [MIT License](LICENSE).  
Originally created by [Olivier Staquet](https://github.com/ostaquet),  
modified and extended by [Samuel Wainaina](https://github.com/MesutEmpire) in 2025.

---

## 🌟 Acknowledgements

Big thanks to Olivier Staquet for the original **Arduino-SIM800L-driver**!

---