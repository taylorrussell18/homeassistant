Home Assistant with Cloudflare Add-On Tutorial using ProxMox
Prerequisites
- Proxmox is already installed on your home server.
- Access to a domain name (via Cloudflare or DuckDNS).
Step 1: Download and Prepare the Home Assistant Image
Open your Proxmox shell and run the following command to download the image:
 wget https://github.com/home-assistant/operating-system/releases/download/15.2/haos_ova-15.2.qcow2.xz
 Then extract the downloaded image using:
 unxz haos_ova-15.2.qcow2.xz
Step 2: Create the Virtual Machine
1. Create a new virtual machine in Proxmox with the following minimum specifications:
- CPU: 2 cores
- RAM: 4096MB (4GB)
- Disk: 6GB or more
 2. Import the disk image to your VM (replace '100' with your VM ID):
 qm importdisk 100 haos_ova-15.2.qcow2 local-lvm
Step 3: Start the Virtual Machine and Access Home Assistant
1. Start the virtual machine from Proxmox.
2. Wait a few minutes for Home Assistant to complete its initial boot.
3. Open a web browser and navigate to:
 http://homeassistant.local:8123
Or the IP Address Given 
 4. Follow the prompts to create a username and password.
Step 4: Set Up Cloudflare and Domain
1. Visit https://www.cloudflare.com/ and create an account.
2. If you already own a domain, connect it to Cloudflare using the DNS settings.
- If the domain is registered through another provider (ex: GoDaddy), follow Cloudflare’s instructions to update your nameservers.
3. Alternatively, you can use a free dynamic DNS provider such as https://www.duckdns.org/.
Step 5: Create a Cloudflare Tunnel
1. In the Cloudflare dashboard, go to the Zero Trust section.
2. Click on 'Tunnels', then 'Create Tunnel'.
3. Choose the Cloudflared option, name the tunnel appropriately, and click 'Next'.
4. Copy the token from the generated command. This will be used in Home Assistant later so make sure to save it somewhere safe.
Step 6: Define the Tunnel Route
1. Specify your public domain route (e.g., http://homeassistant.taylorrussell.net).
2. Set the internal IP address and port of your Home Assistant instance (e.g., 192.168.4.92:8123).
Step 7: Install the Cloudflared Add-On in Home Assistant
1. In Home Assistant, go to Settings > Add-ons > Add-on Store in the bottom right.
2. Search for and install the 'Cloudflared' add-on.
3. Open the add-on and go to the Configuration tab at the top.
4. Under 'External Home Assistant Hostname', enter the domain you configured in Cloudflare.
5. Save the configuration and restart the add-on.
Verify you can access webpage
Open a web browser and access your Home Assistant instance using the domain you just configured on cloudflare. If all steps were followed correctly, you should be able access your Home Assistant VM. This whole process can also be done without Proxmox but my server is currently already on Proxmox. You can set it up with any virtual machine application. 

