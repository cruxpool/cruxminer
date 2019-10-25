# Cruxminer

## Curent version : v0.1.0

Cruxminer is an Ethash Miner (ETH / ETC) for both Nvidia and AMD cards.
Currently (epoch 281), the DAG is a little over 3GB, so you need a graphic card with **at least 4GB**

## How to use:
### Core commands :
* **Name** :
  use `-n` or `--name` with your login (usually, it's your wallet adress)
  
* **Pool** :
  use `-p` or `--pool` with the url of the pool. You can set multiple pools, just add a space between them.
  
  By default, cruxminer will mine on cruxpool but you can specify which pool you want to use 

* **Worker** :
  use `-w` or `--worker` to give a name to your rig.
  
  If you don't set a worker name, you'll have the default name on the pool (0 on Ethermine)

* **Password** :
  use `--password` only if you need a password to connect to the pool.
  
* **Scheme** : 
  use `-s` or `--scheme` to choose a stratum flavor.
  
  By default, it's set on `stratum` for auto-detection or you can choose `stratum+tcp` for regular stratum, `stratum1+tcp` for eth-proxy protocol, `stratum2+tcp` for Nicehash (EthereumStratum/2.0.0) or `stratum3+tcp` (EthereumStratum/2.0.0)
  
* **Coin** :
  use `-c` or `--coin` to choose which coin to mine. For now, only ETC and ETH are available.
  
  By default, cruxminer will mine ETH.
  
  
So on Linux, it should be like this (what's between brackets is optionnal)

` ./cruxminer -n 0x123456789ABCDEF123456789ABDEF [-w John_Doe -p x -s stratum1+tcp -c ETH] `

### Miner options :
You can set 
* **Poll Interval** :
  You can set the interval between job requests to the pool in ms by using `--farm-recheck`.
  
  By default, it's set to 500ms, and the value should be between 1 and 99999.

* **Connection Max Retries** :
  You can set the maximum number of connection retries by using `--farm-retries`.
  
  By default, it's set to 3 and the value should be between 0 and 99999.
  
* **Timeout without job**
  You can set the duration before cruxminer drops the connection if there is no new job by using `--work-timeout`.
  
  By default, it's set to 180s, and the value should be between 180 and 99999.
  
* **Timeout without Response**
  You can set the duration before cruxminer drops the connection if there is no response by using `--response-timeout`.
  
  By default, it's set to 2s, and the value should be between 2 and 999.
  
* **Failover Timeout**
  You can set the duration before cruxminer returns to primary pool after by using `--failover-timeout`.
  
  By default, it's set to 0s, and the value should be between 0 and 999.
   
* **No Report** :
  By default, the software will send your reported hashrate to the pool. If you don't want to, use `--no-report`.
  
* **Display Interval** :
  You can set the interval between each display of the info/stats recap by using `--display-interval`
  
  By default, it's set to 5s and the value should be between 1 and 1800.
  
* **Display Verbosity** :
  You can set how much info is shown by the stat info/stats recap.
  
  By default, it's set to 1 and the value should be between 0 and 2.
  * 0 = Reported Hashrate + Fan Speed + Shares found + Timer
  * 1 = Same as 0 + Temperature
  * 2 = Same as 1 + Power consumption
  
### Graphic Cards commands : 
* **Device Type** :
  You can ask cruxminer to mine using only OpenCL or CUDA by using either `-G` or `--opencl`, or `-U` or `--cuda`.
  
  By default, cruxminer will detect automatically your software and use CUDA for Nvidia and OpenCL for AMD.
* **List Devices** :
  You can ask cruxminer to list the detected OpenCL/CUDA devices by using `--list-devices`.
  
  It will show the output and exit immediatly.
  
* **Temperature** :
  You can set a threshold temperature that will suspend mining if attained by using `--tstop`
  You can also set a temperature from which cruxminer will reset mining by using `--tstart`.
  
  By default, tstop is set to 0 and tstart is set to 40. They should be between 30 and 100.

#### OpenCL
* **CL Devices**
  You can set which OpenCL Device you want to use by using `--opencl-device` or `̀--opencl-devices` or `--cl-devices`.
  
  You need to give a list of the device indexes separated by space (use `--list-devices` if you want the device indexes).

The following are advanced options, change the default values at your own risk.

* **Global Work** :
  You can set the global work multiplier by using `--cl-global-work`.
  
  By default, it's set to 65536, and the value will be adjusted to the nearest power of 2.
  
* **Local Work** :
  You can set the local work multiplier by using `--cl-local-work`.
 
  By default, it's set to 128, and the value should be 64, 128 or 256.
 
* **No Binary** :
  You can ask cruxminer to use the OpenCL kernel instead of the binary ones by using`--cl-nobin`
 
* **No Exit** :
  You can ask cruxminer to not use the fast exit algorithm by using `--cl-noexit`
 
#### CUDA
* **CUDA Devices** :
  You can set which CUDA Device you want to use by using `--cu-devices`.

  You need to give a list of the device indexes separated by space (use `--list-devices` if you want the device indexes).

The following are advanced options, change the default values at your own risk.

* **Grid Size** :
  You can set the grid size by using `--cu-grid-size`

  By default, it's set to 8192, and the value should be between 1 and 131072
* **Block Size** :
  You can set the block size by using `--cu-block-size`

  By default, it's set to 128, and the value should be 32, 64, 128 or 256.
* **Parallel Hash** : 
  You can set the number of hashes per Kernel by using`--cu-parallel-hash`.

  By default, it's set to 4, and the value should be 1, 2, 4 or 8.
* **Streams**
  You can set the number of streams per GPU by using`--cu-streams`.

By default, it's set to 2, and the value should be between 1 and 99.
* **Schedule** :
  You can set a scheduler mode by using `--cu-schedule`.
  The modes are : 
  * **auto** Uses a heuristic to find the best method.
  * **spin** Instructs CUDA to actively spin when waiting for the results from the device.
  * **yield** Instructs CUDA to yield when waiting for the results from the device.
  * **sync** Instructs CUDA to block the CPU thread on a synchronize primitive when waiting for results from device.
The default is set on **sync**.
  
### API commands
#### Launching API : 
* **API** :
  You can ask cruxminer to listen on a certain adress by using : `--api-bind`.
  
  You can either put the port next to the url like for the pool (127.0.0.1:3333 for example), or you can set it with `--api-port`
* **Port** :
  When you use `--api-port`, you can use a negative port number to make it read-only mode.
  
  The port should be between 1 and 65535.
  
* **Password **
  If you want to secure the access to the API, you can set a password by using `--api-password`.
  
  **Careful**, the passwords are sent unencrypted over plain TCP.

#### Commanding the API : 
If you want to send commands to cruxminer, you need to send a JSON-RPC request.

You can use `nc` on linux to send it.

### Additionnal commands
* **Version** :
  use `-V` (capital case is important) or `--version`to show the version.
  
  This command will show the output, and exit immediatly.
  
* **Exit on Error** :
  If you want cruxminer to exit on error, set `--exit` to true.
  
  By default, it's set to false.
  
* **No Color**  :
  You can remove the color in the console line output by using `--nocolor`
  
* **Minimal Cli Log** :
  You can make cruxminer drop the timestamp and the color by using `--syslog`
  
* **Stdout** :
  You can make cruxminer log to *stdout* insead of *stderr*

* **No Eval** :
  You can make cruxminer bypass the re-evaluation of the nounces found.
  
  This makes the submission faster but you might get more rejected shares.
   
* **URL** :
  Additionnaly, you can configure cruxminer like in ethminer, like this `-u scheme://Name.Worker@pool:port`
