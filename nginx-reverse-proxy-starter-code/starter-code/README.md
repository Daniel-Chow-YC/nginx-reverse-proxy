# nginx reverse proxy

## Nginx
- Nginx is a web server which can also be used as a reverse proxy
- The Nginx webserver acts as an intermediary for requests from clients so that the app cannot be directly accessed by users
  - Nginx acts as a middle man. User request goes to nginx, nginx sends request to app, app sends response to nginx, nginx sends response to user.
  - User request --> nginx --> app --> nginx --> response to user
- When successfully set up users should be able to access the app from development.local and will not need to include the port number

# Making the reverse proxy
- Change the file /etc/nginx/sites-enabled/default in the app VM so that it includes:
````
location / {
         proxy_pass http://localhost:3000;
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ =404;
}

location ~ ^/(images|javascript|js|css|flash|media|static)/  {
root    /home/ubuntu/app/public;
expires 30d;
}
````
- The first part provides the reverse proxy for the webpage
- The next part provides the reverse proxy for the image (the sparta global logo)

- In this project this process has been automated so that the reverse proxy is automatically set up when the vm is spun up
- This is done by:
  - creating a new_default file with the correct configuration to set up the reverse proxy in the environment/app folder on the local machine
  - then syncing this folder with a folder in the app vm:
  `` app.vm.synced_folder "environment/app", "/home/ubuntu/environment" ``
  - in the app provision script using a symbolic link to link the /home/ubuntu/environment folder to a folder in the appropriate location
  ````
  sudo rm /etc/nginx/sites-enabled/default
  sudo ln -s /home/ubuntu/environment/new_default /etc/nginx/sites-enabled/default

  sudo systemctl restart nginx
  ````
  - Be sure to include a command to restart Nginx so the changes take effect
