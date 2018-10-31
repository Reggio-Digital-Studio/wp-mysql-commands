# WordPress Database MySQL Commands

The following guide is meant to help you slim down your WordPress MySQL database before distributing it to other developers. It's so you can remove sensative information from the database before providng it to others. These are not meant to be run on a live site.

## WordPress Core

### Deactivate All Plugins

```
UPDATE wp_options 
SET 
    option_value = 'a:0:{}'
WHERE
    option_name = 'active_plugins';
```

### Delete Post Revisions

### Delete Spam Comments

```
DELETE FROM wp_comments
	WHERE comment_approved = 'spam';
```

### Delete Transients

```
DELETE FROM wp_options 
WHERE
    option_name LIKE ('%\_transient\_%')
```

### Delete Pingbacks and Trackbacks

```
DELETE FROM wp_comments
WHERE
	comment_type = 'pingback';
DELETE FROM wp_comments 
WHERE
    comment_type = 'trackback';
```

### Delete Transients

### Delete WordPress Sessions

### Delete Orphaned Post Meta

```
DELETE pm FROM wp_postmeta pm
        LEFT JOIN
    wp_posts wp ON wp.ID = pm.post_id 
WHERE
    wp.ID IS NULL
```

### Change The Email Address of All Users

This is especially helpful to avoid accidental email sending from the staging site.

```
UPDATE wp_users 
SET 
    user_email = 'test@test.test'
WHERE
    ID > '1';
```

## WooCommerce Core

https://woocommerce.com

### Delete webhooks & REST API keys

### Delete Customer User Profile Information

```
UPDATE wp_usermeta 
SET 
    meta_value = NULL
WHERE
    meta_key = 'first_name'
    OR meta_key = 'last_name'
    OR meta_key = 'billing_country'
    OR meta_key = 'billing_first_name'
    OR meta_key = 'billing_email'
    OR meta_key = 'billing_phone'
    OR meta_key = '_stripe_customer_id';
```

## WooCommerce Plugins

### Delete Stripe Payment ID's

https://woocommerce.com/products/stripe/

```
UPDATE wp_postmeta 
SET 
    meta_value = NULL
WHERE
    meta_key = '_stripe_charge_id'
    OR meta_key = 'Stripe Payment ID';
```

### Delete Braintree Live Key

https://woocommerce.com/products/woocommerce-gateway-paypal-powered-by-braintree/

## Misc Plugins

### Delete SendGrid Key

https://wordpress.org/plugins/sendgrid-email-delivery-simplified/

```
UPDATE wp_options 
SET 
    option_value = ''
WHERE
    option_name = 'sendgrid_api_key';
```
