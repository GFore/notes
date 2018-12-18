# notes

<details>
  <summary><h2>Deploying a static site to a new AWS EC2 instance</h2></summary>
  
  - ssh into the ec2 instance

  - update the system: `sudo apt update && sudo apt upgrade -y`

  - reboot: `sudo reboot`

  - (wait a couple minutes or go get coffee)

  - ssh into the ec2 instance

  - install nginx: `sudo apt install nginx`

  - if this is the first time the instance has been used (that is, has never talked to github before), generate keys: `ssh-keygen -t rsa -b 4096 -C "me@me.com"`

  - (preferably, with no passphrase)

  - (otherwise, take all the defaults)

  - output the public key to the terminal: `cat ~/.ssh/id_rsa.pub`

  - select and copy what got printed to the terminal

  - log into github, click menu in upper right corner, click "settings"

  - on settings page, click "ssh and gpg keys"

  - click green button in upper right labeled "new ssh key"

  - give it a title, paste in the public key, click "add ssh key" button

  - then, go to the github project and grab the clone URL for the project you want to deploy (edited)

  - back in the terminal (where you're logged into the ec2 instance): `git clone <clone url>`

  - `cd` into the directory that got created when you cloned

  - type `pwd` and copy this full path

  - and now...edit the nginx config: `sudo nano /etc/nginx/sites-available/default`

  - find the part that starts with `server {`

  - find the line that starts with `root` and ends with `;`

  - delete the path (which defaults to something like `/var/www/html`)

  - paste in the path to the cloned static site (probably something like `/home/ubuntu/LeftCheekRightCheek`)

  - save the file: `ctrl-o`

  - exit nano :`ctrl-x`

  - check that the config has no typos: `sudo nginx -t`

  - if successful, it should print a message with something like `syntax ok`

  - then, restart nginx: `sudo systemctl nginx restart`

  - (take a deep breath)

  - one more thing: in the column to the left of where the public DNS is listed, there's an item labeled "security - groups"

  - click the one labeled "launch-wizard..."

  - make that panel taller by dragging the three dots in the middle and drag up

  - click "add rule"

  - choose "HTTP" from the dropdown menu (which by default is labeled "custom rule")

  - for good measure, click "add rule" again and choose "HTTPS"

  - then, in a browser, go to the public DNS for the aws instance (which you can find in the aws console, under ec2, - under the "running instances", by clicking on the single running instance)

  - yeah! and then, go to the browser and try to pull up the site
</details>
