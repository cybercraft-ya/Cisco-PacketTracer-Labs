Password Break and Recovery

Follow these command step by step:
1)Restart Router
2)Press Ctrl + Break or ctrl + c
3)Rommon 1> confreg 0x2142
4)Rommon 2> reset and press enter
5)Show running-config
6)Copy startup-config running-config
7)No enable secret (to remove previous password) config-register 0x2102