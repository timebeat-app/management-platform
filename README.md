Timebeat Management Platform Installer (recommended method)
Last updated 10 days ago
Timebeat operates best when utilising the elastic database and Grafana front end.

The simple commands below will set you up in minutes with a complete out-of-the-box deployment of all the Timebeat dependencies.

 

During the installation process, you will need to input some IP address information.

For this just insert the host IP address followed by the same again with a hyphen separating the two (example below).

10.101.101.101-10.101.101.101

 

$ sudo dnf install -y snapd

$ sudo ln -s /var/lib/snapd/snap /snap

$ sudo snap install microk8s --classic

$ sudo /snap/bin/microk8s enable dns
$ sudo /snap/bin/microk8s enable hostpath-storage
$ sudo /snap/bin/microk8s enable helm3
$ sudo /snap/bin/microk8s enable metallb

During this step you will be asked to insert an IP address.
This will be in the format of "IPaddress-SameIPaddress" see above example.

$ sudo /snap/bin/microk8s helm3 repo add timebeat https://license.timebeat.app/chart/
$ sudo /snap/bin/microk8s helm3 install timebeat timebeat/timebeat-backend-chart
 

Once complete elastic and grafana will be available.
You can report to elastic using the IP address the installer requests and port 9200.

Grafana will also be on the same IP address using port 80.

Login details will be

username: admin

password: admin

(you will be prompted to change the password upon first login.)

 

To check whether the system is deploying or deployed the below command will provide the information:

$ sudo /snap/bin/microk8s kubectl get all --all-namespaces
The output should look similar to the below:

Screenshot_2022-07-21_at_09.28.32.png

 

This system creates a microk8s system so all the usual kubernetes tricks are possible

To update the system which we recommend from time to time as we release new updates run the following commands:

$ sudo /snap/bin/microk8s helm3 repo update

$ sudo /snap/bin/microk8s helm3 upgrade timebeat timebeat/timebeat-backend-chart
 

To stop the deployed services just run the below command:

$ sudo /snap/bin/microk8s stop
 

To uninstall and remove all timebeat systems.

sudo /snap/bin/microk8s helm3 uninstall timebeat
To remove all of the system setups, use the following command:

sudo /snap/bin/microk8s reset

