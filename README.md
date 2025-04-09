# meyerd10

# Initialize a drupal10 recipe
mkdir my-first-drupal10-app \
  && cd my-first-drupal10-app \
  && lando init \
    --source cwd \
    --recipe drupal10 \
    --webroot web \
    --name my-first-drupal10-app

# Start it up
lando start

# Create latest drupal10 project via composer
lando composer create-project drupal/recommended-project:10.x tmp && cp -r tmp/. . && rm -rf tmp

# Composer can timeout on install for some machines, if that happens, run the following command and then re-run the previous lando composer command:
# lando composer config --global process-timeout 2000

# Install a site local drush
lando composer require drush/drush

# Install drupal
lando drush site:install --db-url=mysql://drupal10:drupal10@database/drupal10 -y

# List information about this app
lando info

# Delete all shortcut sets (this will also delete associated links)
lando drush entity:delete shortcut_set
lando drush cim -y
