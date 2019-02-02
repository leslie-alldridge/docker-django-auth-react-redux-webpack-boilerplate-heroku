# This app is ready for deployment to Heroku (deployed 03/02/2019)

## Technology
- Docker
- Django
- React
- Redux
- Webpack
- SQLite3 / Postgres
- Knox (auth)
- Axios (api calls)

## Breakdown of files
* /frontend <- contains all of the React frontend code
* /leadmanager <- main python application
* /leads <- code related to creating leads
* /accounts <- code related to users/auth
* All of the other files should be self explanatory - reach out if you get stuck though

## Run locally and Deploy to Heroku using Heroku CLI
1. Follow the steps here to spin up a local docker container running Django https://docs.docker.com/compose/django/
2. Replace the contents of your project folder with the contents of this repository
3. Because your code has changed, run 
```
docker-compose build
docker-compose up
```
4. The latest build is ready and should be running locally on localhost:8000
5. Run the following commands to deploy to Heroku 

(you will need Heroku CLI installed https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

```
heroku container:login
heroku create your-app-name-goes-here
heroku container:push web -a your-app-name-goes-here
heroku container:release web -a your-app-name-goes-here
```
6. The app will push to Heroku and deploy successfully but it won't work. The reason for this is we need to provision Postgres as an addon
7. Install Postgres from your Apps Heroku page > Resources > Search for add ons > Heroku Postgres
8. Once provisioned, the app still doesn't work as we will need to run migrations
9. Jump into the console More > Run Console and type python manage.py migrate
10. Once the migrations have completed, the app is ready to go!

## I've changed my react code but my page hasn't updated?
You will need to run webpack locally before pushing to Heroku as the main.js file will contain code relating to your app when webpack was last run. 
```
npm run dev
```
## Pip won't install my dependencies / the right dependencies 
Check the requirements.txt file and ensure the Docker file has 
```
COPY requirements.txt /code/
RUN pip install -r requirements.txt
```

## I had to change my Docker set up / other deployment related files
Ensure you push and release the latest container to Heroku so your changes are live. 

## Can I use this in Production?
No. Heroku documentation doesn't recommend running a Django web server in Production - you should use something such as NGINX. You'll also need to set the SECRET_KEY in Django to an environment variable. 

## Can I use your code? 
Sure thing, Fork it over and deploy in <5 minutes :whale: :cat:
