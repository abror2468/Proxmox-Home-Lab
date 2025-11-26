sudo apt update
sudo apt install -y build-essential git curl

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
sudo systemctl enable nodered.service
sudo systemctl start nodered.service
sudo systemctl status nodered.service

