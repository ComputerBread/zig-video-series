# intro to computers

1. Computer components
2. Electricity, bits, bytes, binary representation
3. How programs are executed (high level)
    - compilation, source code -> assembly -> machine code
    - code loaded from disk into ram
    - RAM representation (big array of bytes with an address)
    - registers, PC pointing to code in memory
4. The software layer
    - BIOS/UEFI
    - Bootloader
    - Operating system (kernel, tty)
    - shell

TODO:
- [] clearly identify what you want to talk about
    - present the components of a computer
    - big model: CPU, Main memory, BUS, disk
    - how CPU execute a program: cpu reads instruction from memory and execute them
    - GOALs:
        - be able to understand how a program written in zig, is compiled and executed by the machine
        - binary representation?
- [] split the work into multiple smaller tasks
    - the CPU, do we talk about the different elements of it?
        - probably not, keep it high level
        - do we talk about the cache now? about the MMU?
    - memory
    - how electricity is used to represent information
- [] watch the videos

le plan:

- computers are made of:
    - motherboard, CPU, RAM, disk, bus, GPU, other I/O
    - power supply
- computers work with electricity, voltage
    - 0V = 0, 1.2V/3.3/5V = 1
    - binary
    - all info = 0 and 1
- CPU
    - made of "logic circuits"
        - AND, OR, NAND, NOR, XOR gates...
        - different units, UAL
    - perform basic work/operations, instructions
    - to instruct a CPU to perform an operation, pretty much equivalent to putting
      0s and 1s on some wires
    - Ok! but where do the 0 & 1 comes from?
    => from MAIN MEMORY

    machine code = 0s and 1s
    Assembly = mnemonics, text, human readable

- Memory
    - the role of the main memory, or the RAM, is to hold the informations that
    the CPU needs to run programs:
        - the program itself
        - any data it needs

shit, I am struggling, like I have a vague idea of what I want to teach, but
not how, don't know about the order...


Maybe a nicer solution is to say:
- let's look at how a computer execute a program!
- a executable program is really a file containing 0s and 1s. This file is store
on some storage device, called the disk, such as an SSD or a HDD.
- to execute the program, the content of this file, is loaded into memory.
this file contains the machine code, the instructions that the CPU needs to
execute.
- the CPU have some small slots of memory called "registers". They are used
by the CPU. On of them is called the Program Counter (PC) also called Instruction
Counter, or Instruction Pointer. And it used to point to the instruction to
execute. The CPU will range


-----------------------------------------

# SCRIPT

## 1-intro

Computers come in different shapes and forms. But they share the components

## 2-hardware components

- Motherboard
- CPU or Central Processing Unit is the brain of the computer, the part
  responsible for executing a program
- RAM or Random Access Memory, is the main memory that is used by the CPU to
  read and write data!
- Drive, or secondary memory, or storage device, is used to stored any data
  persistently
- Bus
- Power supply, to provide electricity to the whole thing
- Cooling system, all that generates at ton of heat, that needs to be removed to
  maintain an optimal work environment and avoid damage

## 3-electricity, binary data representation, instructions

## 4-memory part

EDU GOALS
- student should know:
    - MAIN memory/RAM
        - stores binary data (0, 1). (optional in DRAM cell, 1T1C)
        - each byte has an address

- [] talk about registers
- [] RAM
- [] cache

L1, L2 per CPU core.
L3 cache shared by all cores.

RAM uses 1T1C (DRAM)
Cache uses SRAM 6Transistors per bit

registers store bits in D Flip-flop, 16 transistors per bits

----

Let's begin our discussion on computers by defining what we mean by computers,
because they come in many shapes and places, and would like to share the mental
model that I have in mind when I say the word "computer".

When I think about computers, my mind first goes to a PC, a personal computer,
the one you have on your desk.
When you have a PC, you usually have a monitor, a keyboard, a mouse and a tower.
But the monitor, keyboard and mouse are just peripherals. The computer is inside
the tower. If we look inside, we'll see the motherboard.
The motherboard is responsible to connect every parts together.
Connected to it, we will see the CPU, the RAM, the DISK! differents peripherals, that we can ignore for now

And the power supply. The
To work, the computer and it's different components, use this electric signal
to perform different types of operations, store and retrieve information.
This is the magic of computer, from a physical signal that is electricity, it's
able to do lot of wonderful things. If you're watching this video, is because
of the absolute gigachads who figured out how to shape and control electricity
using some magical stones.

If we want to truly understand computers, we need to learn how electricity can
be used to represent information!

---------

let's not forget about a crucial part, the power supply unit, that transforms
the electricity from some external source into stable continous voltage and
provides it to the different parts of the computer.

Depending of the component, the voltage will be different. A modern CPU will
for example need 1.2 Volts. And using this


The reality is that Computers are made of some sort of magical stones that can
control electricity! If we want really want to understand computers, we need
to talk a bit about Digital electronics.

I mean, no jokes, all the data processed by a computer correspond to the presence
or absence of voltage on a wire.
When the voltage is high, we represent it with a 1, if it's low, when the voltage
is 0, then we represent it with, you guessed it, a 0.
All information in a computer is represented by a bunch of zeroes and ones.


