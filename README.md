```
Docker Build/ Run SMTP (for use by Jenkins Master):

# Clone
git clone https://github.com/EMCC-Maine/docker-postfix-sendgrid-relay.git
cd docker-postfix-sendgrid-relay/

# Build docker container
docker build -t emcc-smtp-relay .

# Start docker container (--detach to run in background) 
docker run --detach -i -t --restart unless-stopped \
	-p 25:25 \
	-e SYSTEM_TIMEZONE="America/New_York" \
        -e MYNETWORKS="10.0.0.0/8 192.168.0.0/16 172.0.0.0/8 192.168.1.1/16" \
	-e API="apikey" \
	-e APIKEY="apikeyfromsendgrid" \
        --name smtp-relay \
	sj-smtp-relay

# To test
sendemail -f jim@bbc.com -t jim@bbc.com -u subject -m "RelayedViaOffice365" -s localhost:25 -o tls=no

# Stop (and remove otherwise the name is help on to)
docker stop smtp-relay && docker rm smtp-relay
```
