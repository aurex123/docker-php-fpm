docker php-fpm
==================

Imagen con PHP-FPM 5.6 expuesto en puerto 9000.
Tiene las siguientes extensiones instaladas:

    php5=5.6.* \
    php5-fpm \
    php5-cli \
    php5-common \
    php5-curl \
    php5-imagick \
    php5-intl \
    php5-json \
    php5-mcrypt \
    php5-memcache \
    php5-readline \
    php5-sqlite \
    php5-redis \
    php5-gd \
    php5-mysql

Uso
-----

Para correr esta imagen primero se tiene que generar según la versión a utilizar:

    docker build -t aurex/php-fpm 5.6

Donde `5.6` es el nombre de la carpeta.
Y para iniciar, ejecutar:

    docker run -d -p 9000:9000 --name phpfpm aurex/php-fpm

Extender configuraciones
-------------------------------

La carpeta `defaults` contiene los archivos de configuración que se instalan por defecto.
Dentro de la carpeta `etc` se encuentran las configuraciones a aplicar.

Para aplicar tus propias configuraciones, monta los archivos de configuración como volumenes:

    docker run -d -p 9000:9000 \
    -v www.conf:/etc/php5/fpm/pool.d/www.conf \
    -v php.ini:/etc/php5/fpm/conf.d/zz-php.ini \
    --name phpfpm aurex/php-fpm

Agregar configuraciones
-------------------------------

Para agregar tus propias configuraciones, crea un nuevo `Dockerfile` con el siguiente contenido:

    FROM aurex/php-fpm
    ...
    COPY config /etc/php5/RUTA/CONFIG.conf
    ...

Despues de eso, genera el nuevo `Dockerfile`:

    docker build -t username/my-image .

Y pruebalo:

    docker run -d -P username/my-image

That's it!
