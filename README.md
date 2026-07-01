# SOS Emergency Tracker

A compact embedded safety device that sends your GPS location to emergency contacts via 4G LTE — triggered by a single pull-pin, no smartphone needed.

> Built with ATmega328P + SIMCom A7672S | Custom 2-layer PCB (KiCad)

---

## Demo

![3D PCB Render](media/pcb_layout.png)

---

## How It Works

1. Pull the pin → ATmega328P detects the interrupt
2. A7672S acquires location via cell tower triangulation (`AT+CIPGSMLOC`)
3. SMS with coordinates sent to all predefined emergency contacts
4. Buzzer confirms activation

No app. No unlock screen. One action.

---

## Hardware

| Component | Role |
|---|---|
| ATmega328P | Main MCU, firmware, GPIO control |
| SIMCom A7672S | 4G LTE modem + GNSS (cell triangulation) |
| TP4056 | Li-Ion battery charging |
| XC6206 | 3.3V LDO regulator |
| USB Type-C | Charging interface |
| 2N2219 | Buzzer driver (NPN BJT) |
| Pull-pin switch | Emergency trigger |

Full BOM with prices → [`hardware/bom.csv`](hardware/bom.csv)  
Schematic → [`hardware/schematic.pdf`](hardware/schematic.pdf)  
PCB layout → [`hardware/pcb_layout.png`](hardware/pcb_layout.png)

---

## Firmware

- Trigger detection via GPIO interrupt
- UART AT command sequences to A7672S for location + SMS dispatch
- Low-power standby between events

Source → [`firmware/sos_tracker.ino`](firmware/sos_tracker.ino)

---

## Challenges

- Built a custom KiCad symbol for the 130-pin A7672S module from scratch
- Resolved multiple ERC violations in the TP4056 charging circuit (TEMP/CE floating pins, USB-C CC resistors)
- Chose cell tower triangulation over a separate GPS module to cut cost and component count
- Debugged XC6206 pin assignment errors and crystal load cap orientation

---

## Repo Structure

```
sos-tracker/
├── README.md
├── hardware/
│   ├── schematic.pdf
│   ├── pcb_layout.png
│   └── bom.csv
├── firmware/
│   └── sos_tracker.ino
├── docs/
│   └── project_report.pdf
└── media/
    └── demo.jpg
```

---

## Future Work

- BLE companion app for contact management
- Live location tracking + cloud dashboard
- Geofencing alerts
- OTA firmware updates
- Miniaturized enclosure

---

## Author

**Anshika Yadav**  
Electrical Engineering, IIT Goa
