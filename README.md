# FreeTON Validation Node
This is validation node (dockerized) adaptation for [FreeTON](https://freeton.org/)

#### Install
Clone project and run  
```docker build -t freenode .```
#### Run
```docker run -d --name ton-node --network host -e "PUBLIC_IP=<YOUR_PUBLIC_IP>" -e "CONSOLE_PORT=<TCP-PORT1>" -e "LITESERVER=true" -e "LITE_PORT=<TCP-PORT2>" -it freenode```  
  
_Note: If you want to run stable validation node, you should link `-v <local_SSD>:/var/ton-work/db` to docker container.   Also you shold use fast SSD as [described here](https://ton.org/Validator-HOWTO.txt)._

If you don't need Liteserver, then remove -e "LITESERVER=true".

#### Use
```docker exec -ti <container-id> /bin/bash```

```./validator-engine-console -k client -p server.pub -a <IP>:<TCP-PORT1>```

IP:PORT is shown at start of container.

#### Lite-client
To use lite-client you need to get liteserver.pub from container.

```docker cp <container-id>:/var/ton-work/db/liteserver.pub /your/path```

Then you can connect to it, but be sure you use right port, it's different from fullnode console port.

```lite-client -a <IP>:<TCP-PORT2> -p liteserver.pub```
