# Progetto Cablaggio – Sogno

## Descrizione della Struttura

La struttura è composta da:

- 1 reception centrale con uffici
- 15 mini-case indipendenti

---

# Hardware di Rete Attivo

## Centro Stella (Reception)

### Switch Principale

| Componente | Quantità | Descrizione |
|------------|---------:|-------------|
| Switch Managed 24 porte PoE+ | 1 | Alimenta PC degli uffici, amministrazione, telefoni VoIP della reception e collegamenti verso le mini-case. |

### Collegamenti verso le Mini-Case

**Opzione Fibra**
- 15 × Media Converter oppure porte SFP sullo switch.

**Opzione Wireless**
- 1 × Base Station / Antenna Settoriale Punto-Multipunto installata sul tetto della reception.

---

## Mini-Case (15 unità)

### Access Point Wi-Fi

| Componente | Quantità | Note |
|------------|---------:|------|
| Access Point Wi-Fi | 15 | 1 per mini-casa, configurato con IP statico sulla VLAN 51. |

### Dispositivi Client (forniti dalla struttura)

| Componente | Quantità |
|------------|---------:|
| Tablet | 15 |
| Smart TV | 15 |

### Collegamento Esterno

| Opzione | Quantità |
|---------|---------:|
| CPE / Antenna Client (Wireless) | 15 |
| Mini-borchia ottica (Fibra) | 15 |

---

# Infrastruttura Passiva

## Armadio Rack

| Componente | Quantità |
|------------|---------:|
| Rack 12U / 15U | 1 |

## Prese RJ45

### Reception

- Circa **10–15 prese RJ45**
  - Uffici
  - Cassa
  - Telefoni VoIP

### Mini-Case

- **30 prese RJ45**
- 2 prese per ogni mini-casa:
  - Smart TV
  - Access Point / Tablet

---

# Stima dei Costi

## 1. Hardware Attivo

| Componente | Quantità | Prezzo Unitario | Totale |
|------------|---------:|----------------:|-------:|
| Switch Managed 24 porte PoE+ | 1 | €300,00 | €300,00 |
| Access Point Wi-Fi Professional | 15 | €120,00 | €1.800,00 |
| Tablet 10" | 15 | €180,00 | €2.700,00 |
| Smart TV 32" Hotel Mode | 15 | €180,00 | €2.700,00 |
| Unità Ricezione Esterna (CPE/Borchia) | 15 | €80,00 | €1.200,00 |
| Media Converter / SFP | 15 | €60,00 | €900,00 |

### Totale Hardware Attivo

**€ 9.600,00**

---

## 2. Infrastruttura Passiva

| Componente | Quantità | Prezzo Unitario | Totale |
|------------|---------:|----------------:|-------:|
| Armadio Rack 12U/15U | 1 | €200,00 | €200,00 |
| Prese RJ45 (posa, terminazione e test) | 45 | €120,00 | €5.400,00 |
| Accessori Rack (Patch Panel, Guide, Ventole) | 1 | €300,00 | €300,00 |

### Totale Infrastruttura Passiva

**€ 5.900,00**

---

# Riepilogo Economico

| Voce | Importo |
|------|---------:|
| Hardware Attivo | **€ 9.600,00** |
| Infrastruttura Passiva | **€ 5.900,00** |

## Investimento Totale Stimato (IVA esclusa)

# **€ 15.500,00**
