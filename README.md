# Apache Tomcat 9 Installation and Configuration Guide

## Prerequisites
Ensure you have root or sudo privileges on your Linux system.

## Installation Steps

1. Navigate to the `/opt` directory:
   ```sh
   cd /opt
   ```

2. Download Apache Tomcat 9.0.99:
   ```sh
   wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.99/bin/apache-tomcat-9.0.99.tar.gz
   ```

3. Extract the downloaded archive:
   ```sh
   tar -xvf apache-tomcat-9.0.99.tar.gz
   ```

4. Install Java if not already installed:
   ```sh
   yum install java -y
   ```

5. Navigate to the extracted Tomcat directory:
   ```sh
   cd apache-tomcat-9.0.99
   ```

6. Start Tomcat:
   ```sh
   cd bin
   ./startup.sh
   ```

## Configuring Tomcat Manager Access

1. Update IP Authorization:
   ```sh
   nano /opt/apache-tomcat-9.0.99/webapps/manager/META-INF/context.xml
   ```
   Replace the IP restriction with `.*` to allow all IPs:
   ```xml
   <Context antiResourceLocking="false" privileged="true">
       <Valve className="org.apache.catalina.valves.RemoteAddrValve"
           allow=".*" />
   </Context>
   ```
   Save and exit the file.

2. Configure Tomcat Users:
   ```sh
   nano /opt/apache-tomcat-9.0.99/conf/tomcat-users.xml
   ```
   Replace the file contents with:
   ```xml
   <?xml version='1.0' encoding='utf-8'?>
   <tomcat-users>
       <role rolename="manager-gui"/>
       <user username="tomcat" password="Tomcat" roles="manager-gui, manager-script, manager-status"/>
   </tomcat-users>
   ```
   Save and exit the file.

3. Restart Tomcat to apply changes:
   ```sh
   cd /opt/apache-tomcat-9.0.99/bin
   ./shutdown.sh
   ./startup.sh
   ```

## Accessing Tomcat Manager
Once Tomcat is running, access the Manager web interface by visiting:
```
http://<your-server-ip>:8080/manager/html
```
Log in with the username **tomcat** and password **Tomcat**.

## Notes
- Ensure that port **8080** is open in your firewall for remote access.
- For security reasons, avoid using weak credentials in a production environment.



