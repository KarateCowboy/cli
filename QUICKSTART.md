# Quick Start Guide to Building the CLI

## Ubuntu and other linux

### Prerequisites

To build on Ubuntu you will need nodejs and npm or yarn. You can install the node binary using apt-get from the repository. However, the repository is usually woefully behind. A much better way to install is to download the latest LTS from [nodejs.org](https://nodejs.org/). Unzip the tar to your home directory, then `mv` it to `/opt` and link. EG: 
```
sudo mv node-v6.9.5-linux-x64/ /opt
sudo ln -s /opt/node-v6.9.5-linux-x64/bin/node /usr/local/bin/node
sudo ln -s /opt/node-v6.9.5-linux-x64/bin/npm /usr/local/bin/npm
```

You will also need the go-lang compiler. Again, you can install via the repositories, but the more reliable way to install go is to follow [the instructions from the vendor](https://github.com/golang/go/wiki/Ubuntu).

Once you have installed go, you'll need to install Godep, a popular client for managing Go-lang modules. To do this, run:

```
 go get github.com/tools/godep
```
This should install the Godep binary to your $GOPATH directory. 

### Putting together the heroku cli

Now for the main event. Use git or your preferred method to get the source from github, eg:

```
git clone http://github.com/heroku/cli
cd cli
```

#### Node dependencies
You will need to install the node modules found in the source's `package.json`. At heroku we use facebook's yarn. If you also use yarn, then you're way ahead and can handle installing the dependencies without help. Otherwise, you can use npm. Just run:
```
npm install
```
#### Go lang dependencies

From the cli source directory, run
```
gedep restore
```
This will install the project`s needed Go modules into whatever folder you specified for your $GOPATH. You may see a warning about not being in your $GOPATH directory, but it should still work. Next, build the project:
```
go build -v
```

This should build the cli`s Go modules. Next, try running the client:
```
./bin/run help
```
You should see the heroku client help text. You're done!