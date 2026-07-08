# Hotel La Meraviglia - Progetto di Cablaggio

## Panoramica della Struttura

La struttura dispone di **100 camere** distribuite su **4 piani** (25 camere per piano), oltre a un **Piano Terreno (PT)** destinato ai servizi comuni.

---

# Hardware di Rete Attivo

## Switch

| Dispositivo | Quantità | Descrizione |
|------------|---------:|-------------|
| Switch Aula Informatica | 1 | Switch principale da 24 porte con almeno 8 porte SFP+ 10 Gbps per l'aggregazione delle dorsali |
| Switch Camere (P1-P4) | 4 | Switch 48 porte PoE+ con uplink 10 Gbps |
| Switch Piano Terreno | 1 | Switch 24/48 porte PoE+ per area svago, ristorante, bar e servizi |

## Access Point Wi-Fi

| Dispositivo | Quantità | Descrizione |
|------------|---------:|-------------|
| AP Wi-Fi High-Density | 3 | Uno per ciascuna delle sale Meeting 1, 2 e 3 |
| AP Wi-Fi Standard | 30 | Circa 6 AP per piano per coprire i 650 m² (camere e corridoi) |
| AP Wi-Fi Ospiti | 1 | Access Point dedicato agli ospiti degli uffici |
| Extender Wi-Fi | 15 | 3 extender per piano per la copertura Wi-Fi degli ospiti |

---

# Infrastruttura Passiva e Carpenteria

| Componente | Quantità | Descrizione |
|------------|---------:|-------------|
| Armadio Rack Principale | 1 | Rack da pavimento 42U (800/1000 mm) con ventilazione forzata |
| Armadi Rack Secondari | 4 | Rack a parete da 12U o 15U |
| Patch Panel RJ45 Cat.6A | 10-12 | Patch panel da 24 porte distribuiti tra i rack |
| Prese RJ45 Cat.6A | 250-300 | 2 prese per ciascuna delle 100 camere, oltre a uffici, sale meeting, bar e telecamere |
| Moduli SFP+ 10G | 10 | Transceiver per collegamenti in fibra |
| Tratte in Fibra Ottica Multimodale | 5 | Dorsali dal Core Switch agli switch di piano e del Piano Terreno |

---

# Riepilogo Costi Stimati

## Hardware di Rete

| Componente | Quantità | Costo Stimato |
|------------|---------:|--------------:|
| Switch Core (Aula Informatica) | 1 | € 1.500 – € 2.500 |
| Switch Camere (P1-P4) | 4 | € 800 – € 1.300 cad. |
| Switch Piano Terreno | 1 | € 400 – € 600 |
| AP Wi-Fi High-Density | 3 | € 300 – € 500 cad. |
| AP Wi-Fi Standard | 30 | € 150 – € 250 cad. |
| AP Wi-Fi Ospiti + Extender | 16 | € 100 – € 150 cad. |

## Infrastruttura Passiva

| Componente | Quantità | Costo Stimato |
|------------|---------:|--------------:|
| Armadio Rack Principale | 1 | € 600 – € 1.200 |
| Armadi Rack Secondari | 4 | € 150 – € 250 cad. |
| Patch Panel RJ45 | 12 | € 50 – € 100 cad. |
| Prese RJ45 a muro | 300 | € 5 – € 10 cad. |
| Moduli SFP+ e Fibra | 15 | € 50 – € 150 cad. |

---

# Stima Economica Complessiva

La spesa totale stimata per i soli componenti hardware è compresa tra:

> **€ 20.000 – € 35.000**

**Nota:** I prezzi sono indicativi e si intendono **al netto di IVA, installazione, configurazione e licenze software**.
