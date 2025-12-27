# fenton-homelab
A simple overview of my current homelab setup

---Main Backbone: Cisco Catalyst 20960-X---
|
+ RaspBerryPi 4: PiHole, WireGuard VPN, Grafana, Prometheus, IP Camera
    This unit, connected to the main gateway, acts as a VPN tunnel endpoint for all of my mobile devices (laptop, phone, vehicle), monitors nodes on ALL prometheus-capable devices, displays network and device telemetries and a live feed on Grafana dashboards, one of which is specifically formatted to display on a MS Surface Pro 5 with no user I/O.  
|
+ Microsoft Surface Pro 5: Running Linux displaying Customized Grafana Dashboard
    This device was retired after the touchscreen failed.  It was brought back into use as a detachable wall-mounted Admin dashboard.  Using OpenWeatherData, I created custom scripts to advise which vehicle to drive for the day and whether the dogs should be in or out.  
|
+ RaspberryPi 3: 315MHzTx-APIWebUI Transmitter, Vehicle Lock/Unlock/Start Transmitter
    System designed for AI and WebUI control of a 315MHz-controlled DC motor and basic vehicle security commands.  See my "315MHzTx-APIWebUI" repository for more details.  For security reasons, vehicle control details are not present.
    |
    315MHz Transmitter Module
        |
        \/\ DC Motor Controller
        \/\ 315MHz automotive Body Control Module
|
+ Libre LePotato S905X-CC: HomeLab & Server Cabinet Climate Controller/Lighting Controller APIWebUI WORK IN PROGRESS
    This system is designed to manage the climate and lighting in both my homelab and in the server cabinet itself.  
    |
    8-channel Mechanical Relay pack
    8-channel SSR I2C Relay pack
    IR Tx/Rx Module
    DHT11 Temp/Humidity sensors (x3)
|
+ Custom Windows Server 2019: NAS & DLNA Server, Analog-Digital Media Conversion Controller, Local Emergency Services Radio Scanner & Recording
    |
    JVC BR-S800U Studio VHS Rack Mount Player/Recorder
    Marantz PMD-500 Cassete Rack Mount Player/Recorder
    DMR Transceiver
        |
        External Antenna Array
|
+ Cisco C220-M3 Rack Mount Server: Host https://razorblade.us Injection Molding Manufacturing Labeling & Production Management SaaS website WORK IN PROGRESS
|
+ Custom Ubuntu Server: Host https://gamekrypt.com Videogame Collector tracking & management SaaS website WORK IN PROGRESS
|
+ Custom Ubuntu Server: Host https://fenton.technology Portfolio website WORK IN PROGRESS
|
+ Custom Ubuntu Server: Host LLM AI, Stable Diffusion, XTTSv2 Text-to-Speech, API extensions
    AMD Ryzen 5 3600x, 32GB 3600MHz RAM and NVIDIA RTX2070Super enable me to simultaneously host .gguf LLM AI models, StableDiffusion image generation models, Text-to-Speech, and custom API extensions for home automation and entertainment using ComfyUI, SillyTavern, Oobabooga, and XTTSv2.  The LLM's capabilities are constantly growing as I create APIs to connect to and control all capable network devices.
|
+ Custom Ubuntu Server: Host private gaming server(s)
    An Intel i5 laptop that can no longer be used for much else, Ubuntu has been installed along with steamcmd for my family and friends to use as a private gaming server.
|
+ Klipper/Mainsail Special-Application 180mm^3 Climate Controlled Enclosed 3D printer & Laser Cutter
    With hundreds of designs and ideas, I needed a 3D printer capable of printing ABS, Nylon, and other materials that required a heated build volume.  I went overboard with this machine and added full air control, complete with shutters and evacuation systems.  

Airgapped Devices:
Custom Marlin 200mm^3 3D printer
Custom Marlin 300x300x400mm 3D printer
Artillery Sidewinder X3 Plus 300x300x400mm 3D printer
