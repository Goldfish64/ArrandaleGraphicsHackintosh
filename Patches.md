# Patches
* [Stride patch](#Stride-patch)
* [Single link patch 1](#Single-link-patch-1)
* [Single link patch 2](#Single-link-patch-2)
* [Single link patch 3](#Single-link-patch-3)
* [Link width patch](#Link-width-patch)
* [FBCControl patch](#FBCControl-patch)
* [FeatureControl patch](#FeatureControl-patch)


# Stride patch
Use 0x2000 for stride (fixes artifacts on resolutions > 1024x768). Located in `AppleIntelHDGraphicsFB::hwSetCRTC`.

## Stride patch for 10.6 x86
Original: `0F8547FEFFFF66B80020`
```asm
jne ...
mov ax, 0x2000
```

Replacement: `90909090909066B80020`
```asm
nop
nop
nop
nop
nop
nop
mov ax, 0x2000
```

## Stride patch for 10.6 x64
Original: `0F8575FEFFFFE96BFEFFFF`
```asm
jne ...
Jmp ...
```

Replacement: `909090909090E96BFEFFFF`
```asm
nop
nop
nop
nop
nop
nop
jmp ...
```

## Stride patch for 10.7 x86
Original: `0F45C8898C3E`
```asm
cmovne ecx, eax
...
```

Replacement: `909090898C3E`
```asm
nop
nop
nop
...
```

## Stride patch for 10.7 x64, 10.8, 10.9, 10.10, 10.11, 10.12, and 10.13
Original: `0F45C842898C`
```asm
cmovne ecx, eax
...
```

Replacement: `90909042898C`
```asm
nop
nop
nop
...
```


# Single link patch 1
Enables single link mode. Located in `AppleIntelHDGraphicsFB::hwGetPanelProperties`.

## Single link patch 1 for 10.6 x86
Original: `C70301000000C7432000000000`
```asm
mov dword [ebx], 0x1
mov dword [ebx+0x20], 0x0
```

Replacement: `C70300000000C7432000000000`
```asm
mov dword [ebx], 0x0
mov dword [ebx+0x20], 0x0
```

## Single link patch 1 for 10.6 x64
Original: `C70201000000C7422000000000`
```asm
mov dword [rdx], 0x1
mov dword [rdx+0x20], 0x0
```

Replacement: `C70200000000C7422000000000`
```asm
mov dword [rdx], 0x0
mov dword [rdx+0x20], 0x0
```

## Single link patch 1 for 10.7 x86
Original: `C70601000000C7462000000000`
```asm
mov dword [esi], 0x1
mov dword [esi+0x20], 0x0
```

Replacement: `C70600000000C7462000000000`
```asm
mov dword [esi], 0x0
mov dword [esi+0x20], 0x0
```

## Single link patch 1 for 10.7 x64, 10.8, and 10.9
Original: `C70301000000C7432000000000`
```asm
mov dword [rbx], 0x1
mov dword [rbx+0x20], 0x0
```

Replacement: `C70300000000C7432000000000`
```asm
mov dword [rbx], 0x0
mov dword [rbx+0x20], 0x0
```

## Single link patch 1 for 10.10
Original: `49C7070100000041C7472000000000`
```asm
mov qword [r15], 0x1
mov dword [r15+0x20], 0x0
```

Replacement: `49C7070000000041C7472000000000`
```asm
mov qword [r15], 0x0
mov dword [r15+0x20], 0x0
```

## Single link patch 1 for 10.11, 10.12, and 10.13
Original: `48C7030100000048B80A000000D0070000`
```asm
mov qword [rbx], 0x1
movabs rax, 0x000007D00000000A
```

Replacement: `48C7030000000048B80A000000D0070000`
```asm
mov qword [rbx], 0x0
movabs rax, 0x000007D00000000A
```


# Single link patch 2
Changes to divisor 14. Located in `AppleIntelHDGraphicsFB::hwRegsNeedUpdate`.

## Single link patch 2 for 10.6 x86
Original: `BB00000009`
```asm
mov ebx, 0x09000000
```

Replacement: `BB00000008`
```asm
mov ebx, 0x08000000
```

## Single link patch 2 for 10.6 x64
Original: `BE00000009`
```asm
mov esi, 0x09000000
```

Replacement: `BE00000008`
```asm
mov esi, 0x08000000
```

## Single link patch 2 for 10.7 x64
Original: `B800000009`
```asm
mov eax, 0x09000000
```

Replacement: `B800000008`
```asm
mov eax, 0x0800000
```

## Single link patch 2 for 10.7 x86 and 10.8
Original: `B900000009`
```asm
mov ecx, 0x09000000
```

Replacement: `B900000008`
```asm
mov ecx, 0x08000000
```

## Single link patch 2 for 10.9
Original: `41B900600009`
```asm
mov r9d, 0x09006000
```

Replacement: `41B900600008`
```asm
mov r9d, 0x08006000
```

## Single link patch 2 for 10.10, 10.11, and 10.12
Original: `B800600009`
```asm
mov eax, 0x09006000
```

Replacement: `B800600008`
```asm
mov eax, 0x08006000
```

## Single link patch 2 for 10.13
Original: `BA00600009`
```asm
mov edx, 0x09006000
```

Replacement: `BA00600008`
```asm
mov edx, 0x08006000
```


# Single link patch 3
Powers down CLKB (fixes pixelated image). Located in `AppleIntelHDGraphicsFB::hwRegsNeedUpdate`.

## Single link patch 3 for all versions
Original: `3C033080`  
Replacement: `00033080`


# Link width patch
Sets the link width. Located in `AppleIntelHDGraphicsFB::TrainFDI`.

## Link width patch for 10.6 x86
Original: `8B87380500000FB64018C1E0130B466C89466C8B575889820C000F008B87380500000FB64018C1E0130B4668`
```asm
mov eax, dword [edi+0x538]
movzx eax, byte [eax+0x18]
shl eax, 0x13
or  eax, dword [esi+0x6C]
mov dword [esi+0x6C], eax
mov edx, dword [edi+0x58]
mov dword [edx+0xF000C], eax
mov eax, dword [edi+0x538]
movzx eax, byte [eax+0x18]
shl eax, 0x13
or  eax, dword [esi+0x68]
```

LW1: `8B466C25FFFFC7FF0D0000000090909089466C8B575889820C000F008B466825FFFFC7FF0D00000000909090`  
LW2: `8B466C25FFFFC7FF0D0000080090909089466C8B575889820C000F008B466825FFFFC7FF0D00000800909090`  
LW3: `8B466C25FFFFC7FF0D0000100090909089466C8B575889820C000F008B466825FFFFC7FF0D00001000909090`  
LW4: `8B466C25FFFFC7FF0D0000180090909089466C8B575889820C000F008B466825FFFFC7FF0D00001800909090`
```asm
mov eax, dword [esi+0x6C]  ; Get FDI_RXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
mov dword [esi+0x6C], eax  ; Set FDI_RXA_CTL register.
mov edx, dword [edi+0x58]
mov dword [edx+0xF000C], eax
mov eax, dword [esi+0x68]  ; Get FDI_TXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
```


## Link width patch for 10.6 x64
Original: `498B85980600000FB64018C1E013410B44246C418944246C498B959800000089820C000F00498B85980600000FB64018C1E013410B442468`
```asm
mov rax, qword [r13+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
or  eax, dword [r12+0x6C]
mov dword [r12+0x6C], eax
mov rdx, qword [r13+0x98]
mov dword [rdx+0xF000C], eax
mov rax, qword [r13+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
or  eax, dword [r12+0x68]
```

LW1: `418B44246C25FFFFC7FF0D00000000909090909090909090498B959800000089820C000F00418B44246825FFFFC7FF0D0000000090909090`  
LW2: `418B44246C25FFFFC7FF0D00000800909090909090909090498B959800000089820C000F00418B44246825FFFFC7FF0D0000080090909090`  
LW3: `418B44246C25FFFFC7FF0D00001000909090909090909090498B959800000089820C000F00418B44246825FFFFC7FF0D0000100090909090`  
LW4: `418B44246C25FFFFC7FF0D00001800909090909090909090498B959800000089820C000F00418B44246825FFFFC7FF0D0000180090909090`  
```asm
mov eax, dword [r12+0x6C]  ; Get FDI_RXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
nop
nop
nop
nop
nop
mov dword [r12+0x6C], eax  ; Set FDI_RXA_CTL register.
mov rdx, qword [r13+0x98]
mov dword [rdx+0xF000C], eax
mov eax, dword [r12+0x68]  ; Get FDI_TXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
```

## Link width patch for 10.7 x86
Original: `8B86380500000FB64018C1E0130B476C89476C8B4E5889810C000F008B86380500000FB64018C1E0130B4768`
```asm
mov eax, dword [esi+0x538]
movzx eax, byte [eax+0x18]
shl eax, 0x13
or  eax, dword [edi+0x6C]
mov dword [edi+0x6C], eax
mov ecx, dword [esi+0x58]
mov dword [ecx+0xF000C], eax
mov eax, dword [esi+0x538]
movzx eax, byte [eax+0x18]
shl eax, 0x13
or  eax, dword [edi+0x68]
```

LW1: `8B476C25FFFFC7FF0D0000000090909089476C8B4E5889810C000F008B476825FFFFC7FF0D00000000909090`  
LW2: `8B476C25FFFFC7FF0D0000080090909089476C8B4E5889810C000F008B476825FFFFC7FF0D00000800909090`  
LW3: `8B476C25FFFFC7FF0D0000100090909089476C8B4E5889810C000F008B476825FFFFC7FF0D00001000909090`  
LW4: `8B476C25FFFFC7FF0D0000180090909089476C8B4E5889810C000F008B476825FFFFC7FF0D00001800909090`
```asm
mov eax, dword [edi+0x6C]  ; Get FDI_RXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
mov dword [edi+0x6C], eax  ; Set FDI_RXA_CTL register.
mov ecx, dword [esi+0x58]
mov dword [ecx+0xF000C], eax
mov eax, dword [edi+0x68]  ; Get FDI_TXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
```

## Link width patch for 10.7 x64
Original: `498B86980600000FB64018C1E0130B436C89436C498B8E9800000089810C000F00498B86980600000FB64018C1E0130B4368`
```asm
mov rax, qword [r14+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
or  eax, dword [rbx+0x6C]
mov dword [rbx+0x6c], eax
mov rcx, qword [r14+0x98]
mov dword [rcx+0xF000C], eax
mov rax, qword [r14+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
or  eax, dword [rbx+0x68]
```

LW1: `8B436C25FFFFC7FF0D000000009090909089436C498B8E9800000089810C000F008B436825FFFFC7FF0D0000000090909090`  
LW2: `8B436C25FFFFC7FF0D000008009090909089436C498B8E9800000089810C000F008B436825FFFFC7FF0D0000080090909090`  
LW3: `8B436C25FFFFC7FF0D000010009090909089436C498B8E9800000089810C000F008B436825FFFFC7FF0D0000100090909090`  
LW4: `8B436C25FFFFC7FF0D000018009090909089436C498B8E9800000089810C000F008B436825FFFFC7FF0D0000180090909090`
```asm
mov eax, dword [rbx+0x6C]  ; Get FDI_RXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
mov dword [rbx+0x6C], eax  ; Set FDI_RXA_CTL register.
mov rcx, qword [r14+0x98]
mov dword [rcx+0xF000C], eax
mov eax, dword [rbx+0x68]  ; Get FDI_TXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
```

## Link width patch for 10.8, 10.9, 10.10, and 10.11
Original: `498B8424980600000FB64018C1E013410B466C4189466C498B8C249800000089810C000F00498B8424980600000FB64018C1E013410B4668`
```asm
mov rax, qword [r12+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
or  eax, dword [r14+0x6C]
mov dword [r14+0x6C], eax
mov rcx, qword [r12+0x98]
mov dword [rcx+0xF000C], eax
mov rax, qword [r12+0x698]
movzx eax, byte [rax+0x18]
shl eax, 0x13
```

LW1: `418B466C25FFFFC7FF0D0000000090909090904189466C498B8C249800000089810C000F00418B466825FFFFC7FF0D000000009090909090`  
LW2: `418B466C25FFFFC7FF0D0000080090909090904189466C498B8C249800000089810C000F00418B466825FFFFC7FF0D000008009090909090`  
LW3: `418B466C25FFFFC7FF0D0000100090909090904189466C498B8C249800000089810C000F00418B466825FFFFC7FF0D000010009090909090`  
LW4: `418B466C25FFFFC7FF0D0000180090909090904189466C498B8C249800000089810C000F00418B466825FFFFC7FF0D000018009090909090`
```asm
mov eax, dword [r14+0x6C]  ; Get FDI_RXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
nop
mov dword [r14+0x6C], eax  ; Set FDI_RXA_CTL register.
mov rcx, qword [r12+0x98]
mov dword [rcx+0xF000C], eax
mov eax, dword [r14+0x68]  ; Get FDI_TXA_CTL register.
and eax, 0xFFC7FFFF        ; Clear link width.
or  eax, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
nop
```

## Link width patch for 10.12 and 10.13
Original: `41894E6C498B84249800000089880C000F00498B8C24980600000FB65118C1E213418B766C09D64189766C89B00C000F00410B5668`
```asm
mov ecx, dword [r14+0x6C]
or  ecx, 0x10
mov dword [r14+0x6C], ecx
mov rax, qword [r12+0x98]
mov dword [rax+0xF000C], ecx
mov rcx, qword [r12+0x698]
movzx edx, byte [rcx+0x18]
shl edx, 0x13
mov esi, dword [r14+0x6C]
or  esi, edx
mov dword [r14+0x6C], esi
mov dword [rax+0xF000C], esi
or  edx, dword [r14+0x68]
```

LW1: `81E1FFFFC7FF81C900000000909090909041894E6C89880C000F00418B566881E2FFFFC7FF81CA0000000090909090909090909090`  
LW2: `81E1FFFFC7FF81C900000800909090909041894E6C89880C000F00418B566881E2FFFFC7FF81CA0000080090909090909090909090`  
LW3: `81E1FFFFC7FF81C900001000909090909041894E6C89880C000F00418B566881E2FFFFC7FF81CA0000100090909090909090909090`  
LW4: `81E1FFFFC7FF81C900001800909090909041894E6C89880C000F00418B566881E2FFFFC7FF81CA0000180090909090909090909090`
```asm
and ecx, 0xFFC7FFFF        ; Clear link width.
or  ecx, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop 
nop
nop
nop
nop
mov dword [r14+0x6c], ecx  ; Set FDI_RXA_CTL register.
mov dword [rax+0xf000c], ecx
mov edx, dword [r14+0x68]  ; Get FDI_TXA_CTL register.
and edx, 0xFFC7FFFF        ; Clear link width.
or  edx, X                 ; Set link width ((link_width - 1) & 7) << 19.
nop
nop
nop
nop
nop
nop
nop
nop
nop
nop
```


# FBCControl patch
Prevents the FBCControl settings in the Info.plist from being read. This has the same effect as setting all the values in the FBCControl section to zero. This is done by replacing string `FBCControl` with `XXXControl`.

## FBCControl patch for all versions
Original: `464243436F6E74726F6C00`  
Replacement: `585858436F6E74726F6C00`


# FeatureControl patch
Prevents the FeatureControl settings in the Info.plist from being read. This has the same effect as setting all the values in the FeatureControl section to zero. This is done by replacing string `FeatureControl` with `XXXtureControl`.

## FeatureControl patch for all versions
Original: `46656174757265436F6E74726F6C00`  
Replacement: `58585874757265436F6E74726F6C00`
