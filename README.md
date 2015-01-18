AVRのプログラムを書くやつ(仮)
=============================

AVRのプログラムを書くためのツールです。

プログラムをAVRに書き込むには、
[AVRを読み書きするやつ](https://github.com/mikecat/avr_io)などが利用できます。

### 参考資料
* [Atmel AVR 8-bit and 32-bit Microcontrollers](http://www.atmel.com/products/microcontrollers/avr/?tab=documents)  
  このページの"AVR Instruction Set"にAVRの命令(ニモニックと機械語)が載っています。

### 擬似命令
* ```!ORG address```  
  プログラムの出力位置をaddressに設定する。戻ることはできない。
* ```!CONST name value```  
  nameを値valueの定数として定義する。nameはラベルと同様に扱われる。
* ```!WORD value```  
  1ワードのデータを直接指定して配置する。

### 命令に関するメモ

* 基本的に第一オペランドを第二オペランドを用いて処理し、第一オペランドに結果を格納する。  
  例：```SUB r1, r2``` → ```r1 -= r2```
* X,Y,Zレジスタを使う命令は、このプログラムではX,Y,Zを命令にくっつけて書く。  
  例：```ST Y+, r1``` → ```STY+ r1```

x86命令     |似たAVR命令
------------|-----------
add r8,r8   |add
add r16,imm8|(adiw)
adc r8,r8   |adc
sub r8,r8   |sub
sub r8,imm8 |subi
sbb r8,r8   |sbc
sbb r8,imm8 |sbci
sub r16,imm8|(sbiw)
and r8,r8   |and
and r8,imm8 |andi
or r8,r8    |or
or r8,imm8  |ori
xor r8,r8   |eor
not r8      |com
neg r8      |neg
inc r8      |inc
dec r8      |dec
mul r8      |(mul)
imul r8     |(muls)
jmp rel16   |rjmp
jmp r16     |(ijmp)
call rel16  |rcall
call r16    |(icall)
ret         |ret
cmp r8,r8   |cp
cmp r8,imm8 |cpi
je/jz       |breq
jne/jnz     |brne
jb/jnae/jc  |brcs/brlo
jae/jnb/jnc |brcc/brsh
js          |brmi
jns         |brpl
jge/jnl     |brge
jl/jnge     |brlt
jo          |brvs
jno         |brvc
mov r8,r8   |mov
mov r16,r16 |(movw)
mov r8,imm8 |ldi
mov r8,m8   |lds/ld/ldd
mov m8,r8   |sts/st/std
push r8     |push
pop r8      |pop
xchg m8,r8  |(xch)
shl r8,1    |lsl
shr r8,1    |lsr
rcl r8,1    |rol
rcr r8,1    |ror
sar r8,1    |asr
stc         |sec
clc         |clc
nop         |nop
