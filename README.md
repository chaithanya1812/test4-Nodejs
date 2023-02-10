## #Project(NodeJs)
# #Project Image
![PROJE (3)](https://user-images.githubusercontent.com/111736742/218160613-1bb52feb-b3c8-4c84-8820-21f10cea0f2f.jpg)
## Install nginx

To changes run the following command
```bash
  amazon-linux-extras install nginx1
  cd /etc/
  chmod 777 -R nginx
```

## Demo  
```bash
  vi nginx.conf
  -------------------------------------
events {}
http {
upstream chaitu{
server  Ip-address;                      
server  Ip-address;              
server  Ip-address;              
}

server {
        listen 9000; ---- you can change port number
      location / {
      proxy_pass http://chaitu;
      }
  }

}
 }
 -----------------------------------------
 ```
 ## Orginal
```bash
  vi nginx.conf
  -------------------------------------
  Place this like this.
  And also change ip-address.
  you can launch as many of containers
  ----------------------------------------
events {}
http {
upstream chaitu{
server 3.110.193.52:8081; -->This my workernode ip-address(3.110.193.52):container-host-port
server 3.110.193.52:8082;                        
server 3.110.193.52:8083;                
server 3.110.193.52:8084;
server 3.110.193.52:8085;                
}

server {
        listen 9000; ---> you can change port number as you like
      location / {
      proxy_pass http://chaitu;
      }
  }

}
 }
