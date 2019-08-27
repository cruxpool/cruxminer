# Cruxminer

## Curent version : v0.0.1

Cruxminer is an Ethash Miner (ETH / ETC) for both Nvidia and AMD cards.
Currently (epoch 281), the DAG is a little over 3GB, so you need a graphic card with **at least 4GB**

## How to use:
### Core commands :
* **Name** :
  use `-n` or `--name` with your login (usually, it's your wallet adress)
  
* **Pool** :
  use `-p` or `--pool`with the adress
  By default, cruxminer will mine on cruxpool but you can specify which pool you want to use 

* **Worker** :
  use `-w` or `--worker` to give a name to your rig.
  If you don't set a worker name, you'll have the default name on the pool (0 on Ethermine)

* **Password** :
  use `--password` only if you need a password to connect to the pool.
  
* **Scheme** : 
  use `-s` or `--scheme` to choose a stratum flavor.
  It's set by default on `stratum` for auto-detection or you can choose `stratum+tcp` for regular stratum, `stratum1+tcp` for eth-proxy protocol, `stratum2+tcp` for Nicehash (EthereumStratum/2.0.0) or `stratum3+tcp` (EthereumStratum/2.0.0)
  
So on Linux, it should be like this (what's between brackets is optionnal)
` ./cruxminer -n 0x123456789ABCDEF123456789ABDEF [-w John_Doe -p x -s stratum1+tcp ] `

### Additionnal commands
* **Version** :
  use `-V` (capital case is important) or `--version`to .
  This command will show the output, and exit immediatly.
  
* **URL** :
  Additionnaly, you can configure cruxminer like in ethminer, like this `-u scheme://Name.Worker@pool:port`
