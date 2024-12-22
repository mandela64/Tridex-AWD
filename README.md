# Tridex-AWD (Work in progress)

Goal is to add AWD to the Voron Tridex.

Purchased parts:
- Common Anomaly X Beam
- Ldo Nema 14 2A S35 (X-Axis)
- Vitalii3D Metal Voron Tap (2)

Printed parts:
- X axis is based on aTinyShellScript AWD mod. 
- Y axis motor mount and X-Beam gantry bracket is my design with a front tensioner inspired by clee BZI tensioner.
- MetalTap adapters allow 6mm belts to pass behind toolheads.

Warning: 
- Klipper Pull Request to allow Multiple steppers per axis on Hybrid CoreXY #6754
- Y-Axis front tensioners require additional z-height clearance. I am using the Mandala Rose Work matched height kinematic kit.

![TridexAWD](https://github.com/user-attachments/assets/9bf6e760-6f2b-454d-bc02-ef340b466081)

Based on:
- eddietheengineers Tridex printer <https://github.com/FrankenVoron/Tridex/tree/main>
- aTinyShellScript AWD <https://docs.atinyshellscript.com/v2.4/awd/)>
- clee BZI <https://github.com/clee/VoronBFI>
