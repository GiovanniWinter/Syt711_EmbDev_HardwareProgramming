# Syt Labor 711 EmbDev Hardware Programming

**Giovanni Winter, 16.12.2020**

# Setup

[Template auf Github](https://github.com/mborko/stm32f3-template)

[Aufgabenstellung](https://elearning.tgm.ac.at/mod/assign/view.php?id=144370)

Das komplette Template habe ich kopiert und auf [mein Repository](https://github.com/GiovanniWinter/Syt711_EmbDev_HardwareProgramming) geladen.

```bash
git remote add origin https://github.com/GiovanniWinter/Syt711_EmbDev_HardwareProgramming.git
git branch -M main
git push -u origin main
(falls es ein Origin schon gibt: git remote remove origin)
```

Weiters habe ich unter *src* den Ordner *Template* kopiert und auf **ampelschaltung** unbenannt und darin die Änderungen der `main.c` unternommen.

# Makefile

Zeile 31 auf `PROJ := src/ampelschaltung` ändern.

# main.c

Hier habe ich das initialisieren der Leds nur auf der beschränkt (rot, gelb, grün). 

In der while Schleife rufe ich nur  `Toggle_Leds();` auf.

Das Auskommentierte könnte man auch entfernen.

![image-20201216105305933](C:\Users\Giovanni\AppData\Roaming\Typora\typora-user-images\image-20201216105305933.png)

# Fragestellungen



- ***Wie sind Datenblätter eines Mikrokontrollers und des Demo-Boards (z.B. STM32F3-Discovery) aufgebaut? Wo finde ich dabei die Interface Description der Toolchain?***

In dem Technical Reference Manual des ARM Cortex-M4 Prozessor gibt es eine kurze Einführung der Interfaces im Chapter 1, *1.3 Interfaces*.

Im STM32F3DISCOVERY User manual werden im *quick start*, Punkt 2.3 die development toolchains aufgelistet.