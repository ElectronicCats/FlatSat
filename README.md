# Flatsat 

<p align="center">
    <a href="https://github.com/ElectronicCats/FlatSat/wiki">
        <img src="https://private-user-images.githubusercontent.com/107638696/595693319-c0883c17-046c-4819-b3c2-2ec70a0c5052.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3OTAxOTE2MTEsIm5iZiI6MTc5MDE5MTMxMSwicGF0aCI6Ii8xMDc2Mzg2OTYvNTk1NjkzMzE5LWMwODgzYzE3LTA0NmMtNDgxOS1iM2MyLTJlYzcwYTBjNTA1Mi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwOTIzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDkyM1QxOTIxNTFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yZGFhZWUyM2FkNTAwYmU5YTljMWQ2OTc5YzA3YzA4ZjgxMWJkYTE3NDhlNjJjYjBiOTdlNTkyNzBhNWI4Y2JhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.7IfkX0f9DTbWNKQIJjl4vGQzU_LSV2SPomvP7GhOxqU" width=70%>
    </a>
</p>

<p align=center>
    <a href="https://electroniccats.com/store/flatsat1/">
        <img src="https://github.com/ElectronicCats/flipper-shields/assets/44976441/0c617467-052b-4ab1-a3b9-ba36e1f55a91" width="200" height="104" />
    </a>
    <a href="hhttps://github.com/ElectronicCats/FlatSat/wiki">
        <img src="https://github.com/ElectronicCats/flipper-shields/assets/44976441/6aa7f319-3256-442e-a00d-33c8126833ec" width="200" height="104" />
    </a>
</p>

Flatsat is a hardware based training platform designed to be vulnerable on purpose. It’s built for hackers, engineers, and space enthusiasts who want to dive deep into space-grade systems, learn cybersecurity concepts, and prototype their own payloads.

Flatsat is designed to help you learn and prototype radio systems safely and legally, all while gaining real-world skills in RF communication, signal analysis, and protocol fuzzing.


## What You Can Do With Flatsat
- **Hands-on Learning:** Use Flatsat as the hardware companion to the [**PwnSat**](https://pwnsat.org/) course, with structured lessons on binary exploitation, secure communication, reverse engineering, and space protocols.
- **Hack Real Vulnerabilities:**  Explore and exploit firmware designed to simulate real-world satellite systems and vulnerabilities. It’s a safe playground for learning and discovery.
- **Join the Mission CTF:**  Participate in space-themed capture-the-flag challenges that simulate real satellite operation scenarios.
- **Prototype Your Payloads:**  Use the onboard components to develop and test your own payload logic, radio communication, or telemetry systems before launching bigger projects.

> [!IMPORTANT]
> **This project was created for educational purposes, to teach and learn aerospace cybersecurity. Neither PWNSAT nor Electronic Cats are responsible for how the knowledge, code, or tools hosted in the official repository are used. Use only against hardware, firmware, or signal sources you own or are explicitly authorized to test.**
> 
> Flatsat uses ISM (Industrial, Scientific, and Medical) band frequencies for all RF communication,  typically 433 MHz or 915 MHz, depending on your region. These frequencies are internationally reserved for unlicensed, experimental, and educational use.
>
> This ensures that Flatsat does not interfere with any production space systems, licensed satellites, or critical ground infrastructure.

## Hardware Infrastructure

The infrastructure is designed for **FlatSat** testing, where hardware components are laid out for accessibility and auditing.

| **Component** | **Description**           | **Interface**            |
| ------------- | ------------------------- | ------------------------ |
| **MCU**       | Raspberry Pi RP2040       | Dual Core ARM Cortex-M0+ |
| **Radio 0**   | SX1262 LoRa (Uplink)      | SPI0 / NSS Pin 17        |
| **Radio 1**   | SX1262 LoRa (Downlink)    | SPI0 / NSS Pin 5         |
| **IMU**       | LIS2DH12 Accelerometer    | I2C (SDA 20, SCL 21)     |
| **ENV**       | BME280 Environment Sensor | I2C (SDA 20, SCL 21)     |
| **Status**    | WS2812B NeoPixel          | GPIO 15                  |

##  FlatSat Firmware

The firmware splits tasks across two cores, the system ensures that high-speed data links do not interfere with time-critical radio operations.

The firmware is located in a different repository: https://github.com/ElectronicCats/flatsat-ground-station

The core of the communication system is the [**CCSDS Space Packet Protocol**](https://ccsds.org/Pubs/133x0b2e2.pdf). This allows the spacecraft to route data using **Application Process Identifiers (APIDs)**, enabling modular subsystem addressing.

Modern satellites are no longer isolated systems; they are software-defined assets. The vulnerabilities identified in this firmware mirror historical "anomalies" and documented attacks on orbiting infrastructure.

Since the firmware lacks a Cryptographic Authentication layer, the system is vulnerable to **Command Spoofing**.

An attacker uses a Software Defined Radio (SDR) to capture a legitimate "Telemetry" packet to identify the `SPACECRAFT_ID` and the current `Sequence Count`.
  
This happened in the real world. In 1998, the **ROSAT** (Röntgen Satellite) was allegedly compromised via a ground station breach, where attackers sent commands to point the solar panels directly at the sun, eventually frying the batteries. While that was a network breach, the lack of authentication on the RF link makes this firmware susceptible to the same outcome.

## Technical Documentation and Guides (Wiki)

All deep technical documentation, source analysis, and setup guides have been centralized. If you want to start debugging, or exploiting the platform, please visit the [FlatSat Wiki](https://github.com/ElectronicCats/FlatSat/wiki). The information from the Pwnsat repository has been included in our wiki.

## How to contribute <img src="https://electroniccats.com/wp-content/uploads/2018/01/fav.png" height="35"><img src="https://raw.githubusercontent.com/gist/ManulMax/2d20af60d709805c55fd784ca7cba4b9/raw/bcfeac7604f674ace63623106eb8bb8471d844a6/github.gif" height="30">

[pwnsat.org](https://pwnsat.org/) and [flatsat.org](https://flatsat.org/)
Contributions are welcome!

Please read the document [**Contribution manual**](https://github.com/ElectronicCats/electroniccats-cla/blob/main/electroniccats-contribution-manual.md) which will show you how to contribute your changes to the project.

✨ Thanks to all our [Contributors](https://github.com/ElectronicCats/Munchkin/graphs/contributors)! ✨

See [**_Electronic Cats CLA_**](https://github.com/ElectronicCats/electroniccats-cla/blob/main/electroniccats-cla.md) for more information.

See the [**Community code of conduct**](https://github.com/ElectronicCats/electroniccats-cla/blob/main/electroniccats-community-code-of-conduct.md) for a vision of the community we want to build and what we expect from it.

## License

Electronic Cats invests time and resources providing this open source design, please support Electronic Cats and open-source hardware by purchasing products from Electronic Cats!

Designed by Electronic Cats and PWNSAT.

Hardware released under an CERN Open Hardware Licence v1.2. See the LICENSE_HARDWARE file for more information.

Electronic Cats and PWNSAT is a registered trademark, please do not use if you sell these PCBs.

## Special Thanks
A special thanks to **Alex Lynd**. His support made it possible to kick off the first version of the project, and his contribution remains a fundamental part of PwnSat. His work will always be embedded in what this project has become.