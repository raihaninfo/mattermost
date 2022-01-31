# mattermost

Mattermost is an open source platform for secure collaboration across the entire software development lifecycle.

# Mattermost install ubuntu

## 1. Update the system

```
sudo apt update
sudo apt upgrade
```

## 2: Install PostgreSQL Database Server

```
sudo apt -y install postgresql postgresql-contrib
```

```
sudo --login --user postgres
```

```
psql
CREATE DATABASE mattermost;
CREATE USER tester WITH PASSWORD 'What@Mattermost';
GRANT ALL PRIVILEGES ON DATABASE mattermost to tester;
\q
```

> _NOTE:_ You can enter the username and password of your choice

> Please ensure to note this username and password because it will be used later to populate the

## 3: Create a system user and group

```
sudo useradd --system --user-group mattermost
```

## 4: Download and Install the Mattermost Server

```
wget https://releases.mattermost.com/5.23.1/mattermost-5.23.1-linux-amd64.tar.gz
```

## Extract file

```
tar xvf mattermost-5.23.1-linux-amd64.tar.gz
```

## move the extracted file to the /opt directory.

```
sudo mv mattermost /opt
```

## Create the storage directory for files and images that users post on Mattermost

```
sudo mkdir /opt/mattermost/data
```

## Change the directory ownership and permission to the mattermost user

```
sudo chown -R mattermost:mattermost /opt/mattermost
sudo chmod -R g+w /opt/mattermost
```

## 5: Configure Mattermost Server.

```
sudo nano /opt/mattermost/config/config.json
```

> Scroll to where you have the sqlSetttings as shown below and apend “postgres” to the DriverName and postgres:/ to the Data Source

```json
    "SqlSettings": {
        "DriverName": "postgres",
        "DataSource": "postgres://tester:What@Mattermost@localhost:5432/mattermost?sslmode=disable&connect_timeout=10",
        "DataSourceReplicas": [],
```
