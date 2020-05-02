# qnapstack
QNAP NVR Automation Stack

########################################### SETUP BEFORE RUNNING STACK#################################################################
# 
#####################!!!!!!!!WARNING MAY BREAK APPS YOU INSTALLED THAT UTILIZE THE QNAP WEBSERVER!!!!!!!!!!############################
#
#       This setup will allow the stack to be deleted and composed while maintaineing all configs and data in your share folders
#
#                                   Setup Assumes Use of Cloudflare for DNS Name                        
# 
# 1. Create the following Share Drive via Control Panel-> Shared Folders - AppData    and   Multimedia
#    - Assign Read and Write Permissions to folder
#       - Via filestation in the AppData folder create one directory for each dockerr to store configs
#           - Directories are Heimdall, Hydra, NZBGet, Ombi, Plex, Radarr, Sonarr, Tautulli and Traefik Note: these are case sensitive
#               - Open Traefik folder and create a folder called acme and open said folder
#               - Use notepad on desktop to create an empty file named acme.json file ensuring that the standard .txt is deleted
#               - Create another empty empty file name traefik.log
#               - Upload acme.json into acme folder and right click and select Properties -> Permissions
#               - Upload traefik.log into root of Traefik folder (no permission change needed
#               - Now deselect all permissions except Owner Read and Write
#        
# 2. Create the following Share Drive via Control Panel-> Shared Folders - Multimedia
#       - Via filestation in the Multimedia folder create directories to store content from NZBGet, Radarr and Sonarr
#       - Directories are Movies, Television and Downloads: these are case sensitive
#
# 3. Install Container Station
#
# 4. Create user other than admin via Control Panel -> Users 
#       - Can be any user name 
#       - Assign R/W Priviledges to these share folders Container Station, AppData and Mulitmedia
#
# 5. Change QNAP default ports from default via Control Panel-> Sysytem -> General Settings -> System Administrator 
#       - Change the System Port and also Enable HTTPS and change this Port too (I used 8880 and 4443) 
# 
# 6. Enable and Change Ports for Webserver via Control Panel-> General Settigs -> Applications -> WebServer
#       - Enable Webserver if not already
#       - Change Port number and also Enable HTTPS and change this Port too (I used 9880 and 9443)
#  
# 7. Enable SSH via Control Panel Telnet/SSH port should be 22      
# 
# 8. Create docker network for stack to utilze via ssh using putty or similiar tool on desktop
#       - Login in as administrator and command in putty is: docker network create web
#       - Obtain and note PUID and PGID of created user while here   
#          - Command is: id (name of created user)
#
# 9. On Router port forward 80 to 80 and 443 to 443 to QNAP IP Address
#
# 10. Go to Cloudflare under DNS and Set AName for Your Domain Name and a CNAME of ombi pointed to your ANAME
#       - Go to SSL/TLS and select full
#
# 11. Proceed below and replace all mared values with your credentials
#  
# 12. Open Container Station
#       - Select Create and on the upper right select Create Application 
#       - Recommend Notepade++ for this Step
#       - Copy entire contents starting from traefik and below and paste below services ensuring all spacing remains the same
