## on Your IR Server</br>

### 1. Connect Server to Cloudflare CDN or ArvanCloud.</br>
 (whichever you choose), I'll go by with Cloudflare</br></br>
&nbsp;&nbsp; 1-1. Login into cloudflare Account</br>
&nbsp;&nbsp; 1-2. Click + to add the domain you purchase from [Freenom](https://www.freenom.com/en/index.html?lang=en) to your account</br>
&nbsp;&nbsp; 1-3. Set cloudflare NS to your domain</br>
&nbsp;&nbsp; 1-4. In DNS > DNS Records</br>
&nbsp;&nbsp; 1-5. Create new A Record, Set Name to your Subdomain and IPv4 address to your IR Server</br>
&nbsp;&nbsp; 1-6. Turn off Proxy </br></br>

#### Now let's set up the server. </br>
If you have any problems on the connections and couldn't get the packages, there are two ways you can solve this</br>
1. Use Shekan DNS  </br>
#### Edit the resolv.conf  </br>
```shell script
sudo nano /etc/resolv.conf
``` 
and set the followings.
```shell script
nameserver 178.22.122.100
nameserver 185.51.200.2
#nameserver 127.0.0.53
#options edns0
``` 
2. Use ArvanCloud mirror servers.  </br>
#### Edit the resource.list  </br>
```shell script
sudo nano /etc/apt/sources.list
``` 
and set the url below for servers
```shell script
deb http://mirror.arvancloud.ir/ubuntu bionic universe
``` 
Personnally I changed the DNS and it works like a charm.</br></br>
Now that you are up and running, let's get started.</br></br>
### 2. Install requirements </br> 
#### 2-1. Install bbr on the Server </br>
```shell script
echo "net.ipv4.ip_forward = 1" | sudo tee /etc/sysctl.d/60-custom.conf
echo "net.core.default_qdisc=fq" | sudo tee -a /etc/sysctl.d/60-custom.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee -a /etc/sysctl.d/60-custom.conf
sudo sysctl -p /etc/sysctl.d/60-custom.conf
``` 
#### 2-2. Disable firewall </br>
```shell script
ufw disable
``` 
#### 2-3. update & upgrade the packages </br>
```shell script
sudo apt update && apt dist-upgrade -y
```
