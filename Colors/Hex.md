    DEC   HEX  DEC  HEX   ...  ...  DEC HEX
      0   0     16  10              240 F0 
      1   1     17  11              241 F1
      2   2     18  12              242 F2
      3   3     19  13              243 F3
      4   4     20  14              244 F4
      5   5     21  15              245 F5
      6   6     22  16              246 F6
      7   7     23  17              247 F7
      8   8     24  18              248 F8
      9   9     25  19              249 F9
      10  A     26  1A              250 FA
      11  B     27  1B              251 FB
      12  C     28  1C              252 FC
      13  D     29  1D              253 FD
      14  E     30  1E              254 FE
      15  F     31  1F              255 FF

### Convert Hex to Decimal
d<sub>n-1</sub> ... d<sub>2</sub> d<sub>1</sub> d<sub>0</sub>

decimal = d<sub>n-1</sub>×16<sup>n-1</sup> + ... + d<sub>2</sub>×16<sup>2</sup> + d<sub>1</sub>×16<sup>1</sup> + d<sub>0</sub>×16<sup>0</sup>

E7A9 = 14x16<sup>3</sup> + 7x16<sup>2</sup> + 10x16<sup>1</sup> + 9x16<sup>0</sup>
= 57344 + 1792 + 160 + 9 = 59305

0.8 = 0x16<sup>0</sup> + 8x16<sup>-1</sup> = 0 + 0.5 = 0.5

### Convert Decimal to Hex
```md
7562 = 1D8A
7562 % 16 = 10            = A | 0
7562 / 16 = 472 % 16      = 8 | 1
472 / 16  = 29 % 16  = 13 = D | 2
29 / 16   = 1 % 16        = 1 | 3
```