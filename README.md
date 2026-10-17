# fenton-homelab
A simple overview of my current homelab setup

---Main Backbone: Cisco Catalyst 2960-X (24-port PoE)---
    Isolates the homelab and smart-home VLANs. Gigabit fiber uplink. The 5 GHz Wi-Fi band is disabled to stay clear of 5.8 GHz analog FPV video. Every node that supports it reports to Prometheus through node_exporter.

+ RaspBerryPi 4 (wirehole): PiHole, WireGuard VPN, Grafana, Prometheus, IP Camera, Sentinel Dashboard
    This unit, connected to the main gateway, acts as a VPN tunnel endpoint for all of my mobile devices (laptop, phone, vehicle), monitors nodes on ALL prometheus-capable devices, displays network and device telemetries and a live feed on Grafana dashboards, one of which is specifically formatted to display on a MS Surface Pro 5 with no user I/O.
    It also hosts Sentinel, a standalone dark-theme dashboard showing the camera feed, weather, vehicle and dog-outing recommendations, PiHole stats, dual-GPU metrics from ariacore, storage levels, and node status indicators.

+ Microsoft Surface Pro 5: Running Linux displaying Customized Grafana Dashboard
    This device was retired after the touchscreen failed.  It was brought back into use as a detachable wall-mounted Admin dashboard.  Using OpenWeatherData, I created custom scripts to advise which vehicle to drive for the day and whether the dogs should be in or out.  It now runs Chromium in kiosk mode displaying the Sentinel dashboard.

+ RaspberryPi 3: 315MHzTx-APIWebUI Transmitter, Vehicle Lock/Unlock/Start Transmitter
    System designed for AI and WebUI control of a 315MHz-controlled DC motor and basic vehicle security commands.  See my "315MHzTx-APIWebUI" repository for more details.  For security reasons, vehicle control details are not present.
    |
    315MHz Transmitter Module
        |
        \/\ DC Motor Controller
        \/\ 315MHz automotive Body Control Module

+ Libre LePotato S905X-CC: HomeLab & Server Cabinet Climate Controller/Lighting Controller APIWebUI WORK IN PROGRESS
    This system is designed to manage the climate and lighting in both my homelab and in the server cabinet itself.  
    |
    8-channel Mechanical Relay pack
    8-channel SSR I2C Relay pack
    IR Tx/Rx Module
    DHT11 Temp/Humidity sensors (x3)

+ Custom Windows Server 2019: NAS & DLNA Server, Analog-Digital Media Conversion Controller, Local Emergency Services Radio Scanner & Recording
    |
    JVC BR-S800U Studio VHS Rack Mount Player/Recorder
    Marantz PMD-500 Cassette Rack Mount Player/Recorder
    DMR Transceiver
        |
        External Antenna Array

+ Cisco UCS C220-M3 Rack Mount Server (cisco22m3): Storage Server, Host https://razorblade.us Injection Molding Manufacturing Labeling & Production Management SaaS website WORK IN PROGRESS
    An LSI MegaRAID 9271-8i controller manages two LVM volumes: a fast SSD volume (4x Samsung 860 PRO 1TB) and a media volume (3x WD 500GB HDD).  Serves Jellyfin and Samba shares, and hosts the PostgreSQL database, Whisper transcription, LLM analysis service, and REST API for the dispatch monitoring pipeline below.

+ Raspberry Pi 3B+ with PoE HAT (radiopi): RTL-SDR Capture Node
    Captures local fire dispatch radio with an RTL-SDR dongle (rtl_fm + sox), then rsyncs the recordings to the storage server and logs their metadata to PostgreSQL.

+ Dispatch Monitoring Pipeline: Host https://harrisonfd.live Public Fire Dispatch Monitor WORK IN PROGRESS
    RTL-SDR → rtl_fm/sox → WAV → rsync → PostgreSQL → Whisper transcription → LLM analysis → REST API → WebUI.  The public site runs behind an Nginx reverse proxy with Let's Encrypt SSL, rate limiting, and security headers, and features an auto-play queue and per-transmission signal stats.  Currently tuning the RTL-SDR capture chain (gain, PPM correction, filtering) for clean end-to-end transmissions.  Spans the radio Pi, the storage server, the OptiPlex 5060, and ariacore.

+ B&W Broadcast CRT Status Displays WORK IN PROGRESS
    Single-board computers driving 4" black-and-white broadcast CRTs over composite video to show live status.  The first build is a Libre LePotato (AML-S905X-CC) rendering to the framebuffer at 720x576 PAL, showing game server status through a custom Python monitor with animated icons.  Next up: a Raspberry Pi 3B+ driving a second tube to display dispatch pipeline status.

+ Custom Ubuntu Server: Host https://gamekrypt.com Videogame Collector tracking & management SaaS website WORK IN PROGRESS

+ Custom Ubuntu Server: Host https://fenton.technology Portfolio website WORK IN PROGRESS

+ Custom Ubuntu Server (ariacore): Host LLM AI, Stable Diffusion, XTTSv2 Text-to-Speech, API extensions
    An MSI X470 board with an AMD Ryzen 5 3600X, 32GB 3600MHz RAM, and dual NVIDIA RTX 3070 + RTX 2070 Super GPUs enable me to simultaneously host .gguf LLM AI models, StableDiffusion image generation models, Text-to-Speech, and custom API extensions for home automation and entertainment using llama.cpp, ComfyUI, SillyTavern, Oobabooga, and XTTSv2.  Services run under systemd, GPU use is isolated per service, and GPU metrics are exported to Prometheus.  A third RTX 2070 is planned for ComfyUI through a PCIe riser.  The LLM's capabilities are constantly growing as I create APIs to connect to and control all capable network devices.

+ Custom Ubuntu Server: Host private gaming server(s)
    An Intel i5 laptop that can no longer be used for much else, Ubuntu has been installed along with steamcmd for my family and friends to use as a private gaming server.

+ Dell OptiPlex 9010 (arkserver): ARK: Survival Ascended Dedicated Server
    Intel i5, 32GB DDR3, SSD, Ubuntu Server 22.04.  Runs in Docker Compose under a systemd unit, set up as family PvE with Steam and PS5 cross-play.

+ Dell OptiPlex 5060: Bench Unit, Dispatch Pipeline Node, Sons of the Forest Dedicated Server
    Ubuntu 22.04.  Originally a bench and scan unit for drive diagnostics.  Now also a node in the dispatch pipeline and the host for a Sons of the Forest dedicated server (Docker).  Dedicated Rust and 7 Days to Die servers are also set up, all as Docker containers with systemd units that keep only one server running at a time.

+ Klipper/Mainsail Special-Application 180mm^3 Climate Controlled Enclosed 3D printer & Laser Cutter (The Doom³)
    With hundreds of designs and ideas, I needed a 3D printer capable of printing ABS, Nylon, and other materials that required a heated build volume.  I went overboard with this machine and added full air control, complete with shutters and evacuation systems.  It started life as an XYZprinting da Vinci 1.0 with all logic replaced by a BigTreeTech Octopus v1.1 and a Raspberry Pi 4, plus a 500mW laser engraver, RGB lighting, and extra I/O.  See my "DoomCube" repository for the config, schematics, and renders.

Client Devices:
Acer Nitro 17 (primary laptop)
iPad Pro 11" (SMB for files, SFTP via Secure ShellFish)
Samsung Galaxy Book Go (Windows 11 ARM, stripped down as an SSH terminal)

Airgapped Devices:
Custom Marlin 200mm^3 3D printer
Custom Marlin 300x300x400mm 3D printer
Artillery Sidewinder X3 Plus 300x300x400mm 3D printer
