all:
	# create CA pri key
	openssl genrsa -out certauth.key 4096
	# create certificate by pri key
	openssl req -new -x509 -days 365 -key certauth.key -out ca.crt -subj '/C=TW/O=NYCU/CN=tsc.Hsinchu'
	# open ip_forward
	sudo sh -c "echo 1 > /proc/sys/net/ipv4/ip_forward"
	# create PREROUTING rule
	sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 9080
	sudo iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-ports 9443
	# check iptables 
	sudo iptables -t nat -L

	mkdir ./tmp
	mkdir ./tmp/sslsplit
	mkdir ./tmp/logdir

	#change sslsplit mode
	chmod +x ./sslsplit_attack

clean:
	sudo rm -f certauth.key
	sudo rm -f ca.crt
	sudo rm -rf ./tmp/
	sudo iptables -t nat -D PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8080 
	sudo iptables -t nat -D PREROUTING -p tcp --dport 443 -j REDIRECT --to-ports 8443




