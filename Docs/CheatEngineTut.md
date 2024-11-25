find health 100 - 90 - 80 etc (address 0161C7A0)
copy address -> new scan -> hex 0161C7A0 
Hope its green (static) -> copy address -> "Tutorial-x86_64.exe"+325AD0 
add address manually -> "Tutorial-x86_64.exe"+325AD0 -> even if pointer resets example reboot game (new health int) we still go to the health variable

code injection (step 7)
find out what writes to address or read to nope stuff
Show dissassambler (can put breakpoints) , mov [rax] edx (rax is location of where it is stored)
sub dword ptr [rsi+000007E0],01 -> substracts
ctrl+a (tools) -> open auto assemble window
template code injection
copy code instead of sub add 2:
add dword ptr [rsi+000007E0],02
Now when we click hit me we go up be 1

Multilevel pointers
we got to trace backwards till we get a static base adress (we go from right to left, back tracing)
 -> = points to
08F2D918 = value = 2527
Find offset 4 (find out what accesses adres) -> rsi+18 so offset4 = 0x18
So first address: 08F2D918 -18 = 8F2 D900
hex search for 8F2D900 -> gives base ptr 015BB620 which is also address of next point
015BB620 -> find out what accesses this adres we dont see a number in the mov rsi, [rsi] so the offset is 0
so address stays the same
Hex search for 015BB620  = base ptr and end address
continue the riddle untill you find the static base address from which you can start.

08F2D918 = value = 2527
(base ptr)015BB620 -> (address)8F2 D900 + (offset4)0x18 = (address)08F2D918

base ptr(01639048) -> 015BB620 + (0)offset3 = 015BB620

base ptr(01658520) -> 1639030 + offset2(0x18) = 01639048

static base("Tutorial-x86_64.exe"+325B00) -> 1658510 + offset1(0x10) = 01658520

add address manually -> "Tutorial-x86_64.exe"+325B00 -> add 4 offsets: 0x10, 0x18, 0, 0x18

freeze change pointer next ez TUT kek Awesum

Template
address = value = ?
base ptr -> address + offset4 = address

base ptr -> address + offset3 = address

base ptr -> address + offset2 = address

static base -> address + offset1 = address


