# ChaosEngineering

# Chaos Engineering - Step by Step guide

## Important Information 
```shell
team id : 6dec412f-9937-46a6-ac41-2f993706a6a1
team secret: 8956e88f-0211-40cc-96e8-8f0211a0cc59
```

### Step #1 Launch command window as Administrator from your desktop machine
#### initiate secured shell using the following command line, SSH stands for 'Secured Shell' -i Stands for '<identity_file>' and last parameter is  [user@]hostIP[:port]
```shell
ssh -i .\chaostraining.pem azureuser@74.235.254.188
```

### Step #2, Add packages needed to install and verify gremlin (already on many systems)
```shell
sudo -i
sudo apt update && sudo apt install -y apt-transport-https dirmngr
```

### Step #3, Add the Gremlin repo
```shell
echo "deb https://deb.gremlin.com/ release non-free" | sudo tee /etc/apt/sources.list.d/gremlin.list
```

### Step #4, Import the GPG key
```shell
	sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9CDB294B29A5B1E2E00C24C022E8EF3461A50EF6
```

### Step #5, Install Gremlin
```shell
sudo apt update && sudo apt install -y gremlin gremlind
```

### Step #6, Initiaize Gremlin
```shell
sudo -i
gremlin init
```
input team ID <cr>
input team secret <cr>

### Step #7, Gremlin check
#### to check you are connected to gremlin type 
```shell
gremlin check
```
##### Under Auth seciton you should see
```shell
auth
====================================================
Auth Input Type                      : Secret
API Response                         : OK
```

### Step #8, Under Gremlin portal run an attack 
#### Launch Browser 
#### Login to Gremlin Portal
#### Select new Experiment 
#### Select Hosts
#### Choose the IP address of the Host
#### Choose Gremlin - CPU - give make Utilization to 100%
#### Run the experiment on the selected host.
#### In the Gremlin  run a CPU attack for your VM using the Gremlin portal

### Step #9, To check the CPU utilization % from the shell  
#### in the command shell type, to view top few processes
```shell
	top
```

## Docker Commands 

### Step #10, Installing Docker
#### in the command shell type, to view top few processes
```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
#### Got OK as response for the above comand 

### Step #11, Installing appropriate repository
#### in the command shell type, to view top few processes
```shell
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
#### Got DONE as response for the above comand 

### Step #12, updates the package index files to get the latest list of available packages in the repositories
#### in the command shell type, to view top few processes
```shell
sudo apt-get update
```
#### Got DONE as response for the above comand 

### Step #13, updates the package index files to get the latest list of available packages in the repositories
#### in the command shell type, to view top few processes
```shell
apt-cache policy docker-ce
```
#### Got NO as response for the above comand 

### Step #14, To install Docker Engine, containerd, and Docker Compose on Ubuntu
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
#### Got NO as response for the above comand 

### Step #15,  to Check If the Docker Daemon or a Container Is Running
```shell
sudo systemctl status docker
```
#### Got a response for the above comand, need to press Ctrl+C to exit  

### Step #16,  to assign or change user permissions docker users
```shell
sudo usermod -aG docker azureuser
```
#### Got NO as response for the above comand 

## Nginx
### Step #17,  create Index.html page in the vm
```shell
sudo -i
mkdir -p ~/docker-nginx/html
cd ~/docker-nginx/html
nano index.html
```
#### Copy the folowing html code and paste into the index.html
```html
<html>
  <head>
    <title>Sample HTML</title>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
      integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container">
      <h1>This is a sample HTML to check our container</h1>
      <p>This signifies nginx container is working fine</p>
      <p>Now i am ready for the attack</p>
    </div>
  </body>
</html>
```
#### To save this file, type Ctrl+x 
#### to save the above file, you need to hit Ctrl+X and then Y

### Step #18,  create Container with name using nginx
```shell
sudo -i
docker run -l service=nginx --name shan-docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx
```

### Step #19,  to view if the Container has been creaed or not.
```shell
docker ps -a
```
#### to view whether the service is up and running use the above command 

### Step #20,  Install Gremlin using docker run.
```shell
docker run -d --net=host \
    --cap-add=NET_ADMIN --cap-add=SYS_BOOT --cap-add=SYS_TIME \
    --cap-add=KILL \
    --pid=host \
    -v $PWD/var/lib/gremlin:/var/lib/gremlin \
    -v $PWD/var/log/gremlin:/var/log/gremlin \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -e GREMLIN_TEAM_ID="6dec412f-9937-46a6-ac41-2f993706a6a1" \
    -e GREMLIN_TEAM_SECRET="8956e88f-0211-40cc-96e8-8f0211a0cc59" \
    gremlin/gremlin daemon
```
#### this creates nginx container in the VM

### Step #21,  to view if the Container has been creaed or not.
```shell
docker ps -a
```
#### to view whether the service is up and running use the above command 
