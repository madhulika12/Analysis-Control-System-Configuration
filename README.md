Analysis
========

Serial Port

NEW MODIFICATIONS - 27:

I edited the testbedinit.sh file to include downloading the python_simplejson. Might as well get everything we need.
-I edited the two run scripts to have a "master" and "slave" specific script

-I edited the mkconfig so that the logic emulated the control_microsystems_old, added the "_old". Looking at his holding registers, they all look like how he has the old system defined. That cleared up one error on the slave system.

-I had to add "sudo" before each of the terminal commands that start the python scripts in the run.sh file. Apparently, the "sudo true" at the beginning isn't enough. I never could open port 502(the ModbusTCP port) because of this. SOLVED.
-In order to run master and slave on different VMs, I had to add exceptions for the particular ports(TCP:502, UDP:9912, UDP:9913)

-In order to run master and slave on different VMs, I had to modify the config file. The master "simiface" receipient IP address needs to be the slave, and the slave's receipient IP address needs to be the master. Likewise, both the master "clientiface" and slave "icsiface" IP address needs to be the slave.

-looks like my USB3.0 port isn't compatible with my VMWare Workstation 10 running Windows XP with a virtual USB3.0 controller. It does work when I put it on a USB2.0 hub and chagned the virtual USB controller to 2.0. This is needed to use the USB hardware key.

-The virtual slave PLC is defined as device 4 in the Modbus protocol. In order to get the ModbusTCP driver working on the XP machine(iFix), I had to get the right IP address for the slave PLC, the right device, and the right register set. The register set is 6 digit, and the first digit is 4(which translates into Modbus blocktype 3. Weird, I know), then the 5 digit address. The configuration is on the XP computer. The register set should be in the config file, and in the excel spreadsheet for the tcppipe simulation.
