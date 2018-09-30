**Introduction**

This project is aiming to build a docker composed Vault service with HA enabled backed by Consul storage.

It's refered to the two passages below to build the cluster in docker.

+ https://www.vaultproject.io/guides/operations/vault-ha-consul.html

+ https://www.hashicorp.com/resources/hashicorp-vault-administrative-guide

The base docker images are from hashicorp official but rebuild locally. 

The detailed reason of this could be refered issue and pr in these two project.


**Usage**

Before launch, generate TLS certs and keys for consul servers, clients and vault servers 
with the same root key and put them according to the location in `docker-compose.yml`
and create data and log dir for consul and vault respectively.

Remember to properly set the domain name of each cert to concord with the consul servers.

After above, first run `docker-compose up` in cli.

Then you can access the vault ui in browser with `http://$HOST_IP:9200/ui` 
while the vault api with `http://$HOST_IP:9200`. A standby vault server is also
availabel on `http://$HOST_IP:9210`.

***WARNING***
Don't forget to modify the config json file under `consul/config/` dir, 
to change the `encrypt` key's value, which should be the same among all servers and clients config
files.

As this document[c] said, you should generate a 16 bytes Base 64 encoded string as the key.

If you use Python, the code below may be helpful:
```
import os
import base64
key = base64.b64encode(os.urandom(16)).decode('utf-8')
print(key)
```

**Something to Improve**

<del>+ The connection between consul client and vault service is still unsecure.</del>

<del>+ The tls connection failed, detailed in this issue:</del>
<del>https://github.com/hashicorp/docker-vault/issues/110</del>

<del>+ Gossip communication among consul neeeds to be set encrypted.</del>

+ add a reverse proxy layer to handle vault server with https+let tls cert by nginx.


[c] https://www.consul.io/docs/agent/encryption.html
