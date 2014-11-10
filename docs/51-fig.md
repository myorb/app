Docker Container with fig
-------------------------

> NOTE! This section is under development

Create project:

    composer create-project --stability=dev --prefer-dist phundament/app p4-docker
    cd p4-docker

### Option: fig

Copy fig config to project root:

    ./init --env=Dotenv
    cp ./environments/_docker/Dockerfile .
    cp ./environments/_docker/fig.yml .

Edit `./.env` to map the fig ENV vars to the Phundament application

    DATABASE_DSN=mysql:host={$DB_PORT_3306_TCP_ADDR};dbname={$DB_ENV_MYSQL_DATABASE}
    DATABASE_USER={$DB_ENV_MYSQL_USER}
    DATABASE_PASSWORD={$DB_ENV_MYSQL_PASSWORD}

> Note: If you are developing on OS X, make sure your host-vm is running (`boot2docker start`).

Start the application containers:

    fig up

To initialize your application run the following commands once:

    fig run backend composer install
    fig run backend ./yii migrate
    fig run backend ./yii app/setup

They will make the `vendor` folder available in your project directory on your host machine.
And sets up the database, along with an admin user.

You should now be able to access the container under `http://docker.local:10080` and `http://docker.local:10081`