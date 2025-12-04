# CYD Home Assistant Touchscreen Control Panel

A comprehensive ESPHome configuration for the ESP32-2432S028R (Cheap Yellow Display) board, creating a smart home control panel with LVGL-based touchscreen interface for Home Assistant integration.

## 🚨 AI Generated Disclaimer

**This project and documentation were primarily generated using AI assistance. While the code has been tested and is functional, users should review and understand all configurations before deployment. Use at your own risk and always test in a safe environment first.**

## 📱 Features

### Main Interface
- **9-Button Grid Layout**: Clean 3x3 grid interface with customizable buttons
- **Real-time Status Updates**: Live status indicators for all connected devices
- **Touch Feedback**: Responsive touch interface with visual feedback
- **Multi-page Support**: Main page + secondary page for additional controls

### Smart Home Integration
- **Home Assistant Integration**: Full bidirectional communication
- **Light Control**: Toggle ceiling lights, desk lamps, and spots
- **3D Printer Management**: Control multiple 3D printers (Shelly) and their LED lighting (ESP32/Tasmota)
- **Environmental Monitoring**: Display temperature, humidity, and air quality data (Dyson Vent API)
- **Real-time Clock**: Current time display on center button

### Advanced Features
- **Anti-burn Protection**: Automatic pixel training during night hours to prevent screen burn-in
- **Scheduled Operations**: Time-based automation for maintenance tasks
- **Touch Interrupts**: Manual override capabilities during automated processes
- **Custom Themes**: Dark theme with yellow accent colors for checked states

## 🛠 Hardware Requirements

- **ESP32-2432S028R** (Cheap Yellow Display board)
- **ILI9341 Display** (320x240 pixels, included with CYD)
- **XPT2046 Touch Controller** (included with CYD)
- **Font Files**: Arimo-Regular.ttf and Material Design Icons font

## 📁 Project Structure

```
├── prod.yaml                    # Main ESPHome configuration
├── fonts/
│   ├── Arimo-Regular.ttf        # Primary text font
│   └── materialdesignicons-webfont.ttf  # Icon font
└── README.md                    # This file
```

## ⚙️ Configuration Overview

### Core Components
- **Time Synchronization**: SNTP time component for scheduling
- **Display Driver**: ILI9341 with optimized settings for performance
- **Touch Interface**: XPT2046 with calibrated touch zones
- **LVGL Integration**: Modern UI framework for smooth graphics

### Automated Features
- **Pixel Training**: Runs at 2 AM, 5 AM, and 8 AM for 30 minutes each
- **Touch Wake**: Interrupts pixel training when screen is touched
- **Status Monitoring**: Continuous monitoring of Home Assistant entities

### Home Assistant Entities

#### Lights
- `light.decke_homeoffice` - Office ceiling light
- `light.spots_ho` - Office spot lighting
- `light.homeoffice_desklamp` - Desk lamp

#### Switches
- `switch.3d_drucker` - Main 3D printer
- `switch.drucker` - CR10 3D printer
- `switch.drucker2` - CR6 3D printer
- `switch.cr10_leds` - CR10 LED lighting
- `switch.cr6_leds` - CR6 LED lighting
- `switch.dinolampe` - Decorative dino lamp

#### Sensors
- `sensor.dyson_vent_temperature` - Air temperature
- `sensor.dyson_vent_humidity` - Air humidity
- `sensor.dyson_vent_air_quality_index` - Air quality index

## 🚀 Installation

### Prerequisites
1. **ESPHome**: Install ESPHome in Home Assistant or standalone
2. **Font Files**: Download required fonts to the `fonts/` directory
3. **Home Assistant**: Ensure all referenced entities exist

### Setup Steps

1. **Clone Repository**
   ```bash
   git clone https://github.com/marcprojer/CYD-HA.git
   cd CYD-HA
   ```

2. **Configure Secrets**
   Create `secrets.yaml` with your credentials:
   ```yaml
   wifi_ssid: "YourWiFiSSID"
   wifi_password: "YourWiFiPassword"
   api_key: "your_api_encryption_key"
   ota_pw_CYD: "your_ota_password"
   fb_pw_CYD: "your_fallback_hotspot_password"
   ```

3. **Install Fonts**
   - Download Arimo-Regular.ttf
   - Download Material Design Icons font
   - Place in `fonts/` directory

4. **Customize Configuration**
   - Update timezone in `prod.yaml`
   - Modify entity IDs to match your Home Assistant setup
   - Adjust pixel training schedule if needed

5. **Flash Device**
   ```bash
   esphome run prod.yaml
   ```

## 📋 Usage

### Main Screen (3x3 Grid)
- **Top Row**: Light controls (Ceiling, Spots, Desk lamp)
- **Middle Row**: Navigation button, Clock, Dino lamp
- **Bottom Row**: Environmental sensors (Temperature, Humidity, Air Quality)

### Sub Screen
- **3D Printer Controls**: Power and LED controls for printers
- **Return Button**: Navigate back to main screen

### Touch Operations
- **Single Tap**: Toggle device state
- **During Pixel Training**: Any touch stops the training mode
- **Navigation**: Tap navigation buttons to switch pages

## 🎨 Customization

### Adding New Devices
1. Add entity sensor in `text_sensor` section
2. Create corresponding button in LVGL configuration
3. Update `binary_sensor` section for Home Assistant integration

### Modifying Layout
- Adjust `grid_cell_column_pos` and `grid_cell_row_pos` for button positioning
- Modify grid layout in LVGL pages section
- Update font sizes and colors in theme section

### Changing Pixel Training Schedule
Modify the `on_time` section in the time component:
```yaml
on_time:
  - hours: 2,5,8  # Adjust hours as needed
    minutes: 5
    seconds: 0
    then:
      - switch.turn_on: switch_antiburn
```

## 🔧 Troubleshooting

### Common Issues
- **Build Errors**: Ensure all font files are present and paths are correct
- **Touch Calibration**: Adjust calibration values in touchscreen section
- **Entity Unavailable**: Verify Home Assistant entity IDs match your setup
- **Network Issues**: Check WiFi credentials and signal strength

### Debug Mode
Enable debug logging by adding:
```yaml
logger:
  level: DEBUG
```

## 📝 License

This project is provided as-is under the MIT License. See LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test your changes thoroughly
4. Submit a pull request with detailed description

## ⚠️ Disclaimer

- **AI Generated**: This project was created with AI assistance
- **No Warranty**: Use at your own risk
- **Security**: Review all configurations before deployment
- **Testing**: Always test in a safe environment first
- **Sensitive Data**: Ensure no sensitive information is exposed in public repositories

## 📞 Support

For issues and questions:
- Review the troubleshooting section
- Check ESPHome documentation
- Verify Home Assistant entity configurations
- Test with minimal configuration first

---

**Note**: This README and the associated code were generated using AI assistance. While functional, users should understand and validate all configurations for their specific environment and security requirements.