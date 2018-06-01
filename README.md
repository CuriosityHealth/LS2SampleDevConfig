# LS2 Sample Development Config

Sample configuration suitable for local mHealth app development using [Lightweight Study Server](https://github.com/CuriosityHealth/LS2) as a backend.

## Prerequisites

## Configuration

## Running

## Bootstrapping the server

Before you can use the server, you will need to do some initial configuration. If you're familiar with Django, this will be familiar.

While the containers are running, open a terminal on the ls2_web container.

```
docker exec -it ls2_web bash
```

Now that we're inside the LS2 container, we first need to setup the database tables by running the initial migrations. Note that we need to preface the typical python manage.py command by our local startup script.

```
./local-secrets-entrypoint.sh python manage.py makemigrations
./local-secrets-entrypoint.sh python manage.py migrate
```

Next, we will create a superuser account which will allow us to sign into the admin console.

```
./local-secrets-entrypoint.sh python manage.py createsuperuser
```

Just follow the instructions on the screen. After you've created the superuser account, we'll finally need to collect the static files.

```
./local-secrets-entrypoint.sh python manage.py collectstatic
```

You can exit the session by typing

```
exit
```

## Configuration via the Admin console

Browse to the admin console (if you are using the default settings, click [here](http://localhost:8000/admin) )

Enter the credentials for the superuser you created earlier.

### Create a study

From the main page of the admin console, click on *Studies* underneath the *Study\_Management* heading.

From there, click *ADD STUDY*.

On the Add Study page, enter a study *Name* and *Description* and select *SAVE*

Go back to the main page of the admin console.

### Create a researcher

From the main page of the admin console, click on *Users* underneath the *AUTHENTICATION AND AUTHORIZATION* heading.

From there, click *ADD USER*.

Enter a *username* and *password* for the new user and select *SAVE*. NOTE: You will need to change the researcher password the first time you log in.

You'll be taken to a screen that will let you edit additional information about the user. You can skip this and select *SAVE*.

Now that you've created a user account, you will need to bind that account to the study that you just created. From the main page of the admin console, click on *Researchers* underneath the *Study\_Management* heading.

From there, click *ADD RESEARCHER*.

On the Add Researcher page, select the user account that you just created, as well as the study that you created and select *SAVE*.

## Study management

Make sure you're logged out of the admin console (you can do so by selecting *Log Out* in the top right corner of the admin console.)

Browse to the study management console (if you are using the default settings, click [here](http://localhost:8000/management) )

Enter the username and password for the user account that you just created.

As mentioned, you will be prompted to change your password when you first sign in.

From the main page of the study management console, you should see the study that you just created. Click on the study.

From the Study detail page, you can view study data as well as add participants. Since there are no data yet, select *Add Participants*.

From the Add Participants page, enter a username, participant label, and password.

You can now authenticate with the [Participant API](https://documenter.getpostman.com/view/753798/ls2-participant-api/RW8Aoonk) using the username and password that you've created.

## SDKs

You can find the iOS SDK [here](https://github.com/CuriosityHealth/LS2SDK-iOS).

You can find the Android SDK [here](https://github.com/CuriosityHealth/LS2SDK-Android).
