First download InfluxDB for it to get its data source from:
sudo apt update
curl -s https://repos.influxdata.com/influxdata-archive_compat.key | gpg --dearmor | sudo tee /usr/share/keyrings/influxdata-archive-keyring.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/influxdata-archive-keyring.gpg] https://repos.influxdata.com/debian stable main" | sudo tee /etc/apt/sources.list.d/influxdata.list
sudo apt update
sudo apt install influxdb2 influxdb2-cli -y
sudo systemctl status influxdb
sudo systemctl start influxdb
sudo systemctl enable influxdb
once done ip address is: http://192.168.1.xxx:8086



Now install Grafana:

sudo apt update
sudo apt install -y curl gnupg apt-transport-https
curl -fsSL https://packages.grafana.com/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt update
sudo apt install grafana -y
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server



once done ip address of grafana:http://yourUbuntuVM:3000
