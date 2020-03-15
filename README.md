# DNSCONFIG
Basic Dns Configuration

# first check nslookup in your system by following cmd - which will list all the packages in all of the configured repos that contain nslookup 
yum provides nslookup

# now Install the bind-utils package 
yum install bind-utils -y

# This resolver configuration file used to configure a DNS server.Primary file to configure your server to translate names to routable IPs.
cat /etc/resolv.conf

# This cmd will search the domains specified in the /etc/resolv.conf file, As it was a non-qualified query,As no domain is specified.
nslookup www

# This is a fully-qualified domain name and will search the dns servers specified in the /etc/resolv.conf file and then follow the recommendations from the queried servers all the way to the root servers.
nslookup www.google.com

# This is the configuration file that contains the list of root servers. you will not edit this file.The file is configured with updates from the package.
cat /var/named/named.ca

# configuring a caching name server- vim /etc/named.conf
# //
#   listen-on port 53{127.0.0.1;};
#   listen-on-v6 port 53{::1;};           This both lines are for listening incoming requests - lines 1 and 2 in file
#   directory  "/var/named";
#   dump-file  "/var/named/data/cache_dump.db"; Directory for config files - lines 3 and 4 in file
#   allow-query  {localhost;};            Whom to answer queries from - line 9 in file
#   recursion yes;                  If you are building an AUTHORITIVE DNS server, do not enaable recursion - on line 20 in file
#   pid-file "/run/named/named-pid";      file containing the BIND PID - on line 26 in file
# //

# Named and RNDC keys 
# RNDC AUTO Key Generation
  systemctl start named
# start the named service.This will automatically create the /etc/rndc.key file and attach to the configuration.
  systemctl enable named
# Enable the named service so it is persistent upon reboot. A symbolic link to the service will be copied to the startup directory.
  cat /etc/rndc.key
# verify that the key was created and there is hashed MD5 data in the key file.

