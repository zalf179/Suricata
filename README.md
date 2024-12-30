# Suricata
Install suricata on ubuntu and integrate it with wazuh

### **How to install on ubuntu server**

sudo apt-get update && sudo ap-get upgrade -y (Update and upgrade the repository)

sudo apt -y install libnetfilter-queue-dev libnetfilter-queue1 libnfnetlink-dev libnfnetlink0 jq (Install Prerequisites)

sudo add-apt-repository ppa:oisf/suricata-stable (Adding suricata repository)

sudo apt install suricata -y

sudo nano /etc/suricata/suricata.yaml (Edit suricata configuration)

![Screenshot 2024-12-30 103701](https://github.com/user-attachments/assets/22367e3b-e775-4413-b366-746d2d235487)

Specify your HOME_NET 

Hold CTRL + W, type af-packet, and hit enter

![Screenshot 2024-12-30 104321](https://github.com/user-attachments/assets/44510bbf-8825-4dec-b9dc-ecff7997ef8c)

Specify the Interface that you want to monitor

After done Hold CTRL + X, hit y and enter
