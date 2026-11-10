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

GOALs:
- high level intro to computers
- know the different parts of computer
- know how electricity is turned into information
- know how a program is executed
- know what compilation is
- have a mental model of a computer

future videos:
- install zig + tools
- your first zig program
    - compilation, zig build exe, zig run
    - execution
    - entry point
- variables, data type
- if, else
- functions
- the standard library
- loops..
- Assignment: guess the number

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

1. Intro
2. Computer components
3. Electricity, bits, bytes, binary representation
4. How programs are executed (high level)
    - compilation, source code -> assembly -> machine code
    - code loaded from disk into ram
    - RAM representation (big array of bytes with an address)
    - registers, PC pointing to code in memory
5. The software layer
    - BIOS/UEFI
    - Bootloader
    - Operating system (kernel, tty)
    - shell

## 1-intro

Computers come in different shapes and forms. But they pretty much share the
same components.

## 2-hardware components

- The **Motherboard** is the spine of the computer, it is the main circuit board
to which all the other components connect. It has sockets, slots, ports,
connectors, chips and wires to ensure the communication between all the components.
[search for motherboard datasheet, you'll find nice images]
- The CPU or Central Processing Unit is the brain of the computer, the part
responsible for executing program instructions.
- The RAM or Random Access Memory, is the main memory that is used by the CPU to
  temporarily store and access data! But it is volatile memory, meaning that
  all the data stored is lost when the computer is turned off.
- But this isn't the case for the Drive, the secondary memory, which is used to
  stored any data persistently.
  - We usually use a "Hard Disk Drive" (HDD), or a Solid-State Drive (SDD), or
    both!
- Computers often comes with a dedicated Graphics card, also known as a GPU,
  Graphics Processing Unit. It's responsible for rendering images, videos,
  animations, 3D rendering, or really just any graphical application!
  - Some CPUs have an integrated GPU, but its performance is limited!
- All of these components need electricity to work, and it's the role of the
  Power supply, to provide the required voltages and currents to the whole system.
- All that generates at ton of heat, that needs to be cooled using fans or
  liquid cooling to maintain an optimal work environment and avoid damages.
- Anything else are peripherals. Monitor, mouse, keyboard, printer, microphone,
  webcam, gaming controller are peripherals, also known as Input and Output
  devices...

## mental model

Knowing all the different components in details isn't that useful for programmers.
Instead it's usually preferable to keep a simpler mental model of what a computer
is. For now, it's going to be very simple, and composed of only 4 parts:
- the **CPU**, responsible for executing programs,
- the **RAM**, or main memory responsible for storing the data used by the CPU
- the **I/O devices**, anything that we'll want to interact with including the
  disk, keyboard, monitor, network...
- and the **bus**, the name given to the wires that connects the different components

but it will evolve with time as we learn more about computers.
A more accurate model would look like this, showing CPU cores, caches, the memory
controller, the Platform Controller Hub (PCH)... and we will eventually talk
about all of this! But the simpler model will be sufficient for now!

But before using this model, we need to learn about electricity and how computers
represents and store information:

## 3-electricity, binary data representation, instructions

So, you all know that computers are powered by electricity ; well actually not
all computers are ... shut up.

Electricity is a physical phenomenon that humans have learned to produce and
manipulate. We distinguish two main types of electric current:

- alternating current (AC)
- direct current (DC)

Both are useful, and the power supply converts the alternating current coming
from the power outlet into direct current that the computer uses.
I am talking about current, but we usually talk about voltage rather than current.
The branch 

The electric signal can be either High, or Low.
The high value can be 12V, 5V, 3V or 1.2V. And the low value is usually 0V.
But instead of talking about high or low values, we assign the high voltage to
the number 1, and the low to 0. So if we look at the signal on a wire, we can
see 0, or 1. And so it gives us the ability to count up to 1. But being able to
to count up to 1, isn't really that interesting. But if we have 2 wires instead,
we can have the following signals:
- both at 0
- the first one at 0, and second at 1
- the first one at 1, and second at 0
- and both at 1.
Now we have 4 values, which means we can count from 0 to 3!
If we add a third wire, we end up with 8 possible values.
Here we see that we can represent numbers using only 0s and 1s. These are called
binary numbers.

And the way they work isn't that different from how regular numbers work!
The numbers we are used to use are in "Base 10", because we have 10 symbols,
from 0 to 9. And we are all used to these numbers, and feel natural to us.
But we can make some useful observations, take the number 1689*, we can associate
for each column a power of ten. 10^0 for 9, 10^1 for 8, 10^2 to 6 and 10^3, to
1, such that if we multiply each digit with it's associated power of ten and take
the sum, we get 1689.
(1689: modern binary number system, year of invention by Leibniz)

But with binary digits, we only have two symbols, 0 and 1. So we can use base 2
to count. Instead of using powers of 10, we use powers of 2. Each power of 2,
is multiplied by either 0 or 1.
For example, the binary number 1101, is equal to 1*2^3 + 1*2^2 + 0*2^1 + 1*2^0,
which is equal to 13.
The 0s and 1s in a binary number are called "bits", which comes from
the contraction of "binary digit". A bit is the smallest and most fundamental
unit of information in computing, the smallest, just a lil bit of information.
(get it?)
The more bits you add to a number, the bigger it can get. If you have "n" bits,
you can encode 2^n values.

Computers don't handle bits individually, but handle "bytes". A byte is 8 bits,
but historically, the size of a byte was hardware-dependent. But now, whenever
people talk about bytes, it's safe to assume they are talking about 8 bits.

TODO: ... 'explain a bit more, show an example'

I think that's enough, if you want to know more, there are tons of videos, books
or articles you can consume. But it's pretty simple, the math is the same, and
if you need to convert some numbers, you can use a calculator app.
Maybe I'll make a full video about it, for the sake of completeness...

BASE 16: hexadecimal

binary game: <https://learningcontent.cisco.com/games/binary/index.html>


The reason why I am talking about this, is because I want to show you how programs
are executed by computers!



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

## 5-software layer, operating system

(chatgpt below)
Modern CPU architectures and operating systems have co-evolved: hardware provides mechanisms for protection, memory management, interrupts, and synchronization, while operating systems build abstractions on top of those mechanisms. The requirements of increasingly sophisticated operating systems, in turn, have influenced CPU architecture.

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

[x] watch <https://www.youtube.com/watch?v=geBcfKn3B1g> (49min en FR) ----------

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


-----------------------
Personal Computer Architecture <https://www.youtube.com/watch?v=_I8CLQazom0>> (18 min)

- CPU: ALU, Control Unit (transform machine-code into microcode), registers
- old architecture:
    - CPU <- front side bus -> Northbridge (memory controller)
    - Northbridge <-- memory bus --> DRAM
    - Northbridge <-- PCI Express --> Graphics Adapter
    - Northbridge <-- DMI --> Southbridge
    - SouthBridge (IO controller) ---> different IO devices
- modern archi:
    - CPU, made of:
        - multiple cores (1 core = ALU, CU, Reg)
        - cache (L1, L2, L3)
        - Graphics Controller <-- PCIe --> Graphics adapter
        - Memory Controller <-- Memory Bus --> DRAM
    - CPU <-- DMI --> Chipset (PCH)

    - CPU, RAM and chipset must be compatible

- DMI (Direct Media Interface)
- PCI (Peripheral component interconnect)
- AGP (Accelerated Graphics Port)

- The motherboard has a crystal oscillator, base clock
- CPU has special circuits called freq dividers and freq multipliers takes this
  base clock and "divided/multiply it" to a much higher freq.

-------------------------------------------------------------------------------

[] (57 min) digital electronics - the first video you should watch <https://www.youtube.com/watch?v=pDELW2pIvWw>

- bit (a little bit), but originally comes from the contraction of "binary digit"



[x] PC architecture <https://youtu.be/_I8CLQazom0?si=IL8OkccuWxD3bu9V&t=316> (18 min)
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
- https://www.contec.com/support/basic-knowledge/edge-computing/cpu/
