# Pokemon GO Optimizer
In Pokemon GO, each Pokemon has hidden values that determine its maximum attainable HP and CP known as individual values — or IVs for short. The goal of this project is to display these hidden values to the user as painlessly as possible, while giving insight into each Pokemon's combat abilities.

While this app is relatively undetectable, if Niantic contacts me and requests that I discontinue development, I will comply. Until then, please be aware that you are using this at your own risk.

![example](http://i.imgur.com/3V8xw1G.png)

# Host Setup

### Mac OSX

Run these commands:

```
brew install node
brew install git
brew install pkg-config
brew install --devel protobuf
npm install -g bower
git clone https://github.com/justinleewells/pogo-optimizer
cd pogo-optimizer
npm install
bower install
node index
```

### RPM-based Linux (Fedora, CentOS, RHEL)

Run these commands:

```
sudo dnf install nodejs protobuf protobuf-devel npm
sudo npm install -g bower
git clone https://github.com/justinleewells/pogo-optimizer
cd pogo-optimizer
npm install
bower install
node index
```

### Arch Linux

Run these commands:
```
sudo pacman -S nodejs protobuf npm bower
git clone https://github.com/justinleewells/pogo-optimizer
cd pogo-optimizer
npm install
bower install
node index
```

Now you should have a webserver running. Make sure your phone and computer are connected to the same wireless network.

### Setup using Docker
To install and setup everything using Docker, build the image in the root directory of this repository with:

```bash
$ git clone https://github.com/justinleewells/pogo-optimizer.git
$ cd pogo-optimizer
$ docker build -t pogo .
```

Then create a container with the same ports as described above with this command:

```bash
$ docker run -d -p 3000:3000 -p 8081:8081 -it pogo
```

All ports are not accessible and usable as described above.

### Docker setup for Windows (Docker)
Docker is VM software that will make running Pokemon Go Optimizer easier on Windows.
This will require Hyper-V to be enabled on your CPU, this may need enabling in the BIOS if your CPU supports it.
Some CPU's are not supported but if you have (Intel) VT-x or (AMD) AMD-V on the CPU this should work.

First install [Docker](https://docs.docker.com/docker-for-windows/)
If you do not have the Hyper-V installed from Microsoft, after running Docker for the first time, it will give you a warning.
Accept this warning to install and restart your PC, if this does not work, there are manual instructions on how to complete this installation.

Next launch Command Line and use the docker commands above using the lastet version by downloading the ZIP file (if you have Git installed you can grab the latest version using the git command as well).

```
git clone https://github.com/justinleewells/pogo-optimizer.git
cd pogo-optimizer
docker build -t pogo .
```

If you do not have git installed you can use the following command to automatically get the lastest version of PoGo Optimizer (I have not tested this).

```
docker run -d -p 3000:3000 -p 8081:8081 -it cmeter/pogo-optimizer
```

This should now run the latest version of Pokemon Go Optimizer! check using http://localhost:3000/

If this website is not accessible on other devices in your network, then you have some problems with your firewall setup and should disable it for ease of use. You could also setup firewall policies that allow inbound and outbound traffic on port 3000 and 8081.

## Phone Setup

Next, check your network settings for your internal ip address.
If your host computer's IP is 10.0.1.3, you'll add 10.0.1.3:8081 as a proxy on your phone.

Next, visit http://10.0.1.3:3000/ca.pem and install the certificate.

After accepting the certificate, open Pokemon GO on your phone. After you can see your character walking around, go to localhost:3000 on your host machine. Enjoy.

## iOS

To set up a WiFi proxy on your iOS 9.0.0+ phone, follow these steps:

* Go to Settings > Wi-Fi
* Click the information icon beside the network you are connected to
* Select 'Manual' in the HTTP Proxy settings at the bottom
* Enter e.g. 10.0.1.3 as the server
* Enter 8081 as the port

### Android

If your Android doesn't understands ".pem" certificates you will have to convert it to a ".crt".
Convert it with `openssl x509 -inform PEM -outform DER -in ca.pem -out ca.crt` on a system with openssl available.

To set up a WiFi proxy on your Android 6.0.1+ phone, follow these steps:

* Go to Settings > WiFi.
* Choose your WiFi network from the list.
* Select 'edit'
* Select 'Show advanced options'
* Under "Proxy," change the setting from None to Manual.
* Enter e.g. 10.0.1.3 as the proxy name.
* Enter 8081 as the port

There is currently a problem with some Android phones not accepting ca.pem or ca.crt certificated (Sony Z5 series on 6.0.1 has this problem).

The only way I have found to solve this problem is to install OpenSSL on your PC/Mac and use the above command to create a ca.crt.
Once created this needs transfering to the phone manually and then installed at Root acccess level. For this task I used [Root Certificate Manager](https://play.google.com/store/apps/details?id=net.jolivier.cert.Importer&hl=en_GB), this is quite easy, just launch the tool, it will ask for Super User prividges, accept them then use the browser to find your new ca.crt file.

## A Note About Windows
Currently, it is very difficult to get this program working on Windows. Until a fully javascript implementation of protobuf can be utilized, Windows support will not be provided. For the time being, the recommended solution is Docker. If anyone would like to contribution documentation on how to get this project running flawlessly on Windows with Docker, please contact me.

## TODO

* Display more information (level, dust efficiency, optimal moves, etc)
* Improve user experience
* Utilize fully javascript protobuf implementation
* Create Electron app

## Feature Requests/Suggestions

I'd love to hear what feature requests and suggestions you all have, so feel free to shoot me an email or open an issue.
