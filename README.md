# ESP32 ThingsBoard Client Attributes

This project demonstrates **Client Attributes** functionality with ESP32 and **ThingsBoard** IoT platform. The ESP32 controls an LED that maintains its state persistently using ThingsBoard client attributes, simulated in **Wokwi**.

## 🎯 Features

- **LED Control**: Toggle LED with physical button
- **Persistent State**: LED state is saved as client attribute in ThingsBoard
- **State Recovery**: LED state is restored on device restart
- **Simple Design**: Minimal code, maximum functionality
- **Wokwi Simulation**: Complete hardware simulation with LED and button

## 📚 Dependencies and Libraries

### PlatformIO Libraries
```ini
lib_deps = 
    thingsboard/ThingsBoard@0.14.0                    # ThingsBoard MQTT Client
    arduino-libraries/ArduinoHttpClient@^0.6.1        # HTTP Client
    arduino-libraries/ArduinoMqttClient@^0.1.8        # MQTT Client
    knolleary/PubSubClient@^2.8                       # MQTT Pub/Sub
```

### System Libraries
- `WiFi.h` - WiFi connectivity (ESP32)
- `Arduino_MQTT_Client.h` - MQTT client for ThingsBoard
- `Attribute_Request.h` - Client attributes management

## ⚙️ Configuration

### 1. WiFi Credentials
```cpp
constexpr char WIFI_SSID[] = "Wokwi-GUEST";      // WiFi Network
constexpr char WIFI_PASSWORD[] = "";             // Password (empty for Wokwi)
```

### 2. ThingsBoard Configuration
```cpp
constexpr char TOKEN[] = "xxxxxxxxxxxxxxxxxxxx";           // Device token (from ThingsBoard)
constexpr char THINGSBOARD_SERVER[] = "thingsboard.cloud"; // ThingsBoard server
constexpr uint16_t THINGSBOARD_PORT = 1883U;               // MQTT port
constexpr const char LED_STATE_ATTR[] = "ledState";        // Client attribute name
```

### 3. Hardware Configuration
```cpp
#define LED_PIN 2        // LED connected to GPIO 2
#define BUTTON_PIN 0     // Button connected to GPIO 0
```

## 🚀 Installation and Usage

### 1. Prerequisites
- [PlatformIO IDE](https://platformio.org/platformio-ide) or [PlatformIO Core](https://platformio.org/install/cli)
- Account on [ThingsBoard Cloud](https://thingsboard.cloud/) or local server
- Access to [Wokwi](https://wokwi.com/) for simulation

### 2. Project Setup
```bash
# Clone the repository
git clone <repository-url>
cd esp32-thingsboard-platformio-wokwi-telemetry
```

### 3. ThingsBoard Configuration
1. Create a new device in ThingsBoard
2. Copy the device **Access Token**
3. Replace the `TOKEN` in `main.cpp`
4. The device will automatically create the `ledState` client attribute

### 4. Wokwi Simulation
1. Open the project in Wokwi
2. The `diagram.json` contains:
   - ESP32 DevKit C V4
   - Red LED on GPIO 2
   - Blue button on GPIO 0
3. Run the simulation
4. Monitor serial port for connection status

## 🔧 How It Works

### Client Attributes Flow
1. **Connection**: ESP32 connects to WiFi and ThingsBoard
2. **Request**: Automatically requests `ledState` client attribute
3. **Restore**: If attribute exists, LED state is restored
4. **Control**: Press button to toggle LED state
5. **Save**: New LED state is sent as client attribute to ThingsBoard

### Hardware Components
- **LED (GPIO 2)**: Visual indicator of current state
- **Button (GPIO 0)**: Toggle control (with pull-up resistor)
- **Serial Monitor**: Status messages and debugging

## 📊 ThingsBoard Integration

### Client Attributes
- **ledState** (boolean): Stores LED on/off state persistently

### Device Behavior
- **First Connection**: Uses default state (LED OFF)
- **Subsequent Connections**: Restores last saved state
- **Button Press**: Toggles LED and saves new state
- **State Persistence**: Survives device restarts and reconnections

## 🎮 Usage

1. **Power On**: Device connects and restores last LED state
2. **Press Button**: Toggle LED between ON/OFF
3. **Check ThingsBoard**: View `ledState` client attribute updates
4. **Restart Device**: LED returns to last saved state

## 📄 License

This project is an open source educational template. Free to use and modify.


## 📞 Support

For questions or issues:
- Create an issue in the repository
- Review [ThingsBoard documentation](https://thingsboard.io/docs/devices-library/esp32-dev-kit-v1/)
- Check [Wokwi documentation](https://docs.wokwi.com/)

## 🔍 Troubleshooting

### Common Issues
- **"Failed to connect to ThingsBoard"**: Check device token and internet connection
- **"LED value not found on server"**: Normal for first-time connections
- **"Timeout: No response from ThingsBoard"**: Network or server issues

### Serial Monitor Messages
- `LED restored: ON/OFF` - State successfully recovered from ThingsBoard
- `LED value not found on server` - Using default state (first connection)
- `LED: ON/OFF` - Button pressed, new state sent to ThingsBoard

---
**Author**: Mirutec - Roger Chung  
**Version**: 1.0 - Client Attributes  
**Date**: November 2025
