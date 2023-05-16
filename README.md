# Network Scanning Web Application

# Description
NetScanWeb is a lightweight web application designed for network scanning and monitoring. It simplifies the process of setting up and configuring network scanning tasks using Nmap, Apache2, and PHP on a Debian-based operating system. The application allows users to conveniently view the network scan results in real-time through a user-friendly web interface. With NetScanWeb, network administrators can easily monitor network activity, identify active hosts, and track open ports within a specified IP range.

# Assumptions

- Using debian based OS (if using other OS use appropriate package manager)
- Using root user, use standard user for better security and change ownership permissions of web page (var/www/html)

# Install Software

## Install - Apache2

```bash
sudo apt install apache2 -y
```

## Install - PHP

```bash
sudo apt install php -y
```

## Install nmap

```bash
sudo apt install nmap -y
```

# Configure Ownership and Permissions

## Check permissions in directory below

```bash
ls -l /var/www/html
```

## Change Owner

```bash
sudo chown root /var/www/html
```

## Change Permissions

```bash
sudo chmod 777 /var/www/html
```

# Cron Job Configuration

## Edit cron config

```bash
sudo crontab -e
```

## Add Line to cron tab

Runs the command every 10 minues

```bash
*/10 * * * * nmap 192.168.0.0/24 -oN /var/www/html/nmap.html
```

## create network.php

```php
<?php

echo "Server Timestamp: ";
echo date("h:i:sa");

echo "<pre>";
include("nmap.html");
echo "</pre>";

?>
```