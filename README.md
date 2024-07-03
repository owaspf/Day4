# Day4
* Hafnium web apache manipulation openssl
```
mkdir openssl
```
```
cd openssl
```
```
openssl genpkey –algorithm RSA –out pk.pem –pkeyopt rsa_keygen_bits:2048
```
```
ls
```
```
cat pk.pem
```
(le mieux c’est ajouter un chiffrement  et non en clair)
```
openssl  rsa –in pk.pem –text
```
```
openssl  rsa –in pk.pem –text –noout
```
Calculer la clé publique de la clé privée : 
```
openssl  rsa –in pk.pem –pubout –out pub.pem
```
```
ls
```
```
openssl rsa –pubin –in pub.pem –text –noout
```
(modulus et exponents)

* Hafnium Serveur https auto-signé
```
apt update
```
```
apt install apache2
```
configure host
```
getent hosts
```
At broswer : 127.0.0.1
```
sudo nano var/www/html/index.html
```
Personalized data
```
sudo nano /etc/hosts/
```
change 127.0.0.1  localhost </br>
by  127.0.0.1  localhost www.monsite.tn </br>
```
systemctl status apache2
```
```
systemctl stop nginx 
```
```
systemctl start apache2
```
```
ip addr
```
Configuration du serveur web : </br>
Les certificats se trouvent dans : 
```
ls /etc/ssl/certs
```
```
cp cert.pem  /etc/ssl/certs/dast.pem
```
```
cp pk.pem /etc/ssl/private
```
```
cd /etc/apache2
```
```
cd ..
```
```
cd sites-available
```
```
cat 000-default.conf
```
```
nano 000-default.conf
```
Mettre sslengine  On
```
sslengine  On
```

Ajouter : 
```
SSLCertificateFile /etc/ssl/cert/dast.pem
SSLCertificateKeyFile /etc/ssl/private/pk.pem
```
```
systemctl reload apache2
```
Erreur : 
```
journalctl –xeu apache2.service
```

Activer le module SSL:
```
a2enmod ssl
```
```
systemctl restart apache2
```
https://192.x.x.x
```
Revenir à 000-default.conf
```
Virtualhost port 443 
```
Ajouter  ServerName hacking.local
```
ServerName hacking.local
```
```
systemctl restart apache2
```

Warning du candenas
