# A good way to install packages

## Virtual enviroment in python
### Intro

`virtualenv` is a tool to create isolated Python environments.

The basic problem being addressed is one of dependencies and versions, and indirectly permissions. Imagine you have an application that needs version 1 of LibFoo, but another application requires version 2. How can you use both these applications? If you install everything into `/usr/lib/python2.7/site-packages` (or whatever your platform’s standard location is), it’s easy to end up in a situation where you unintentionally upgrade an application that shouldn’t be upgraded.

Or more generally, what if you want to install an application and leave it be? If an application works, any change in its libraries or the versions of those libraries can break the application.

Also, what if you can’t install packages into the global `site-packages` directory? For instance, on a shared host.

In all these cases, virtualenv can help you. It creates an environment that has its own installation directories, that doesn’t share libraries with other virtualenv environments (and optionally doesn’t access the globally installed libraries either).

### Usage
Install virtualenv:
```
$ pip install virtualenv
```

Create new virtual enviroment. For example, let's create enviroment called "my_env":
```
$ virtualenv my_env
```
`my_env` is a directory to place the new virtual environment. The python in your new virtualenv is effectively isolated from the python that was used to create it.

In a newly created virtualenv there will be a `activate` shell script. Run:
```
$ source my_env/bin/activate
```
After this command your terminal would look like:
```
(my_env)$
```
Then let's install `jupyter` in `my_env`:
```
(my_env)$ pip install jupyter
```
After installation, let's run jupyter notebook. By default jupyter notebook uses port 8888. But this port most likely is already used, so let's choose another one, say, 12345:
```
(my_env)$ jupyter notebook --ip 0.0.0.0 --port 12345
```
Now `jupyter notebook` is running on server in virtual enviroment. Let's connect to it from our local machine using web browser. To do it, we have to use `PuTTY`.

## PyTTY
Download, install and run `PuTTY`. You will see this window:

<img src='111.PNG' width=500 height=400>

You have to fill the "Host Name (or IP adress)" field using your username and host name like this:

<img src='222.PNG' width=500 height=400>

After filling, press the '+' button near field 'SSH' on the left side of the window. Then you will see the 'Tunnels' field. Press it.

<img src='333.PNG' width=500 height=400>

Then you will see new fields. You have to fill fields 'Source port' and 'Destination' click button 'Add'. After this new line should appear in.

<img src='444.PNG' width=500 height=400>

In the field 'Destination' enter 'localhost:12345', since port 12345 is the one that Jupyter Notebook is running on.
In the field 'Source port' enter the port that you want to use to access Jupyter on your local machine (for example, 9999). It is recommended to use a port greater or equal to 8000 as those port numbers are unlikely to be used by another process. If choosen port is used by another process, though, select a different, unused port number.

<img src='555.PNG' width=500 height=400>

After filling fields 'Source port' and 'Destination' click button 'Add'. After this new line should appear in 'Forwarded ports' window:

<img src='666.PNG' width=500 height=400>

Then ckick the 'open' button to open the connection. After this you may see this window:

<img src='777.PNG' width=500 height=400>

Press the 'Yes' button. Now the connection is established.

## Connect jupyter notebook with browser
When you run jupyter notebook, some lines appeared in the terminal. Found among them one line, that looks like:
```
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://(jump.dev.nbs or 127.0.0.1):12345/?token=e87a50a9ae82e9e002ec10591c1192b110b276e7d3649afb
```

From here copy token and use it to create link. In this example, link should be:
```
http://127.0.0.1:9999/?token=e87a50a9ae82e9e002ec10591c1192b110b276e7d3649afb
```
Every time there would be another token. So, link looks like:
```
http://127.0.0.1:SOURCEPORT/?token=TOKEN
```
Where:
- SOURCEPORT is the number you've entered in the 'Source port' field.
- TOKEN you have to copy from terminal in which jupyter is running.

Paste composed link into your web browser. 

That's it!






## Usefull links:
- Download `PuTTY`: https://www.putty.org/

