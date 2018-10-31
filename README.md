# WordPress Database MySQL Commands

The following guide is meant to help you slim down your WordPress MySQL database before distributing it to other developers. It's so you can remove sensative information from the database before providng it to others. These are not meant to be run on a live site.

## WordPress Core

### Deactive all plugins

```
UPDATE wp_options 
SET 
    option_value = 'a:0:{}'
WHERE
    option_name = 'active_plugins';
```

### Delete Post Revisions

### Delete Spam Comments

### Delete Transients

### Delete Pingbacks and Trackbacks

### Delete Transients

### Delete WordPress Sessions

## WooCommerce Core

### Delete webhooks & REST API keys

## WooCommerce Plugins

### Delete Stripe Live Key

### Delete Braintree Live Key
