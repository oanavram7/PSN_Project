# Automat pentru Cumpărarea Biletelor de Tren (FPGA / VHDL)

## Descriere Generală

Acest proiect reprezintă implementarea unui automat digital pentru vânzarea biletelor de tren, realizat pe o placă de dezvoltare FPGA **Basys 3**. Sistemul permite utilizatorului să introducă distanța, calculează prețul, primește plata și eliberează biletul și restul, semnalizând totodată diverse situații de eroare.

[cite_start]Proiectul a fost dezvoltat în cadrul disciplinei **Proiectarea Sistemelor Numerice** (PSN)[cite: 216, 220].

## Detalii Implementare

| Detaliu | Valoare | Sursă |
| :--- | :--- | :--- |
| **Autor** | [cite_start]Avram Oana-Teodora | [cite: 217, 221] |
| **Placă de Dezvoltare** | [cite_start]Digilent Basys 3 (Xilinx Artix-7, **xc7a35tcpg236-1**) | [cite: 330, 345] |
| **Limbaj** | [cite_start]VHDL | [cite: 331] |
| **Software** | [cite_start]Xilinx Vivado (v2024.2) | [cite: 336, 340] |
| **Profesor Coordonator** | [cite_start]Ella Seres | [cite: 219, 223] |

## Funcționalități Cheie

[cite_start]Sistemul este un automat de stat finit (FSM) împărțit în Unitatea de Control (UC) și Unitatea de Execuție (UE)[cite: 231, 290], care gestionează următorii pași:

1.  [cite_start]**Introducerea Distanței:** Utilizatorul introduce distanța dorită (în zeci de km) folosind un set de comutatoare (switches)[cite: 245, 253].
2.  [cite_start]**Generarea Prețului:** Prețul biletului este calculat automat pe baza unei rate prestabilite de **5 Euro per kilometru**[cite: 254, 326].
3.  [cite_start]**Plata și Afișarea:** Prețul, suma introdusă și restul sunt afișate pe display-ul cu 7 segmente controlat prin multiplexare[cite: 246, 255, 260, 264, 314].
4.  [cite_start]**Managementul Plății:** Automatul acceptă sume sub formă de bancnote și monede (între 1€ și 50€)[cite: 247, 248].
5.  [cite_start]**Eliberarea Biletului:** După confirmarea restului, biletul este eliberat, semnalizat printr-un LED (**`bilet_eliberat`**)[cite: 266].
6.  [cite_start]**Renunțare:** Se poate renunța la operație în orice moment, cu restituirea sumei introduse[cite: 250].

### Semnalizări de Eroare

[cite_start]Sistemul semnalizează luminos (LED **`eroare`**) următoarele situații critice[cite: 249, 267]:

* [cite_start]Suma introdusă este mai mică decât prețul biletului[cite: 268].
* [cite_start]Nu există suficiente bilete disponibile[cite: 269].
* [cite_start]Automatul nu poate restitui restul necesar (din lipsă de bancnote/monede în casierie)[cite: 270].

### Componente Logice Cheie

* [cite_start]**Convertor Binary to BCD:** Realizează conversia de la binar la BCD (Binary-Coded Decimal) pentru afișarea separată a sutelor, zecilor și unităților pe display-ul cu 7 segmente[cite: 294, 301].
* [cite_start]**Metoda Utilizată:** **Double Dabble** (pentru conversia binar-BCD)[cite: 307].
* [cite_start]**Afișor:** Utilizează multiplexare pentru a afișa pe rând sutele, zecile și unitățile [cite: 314, 319-321].

## Instrucțiuni de Utilizare (Hardware Basys 3)

[cite_start]Pentru a rula proiectul pe placa Basys 3, urmați diagrama de mai jos pentru alocarea pinilor de intrare/ieșire[cite: 354]:

| Semnal | Tip | Locație pe Basys 3 | Descriere |
| :--- | :--- | :--- | :--- |
| **`distanța`** | Intrare | Switches (SW) | [cite_start]Introducerea distanței dorite (în zeci de km)[cite: 275]. |
| **`suma_plătită`** | Intrare | Switches (SW) | [cite_start]Introducerea sumei de bani pentru plată[cite: 277]. |
| **`btn_confirm1`** | Intrare | Buton (BTN_C) | [cite_start]Confirmă continuarea procesului (ex: confirmare preț)[cite: 257, 282]. |
| **`cancel`** | Intrare | Switch (SW) | [cite_start]Renunțarea la tranzacție[cite: 279]. |
| **`reset`** | Intrare | Buton (BTN_R) | [cite_start]Resetează automatul în starea inițială[cite: 280]. |
| **Afișor** | Ieșire | Display 7 segmente | [cite_start]Afișează prețul, suma introdusă și restul[cite: 285, 354]. |
| **`bilet_eliberat`** | Ieșire | LED (LD) | [cite_start]Se aprinde la eliberarea cu succes a biletului[cite: 287, 354]. |
| **`eroare`** | Ieșire | LED (LD) | [cite_start]Se aprinde la orice situație de eroare[cite: 288, 354]. |

## Posibilități de Dezvoltări Ulterioare

[cite_start]Proiectul poate fi extins cu următoarele funcționalități[cite: 365, 367]:

* [cite_start]**Selectarea Clasei de Călătorie:** Adăugarea opțiunii pentru Clasa I / Clasa a II-a, cu tarife diferite per kilometru[cite: 368, 369].
* [cite_start]**Suport pentru Mai Multe Valute:** Adaptarea sistemului pentru a accepta diferite valute (nu doar Euro)[cite: 371, 372].
* [cite_start]**Interfață Grafică:** Conectarea la un ecran VGA pentru a simula un panou grafic mai avansat[cite: 373, 374].
