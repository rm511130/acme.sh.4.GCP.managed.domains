# acme.sh.4.GCP.managed.domains

[Configure LetsEncrypt and Acme.sh](https://github.com/acmesh-official/acme.sh)

- As more and more solutions are built using microservices architecture, it is very important to have all your public endpoints encrypted. The good news is that you can achieve it without spending any additional penny. LetsEncrypt is one such project which is a free and open Certificate Authority and you can easily integrate it with your setup to automatically generate SSL certificates free of cost, FOREVER…


- The domain `pks4u.com` is being managed by Google, so we're going to use the Google Instructions:

```
gcloud init              # it may ask you to run $ sudo snap install google-cloud-sdk --classic
```

- You should see:
```
Welcome! This command will take you through the configuration of gcloud.

Settings from your current configuration [default] are:
compute:
  region: us-east1
  zone: us-east1-b
core:
  account: rmeira@pivotal.io
  disable_usage_reporting: 'True'
  project: fe-rmeira
```

```
cd ~
git clone https://github.com/acmesh-official/acme.sh.git
cd ./acme.sh
./acme.sh --install
export CLOUDSDK_ACTIVE_CONFIG_NAME=default
```

```
./acme.sh --issue --dns dns_gcloud -d '*.pks4u.com' -d '*.pks.pks4u.com' -d '*.apps.pks4u.com' -d '*.sys.pks4u.com' -d '*.login.sys.pks4u.com' -d '*.uaa.sys.pks4u.com'
```
- And then you wait for `acme.sh` to do its magic... and eventually you will see:

```
[Mon Jul  6 00:32:52 UTC 2020] Your cert is in  /home/ubuntu/.acme.sh/pks4u.com/pks4u.com.cer 
[Mon Jul  6 00:32:52 UTC 2020] Your cert key is in  /home/ubuntu/.acme.sh/pks4u.com/pks4u.com.key 
[Mon Jul  6 00:32:52 UTC 2020] The intermediate CA cert is in  /home/ubuntu/.acme.sh/pks4u.com/ca.cer 
[Mon Jul  6 00:32:52 UTC 2020] And the full chain certs is there:  /home/ubuntu/.acme.sh/pks4u.com/fullchain.cer 
```

- You can use https://www.sslshopper.com/certificate-decoder.html to decode the cert:

```
Certificate Information:
Common Name: pks4u.com
Subject Alternative Names: *.apps.pks4u.com, *.login.sys.pks4u.com, *.pks.pks4u.com, *.pks4u.com, *.sys.pks4u.com, *.uaa.sys.pks4u.com, pks4u.com
Valid From: July 5, 2020
Valid To: October 3, 2020
Issuer: Let's Encrypt Authority X3, Let's Encrypt Write review of Let's Encrypt
Serial Number: 039b90fdb27a6487b880c7aa4523181c8c37
```






