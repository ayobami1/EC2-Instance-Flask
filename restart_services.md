# Restart Services Script

This script restarts Nginx, Supervisor, and the helloworld service, reloads the systemd daemon, and enables the helloworld service to start on boot.

```bash
#!/bin/bash

# Restart Nginx
sudo systemctl restart nginx

# Restart Supervisor
sudo systemctl restart supervisor

# Reload helloworld service
sudo systemctl daemon-reload

# Restart helloworld service
sudo systemctl restart helloworld

# Enable helloworld service to start on boot
sudo systemctl enable helloworld


# create the `restart_services.sh` script using the nano text editor:
`nano restart_services.sh`

# Then paste the following script into the nano editor

#!/bin/bash

# Restart Nginx
sudo systemctl restart nginx

# Restart Supervisor
sudo systemctl restart supervisor

# Reload helloworld service
sudo systemctl daemon-reload

# Restart helloworld service
sudo systemctl restart helloworld

# Enable helloworld service to start on boot
sudo systemctl enable helloworld
