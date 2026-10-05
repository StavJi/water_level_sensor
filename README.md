# Snímač hladiny vody
Tento projekt je založený na ESP32 s ethernetovým modulu W5500 Lite v kombinaci s diferenciálním snímačem tlaku, které slouží pro měření výšky vodního sloupce. Testováno s komponentami uvedenými v sekci **Hardware**.

Konfigurační YAML soubor je k dispozici ve složce `conf`.

## Hardware
- [ESP32](https://www.laskakit.cz/laskakit-esp32-devkit/?variantId=11481)
- [Ethernet modul](https://www.laskakit.cz/mikro-ethernet-modul-w5500/)
- [DC/DC měnič](https://www.laskakit.cz/step-down-menic-s-lm2596/)
- 2x Dioda 1N4148
- 2x Tranzistor BC337
- Rezistory
- Wago svorky
- Voděodolná zásuvka [kvelektro](https://www.kvelektro.cz/zasuvka-scame-protecta-ip66-137-4411-do-sestav-bez-krabice-p1236195?gad_source=1&gad_campaignid=17190396887&gbraid=0AAAAAD-VuyPnHEREix-929r3cyI4Gn25q&gclid=Cj0KCQjw8ofWBhCHARIsANBj4LuaqYDFaWN9vGrd28l4m9X17WJbFi2rODPSiF-mbKyAsUfMfjdafxYaAp3GEALw_wcB) nebo [Alza](https://www.alza.cz/hobby/solight-zasuvka-ip66-vodotesna-a-prachotesna-d12895804.htm?kampan=adwho_hobby-a-zahrada_rh-top-levne-produkty_rh-top-levne-produkty_c_9218341__HoBMiM0591&gad_source=1&gad_campaignid=23509599327&gbraid=0AAAAAD2xsm4gjmrXh_q85SJiQiOYb9lxi&gclid=Cj0KCQjw8ofWBhCHARIsANBj4Lt8XwN3b0KZbHz5n99WY7XugO_A-4r8aYe3YXQcR49oQoVStNxTglYaAqP9EALw_wcB)
- Relé s držákem na DIN lištu
- Snímač hladiny vody 







# Rest TBD
## Software
1. Copy and rename `secrets.yaml.example` to `secrets.yaml` and update it with your WiFi credentials (`wifi_ssid` and `wifi_password`).

2. Build the image with [ESPHome](https://esphome.io/guides/getting_started_command_line.html)

```sh
make compile
```

3. Upload/flash the firmware to the board.

```sh
make upload
```

> By default the project builds for the AtomS3 board. To change your board, you can specify the `BOARD` parameter. For example for the Olimex ESP32-EVB:
>```sh
>make compile BOARD=esp32-evb
>make upload BOARD=esp32-evb
>```

Now when you go to the Home Assistant “Integrations” screen (under “Configuration” panel), you should see the ESPHome device show up in the discovered section (although this can take up to 5 minutes). Alternatively, you can manually add the device by clicking “CONFIGURE” on the ESPHome integration and entering “<NODE_NAME>.local” as the host.

![Comfoair Q Home Assistant](docs/homeassistant.png?raw=true "Comfoair Q Home Assistant")

Optional: for the ventilation card with the arrows, see [`docs/home-assistant/example-picture-elements-card.yaml`](docs/home-assistant/example-picture-elements-card.yaml)

## Software (Already running ESPhome somewhere)
If you are already running an instance of ESPHome, you can also include this repository directly by including it as a package. The main benefit here is having centralized management of all your ESPhome devices. To do this, you can use the following config for your device:
```
substitutions:
  wifi_ssid: !secret wifi_ssid
  wifi_password: !secret wifi_password
  wifi_hotspot_password: !secret wifi_hotspot_password
  ota_password: !secret ota_password
  api_encryption_key: !secret api_encryption_key

packages:
  remote_package_shorthand: github://yoziru/esphome-zehnder-comfoair/zehnder-comfoair-q-esp32-evb.dashboard.yml@main
```

Be sure to use the correct `.dashboard.yml` file for your board. Also make sure you have the secrets defined otherwise it will not work and use defaults from this repository. Finally, make sure you set your `flash_size` correctly, because otherwise you will get errors after booting, by adding this to your `substitutions`:

```
  flash_size: 4MB
```
