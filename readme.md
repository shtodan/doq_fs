# description
-  Test system for basic file serving.
-  System can be used to serve home server files (without static IP address) 
-  Frontend app can be hosted on some free hosting like Heroku
-  System is sustained of 2 seporated web apps:

 ## "frontend app"
   - project is stored in doq directory
   -  Django app used for viewing and serving FileSystem content hosted on "backend app"
   - Comunicate with "backend app" through API
   - User auth			- project is stored in doq directory

 ## "backend app"
 - project is stored in fs directory
-  Flask app used for serving FileSystem content to "frontend app"
-  sending access tokens to "frontend app/s"
-  desired serving directories must be on machine where this app is hosted

# installation
## frontend Django app 
- install "pipenv" for python 2.7
- run "pipenv install" to to install dependencies
- activate env with command "pipenv shell"

1. set doq database params at doq/doq/settings.py
2. run "python manage.py migrate" to make init model tables
3. run "python manage.py createsuperuser" to createsuperuser
4. run "python manage.py runserver" to start frontend app server
5. visit started frontend app to add needed inital data:
	5.1 add new location(full path) which will be served as root dir to logged user http://127.0.0.1:8000/admin/fs/location/add/
	5.2 link location to user http://127.0.0.1:8000/admin/fs/userroot/add/
	5.3 add new user which will be used by backend app to post tokens to frontend http://127.0.0.1:8000/admin/auth/user/add/

## backend Flask app
- install "pipenv" for python 2.7
- run "pipenv install" to to install dependencies
- activate env with command "pipenv shell"

1. in backend app fs/fs.py 
	1.1 set inserted backend user (5.3) creadentoials 
	1.2 set frontend app addresses (possible to have multiple frontend apps)
2. start backend app with default port 5000 or custom port which is needed to be set in doq/fs/views.py in method "backend_auth"