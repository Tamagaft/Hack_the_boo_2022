202210262142
Status:: #ctf
Tags: [[hack_the_boo]], [[reversing]]

# hack_the_boo_ghost_wrangler
Platform: *hackthebox*
event: *hack the boo*
type: *reversing*
task: *Who you gonna call?*
flag: **HTB{h4unt3d_by_th3_gh0st5_0f_ctf5_p45t!}**

# steps
Extract text using `strings` linux command:
```bash
strings ghost                                                                                            
/lib64/ld-linux-x86-64.so.2
printf
memset
malloc
__cxa_finalize
__libc_start_main
libc.so.6
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
[]A\A]A^A_
[GQh{'f}g wLqjLg{ Lt{#`g&L#uLpgu&Lc'&g2n%s
[4m%*.c
[24m| I've managed to trap the flag ghost in this box, but it's turned invisible!
Can you figure out how to reveal them?
;*3$"
GCC: (Debian 10.2.1-6) 10.2.1 20210110
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.0
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
ghost.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
get_flag
_edata
printf@GLIBC_2.2.5
memset@GLIBC_2.2.5
__libc_start_main@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
malloc@GLIBC_2.2.5
__bss_start
main
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.gnu.build-id
.note.ABI-tag
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.got.plt
.data
.bss
.comment
```

Let [cyberchef's](https://gchq.github.io/CyberChef/#recipe=Magic(3,true,false,'HTB')&input=W0dRaHsnZn1nIHdMcWpMZ3sgTHR7I2BnJkwjdUxwZ3UmTGMnJmcybiVzCg) magic reciepe do all the work:
![[Pasted image 20221026214734.png]]