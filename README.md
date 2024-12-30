# Suricata
Install suricata on ubuntu and integrate it with wazuh

### **How to install Suricata on ubuntu server** :inbox_tray:

update and upgrade repository
```bash
sudo apt-get update && sudo ap-get upgrade -y
```

install prereq
```bash
sudo apt -y install libnetfilter-queue-dev libnetfilter-queue1 libnfnetlink-dev libnfnetlink0 jq 
```

add suricata repo
```bash
sudo add-apt-repository ppa:oisf/suricata-stable 
```

install suricata
```bash
sudo apt install suricata -y 
```

edit suricata configuration
```bash
sudo nano /etc/suricata/suricata.yaml 
```


![Screenshot 2024-12-30 103701](https://github.com/user-attachments/assets/22367e3b-e775-4413-b366-746d2d235487)

Specify your HOME_NET 

Hold CTRL + W, type af-packet, and hit enter

![Screenshot 2024-12-30 104321](https://github.com/user-attachments/assets/44510bbf-8825-4dec-b9dc-ecff7997ef8c)

Specify the Interface that you want to monitor

After done with configuration, Hold CTRL + X, hit y and enter

view available rules
```bash
sudo suricata-update list-sources 
```

NOTE: Not every rules is free, if you see License:Commercial , its paid

![Screenshot 2024-12-30 111437](https://github.com/user-attachments/assets/3aad99c2-621c-4535-8858-ee61e4116cc8)


Install suricata rules,replace Name: with rules name
```bash
sudo suricata-update enable-source Name:
```
test suricata
```bash
sudo suricata -T -c  /etc/suricata/suricata.yaml -v 
```

![Screenshot 2024-12-30 112311](https://github.com/user-attachments/assets/6b8e0a32-e1b0-4d2d-9934-ba8c8c63bd3b)

if you see this message, it means suricata is running properly without any problems.

enable suricata service
```bash
sudo systemctl enable suricata.service 
```

start suricata service
```bash
sudo systemctl start suricata.service 
```

check status suricata service
```bash
sudo systemctl status suricata.service 
```
![Screenshot 2024-12-30 113830](https://github.com/user-attachments/assets/898e91b5-d1cf-4b9f-b5ea-898f6c21f116)

### **Integrate with Wazuh** :computer:	

Add the following configuration to the /var/ossec/etc/ossec.conf file of the Wazuh agent. This allows the Wazuh agent to read the Suricata logs file:

```xml
<ossec_config>
  <localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>
</ossec_config>
```

Restart the Wazuh agent to apply the changes:

```bash
sudo systemctl restart wazuh-agent
```

