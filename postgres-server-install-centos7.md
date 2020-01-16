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