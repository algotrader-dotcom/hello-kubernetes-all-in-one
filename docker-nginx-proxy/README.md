# Let's follow this to automate SSL for vhosts => https://gist.github.com/mattiaslundberg/ba214a35060d3c8603e9b1ec8627d349

docker build -t nginx .
docker run -ti nginx

# Deploy drupal
https://circleci.com/blog/continuous-drupal-p1-maintaining-with-docker-git-composer/
https://gist.github.com/delphian/6043424

```
composer create-project drupal-composer/drupal-project:8.x-dev /var/www/drupal/ --stability dev --no-interaction
cd /var/www/drupal/ && drush site-install standard --account-name=admin --account-pass=admin --db-url=mysql://root:root@mysql/drupal -y
```

# GCloud config
```
gcloud config set project k8s-test-218207
gcloud config set compute/zone us-central1-a
export PROJECT_ID="$(gcloud config get-value project -q)"
```
# Build & Upload to Google Container Registry
```
docker build --no-cache -t gcr.io/${PROJECT_ID}/drupal-app:v1.2 .
gcloud docker -- push gcr.io/${PROJECT_ID}/drupal-app:v1.2

cd ..
kubectl apply -f yaml/drupal-mysql-pv.yaml
kubectl apply -f yaml/drupal-mysql.yaml
kubectl apply -f yaml/drupal-app.yaml
```
