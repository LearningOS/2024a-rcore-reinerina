**功能总结**  

本次实验实现了查询当前正在执行的任务的信息的功能，能够查询的信息包括任务控制块相关信息（任务状态）、任务使用的系统调用及  
调用次数、系统调用时刻距离任务第一次被调度时刻的时长（单位ms）。执行成功时返回 0，执行错误返回 -1 （只有执行成功的情况）。  

**简答作业**  
1. 
   ch2b_bad_address.rs 错误：PageFault in application, bad addr = 0x0, bad   instruction = 0x804003a4, kernel killed it.  
   表示程序访问了错误的地址  
   ch2b_bad_instructions.rs 错误：IllegalInstruction in application, kernel killed it.  
   表示程序使用了非法的指令  
   ch2b_bad_register.rs 错误：IllegalInstruction in application, kernel killed it.  
   表示程序使用的非法的指令  
   RustSBI版本：RustSBI-QEMU Version 0.2.0-alpha.3  
2. 
   1. a0表示程序内核栈的栈指针，场景：处理Trap和程序上下文之间的切换  
   2. sstatus是S模式下的状态寄存器，意义是返回用户态时特权级设置正确  
      spec用于保存特权级从用户态切换至内核态时的程序计数器，意义是返回用户态时程序能从正确的位置开始执行  
      sscratch同于保存用户栈的栈指针，意义是返回用户态时恢复正确的栈指针  
   3. x2：需要根据sp找到各个寄存器位置，无需保存  
      x4：在程序运行时期不会变化  
   4. sscratch为用户栈的栈指针，sp为内核栈的栈指针  
   5. sret，因为sstatus的SPP位被设为0  
   6. sp为用户栈的栈指针，sscratch为内核栈的栈指针  
   7. call trap_handler  

**荣誉准则**

1. 在完成本次实验的过程（含此前学习的过程）中，我曾分别与 以下各位 就（与本次实验相关的）以下方面做过交流，还在代码中对应的位置以注释形式记录了具体的交流对象及内容：
```
无
```
2. 此外，我也参考了 以下资料 ，还在代码中对应的位置以注释形式记录了具体的参考来源及内容：
```
1. [rCore-Camp-Guide-2024A](https://learningos.github.io/rCore-Camp-Guide-2024A/)   
2. [rCore-Tutorial-Book-v3](https://rcore-os.github.io/rCore-Tutorial-Book-v3/)  
```
3. 我独立完成了本次实验除以上方面之外的所有工作，包括代码与文档。 我清楚地知道，从以上方面获得的信息在一定程度上降低了实验难度，可能会影响起评分。
4. 我从未使用过他人的代码，不管是原封不动地复制，还是经过了某些等价转换。 我未曾也不会向他人（含此后各届同学）复制或公开我的实验代码，我有义务妥善保管好它们。 我提交至本实验的评测系统的代码，均无意于破坏或妨碍任何计算机系统的正常运转。 我清楚地知道，以上情况均为本课程纪律所禁止，若违反，对应的实验成绩将按“-100”分计。

by reinerina  