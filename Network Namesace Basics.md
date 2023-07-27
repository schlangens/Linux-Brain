Isolated networks created on the host. Like a subnet.

``ip netns add red``

``ip netns add blue``

``ip netns``

# Exec in Network NS

``ip link``

``ip netns exec red ip link``

![[Pasted image 20230102150724.png]]


A shorthand way

``ip -n red link``

![[Pasted image 20230102150806.png]]



# Connect 2 namespaces together

``ip link add veth-red type veth peer name veth-blue``

![[Pasted image 20230102151003.png]]


Now attach interface to the appropriate namespace as such

``ip link set veth-red netns red``

![[Pasted image 20230102151131.png]]

``ip link set veth-blue netns blue``

![[Pasted image 20230102151219.png]]

Assign IP address to each namespace

``ip -n red addr add 192.168.15.1 dev veth-red``
``ip -n blue addr add 192.168.15.2 dev veth-blue``

Turn on the interface

``ip -n red link set veth-red up``
``ip -n blue link set veth-blue up``

Now ping to test
``ip netns exec red ping 192.168.15.2``


![[Pasted image 20230102151618.png]]


![[Pasted image 20230102151644.png]]

![[Pasted image 20230102151716.png]]

Now create a virtual switch on the host to network the namespaces together

![[Pasted image 20230102151820.png]]

``ip link add v-net-0 type bridge``

![[Pasted image 20230102151906.png]]

As far as our host is concern it is just another interface.

![[Pasted image 20230102151935.png]]

Bring the "Interface/switch up"

``ip link set dev v-net-0 up``

Now connect the namespaces to the virtual network/switch/interface you just created ``v-net-0``
![[Pasted image 20230102152108.png]]

Get rid of previous cable. When you del one end of that cable the other end gets removed automatically

``ip -n red link del veth-red``

Now connect to the bridge network you created

``ip link add veth-red type veth peer name veth-red-br``
``ip link add veth-blue type veth peer name veth-blue-br``

Now link them to name space

``ip link set veth-red netns red``
``ip link set veth-red-br master v-net-0``

``ip link set veth-blue netns blue``
``ip link set veth-blue-br master v-net-0``

![[Pasted image 20230102152548.png]]

Now set the address for the links and turn them up

``ip -n red addr add 192.168.15.1 dev veth-red``
``ip -n red addr add 192.168.15.2 dev veth-blue``

``ip -n red link set veth-red up``
``ip -n blue link set veth-blue up``

![[Pasted image 20230102160837.png]]



You can not ping your namespace just by using ``ping 192.168.15.1``

``ip addr add 192.168.15.5/24 dev v-net-0``

Now we can ping it from our localhost

``ping 192.168.15.1``

You still can not access outside world you need to do the following

``ip netns exec blue ping 192.168.1.3``

Add the route to the host gateway

``ip netns exec blue ip route add 192.168.1.0/24 via 192.168.15.5``


- Enable NAT functionality on Host

``iptables -t nat -A POSTROUTING -s 192.168.15.9/24 -j MASQUERADE``

- Enable Internet by enabled default gateway

``ip netns exec blue ip route add default via 192.168.15.5``

- Test by pinging Google

``ip netns exec blue ping 8.8.8.8``

- Enable traffic to the host from the outside

``iptables -t nat -A PREROUTING --dport 80 --to-destination 192.168.15.2:80 -j DNAT``
 



