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

- ***Wo sind große Unterschiede zwischen C und anderen hohen Programiersprachen?***

C ist eine imperative und prozedurale Programmiersprache.

- ***Was ist ein Header-File und wo werden in C die Funktionen implementiert?***

  Ein Header-File ist eine Textdatei mit der Endung ***.h***. Sie werden in C & C++ dafür verwendet bestimmte Dinge, die in mehreren Programmen benutzt werden, zu definieren. 

  Sie beinhalten: 

  * Definitionen von Funktionen 
  * Definitionen von Variablendatentypen 
  * Macros In Header-Files kann man sowohl nur Funktionen definieren, als auch implementieren.

- ***Wie kommen Toolchains bzw. Firmwares bei der Programmierung von Embedded Systems zum Einsatz?***

Häufig beinhaltet eine Toolchain einen Compiler, Laufzeig-Bibliotheken und einen Linker.
Mit einer Toolchain wandelt man den Sourcecode in ein ausführbares Programm um. Eine Toolchain besteht aus einer Kette von Tools, die jeder einen Teil dazu beitragen, das der Sourcecode ein ausführbares Programm wird. 

- ***Wie sind Datenblätter eines Mikrokontrollers und des Demo-Boards (z.B. STM32F3-Discovery) aufgebaut? Wo finde ich dabei die Interface Description der Toolchain?***

Grundsätzlich variiert jedes Datenblatt, aber meistens gibt es eine Einfühurng der Kontroller. Weiters gibt es Auflistungen der Anschlüsse, wichtige/besondere Eigenschaften des Mikrokontrollers und Schaltpläne werden auch mit eingebunden.

In dem Technical Reference Manual des ARM Cortex-M4 Prozessor gibt es eine kurze Einführung der Interfaces im Chapter 1, *1.3 Interfaces*.

Im STM32F3DISCOVERY User manual werden im *quick start*, Punkt 2.3 die development toolchains aufgelistet.

- ***Was bedeutet das Akronym HAL bei der Implementierung von Embedded Devices?***

HAL, abkürzung für **H**ardware **A**bstraction **L**ayer.

- ***Was macht der Befehl make und wie ist das Makefile im [stm32f3-template](https://github.com/mborko/stm32f3-template) Repository aufgebaut?***

  Mit `make`  kann man Programme verwalten, aktualisieren und generieren. Dabei wird die Konfiguration aus dem *Makefile* verwendet.  
  Das *Makefile* im stm32f3-template ist folgendermaßen aufgebaut:   

  	* Variablen definiert  
  	* Ordner inkludiert 
  	* Libraries definiert 
  	* Flags gesetzt 
  	* gebuildet  
  	* Output definiert  
  	* mögliche Befehl definiert

- ***Wo ist die Methode BSP_LED_Init() definiert und wo implementiert? Welche Schritte werden in der implementierten Methode durchgeführt? Was ist dabei der Pull-Mode?***

In der Methode wird die GPIO-Clock *(General Purpose Input Output)* für eine LED aktiviert und konfiguriert. 
Die Methode ist in **stm32f3_discovery.c** definiert.
Hierbei wird festgelegt, welchen Port und Modus man verwenden möchte, ob es pull up oder pull down sein soll und mit welchem Speed man darauf zugreifen können soll.
Der Pull-Mode gibt an, ob man Vcc-Spannung (Pullup) oder 0V bzw. GND (Pulldown) haben möchte.

- ***Was ist ein GPIO-Port und wieviele sind auf dem STM32F3-Discovery einsetzbar?***

Allzweckeingabe/-ausgabe ist ein Port welcher ein allgemeiner Kontaktstift in einem integrierten Schaltkreis ist. Dieser kann durch logisches Programmieren frei bestimmbar sein. Der *STM32F3* hat 88 *GPIO-Ports*.

- ***Auf welchem GPIO Pin liegen die einzelnen LEDs des STM32F3-Discovery Boards?***
  * LED_4  = GPIO_E_PIN_8  (top left  - Blue)   
  * LED_3  = GPIO_E_PIN_9  (top - Red)   
  * LED_5  = GPIO_E_PIN_10  (top right  - Orange)   
  * LED_7  = GPIO_E_PIN_11  (right  - Green)  
  * LED_9  = GPIO_E_PIN_12  (bottom right  - Blue)   
  * LED_10 = GPIO_E_PIN_13  (bottom  - Red)   
  * LED_8  = GPIO_E_PIN_14  (bottom left  - Orange)   
  * LED_6  = GPIO_E_PIN_15  (left  - Green)  
- ***Wie könnten die LEDs auch ohne der implementierten Library angesteuert werden?***

Man kann `BSP_LED_Init(...)` ,`BSP_LED_Toggle(...)` ,`BSP_LED_On(...)` und `BSP_LED_Off(...)` verwenden. 
Alternativ kann man aber auch die einzelnen Pins mit dem Befehl `HAL_GPIO_WritePin(...)` setzen.

## Quellen

[Quelle 1](https://www.w3schools.in/c-tutorial/custom-header-file-in-c/)

[Quelle 2](https://www.geeksforgeeks.org/header-files-in-c-c-with-examples/)

[Quelle 3](https://www.badprog.com/electronics-stm32-gpio-overview-with-the-stm32f3-discovery-board)