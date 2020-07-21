# docker-class---02

The second day we have learned following things

cgroups
namespace

PCB- Process control block

Network Namespace creation
-

To create network namespace

sudo ip netns add red
sudo ip netns add green

To list out network namespace
sudo ip netns 

To check interfaces
sudo ip netns exec red ip link


To create virtual interface pair
sudo ip link add veth-red type veth peer name veth-green

Assign the interfaces to Namespaces
sudo ip link set veth-red netns red
sudo ip link set veth-green netns green

Again login to namespace to check interfaces
sudo ip netns exec red ip link


Assign an IP address to each interface
sudo ip netns exec red ip addr add 192.168.15.1/24 dev veth-red
sudo ip netns exec green ip addr add 192.168.15.2/24 dev veth-green

To check whether IP is perfectly assigned or not
sudo ip netns exec red ip addr
sudo ip netns exec green ip addr

To bring up interfaces
sudo ip netns exec red ip link set lo up
sudo ip netns exec green ip link set lo up

sudo ip netns exec red ip link set veth-red up
sudo ip netns exec green ip link set veth-green up

 
To ping another namespace by IP
sudo ip netns exec green ping 192.168.15.1
