# Demo (Python) app for Docker ONBUILD

## How to build this application?

```
$ rm -fr my-python-app-onbuild
```

```
$ git clone https://github.com/sudhaker/my-python-app-onbuild
Cloning into 'my-python-app-onbuild'...
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.
```

```
$ cd my-python-app-onbuild/
```

```
$ docker rmi -f "$(basename $(pwd))"
Untagged: my-python-app-onbuild:latest
Deleted: sha256:b802abf729fb4daf3d402f9d67cc186b64149efeaf1bd5821f2ac1ac85dfe21d
Deleted: sha256:65aa241f2625ffadd53acf3845650f1e852b242bb42c1368683b7736adb30bba
Deleted: sha256:60532329c19bf53697cee6072dbf2cac3989357d52da2218dd40ae465370245c
Deleted: sha256:69db3c4b3b3b8d8edbfead2cdba8bac0e3ee4739e20b2236f5e437ef0d6cda7f
Deleted: sha256:8d422d9e1bcc8b01cb8a0db4a0d8a9187d8f30152b06a33b7883554743f89dda
Deleted: sha256:e155170a17fb6fbfab874b2372b0248eecdf131ac3e59d1f2ebd26977a7719b5
Deleted: sha256:dc87c330da9c8e74b7d45db18470e013577002a3926e87b870cf0b7dd6aef7ce
```

```
$ docker build -t "$(basename $(pwd))" .
Sending build context to Docker daemon 56.32 kB
Step 1 : FROM python:3.3-onbuild
# Executing 3 build triggers...
Step 1 : COPY requirements.txt /usr/src/app/
Step 1 : RUN pip install --no-cache-dir -r requirements.txt
 ---> Running in c1fe4e2e104a
Collecting Flask==0.11.1 (from -r requirements.txt (line 1))
  Downloading Flask-0.11.1-py2.py3-none-any.whl (80kB)
Collecting Jinja2>=2.4 (from Flask==0.11.1->-r requirements.txt (line 1))
  Downloading Jinja2-2.8-py2.py3-none-any.whl (263kB)
Collecting click>=2.0 (from Flask==0.11.1->-r requirements.txt (line 1))
  Downloading click-6.6.tar.gz (283kB)
Collecting itsdangerous>=0.21 (from Flask==0.11.1->-r requirements.txt (line 1))
  Downloading itsdangerous-0.24.tar.gz (46kB)
Collecting Werkzeug>=0.7 (from Flask==0.11.1->-r requirements.txt (line 1))
  Downloading Werkzeug-0.11.11-py2.py3-none-any.whl (306kB)
Collecting MarkupSafe (from Jinja2>=2.4->Flask==0.11.1->-r requirements.txt (line 1))
  Downloading MarkupSafe-0.23.tar.gz
Installing collected packages: MarkupSafe, Jinja2, click, itsdangerous, Werkzeug, Flask
  Running setup.py install for MarkupSafe: started
    Running setup.py install for MarkupSafe: finished with status 'done'
  Running setup.py install for click: started
    Running setup.py install for click: finished with status 'done'
  Running setup.py install for itsdangerous: started
    Running setup.py install for itsdangerous: finished with status 'done'
Successfully installed Flask-0.11.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.11 click-6.6 itsdangerous-0.24
Step 1 : COPY . /usr/src/app
 ---> 29cbb254a882
Removing intermediate container c1fe4e2e104a
Removing intermediate container aaf998957023
Removing intermediate container 85e6530db2e8
Step 2 : CMD python ./app.py
 ---> Running in f674e3b73b90
 ---> 8037c824dd69
Removing intermediate container f674e3b73b90
Successfully built 8037c824dd69
```

```
$ docker run --rm -p 8080:8080 "$(basename $(pwd))"
 * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
192.168.0.3 - - [28/Sep/2016 16:33:39] "GET / HTTP/1.1" 200 -
```

** Enjoy! **
