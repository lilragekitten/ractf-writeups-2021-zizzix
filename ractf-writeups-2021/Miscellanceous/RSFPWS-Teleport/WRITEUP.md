# RSFPWS - Teleport
## TEAM: Kittens
### SOLVER: Zizzix
-----------------------------------------------------------

1) Download the client and unzip it in a location.  
I used the windows one as I was going to use cheatengine.

2) Run the game and login to the IP and Port. (username doesnt matter)

3) Load up cheatengine and attach to the RARPG.exe process

4) I wanted to find a way to clip inside the box. So I went up and stood next to the box and did a scan:  
    a) Scan type: Unknown initial value
    b) Value type: float

5) Then I went to the middle of the room away from all boxes and scanned again for changed values.  

6) I found a value that cycled between 0(when not touching a wall, and 0.3000000119(when touching a wall of one of the boxes))

7) I right clicked on it and went to "Find out what accesses this address" and attached the debugger

8) When touching a wall I found these opcode being accessed:
```
7FFB336453C4 - 44 0F29 A8 78FFFFFF  - movaps [rax-00000088],xmm13
7FFB336459E6 - 45 0F28 6B 80  - movaps xmm13,[r11-80]
```

9) I opened the first one in the Assembler and looked for a jmp of some sort, and found the below:
```
UnityPlayer.dll+132554C - 0F85 51FFFFFF - jne UnityPlayer.dll+13254A3
```

10) Changed that to je and was able to clip through the wall:
```
UnityPlayer.dll+132554C - 0F84 51FFFFFF - je UnityPlayer.dll+13254A3
```

Flag: ractf{T3l3port1ng_iS_fuN!}