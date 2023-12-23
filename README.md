## Grafana Stack 

Build the grafana stack using Docker Compose.

### Prerequisites

- Docker
- Docker Compose
- smartmontools

### Usage

```bash
yum install smartmontools
```

```bash
docker-compose up -f docker-compose.yml -d
```

The alert system configuration is placed in the 'alert' directory, and the alert rules are placed in the 'prometheus rules' directory.

The alert rules use all configurations with the `.yml` extension.

### SMART

To periodically scan disk information and save it to a specific directory using SMART information, you need to create a bash or python script and schedule it using crontab. Here's a basic example of how you might do this:

Pseudocode:
1. Write a bash or python script that scans the disk information using SMART and saves it to a specific directory.
2. Schedule this script to run at regular intervals using crontab.

```bash
# Bash script (smartmon.sh)
#!/bin/bash
smartctl -A /dev/sda > /path/to/directory/xx.txt

# Crontab entry (runs the script every hour)
0 * * * * /path/to/script/xx.sh
```

### Alert Manager 

To test the alert system, you can push alerts proactively using the webhook method. 

Pseudocode:
- Configure the alert system to use a webhook for notifications.
- Trigger a test alert to verify that the alert is sent to the webhook.

You can refer to the alertmanager component in the arc repository for more information.

bash the following command to send a test alert to the webhook:

```bash
## using alert.sh
curl -XPOST -d"$alerts_message" http://127.0.0.1:9093/api/v1/alerts 
```

### Alertmanager API

refer to the following link for more information on the alertmanager API.

- (https://github.com/prometheus/alertmanager)

import Alertmanager_API.postman_collection.json to postman.

postman post request example(send to alertmanager)

```bash
http://ip:9093/api/v2/alerts
```