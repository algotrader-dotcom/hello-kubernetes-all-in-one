docker build -t drupal01 .
docker run -ti drupal01

# Deploy drupal
https://circleci.com/blog/continuous-drupal-p1-maintaining-with-docker-git-composer/
https://gist.github.com/delphian/6043424

```
composer create-project drupal-composer/drupal-project:8.x-dev /var/www/drupal/ --stability dev --no-interaction
drush site-install standard --account-name=admin --account-pass=admin --db-url=mysql://root:root@mysql/drupal -y
```