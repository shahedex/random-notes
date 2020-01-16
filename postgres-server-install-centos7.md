# Install Postgres as a server on CentOS 7

## Installation

### Install PostreSQL from CentOS Repo
```bash
sudo yum install postgresql postgresql-contrib
```
### Initialize PostgreSQL Database 
```bash
sudo postgresql-setup initdb
```
### Start Postgres on boot
```bash
sudo systemctl start postgresql
```
```bash
sudo systemctl enable postgresql
```
### Check if postgres is working
```bash
sudo -u postgres psql -c "SELECT version();"
```

## Setting up Database and Roles

### Create new Database
```bash
sudo su - postgres -c "createdb demo_db"
```
### Create new Role
```bash
sudo su - postgres -c "createuser demo_user"
```
### Grant permission to new role
```bash
sudo -u postgres psql
```
```bash
psql# grant all privileges on database test_db to test_user;
```
### Add new user as a Linux User
```bash
sudo adduser demo_user
```
### Sign in with new user
```bash
sudo -u sammy psql
```

## Enable Remote Access to PostgreSQL server

### Change listening address and port
```bash
sudo nano /etc/postgresql/10/main/postgresql.conf
```

Update **listen_addresses** under **Connection Settings**
```bash
listen_addresses = '*'   
```

Restart the PostgreSQL to take effect
```bash
sudo systemctl restart postgresql
```

### Update **pg_hba.conf** to allow connections
```bash
# Allow access to all Databases
host    all             demo_user           0.0.0.0/0              md5

# For limit access only to a specific database
host    demo_db         demo_user           0.0.0.0/0              md5

# For limit access from only an specific IP
host    all             demo_user           192.168.11.111         trust