## OpenThread Command Line Example on ESP32  
  
<img src="/Images/m2e-ot-cli.jpg" height="200"> 

This example demonstrates how to use [OpenThread](https://openthread.io/), an open-source implementation of the Thread networking protocol, on Espressif SoCs through ESP-IDF. Thread is a low-power, IPv6-based mesh networking protocol designed for connected devices in smart homes and IoT applications. It provides reliable communication, self-healing mesh capabilities, and secure commissioning, making it an important foundation for modern connected ecosystems, including Matter (formerly CHIP).  

The `ot_cli` example exposes the full OpenThread command-line interface (CLI) over a serial console. Developers can interact with the Thread stack directly, issue commands to create or join a Thread network, configure devices as routers or end devices, and test connectivity between nodes. By using this example, you can gain hands-on experience with how Thread devices form a network, route messages, and communicate securely.  

Beyond basic networking commands, the CLI can be extended to experiment with application-layer communication, such as sending UDP/TCP messages between nodes, integrating with higher-level protocols, or even bridging Thread with Wi-Fi or Ethernet via an OpenThread Border Router (OTBR). This makes the `ot_cli` example a flexible starting point for exploring both Thread fundamentals and advanced use cases on ESP platforms.  

  
### Prerequisites 🧰
  
To run this OT-CLI example on ESP32 boards, there are following Hardware-software Prerequisites - 
  
### Hardware
- To run this example, a board with IEEE 802.15.4 module (for example ESP32-H2)/ESP32-C6 is required.
- We used ESP32-H2-DevKitM-1
- ESP32-C6-DevKitC-1    
- PC with Windows/Linux/MacOS
  
### Software  
- Latest version of ESP-IDF 
- Or You can use VSCode with ESP-IDF extensions  
  

------------------------------------------------------------------------------------------------------

📕 **YouTube Video Links**  

- In this tutorial we will see How to run ot-cli example on ESP32 boards  

▶️ OpenThread Command Line Example on ESP32 Boards  - 🔗  https://youtu.be/   
  

-------------------------------------------------------------------------------------------------------
📒 **Important Links**  
 
🌐 What is OpenThread -  Docs - 🔗 https://github.com/openthread/openthread    
📙 ESP-IDF Programming Guide - 🔗 https://docs.espressif.com/projects/esp-idf/en/stable/esp32/index.html  
📙 ESP-IDF Extension for VSCode - 🔗 https://docs.espressif.com/projects/vscode-esp-idf-extension/en/latest/  
🌐 OT-CLI Repository - 🔗 https://github.com/espressif/esp-idf/tree/master/examples/openthread/ot_cli  
🌐 OpenThread CLI Reference 🔗 https://github.com/openthread/openthread/blob/main/src/cli/README.md

------------------------------------------------------------------------------------------------------

📜 Source Code, Circuit Diagrams and Documentation : 

🌐 GitHub Repository - 🔗 https://github.com/make2explore/ESP32-OpenThread-Command-Line-Example   
  
🌐 Hackster Blog - 🔗 https://www.hackster.io/make2explore  
  
🌐 Instructable Blog - 🔗 https://www.instructables.com/make2explore  
  

------------------------------------------------------------------------------------------  

[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg