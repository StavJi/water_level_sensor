# Snímač hladiny vody
Tento projekt je založený na ESP32 s ethernetovým modulu W5500 Lite v kombinaci s diferenciálním snímačem tlaku, který slouží pro měření výšky vodního sloupce. Testováno s komponentami uvedenými v sekci **Hardware**.

Konfigurační YAML soubor je k dispozici ve složce `conf`.
Fotografie hotového prototypu jsou pak k nalezení ve složce `foto`.

## Hardware
- [ESP32](https://www.laskakit.cz/laskakit-esp32-devkit/?variantId=11481)
- [Ethernet modul](https://www.laskakit.cz/mikro-ethernet-modul-w5500/)
- [DC/DC měnič](https://www.laskakit.cz/step-down-menic-s-lm2596/)
- 2x [Dioda 1N4148](https://www.gme.cz/v/1487018/semtech-1n4148-dioda)
- 2x [Tranzistor BC337](https://www.gme.cz/v/1485969/semtech-bc337-25-bipolarni-tranzistor)
- Rezistory
- Wago svorky

oranzova https://www.gme.cz/v/1499108/wago-256-746-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina
tmave seda https://www.gme.cz/v/1499047/wago-256-742-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina
modra https://www.gme.cz/v/1499107/wago-256-744-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina
svetle seda https://www.gme.cz/v/1499111/wago-256-401-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina
zelena https://www.gme.cz/v/1499109/wago-256-747-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina
bocnice


- Voděodolná zásuvka [kvelektro](https://www.kvelektro.cz/zasuvka-scame-protecta-ip66-137-4411-do-sestav-bez-krabice-p1236195?gad_source=1&gad_campaignid=17190396887&gbraid=0AAAAAD-VuyPnHEREix-929r3cyI4Gn25q&gclid=Cj0KCQjw8ofWBhCHARIsANBj4LuaqYDFaWN9vGrd28l4m9X17WJbFi2rODPSiF-mbKyAsUfMfjdafxYaAp3GEALw_wcB) nebo [Alza](https://www.alza.cz/hobby/solight-zasuvka-ip66-vodotesna-a-prachotesna-d12895804.htm?kampan=adwho_hobby-a-zahrada_rh-top-levne-produkty_rh-top-levne-produkty_c_9218341__HoBMiM0591&gad_source=1&gad_campaignid=23509599327&gbraid=0AAAAAD2xsm4gjmrXh_q85SJiQiOYb9lxi&gclid=Cj0KCQjw8ofWBhCHARIsANBj4Lt8XwN3b0KZbHz5n99WY7XugO_A-4r8aYe3YXQcR49oQoVStNxTglYaAqP9EALw_wcB)
- [Relé](https://www.gme.cz/v/1502113/finder-405290240000-rele-civka-24vdc-kontakt-250vac-8a-2x-prepinaci) s [držákem](https://www.gme.cz/v/1498684/finder-9505-patice-pro-rele-4051-52-61-na-din-listu) na DIN lištu
- [AC/DC měnič](https://www.gme.cz/v/1506306/mean-well-hdr-15-24-spinany-zdroj-na-din-listu) z 230V na 24V. Při změně napájecího napětí cívky relé lze použít 12V případně 5V.
- Snímač hladiny vody 

## Software
1. Změň IP adresu MQTT brokeru na svůj. Nezapomeň vyplnit svoje přihlašovací údaje.
2. Build firmware podle návodu z [ESPHome](https://esphome.io/guides/getting_started_command_line.html)

```sh
make compile
```

3. Nahrání firmware do desky.

```sh
make upload
```
