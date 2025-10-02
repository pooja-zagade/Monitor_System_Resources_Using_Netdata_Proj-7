# System Monitoring with Netdata

 Objective:

 --
Set up Netdata** on an Ubuntu server using Docker to visualize and monitor system and application performance in real-time.

---

##  Tools & Technologies
- **Ubuntu** (server/EC2 instance)
- **Docker**
- **Netdata** (lightweight monitoring tool)
- **stress** (to generate system load for testing)

---

## Setup Steps

### 1. Install Docker
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io

#Access Netdata Dashboard
http://<server-ip>:19999

------------Generate System Load with stress

##Install stress:
sudo apt install stress -y


##Run CPU stress test (for 2 minutes):
stress --cpu $(nproc) --timeout 120

##Memory stress:
stress --vm 2 --vm-bytes 256M --timeout 60

##Alerts & Logs----
##Logs available inside container:

docker exec -it netdata cat /var/log/netdata/error.log
docker exec -it netdata cat /var/log/netdata/access.log
