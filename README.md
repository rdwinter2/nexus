# Sonatype Nexus3

https://datacenteroverlords.com/2012/03/01/creating-your-own-ssl-certificate-authority/

```bash
openssl genrsa -des3 -out rootCA.key 2048

openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem

# Install Root Certificate Into Workstations

# Create A Certificate (Done Once Per Device)
openssl genrsa -out device.key 2048

openssl req -new -key device.key -out device.csr

openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 500 -sha256


```


```
[winterb@airgap-repo-sync rootCA]$ openssl genrsa -des3 -out rootCA.key 2048
Generating RSA private key, 2048 bit long modulus
............................+++
..........................................+++
e is 65537 (0x10001)
Enter pass phrase for rootCA.key:
Verifying - Enter pass phrase for rootCA.key:
[winterb@airgap-repo-sync rootCA]$ ls
rootCA.key
[winterb@airgap-repo-sync rootCA]$ openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
Enter pass phrase for rootCA.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:NE
Locality Name (eg, city) [Default City]:Offutt AFB
Organization Name (eg, company) [Default Company Ltd]:USSTRATCOM
Organizational Unit Name (eg, section) []:AFLCMC/HBC
Common Name (eg, your name or your server's hostname) []:CA Certificate for grdn.pocnet.mil
Email Address []:robert.d.winter.ctr@mail.mil
```