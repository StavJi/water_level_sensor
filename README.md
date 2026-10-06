# Snímač hladiny vody s ovládáním čerpadla pro automatickou závlahu

Projekt je postavený na ESP32 s ethernetovým modulem W5500 Lite a diferenciálním snímačem tlaku, který měří výšku vodního sloupce. Otestováno s komponentami uvedenými v sekci **Hardware**.

Konfigurační YAML soubor najdete ve složce `sw`, fotografie hotového prototypu ve složce `foto`.

## Historie verzí

Zde popsané zapojení je už třetí iterací:

1. **Bateriová verze** – ESP32 byl většinu času uspaný a jednou za 30 minut odeslal data přes WiFi. Napájel ho jeden článek s kapacitou 4 Ah, který na jedno nabití vydržel přibližně rok. Kvůli plánovanému rozšíření o automatickou závlahu trávníku bylo potřeba přejít na novou verzi.
2. **Verze s trvalým napájením** – zařízení je napájené trvale z 24 V a umí spínat 230V čerpadlo, včetně jeho ochrany při poklesu hladiny pod nastavenou mez. Data se stále odesílala přes WiFi, což kvůli slabému signálu občas způsobovalo výpadky (anténa je v šachtě pod poklopem).
3. **Verze s ethernetem** – přibyl ethernetový modul W5500, takže data jdou po kabelu a výpadky WiFi už nehrozí.

## Hardware

### Zapojení

**TBD**

### BOM

- [ESP32](https://www.laskakit.cz/laskakit-esp32-devkit/?variantId=11481)
- [Ethernetový modul W5500](https://www.laskakit.cz/mikro-ethernet-modul-w5500/)
- [DC/DC měnič s LM2596](https://www.laskakit.cz/step-down-menic-s-lm2596/)
- 2× [dioda 1N4148](https://www.gme.cz/v/1487018/semtech-1n4148-dioda)
- 2× [tranzistor BC337](https://www.gme.cz/v/1485969/semtech-bc337-25-bipolarni-tranzistor)
- 1× [kondenzátor 100 nF](https://www.gme.cz/v/1489676/hitano-ck-100n-50v-x7r-rm508-10-keramicky-kondenzator)
- 1× [kondenzátor 470 µF / 35 V](https://www.gme.cz/v/1489656/hitano-ce-470u-35vit-hit-esx-10x20-rm5-bulk-elektrolyticky-kondenzator)
- Rezistory **(TBD hodnoty)**
- Svorky WAGO
  - 3× [oranžová](https://www.gme.cz/v/1499108/wago-256-746-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina)
  - 3× [světle šedá](https://www.gme.cz/v/1499111/wago-256-401-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina)
  - 1× [modrá](https://www.gme.cz/v/1499107/wago-256-744-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina)
  - 1× [zelená](https://www.gme.cz/v/1499109/wago-256-747-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina)
  - 1× [tmavě šedá](https://www.gme.cz/v/1499047/wago-256-742-svorkovnice-1pol-roztec-508mm-24a-320v-vstup-45-pruzina)
  - 1× [bočnice oranžová](https://www.gme.cz/v/1501453/wago-256-600-bocnice-pro-256-oranzova)
  - 1× [bočnice modrá](https://www.gme.cz/v/1501452/wago-256-400-bocnice-pro-256-modra)
  - 1× [bočnice tmavě šedá](https://www.gme.cz/v/1501440/wago-236-200-bocnice-pro-236-tmave-seda)
- Voděodolná zásuvka – [KV Elektro](https://www.kvelektro.cz/zasuvka-scame-protecta-ip66-137-4411-do-sestav-bez-krabice-p1236195) nebo [Alza](https://www.alza.cz/hobby/solight-zasuvka-ip66-vodotesna-a-prachotesna-d12895804.htm)
- [Relé](https://www.gme.cz/v/1502113/finder-405290240000-rele-civka-24vdc-kontakt-250vac-8a-2x-prepinaci) s [paticí](https://www.gme.cz/v/1498684/finder-9505-patice-pro-rele-4051-52-61-na-din-listu) na DIN lištu
- [AC/DC zdroj](https://www.gme.cz/v/1506306/mean-well-hdr-15-24-spinany-zdroj-na-din-listu) 230 V → 24 V. Při použití relé s jiným napětím cívky lze zvolit i 12V nebo 5V zdroj.
- [Snímač hladiny vody](https://allegro.cz/produkt/fotoelektricky-snimac-hladiny-kapaliny-4-20ma-ip68-ponorny-5d731506-9f41-4c8e-a7c2-fc99b2056e58?offerId=18372650584) – snímačů existuje celá řada, na AliExpressu je najdete pod heslem **Liquid Level Transmitter**. Já používám verzi s napájením 5 V a napěťovým výstupem (0–3.3) V, který odpovídá výšce hladiny (0–3) m. Napájecí napětí snímače 5 V jsem historicky zvolil kvůli napájení z baterie. S vyšším napájecím napětí (24 V) rapidně roste množství snímáčů ze kterých lze vybírat.
- [Univerzální DPS 160 × 100 mm](https://www.gme.cz/v/1508180/rademacher-up830ep-univerzalni-spoj-160x100mm)
- Voděodolná krabička **(TBD typ)**

## Software

1. V konfiguraci změňte IP adresu MQTT brokeru na svou a vyplňte přihlašovací údaje.
2. Změna tvaru a velikosti nádrže:
  - **TBD**
3. Sestavte firmware podle [návodu ESPHome](https://esphome.io/guides/getting_started_command_line.html):

```sh
   make compile
```

4. Nahrajte firmware do desky:

```sh
   make upload
```
