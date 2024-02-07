# DNS_forwarder
project using Python to build a simple DNS forwarder with domain blocking and DoH capabilities. This DNS forwarder will need to do the following: (1) receive an arbitrary DNS message from a client, (2) check if the domain name should be blocked, and if so respond with an NXDomain message, (3) if the queried domain name is allowed, forward the DNS message to either standard DNS resolver or a DoH-capable resolver, (4) wait for the response from the resolver and forward it back to the client. Command line parameters should be dns_forwarder.py [-h] [-d DST_IP] -f DENY_LIST_FILE 
                        [-l LOG_FILE] [--doh] [--doh_server DOH_SERVER]  Requirements are If --doh or --doh_server are specified, the forwarder MUST forward the DNS query using the DoH protocol
If neither --doh nor --doh_server are specified (in which case -d MUST be present), the forwarder MUST forward the DNS query using the DNS protocol
The DNS forwarder MUST receive DNS messages from the client via a simple UDP server socket.
When DoH is not used, the -d option will be specified and the forwarder must use a simple UDP client socket to forward the client's query to the DNS resolver
The DENY_LIST_FILE file MUST contain a (potentially empty) list of domain names that MUST be blocked by the forwarder. 
DoH REQUESTS
You are required to use GET requests as defined in RFC 8484.  when a domain is blocked, your DNS forwarder MUST reply to the client with a properly formatted NXDOMAIN response.

LOG FILE ENTRY FORMAT
The log file should be a text file containing a record of all domain names and query types that have been requested, and whether the request was blocked or allowed. Here is an example of how the code will be executed:

# ./dns_forwarder.py --doh_server 1.1.1.1 -l ./queries.log -f ./deny_list.txt
