androidto-alertspusher
=====

androidto-alertspusher is a Django project for pushing simple alert messages to Android Devices over the C2DM framework. It requires the recipient Android devices to have the androidto-alerts client app installed found [here](http://github.com/bc0nt13/androidto-alerts). The client app will register the device with the server using this project and then listen for alerts using C2DM.

## Setup
Here are the default django settings used in the project:

    DATABASE_ENGINE = 'mysql'
    DATABASE_NAME = 'alertspusher'
    DATABASE_USER = 'root'

You can overwrite these with your preferred settings in the settings.py file. If using mysql, you will need to create a new database called 'alertspusher' or whatever database name you choose for the DATABASE_NAME setting.

## C2DM Configs
Add the following line to your settings.py file:

    C2DM_AUTH_TOKEN = 'YOUR_PUSH_ACCOUNT_AUTH_TOKEN'

Where YOUR_PUSH_ACCOUNT_AUTH_TOKEN is the ClientLogin token for your push account.

You can retrieve the ClientLogin token for your push account via cURL:

    curl -X POST https://www.google.com/accounts/ClientLogin -d Email=ACCOUNT -d Passwd=PASSWORD -d accountType=HOSTED_OR_GOOGLE -d service=ac2dm

Replace ACCOUNT and PASSWORD with the relevant information. Copy everything in the response following Auth= to get your AUTH_TOKEN value.

## Usage
To setup the database and sync the models:

    python manage.py syncdb

To run the django development server:

    python manage.py runserver

By default the server will run at http://127.0.0.1:8000.
To push an alert go to the following URL:

    http://127.0.0.1:8000/alertspusher/alert

The app stores all the registered devices in a model. You can manage this model using the django admin interface at:

    http://127.0.0.1:8000/admin
