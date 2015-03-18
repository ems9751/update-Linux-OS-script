# update-Linux-OS-script
# Update Fedora, CentOS and Ubuntu with text conformation



#------------------------#
# ram                    #
# update packages script #
#------------------------#

# 26 Jan 2015	- create program
# 26 Feb 2015	- fixed spelling of upgrade
#		          - added texting to cell
# 17 Mar 2015	- added code to check for OS Version		
# 18 Mar 2016	- fixed OS version check for Fedora, CentOS & Ubuntu 		

#++++++++++++++++++++++++ README +++++++++++++++++++++++#
#                                                       #
# First time using this script,                         #
# update variable "LOG" with your log path of choice,   #
# update variable "RAM" with your name and phone number #     
#                                                       #
# Set crontab to run every night, and wait for the text #
#+++++++++++++++++++++++++++++++++++++++++++++++++++++++#


#!/bin/bash


LOG=/var/log/updateOS.log
RAM='123456789'

tee='tee -a'

PLATFORM='unknown'
OS=`python -c "import platform;print(platform.linux_distribution()[0])"`
if [[ "$OS" == 'Fedora' ]]; then
	echo -e "Starting $OS update: $(date)\n\n"| $tee $LOG
	yum update -y 2>&1 | $tee $LOG 
	yum upgrade -y 2>&1 | $tee $LOG
	echo -e "Yo, the $OS update is done: $(date)\n\n"|$tee $LOG
	echo 
	curl http://textbelt.com/text -d "number=$RAM" -d "message=$OS has been updated sir" |$tee $LOG
elif [[ "$OS" == 'CentOS' ]]; then
        echo -e "Starting $OS update: $(date)\n\n"| $tee $LOG
        yum update -y 2>&1 | $tee $LOG
        yum upgrade -y 2>&1 | $tee $LOG
        echo -e "Yo, the $OS update is done: $(date)\n\n"|$tee $LOG
        echo
	curl http://textbelt.com/text -d "number=$RAM" -d "message=$OS has been updated sir" |$tee $LOG
elif [[ "$OS" == 'Ubuntu' ]]; then
	echo -e "Starting $OS update: $(date)\n\n"| $tee $LOG
	apt-get update -y 2>&1 | $tee $LOG
	apt-get upgrade -y 2>&1 | $tee $LOG
	apt-get autoclean  -y 2>&1 | $tee $LOG
	echo -e "Yo, the $OS update is done: $(date)\n\n"|$tee $LOG
	echo 
	curl http://textbelt.com/text -d "number=$RAM" -d "message=$OS has been updated sir" |$tee $LOG
elif [[ "$OS" == 'unknown' ]]; then
        echo -e "$OS Operating System detected: $(date)\n\n"| $tee $LOG
	curl http://textbelt.com/text -d "number=$RAM" -d "message=$OS Opearting System sir, please check it out." |$tee $LOG
fi
