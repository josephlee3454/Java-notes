
### Local Processing 
* Your browser extracts the "scheme"/protocol (we have established
that this will be HTTP)
* Now that the browser has the intended hostname for the request, it needs to resolve an IP address.

### REsolve an ip 
* If the cache lookup fails (we will assume it does), your browser fires off a DNS request using UDP3. The DNS request contains the preconfigured IP for your DNS server and your return IP in its header.
* Your request will now have to travel many network devices to reach its target DNS server. Whenever the packet hits a piece of networking equipment, the device uses a routing table to determine which other device it is connected to that is most likely situated along the shortest path to the destination
* Once your request arrives at your configured DNS server, the server looks for the address associated with the requested hostname. If it finds one, it sends a response.
* We will assume the request is successful though, given that all of this is still a precursor. 

## EStablish TCP connection 
* Now that the client has an IP address, it can send an HTTP5 request, right? Almost, but first, since the request is sent over TCP6, which is a transport layer protocol like UDP, the client must open a TCP connection.

## Send an HTTP Request
* The request is made up of a "request line", request header, and a body. The "request line" is simply a line that indicates the HTTP method, the resource being requested, and the protocol version. The header of the request is made up of pairs in the form name:value <CR><LF>. Two consecutive <CR><LF> pairs indicate the end of the header section. The only mandatory field in an HTTP request is HOST, which contains the domain and port that the request is being sent to (domain.com:8080), although in some cases the port can be omitted. Outside of the host field, common standard HTTP header fields include Origin, Accept, Accept-Encoding, and many more. The request can also include any non-standard header fields, and historically non-standard fields are indicated by prefixing X- to the field’s name. The body content of an HTTP request is completely optional, but often contains something like form data or JSON.