# Prestashop Local Development Environment

```bash
# Add permissions
sudo chown albertodsosa:albertodsosa -R prestashop/
rm -rf prestashop/install

# optional
chmod -R 775 prestashop/
chmod -R g+s prestashop/

# Rename admin folder
cd prestashop/
mv admin admin-dev
```

```bash
chmod +w -R admin-dev/autoupgrade app/config app/logs app/Resources/translations cache config download img log mails modules themes translations upload var

sudo chgrp -R www-data /prestashop/
sudo chmod -R g+w /prestashop/
sudo find /prestashop/ -type d -exec chmod 2775 {} \;
sudo find /prestashop/ -type f -exec chmod ug+rw {} \;

sudo usermod -a -G www-data albertodsosa
sudo usermod -a -G www-data otrousuario
```

## Build CSS and Javascript

```yml
js-core-dev:
    build: ./build/js-core-dev
    volumes:
      - ./prestashop/themes:/usr/src/app
    depends_on:
      - prestashop
storefront-dev:
    build: ./build/storefront-dev
    volumes:
      - ./prestashop/themes/storefront-dev:/usr/src/app
    depends_on:
      - js-core-dev
```

```bash
docker build -t js-core-dev_test ./build/js-core-dev
cd prestashop/themes
docker run -it -d --name prestashop_js-core-dev_test -v `pwd`:/usr/src/app js-core-dev_test /bin/bash
docker exec prestashop_js-core-dev_test npm run build

docker build -t storefront-dev_test ./build/storefront-dev
cd prestashop/themes/storefront-dev
docker run -it -d --name prestashop_storefront-dev_test -v `pwd`:/usr/src/app storefront-dev_test /bin/bash
docker exec prestashop_storefront-dev_test npm run watch
```