1.2 Volts for modern CPU (ex: [AMD Ryzen 7 5800X3D](https://valid.x86.fr/2rakg0))



---------

"As shown in exhibit A"...

[] watch <https://www.youtube.com/watch?v=geBcfKn3B1g> (49min en FR) ----------

notes:

- la vidéo ne parpe du CPU, ni du boîter d'alimentation
- carte mère
    - une pure merveille d'innovation
- boîtier d'alimentation ATX (mis de côté), son rôle se résume à deux fonctions:
    - fournir les 4 tensions requises: +12V, -12V, +5V, +3,3V
    - fournir une intensité de courant suffisamment dimensionnée pour tenir la charge nécessaire

Tour d'horizon (~3min30, cool closeup footage):
- carte mère:
    - circuit imprimé principal sur lequel tous les autres composants viennent
      se connecter. C'est elle qui assure la communication entre eux.
    - contient des ports pour connecter les différents péripheriques
    - sockets pour le processeur
    - slots pour la RAM
    - ports PCI pour les cartes d'extension
    - des connecteurs pour le stockage
- CPU
    - le cerveau de l'ordinateur
    - responsable de l'exe des instru des programmes
    - dégage beaucoup d'énergie calorifique
      doit être refroidi efficassement par ventilateur ou autre
      sinon risque de panne ou dégradation de composant
    - gère la mémoire et les connexions au débit
- RAM
    - utilisé pour stocker temporairement les données utilisées par le processeur
    - mémoire volatile, toutes les données stockées sont perdues lorsqu'elle
      n'est plus électriquement alimentée
- stockage
    - soit HDD (disque dur mécanique à plateau magnétique)
    - soit SSD, puces de mémoire flash (max 8TB)
- GPU, carte graphique
    - responsable du rendu des images vidéos et animations
    - modélisation, rendu 3D, montage vidéo, VR
    - certain processeur ont un gpu intégré mais performance limitées

- boîter d'alimentation ATX
    - alimente l'ensemble des composants
    - convertit courant alternatif 230V en courant continu

- périph
    - pavé tactile, scanner, micro, webcam, tablette graphique, manette de jeu,
      volant/pédalier de course, casque VR, lecteur CD...
    - entrée: souris, clavier
    - sortie: moniteur, haut-parleur, casque audio, imprimante...

- carte mère
    - la colonne vertebrale du pc
    - transporte les signaux analogique, numérique, fort courant de plusieurs dizaines d'ampères
    - socket du CPU, 1200 micro contacteurs
    - entrée 12V, CPU ~1,3V
      CPU peut dépasser les 90 ampères à pleine charge
    - voltage regulator
    - PCH: Platform Controller Hub (chipset de la carte mère)
        - hub central qui gère les communication entre processeur et les différents composants
        - les anciennes architectures avaient 2 chipsets: North bridge & south bridge
          mais les CPUs modernes intègrent le controleur mémoire et le contrôleur PCI express
          le north bridge est devenu obsolète
        - gère les fonctions bas débit
          USB, SaTA, PCI Express, ethernet, wifi, audio...
        - Clock!
        - PCH & CPU communiquent entre eux via l'interface DMI (direct media interface)
          (check 15:53min)

- le BIOS (18:31)
    - micro logiciel = firmware stocker dans une petite EEPROM
    - se charge en mémoire au démarrage de l'ordinateur pour init le matériel
      avant de lancer l'OS
    - !!!!!
      1. Allumage PC
      2. BIOS/UEFI s'initialise, vérification du firmware
      3. power-on self-test (POST), vérification du matériel
      4. si problème détecté -> affichage erreur, FIN, sinon 5
      5. Détection des périphériques (HDD, SSD, USB, RAM, GPU...)
      6. chargement du bootloader (MBR/EFI) (lecture disque de démarrage)
      7. Démarrage du système d'exploitation

- mémoire CMOS
    - petite pile/batterie
    - stocke info utile quand le pc est éteint
        - date, heure système, ordre du démarrage au boot
    - alimente real time clock, meme hors tension

- RAM, SRAM, SDRAM
    - barre de ram peut posséder une puce de correction d'erreur
    - communique directement avec le CPU sans aucun autre élement intermédiaire

35:00





-------------------------------------------------------------------------------


[] (57 min) digital electronics - the first video you should watch <https://www.youtube.com/watch?v=pDELW2pIvWw>
[] PC architecture <https://youtu.be/_I8CLQazom0?si=IL8OkccuWxD3bu9V&t=316> (18 min)
[] (19 min) Architecture All Access: Modern CPU arch PART 1 <https://www.youtube.com/watch?v=vgPFzblBh7w>
[] (25 min) Part 2 <https://www.youtube.com/watch?v=o_WXTRS2qTY>
[] smallest "hello world" <https://www.youtube.com/watch?v=BdMkqouFbBw>

[] the von neumann model <https://www.youtube.com/live/T0Ka9QG9t-o?si=pizaeehc4fiVh6rm&t=605>



To learn more about physical reality of RAM, with transistor and shit:
[Dynamic Random Access Memory (DRAM). Part 1 to 7](https://www.youtube.com/watch?v=-Df09el4yDU&list=PLTd6ceoshprfg23JMtwGysCm4tlc0I1ou&index=13)


## the von Neumann Model ?

maybe not


# SAUCE

- https://www.youtube.com/watch?v=TfhL5kBiQVI
