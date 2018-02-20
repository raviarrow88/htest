# Deploying a Django-app in Heroku
 
**Steps to be followed**

1.If you are new to Django - click this link  [how to create Django project](https://docs.djangoproject.com/en/2.0/intro/tutorial01/)

2.To use heroku,first step is download the Heroku CLI in system [link](https://devcenter.heroku.com/articles/heroku-cli)
 
3.Create a heroku account after installing CLI 

4.Add a **Procfile** in the project root directory 
 
- Install gunicorn 
  > pip install gunicorn


- General Format
  > web: gunicorn myproject.wsgi --log-file -

- For my Django project:

    - Project Name: htest
    - App name: website
   
- My project **Procfile**

    > web: gunicorn --pythonpath website website.wsgi

5.Add requirements.txt in Project Root Directory

     pip freeze > requirements.txt
    
**Note:** Dont create a sub folder for requirements.txt in project root directory,place it in the project root directory

6. Add .gitignore file  which consists of
```
venv
*.pyc
staticfiles
.env
```
7.Push the code/project to heroku master branch

- Intialize git
> git init

- status of your project 
> git status

- Add project files to git by

> git add .

- Commit your project 
 
> git commit -m "your message"

7. Login into Heroku 

> heroku login

8. Create a heroku app 

> heroku createapp 

By Default, heroku creates a random appname,if you want to specify the app you can do it by 

> heroku createapp myapp

9.Push your project to code heroku via git by 
  
> git push heroku master 

here you are pushing your project to heroku from your git master branch, suppose if you are working on the some testbranch or develop branch,you can push by

> git push heroku develop:master

Before pushing to heroku, there are two cases

- **Case1: Push to heroku without Static Files**
   
   -  >heroku config:set DEBUG_COLLECTSTATIC=1
   
   disbale the collectstatic build step,if your are not pushing static files to heroku.
   
-**Case2: Push to heroku with static Files**
   
   - Install whitenoise
        > pip install whitenoise
        
   - Add this middleware in your Django settings.py file 
   
        ```
        MIDDLEWARE_CLASSES = (
    
        'whitenoise.middleware.WhiteNoiseMiddleware',
        ...)
        
        ```
   - Add this piece of code in settings.py file to store your project static files
        ```
        # https://docs.djangoproject.com/en/1.9/howto/static-files/
            STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
            STATIC_URL = '/static/'
            
            # Extra places for collectstatic to find static files.
            STATICFILES_DIRS = (
                os.path.join(BASE_DIR, 'static'),
            )
        
      ```
   - Run the command in terminal:
   
        > python manage.py collectstatic
     
     By running this command,static file is create in your project directory with all your static files 
     
   - Enable the collectstatic build 
   
       > heroku config:set DEBUG_COLLECTSTATIC=0
   - Before pushing to heroku if you want to check how your app run in  local heroku host
       
       > heroku local web
       
       This command runs your app in localhost 
       
   - Commit the code, Push to heroku master
   
   - Run your heroku by using command
       
       > heroku open
 
 
 My sample webiste : https://test-app501.herokuapp.com/
 
 