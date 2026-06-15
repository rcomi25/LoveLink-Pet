# LoveLink-Pet
A pair of LTE-connected virtual pets powered by ESP32-S3, MQTT and Raspberry Pi.

# Overview
LoveLink Pet is a pair of portable LTE-connected virtual pets designed to allow two people to exchange emotions, status updates and messages in real time.

Each device connects independently to the cellular network using a SIM7080 modem and communicates through an MQTT broker hosted on a Raspberry Pi 4.

The goal is to create a modern interpretation of a Tamagotchi-like companion that allows two users to stay connected through a dedicated physical device.

# Features
- LTE communication using SIM7080
- MQTT messaging through Raspberry Pi
- Real-time emotion sharing
- Virtual pet system
- Battery monitoring
- Deep sleep power saving
- Touch-free button interface
- LVGL graphical user interface
- Fully portable
- 3D printed enclosure
- Open-source firmware

# Bill of Materials
- 2	LilyGO T-SIM7080G-S3
- 2	Nano SIM cards
- 2	LiPo batteries
- 10	Push buttons
- 1	Raspberry Pi 4
- 1	MicroSD card
- 2	240×280 ST7789 displays (integrated on LilyGO board)
- 8 M2x30 Screws
- 8 M2x8 Screws
- 16 M2 Nuts
- 12 5x3mm circular magnets

# System Architecture
Both devices communicate exclusively through the MQTT broker.

Device A:
- Sends messages using r_*
- Receives messages using d_*

Device B:
- Sends messages using d_*
- Receives messages using r_*

# MQTT Server Setup (Raspberry Pi 4)
Prerequisites
- Raspberry Pi 4
- Raspberry Pi OS Lite
- Internet connection

This guide assumes Raspberry Pi OS Lite is already installed!

1. Update the system <br>
sudo apt update <br>
sudo apt upgrade -y <br>
2. Install Mosquitto MQTT Broker <br>
sudo apt install -y mosquitto mosquitto-clients <br>
sudo systemctl enable mosquitto <br>
3. Create MQTT User <br>
sudo mosquitto_passwd -c /etc/mosquitto/passwd *USERNAME* --> *Enter your MQTT password when asked* <br>
4. Configure Mosquitto <br>
sudo nano /etc/mosquitto/mosquitto.conf <br>
*PASTE PI_1 and save it* <br>
sudo systemctl restart mosquitto <br>
sudo systemctl status mosquitto --no-pager <br>
5. Install Python MQTT Library <br>
sudo apt install -y python3-paho-mqtt <br>
6. Create the script <br>
nano /home/pi/mqtt_history_bridge.py <br>
*PASTE PI_2, change username and password and save it* <br>
7. Set the permissions <br>
sudo chown pi:pi /home/pi/mqtt_history_bridge.py <br>
chmod +x /home/pi/mqtt_history_bridge.py <br>
8. Create a systemd Service <br>
sudo nano /etc/systemd/system/mqtt-history-bridge.service <br>
*PASTE PI_3  and save it* <br>
9. Enable and start <br>
sudo systemctl daemon-reload <br>
sudo systemctl enable mqtt-history-bridge <br>
sudo systemctl start mqtt-history-bridge <br>

# Hardware wiring
Single-cell LiPo battery connected directly to the LilyGO board.

Button Connections: <br>
- LEFT 	8
- RIGHT	18
- UP	9
- DOWN	45
- SELECT	17

Display ST7789: <br>






