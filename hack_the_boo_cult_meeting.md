202210262100
Status:: #ctf
Tags: [[hack_the_boo]], [[reversing]]

# hack_the_boo_cult_meeting
Platform: *hackthebox*
event: *hack the boo*
type: *reversing*
task: *After months of research, you're ready to attempt to infiltrate the meeting of a shadowy cult. Unfortunately, it looks like they've changed their password!*
flag: **HTB{1nf1ltr4t1ng_4_cul7_0f_str1ng5}**

# steps
Extract text using `strings` linux command:
```bash
strings meeting 
/lib64/ld-linux-x86-64.so.2
mgUa
puts
stdin
fgets
stdout
system
fwrite
strchr
__cxa_finalize
setvbuf
strcmp
__libc_start_main
libc.so.6
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
[]A\A]A^A_
[3mYou knock on the door and a panel slides back
[3m A hooded figure looks out at you
"What is the password for this week's meeting?" 
sup3r_s3cr3t_p455w0rd_f0r_u!
[3mThe panel slides closed and the lock clicks
|      | "Welcome inside..." 
/bin/sh
   \/
 \| "That's not our password - call the guards!"
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
_ITM_deregisterTMCloneTable
stdout@GLIBC_2.2.5
puts@GLIBC_2.2.5
stdin@GLIBC_2.2.5
_edata
system@GLIBC_2.2.5
strchr@GLIBC_2.2.5
__libc_start_main@GLIBC_2.2.5
fgets@GLIBC_2.2.5
__data_start
strcmp@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
setvbuf@GLIBC_2.2.5
fwrite@GLIBC_2.2.5
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

Here we get password:
`sup3r_s3cr3t_p455w0rd_f0r_u!`

Use this password to get shell:
```bash
nc 178.62.85.130 31371
You knock on the door and a panel slides back
|/👁 👁 \| A hooded figure looks out at you
"What is the password for this week's meeting?" sup3r_s3cr3t_p455w0rd_f0r_u!
sup3r_s3cr3t_p455w0rd_f0r_u!
The panel slides closed and the lock clicks
|      | "Welcome inside..." 
/bin/sh: 0: can't access tty; job control turned off
$ ls
ls
flag.txt  meeting
$ cat flag.txt  
cat flag.txt
HTB{1nf1ltr4t1ng_4_cul7_0f_str1ng5}
```
