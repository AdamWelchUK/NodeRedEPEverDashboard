# Node Red EPEver Dashboard
A node red based dashboard for most EPEver/EPSolar solar charge controllers.

This dashboard has been tested with EPSolar Landstar PWM, EPEver Tracer A, Tracer AN and TriRon solar charge controllers.  
It reads live and historical stats and displays them in graphs using the standard Node Red UI.
It also allows you to change a number of the charging parameters which are accessible when you select 'User' battery type.

Full instructions for installing raspbian, node red and the flows is below.

# Node Red install instructions

1. Download the latest Raspbian from here... https://www.raspberrypi.org/downloads/raspbian/  I choose to use the lite version.
2. Copy the image to an SD card. I used Etcher available from...  https://www.balena.io/etcher/
3. Once completed, create a file on the boot partition of your SD card called 'ssh'.  It should just be called ssh and not have an extension.
4. Pop the SD card in your raspberry pi and give it some power and network.
5. Find the IP given to the pi either by plugging in a monitor, or by checking your dhcp server settings on your router.
6. SSH into your pi.  I use putty on windows, available from here... https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
7. Log in to your pi.  The default username is 'pi' and the default password is 'raspberry'.
8. Type and run 
> sudo raspi-config
9. Change the password, expand the file system (in advanced menu) and allow the pi to reboot.
10. Log back in via SSH and run 
> sudo apt-get update && sudo apt-get upgrade
11. At this point you have three options, and I recommend the second - using the official script to install the latest version of node red and npm (the package manager)

1st method - run
> sudo apt-get install nodered

2nd method - run
> bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

3rd method - use Peter Scargills Super Script https://tech.scargill.net/the-script/ (it can be used to install node-red against a load of other handy packages, but is beyond the scope of this guide)

12. Once either version is installed you can install it as a service...
> sudo systemctl enable nodered.service 
13. Now you can start node red by running 
> node-red-start
14. Open the user interface in your browser by visiting http://Your.IP.Add.ress:1880
15. To use all the elements of the flow you will need to install the following packages.  It is possible to do this via the node red user interface, so click on the burger in the top right and select palette manager.
Search for, and install...    
- node-red-dashboard
- node-red-contrib-modbus
- node-red-contrib-influxdb
- node-red-contrib-moment
16. Jump back to the command line and restart node red, to ensure the nodes are installed.  Because node red is installed as a service, I restart the pi.
> sudo reboot now
17. Back on the dashboard click the burger icon in the top right.
18. Click on Import.
19. Paste in the latest code from here:  https://github.com/AdamWelchUK/NodeRedEPEverDashboard/blob/master/EPEverDashboardv0.1.json
The two flows will have been imported and you can now set about configuring them.
You will need to configure the Modbus Server by double clicking on one of the red modbus nodes.
If you'd like to log the data to a influxDB or to a csv files these nodes can be enabled and configured by double clicking them.
