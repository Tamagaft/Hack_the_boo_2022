202211011309
Status:: #ctf
Tags: [[hack_the_boo]] [[reversing]]

# hack_the_boo_oujia
Platform: *Hackthebox*
event: *Hack the boo*
type: *reversing*
task: **
flag: **HTB{Adding_sleeps_to_your_code_makes_it_easy_to_optimize_later!}**

# steps
Use `strings` tool to get all text data from binary:
```bash
strings ouija 
/lib64/ld-linux-x86-64.so.2
puts
putchar
strdup
printf
stdout
sleep
__cxa_finalize
setvbuf
__libc_start_main
libc.so.6
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
gfffH
gfffH
gfffH
gfffH
gfffH
gfffH
gfffH
gfffH
gfffH
gfffH
[]A\A]A^A_
ZLT{Svvafy_kdwwhk_lg_qgmj_ugvw_escwk_al_wskq_lg_ghlaearw_dslwj!}
Retrieving key.
     
 done!
Hmm, I don't like that one. Let's pick a new one.
Yes, 18 will do nicely.
Let's get ready to start. This might take a while!
This one's a lowercase letter
Wrapping it round...
This one's an uppercase letter!
We can leave this one alone.
Okay, let's write down this letter! This is a pretty complex operation, you might want to check back later.
You're still here?
;*3$"
GCC: (Debian 10.2.1-6) 10.2.1 20210110
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.0
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
main.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
putchar@GLIBC_2.2.5
_ITM_deregisterTMCloneTable
stdout@GLIBC_2.2.5
puts@GLIBC_2.2.5
_edata
printf@GLIBC_2.2.5
__libc_start_main@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
setvbuf@GLIBC_2.2.5
__TMC_END__
_ITM_registerTMCloneTable
flag
strdup@GLIBC_2.2.5
sleep@GLIBC_2.2.5
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

Here we can see flag, which seems to be rot encoded:
`ZLT{Svvafy_kdwwhk_lg_qgmj_ugvw_escwk_al_wskq_lg_ghlaearw_dslwj!}`

Rot34 [cyberchef](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,34)  reciepe returns the flag:
`HTB{Adding_sleeps_to_your_code_makes_it_easy_to_optimize_later!}`

`
	

