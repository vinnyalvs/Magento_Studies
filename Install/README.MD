# Instalando Magento2
        https://devdocs.magento.com/guides/v2.4/install-gde/composer.html
        
        composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .

        composer install

        bin/magento setup:install --no-interaction \
        --admin-firstname=Webjump \
        --admin-lastname=Admin \
        --admin-email=admin@webjump.com.br \
        --admin-user=admin \
        --admin-password=admin123 \
        --use-secure=1 \
        --base-url-secure=https://m2clean.local \
        --use-secure-admin=1 \
        --backend-frontname=admin \
        --db-host=mysql_m2clean \
        --db-name=magento2 \
        --db-user=magento2 \
        --db-password=magento2 \
        --language=pt_BR \
        --page-cache=redis \
        --page-cache-redis-server=redis_m2clean \
        --page-cache-redis-db=0 \
        --cache-backend=redis \
        --cache-backend-redis-server=redis_m2clean \
        --cache-backend-redis-db=1 \
        --session-save=redis \
        --session-save-redis-host=redis \
        --session-save-redis-db=2 \
        --elasticsearch-host=elasticsearch_m2clean \
        --amqp-host=rabbitmq_m2clean \
        --amqp-port=5672 \
        --amqp-user=guest \
        --amqp-password=guest \
        --cleanup-database

        bin/magento deploy:mode:set developer


        find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
        find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
        chown -R :www-data .
        chmod u+x bin/magento

