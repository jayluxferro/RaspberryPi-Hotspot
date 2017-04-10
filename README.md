# Hotspot Configuration of a Raspberry-Pi

## Install required packages
Run __install.sh__

## Edit Network configuration file
1. Run __sudo nano /etc/network/interfaces__
2. Clear the inital configuration for your wireless interface
3. Paste the contents of "__wlanConfig__"

## Edit Hostapd configuration
1. Run "__sudo nano /etc/hostapd/hostapd.conf__"
2. Paste the contents of hostapd.conf

## Add default configuration hostapd daemon file
1. Run "__sudo nano /etc/default/hostapd__"
2. Find the line __#DAEMON_CONF=""__
3. Replace it with  __DAEMON_CONF="/etc/hostapd/hostapd.conf"__

## Create dnsmasq dhcp configuration file
Run "sudo nano /etc/dnsmasq.conf"
Replace all its contents with the contents of "dnsmasq.conf"

## Enable ipv4 forwarding
Run "sudo nano /etc/sysctl.conf"
Remove "#" from the beginning of the line containing __net.ipv4.ip_foward=1__

## Creating nat routing rule using iptables
Run "iptables_ipv4.sh"
Save the iptables rule by running: sudo -c "iptables-save > /etc/iptables.ipv4.nat"
Run "sudo nano /etc/rc.local"
Type the following line just before the "exit 0" line
iptables-restore < /etc/iptables.ipv4.nat

## Starting services upon reboot
Run the following lines:
sudo update-rc.d -f hostapd enable
sudo update-rc.d -f dnsmasq enable
sudo reboot
