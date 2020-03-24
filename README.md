# aws-godaddy-domain-to-lightsail-instance
Documentation for changing GoDaddy domain nameservers to point to AWS Lightsail instance

GoDaddy
- Buy domain name
- Once domain is purchased, click on your profile name (upper right) and select "My Products"
- Scroll down to your Domains and click "DNS"
- Click "Change" on the Nameservers section (keep this tab open, you'll find what to change them to next)

Amazon AWS Lightsail
- Click "Networking" tab (from Home -- click Amazion Lightsail logo in top left to go "Home")
- Click "Create DNS Zone"
- Enter your newly purchased Domain name
- Go back to Home -> Networking tab
- Click "Create static IP"
- Attach your static IP address to your Lightsail instance
- Under "Networking", select your newly created DNS zone (click Manage in the right three-dot menu)
- Create A record, and CNAME records (replacing "yoursite" with uhh, your site):
  + A: @.yoursite.com points to the static IP that you just created
  + CNAME: www.yoursite.com points to yoursite.com
- At the bottom of this DNS records page, you'll see your Nameservers. Copy and paste these into the GoDaddy Nameservers section.

If you've done the above, in a few hours, your static IP will resolve to your new domain name

AWS Lightsail - Get your app ready
- ssh into your instance using the AWS terminal tool
- create some ssh keys (ssh-keygen)
- copy these to your github SSH/GPG keys 
- install node app environment
  + git clone git@github.com:ericposas/ubuntu-server-setup-script.git
  + cd ubuntu-server-setup-script
  + ./ubuntu-install-env
  + (follow prompts)
- install certbot (get ssl certs)
  + git clone git@github.com:ericposas/install-certbot.git
  + cd install-certbot
  + ./install-certbot
  + (follow prompts)
  + comment out previous server{} block in /etc/nginx/sites-available/default
  + restart nginx!
  
Enable port 443 for SSL/HTTPS:
- Home -> [YOUR_INSTANCE] -> Networking
- Under "Firewall" add a rule to allow for HTTPS (port 443)

If you've done these steps you should be able to see your site using SSL encryption and HTTPS!
