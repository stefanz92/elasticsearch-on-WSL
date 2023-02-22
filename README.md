# elasticsearch-on-WSL
How to install and run elasticsearch on WSL


# reffrence: https://www.elastic.co/guide/en/elasticsearch/reference/8.6/deb.html#deb-repo

Open your WSL terminal and update the package list:
sudo apt-get update

Install the OpenJDK 11 runtime environment, which is required to run Elasticsearch:

```sudo apt-get install openjdk-11-jre-headless```

Download the Elasticsearch Debian package from the official website using wget:
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.2-amd64.deb
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.2-amd64.deb.sha512
shasum -a 512 -c elasticsearch-8.6.2-amd64.deb.sha512 
sudo dpkg -i elasticsearch-8.6.2-amd64.deb
```

Elasticsearch should not be run as the root user due to security concerns. Running Elasticsearch as root could allow an attacker to gain control of the entire system.

To start Elasticsearch as a non-root user, you can create a new user account and grant it the necessary permissions to run Elasticsearch. Here's how:


Create a new user account:

```sudo adduser elasticsearch```

Grant ownership of the Elasticsearch installation directory to the new user:

```sudo chown -R elasticsearch:elasticsearch /usr/share/elasticsearch/```

Grant the new user permission to write to the Elasticsearch data directory:

```
sudo chmod 775 /var/lib/elasticsearch/
sudo chown -R elasticsearch:elasticsearch /var/lib/elasticsearch/
```

Start Elasticsearch as the new user:

```sudo -u elasticsearch /usr/share/elasticsearch/bin/elasticsearch```

