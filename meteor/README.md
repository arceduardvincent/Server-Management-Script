#### Backup Reffrence for meteor
http://sheharyar.me/blog/regular-mongo-backups-using-cron/

#### Connecting a MongoDB to another Machine
To connect other SmartMachines over a private network to your MongoDB appliance:

SSH into your MongoDB appliance.
Open `/opt/local/etc/mongodb.conf` for edit. 

Locate the bind_ip property.
 Set the value of the bind_ip property to the private IP of your MongoDB appliance. You can find the private IP of your appliance in your my.joyentcloud.com portal or by using `ifconfig -a`.

For more information on private IPs, see here.
Save the file and close it. You will need to restart the MongoDB server to set the changes.
Run command to restart the MongoDB server.
