


[[Meterpreter]]

## Different shell types

#### Bind shells
- instructs the target machine to open a command shell and listen on a local port
- The attack machine then connects to the target machine on the listening port.
- blocked by firewalls: 
	- any correctly configured firewall will block traffic to some random port like 4444.



#### Reverse shells
- actively pushes a connection back to the attack machine rather than waiting for an incoming connection
- on our attack machine we open a local port and listen for a connection from our target
- 