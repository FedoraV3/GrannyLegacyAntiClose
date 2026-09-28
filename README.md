# Installing the mod
Head to your Granny Legacy installation folder and drag the dll in this repository to /path/to/grannylegacy/Granny Legacy_Data/Plugins/x86_64 folder. After that you can close steam or if you don't have granny installed or bought, you can just open the game and it will work

# If you are paranoid
You can get the dll from this repo and compare it to the original dll. You will see that there is only a 7 byte difference, which makes it impossible for me to add any stuff.

# If you are still paranoid but want the crack by doing what i did for you already
You can patch these specific array of bytes: `33 C9 E9 99 F2 FF FF`

Replace it with `90 90 EB 0C 90 90 90`

In assembly the original code is before replacing it:
```asm
xor ecx, ecx ; parameter one to a jmp to sub_13B405C90 idk what calling convention is this
jmp sub_13B405C90 ; jmp here
```
Now the code after it is replaced:
```asm
nop
nop ; so that it lines up with the last bytes of xor ecx,ecx
jmp short SteamAPI_InitAnonymousUser() ; this is basically what it does
```
That is basically what it does. it makes SteamAPI_Init() jump to SteamAPI_InitAnonymousUser() so that SteamAPI_Init() does not error due to the game not being owned


# Thoughts
I am pretty surprised. this is oddly simple mechanisms so it makes sure people own the game by using an error steamapi_init() returns
