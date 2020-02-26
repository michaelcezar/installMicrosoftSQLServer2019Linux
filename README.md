# Install Microsoft SQL Server on Linux

.----------------------------------------- RHEL 7 / AMAZON LINUX 2 AMI / CENTOS ------------------------------------------.

#Download mssql

sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo


#Download mssql command-line tools and unixODBC developer package

sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo


#Install mssql

sudo yum install -y mssql-server


#To config mssql and set SA user

sudo /opt/mssql/bin/mssql-conf setup


#Install mssql command-line tolls and unixODBC developer package

sudo yum -y install mssql-tools unixODBC-devel


#Start mssql server

sudo systemctl start mssql-server


#Enable mssql server

sudo systemctl enable mssql-server


#Include mssql tools on path

echo 'export PATH=$PATH:/opt/mssql/bin:/opt/mssql-tools/bin' | sudo tee /etc/profile.d/mssql.sh


#Source the file to start using mssql

source /etc/profile.d/mssql.sh

.-----------------------------------------------------------------------------------------------------------------------.

.------------------------------------------------------ UBUNTU -------------------------------------------------------.

#Import mssql repository

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -


#Register the Microsoft SQL Server Ubuntu repository

sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"


#Import mssql command-line tools and unixODBC developer package repository

curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -


#Register the Microsoft Ubuntu repository

curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list


#update sources

sudo apt-get update


#Install mssql

sudo apt-get install -y mssql-server


#To config mssql and set SA user

sudo /opt/mssql/bin/mssql-conf setup


#Install mssql command-line tolls and unixODBC developer package

sudo apt-get install mssql-tools unixodbc-dev


#Start mssql server

sudo systemctl start mssql-server


#Enable mssql server

sudo systemctl enable mssql-server


#Include mssql tools on path

echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc


#Source the file to start using mssql

source ~/.bashrc

.---------------------------------------------------------------------------------------------------------------------.

.------------------------------------------------------- TEST --------------------------------------------------------.

#To Connect

sqlcmd -S localhost -U SA

or

sqlcmd -S 127.0.0.1\\SQLEXPRESS,1433 -U SA

#Create login for server

CREATE LOGIN test WITH PASSWORD = '#T3st123@';
GO

#Kill user session

select session_id from sys.dm_exec_sessions where login_name = 'test'

kill id

#Drop user

DROP USER test

.---------------------------------------------------------------------------------------------------------------------.
