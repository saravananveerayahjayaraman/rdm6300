# RDM6300
RDM6300 For Raspberry pi in Python

It was challenging to use a the RDM6300 module but it was a plain HEX to integer conversion.

RDM6300 generates 12 Hexed byte with header, checksum and end bit.

Serial Parameters 9600,8,N,1

Module Look
===========
<p>
+-------------------------------+
|RDM6300          P1  O O O O O |
|                               |
|                               |
|                               |
| O O  P2             P3  O O O |
+-------------------------------+ 
</p>
P1 : +5v, Gnd, NC, Rx, Tx
P2 : Ant1, Ant2
P3 : Gnd, +5v, Led


Data stream
===========
+----+------------+--------+----+
| 02 | 0123456789 | chksum | 03 |    
+----+------------+--------+----+
02 - Header
X - 10 ASCII characters
chksum (01) xor (23) xor (45) xor (67) xor (89)
03 - stop bit


RFID Card typical look
======================
+------------------------------------+
|                                    |
|                                    |
|                                    |
|                                    |
|                                    |
|            0015410698  235,09738   |
+------------------------------------+

When RDM6300 reads for the above test card, it produces 
  02 | 4D00EB260A | 8A | 03
  
  ASCII   4    D    0    0    E    B    2    6    0    A
  HEX     0x34 0x44 0x30 0x30 0x45 0x42 0x32 0x36 0x30 0x41
  CHKSUM (00) XOR (EB) XOR (26) XOR (0A) = 8A
  
  Card No Format 1
  ----------------
  HEX     -    -    0    0    E    B    2    6    0    A
  DEC     0    0    1    5    4    1    0    6    9    8
  
  Card No Format 2
  ----------------
  HEX     ( 0    0    E    B ) (  2    6    0    A )
  DEC     (235)                (09738)        
