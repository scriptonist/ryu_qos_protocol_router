# What are we building ?
We are building an intelligent switch which can satisfy a particular bandwidth/delay requirement. It classifies the packet according to the protocol of the packet.

What we'll accomplish is 
- TCP packets will be send on a bandwidth. Say 500 kb/s
- UDP packets will be send on a different bandwidth. 1000 kb/s

# Steps to setup
- Clone this repository
- `cd` into this repository
- Create a new virtualenv of python2 in this repository
```
virtualenv env
```
- Activate this environment
```
source env/bin/activate
```
- Install ryu using pip
```
pip install ryu
```
- Clone RYU repository
```
git clone https://github.com/osrg/ryu.git
```
- Install ryu
```
cd ryu
pip install .
```
- Come out from ryu directory
```
cd ..
```
- Start mininet topology
```
sudo mn -c
./start_mininet.sh
```
- Setup switch, open xterm window in s0
```
xterm s0
```
- In switch's xterm do, 
```
./setup_switch.sh
```
- Open two xterm windows of c0
```
xterm c0 c0 
```
- In one xterm window, Do the following
```
source env/bin/activate
./start_ryu_manager.sh
```
- In the other xterm window, dot the following
```
./set_ovsdb_addr.sh
./setup_q.sh
./add_qos_rules.sh
```
- Now open 2 windows of h1 and h2 each.
```
xterm h1 h1 h2 h2
```
- In first window of h1, do the following
```
./create_tcp_server.sh
```
- In second window of h1, do
```
./create_udp_server.sh
```
- In first window of h2, do
```
./send_traffic_tcp.sh
```
- In second window of h2, do
```
./send_traffic_udp.sh
```
- Now examine the bandwidth in h1 xterm windows and see the difference for tcp and udp.

Note: This is a modified version of RYU Book QoS Example 1 (12.2) , so refer that. The only difference is there the classification is based on destination port and here it is based on protocol of the packet.
