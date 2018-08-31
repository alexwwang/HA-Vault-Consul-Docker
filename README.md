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

After above, first run `docker-compose up` in cli.

Then you can access the vault ui in browser with `https://$HOST_IP:9200/ui` 
while the vault api with `https://$HOST_IP:9200`.


**Something to Improve**

The connection between consul client and vault service is still unsecure.

The tls connection failed, detailed in this issue:
https://github.com/hashicorp/docker-vault/issues/110

