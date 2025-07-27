# 🌿 OrtoWan

**OrtoWan** è un sistema di irrigazione automatizzata e connessa via LoRaWAN, progettato per monitorare l’umidità del terreno e gestire l’irrigazione in modo intelligente. La versione 0.3.1 introduce una modalità di test fittizio per la Heltec, utile quando Arduino non è collegato o non trasmette.

## 🚀 Funzionalità

- Irrigazione in due fasi:
  - **Fase fissa**: 5 minuti garantiti
  - **Fase estesa**: +5 minuti se l'umidità > 500
- Fasce orarie **compatte da 30 minuti**, variabili per mese
- Irrigazione **automatica di 3 minuti al riavvio** (reset)
- Sensori analogici per umidità del terreno
- Conteggio litri irrigati tramite impulsi (flussometro)
- Trasmissione dati via LoRaWAN (5 byte) su TTN
- Log diagnostico via seriale
- **Generazione automatica di dati fittizi** sulla Heltec se Arduino non comunica
- Codice errore `7` per segnalare assenza di dati reali

## 🛠️ Componenti

### Arduino
- Sensori umidità (A0, A1)
- Pompa su pin digitale
- RTC DS1307 per controllo orario

### Modulo Heltec LoRa
- Ricezione UART dei dati da Arduino
- Invio ciclico su The Things Network
- Simulazione dati se Arduino non trasmette
- Codifica compatta del payload

## 📡 Payload TTN

```plaintext
Byte 0: Umidità 1 (%)
Byte 1: Umidità 2 (%)
Byte 2: Stato pompa (0/1)
Byte 3: Impulsi flusso
Byte 4: Codice errore
