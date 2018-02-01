# Mining / block propagation simulator

Simulates new block announcements propagating across the Nimiq
network.

Use these command-line options to control the simulation parameters:

```
  --help                     show options
  --blocks arg (=2016)       number of blocks to simulate
  --latency arg (=1)         block relay/validate latency (in seconds) to
                             simulate
  --runs arg (=1)            number of times to run simulation
  --rng_seed arg (=0)        random number generator seed
  --config arg (=mining.cfg) Mining config filename
```

The network topology and miner configuration is specified in
a config file; see the .cfg files here for examples.

Config file options:
```
miner=hashrate type
biconnect=m n connection_latency
```

I don't do autotools, so you'll have to edit the Makefile
unless you're compiling on OSX. The only dependency is
boost (but you do need a c++11-capable C++ compiler).


Example runs:

```
$ ./mining_simulator
Simulating 2016 blocks, default latency 1secs, with 10 miners over 1 runs
Configuration: Ten equal miners, connected in a ring
Orphan rate: 4.117%
Miner hashrate shares (%): 10 10 10 10 10 10 10 10 10 10
Miner block shares (%): 10.19 9.26 10.66 10.4 9.933 10.19 9.208 9.984 10.61 9.571

$ mining_simulator --latency 2
Simulating 2016 blocks, default latency 2secs, with 10 miners over 1 runs
Configuration: Ten equal miners, connected in a ring
Orphan rate: 7.688%
Miner hashrate shares (%): 10 10 10 10 10 10 10 10 10 10
Miner block shares (%): 10.21 9.135 10.69 10.21 10.1 10.32 9.135 9.995 10.85 9.35

$ mining_simulator --latency 2 --config mining_30.cfg --runs 100
Simulating 2016 blocks, default latency 2secs, with 8 miners over 100 runs
Configuration: 30% miner, with 7 10% miners, selected connectivity
Orphan rate: 3.454%
Miner hashrate shares (%): 30 10 10 10 10 10 10 10
Miner block shares (%): 29.89 10.09 10.04 10.01 9.952 9.89 10.08 10.04
```

