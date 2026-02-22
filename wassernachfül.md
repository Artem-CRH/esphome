# Kaffee-Nachfuellanlage (ESPHome + Home Assistant)

Dieses Projekt steuert eine Wasser-Nachfuellanlage mit ESPHome auf einem Seeed XIAO ESP32-C3.

## Funktionen

- Abstandsmessung per Ultraschall (cm) in Home Assistant und Terminal-Log.
- Pumpensteuerung per MOSFET mit PWM.
- Start/Stop-Automatik ueber Min/Max-Abstand.
- Anlagen-Freigabe ueber Schalter `Wassernachfuehlanlage`.
- Taster auf GPIO10 toggelt die Anlagen-Freigabe.
- Ozongenerator per MOSFET als eigener HA-Schalter.
- Sicherheitslogik: Wenn Anlage AUS, dann Pumpe AUS und Ozon AUS.

## Pinbelegung

- `GPIO21`: Button-Beleuchtung / Anlagenstatus-LED
- `GPIO10`: Taster (INPUT_PULLUP, inverted)
- `GPIO5`: Pumpen-MOSFET (PWM, LEDC)
- `GPIO4`: Ozongenerator-MOSFET (On/Off)
- `GPIO2`: Ultraschall Trigger
- `GPIO3`: Ultraschall Echo

## Wichtige HA-Entitaeten

- `switch.wassernachfuehlanlage`
- `switch.ozongenerator`
- `sensor.abstand_wasserstand`
- `number.pumpe_pwm_soll`
- `number.abstand_min`
- `number.abstand_max`
- `binary_sensor.anlage_aktiv`
- `binary_sensor.pumpe_laeuft`

## Regelung

- Anlage muss aktiv sein (`switch.wassernachfuehlanlage = ON`).
- Pumpe startet, wenn `Abstand >= Abstand Max`.
- Pumpe stoppt, wenn `Abstand <= Abstand Min`.
- PWM wird bei laufender Pumpe sofort uebernommen, wenn `Pumpe PWM Soll` geaendert wird.
- Wenn Anlage AUS:
  - Pumpe wird sofort ausgeschaltet.
  - Ozongenerator wird sofort ausgeschaltet.
  - Ein manuelles Einschalten von Ozon wird blockiert.

## ESPHome Befehle

Config pruefen:

```powershell
esphome config xiao-esp32c3_kaffe.yaml
```

Flashen:

```powershell
esphome run xiao-esp32c3_kaffe.yaml
```

Live-Logs:

```powershell
esphome logs xiao-esp32c3_kaffe.yaml
```

## Hinweise

- Bei falscher Logik (Relais/MOSFET "verkehrt herum") `inverted: true` am jeweiligen Ausgang setzen.
- `GPIO2` ist ein Strapping-Pin. Falls Boot-Probleme auftreten, Ultraschall-Pins auf andere GPIOs legen.
