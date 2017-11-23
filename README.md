# Django Storages Libcloud Demo

A demo Django app using django-storages with Libcloud backend to display images from S3 or Tencent COS bucket, uploaded from admin interface.

## Running Locally

Make sure you have Python [installed properly](http://install.python-guide.org).  Also, install the [Heroku Toolbelt](https://toolbelt.heroku.com/) and [Postgres](https://devcenter.heroku.com/articles/heroku-postgresql#local-setup).

```sh
$ git clone git@github.com:itamaro/django-storages-boto3-demo.git
$ cd django-storages-boto3-demo

$ pipenv install

$ createdb django_storages_boto3

$ pipenv run python manage.py migrate
$ pipenv run python manage.py createsuperuser
$ pipenv run python manage.py collectstatic
$ cat <<EOF >.env
LIBCLOUD_PROVIDER="<aws-s3 OR tencent-cos>"
AWS_ACCESS_KEY="<Access-Key>"
AWS_SECRET_KEY="<Secret-Key>"
AWS_S3_BUCKET="S3-Bucket"
COS_API_KEY_ID="<COS-Key-ID>"
COS_API_SECRET_KEY="<COS-Secret-Key>"
COS_APP_ID=<App-ID>
COS_REGION="<COS-Region>"
COS_BUCKET_NAME="<COS-Bucket>"
EOF

$ pipenv run heroku local -p 8000 web
```

Your app should now be running on [localhost:8000](http://localhost:8000/).

## Deploying to Heroku

```sh
$ heroku create
$ git push heroku master

$ heroku run python manage.py migrate
$ heroku run python manage.py createsuperuser
$ heroku config:set \
    LIBCLOUD_PROVIDER="<aws-s3 OR tencent-cos>" \
    AWS_ACCESS_KEY="<Access-Key>" \
    AWS_SECRET_KEY="<Secret-Key>" \
    AWS_S3_BUCKET="S3-Bucket" \
    COS_API_KEY_ID="<COS-Key-ID>"
    COS_API_SECRET_KEY="<COS-Secret-Key>" \
    COS_APP_ID=<App-ID> \
    COS_REGION="<COS-Region>" \
    COS_BUCKET_NAME="<COS-Bucket>"
$ heroku open
```
or

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Using the Demo

Using the admin interface (with the credentials of the superuser created), create "UploadedImage" records, uploading images from your local machine, then view the images ob the home page of the app.

## Documentation

For more information about using Python on Heroku, see these Dev Center articles:

- [Python on Heroku](https://devcenter.heroku.com/categories/python)
