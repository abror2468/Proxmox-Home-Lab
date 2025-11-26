sudo apt update
sudo apt install mosquitto mosquitto-clients -y
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
sudo systemctl status mosquitto
Active: active (running)


to test it out run this command on ubuntu:
mosquitto_sub -h 192.168.1.229 -t soil/test

to test it out on windws machine requires: 
mosquitto_pub -h 192.168.1.229 -t soil/test -m "hello from windows"

this however requires Mosquitto to be installed on the windows 
