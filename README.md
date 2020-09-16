# Prestashop Local Development Environment

## Docker configuration

```bash
# Run containers
docker-compose up -d

# Add permissions
sudo chown <local_user>:<local_user> -R prestashop/
rm -rf prestashop/install

# Optional permissions
chmod -R 775 prestashop/
chmod -R g+s prestashop/

chmod +w -R admin-dev/autoupgrade app/config app/logs app/Resources/translations cache config download img log mails modules themes translations upload var

# Rename admin folder
cd prestashop/
mv admin admin-dev

# Build CSS and Javascript

docker build -t ps_js-core-dev_img ./build/js-core-dev/<tag>
cd prestashop/themes
docker run -it -d --name ps_js-core-dev_cont -v `pwd`:/usr/src/app ps_js-core-dev_img /bin/bash
docker exec ps_js-core-dev_cont npm run build

docker build -t ps_theme-dev_img ./build/theme-dev/<tag>
cd prestashop/themes/<theme_folder>
docker run -it -d --name ps_theme-dev_cont -v `pwd`:/usr/src/app ps_theme-dev_img /bin/bash
docker exec -it ps_theme-dev_cont bash
npm run build
# or
npm run watch
```

## Debug VSCode Configuration

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "pathMappings": {
              "/var/www/html": "${workspaceRoot}/prestashop"
            },
            "port": 9000
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```
