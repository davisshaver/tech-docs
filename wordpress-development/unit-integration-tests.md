# Unit and Integration Tests

## How to run fusion-theme tests
1. Run `vagrant up` to start the machine. SSH into the machine using `vagrant ssh`.
2. Change to the theme directory inside of the machine. It's likely something like this:
```
cd /srv/www/wp-content/themes/vip/fusion-theme
```

3. Once inside the theme directory, you'll need to run `composer install` to install the dependencies we've defined using Composer. These dependencies are only needed for our testing harness, which is why they're not committed to the repo.

4. To set up WordPress unit tests, run:
```
bin/install-wp-tests.sh wordpress_test root ''
```

5. To run our unit tests, run `phpunit` from the theme root.

## Making test content

Most likely you need to deal with different kinds of post types within WordPress when creating test cases. [WP_UnitTestCase](https://core.trac.wordpress.org/browser/trunk/tests/phpunit/includes/factory.php) is really your best friend. Here's how we make some of our post types using our Fusion factory.

**Post**

```php
$post_id = $this->factory->post->create(array(
    'post_title' = > 'Video',
    'post_content' = > 'Post Content for Video',
    'post_date' = > '2014-10-01 17:28:00',
    'post_status' = > 'publish',
    'post_type' = > 'post',
    'post_author' = > $user_id, ));

$post = \Fusion\Objects\Post::get_by_post_id($post_id);
```

**Video**

```php
$post_id = $this->factory->post->create(array(
    'post_title' = > 'Video',
    'post_content' = > 'Post Content for Video',
    'post_date' = > '2014-10-01 17:28:00',
    'post_status' = > 'publish',
    'post_type' = > 'fusion_video',
    'post_author' = > $user_id, ));

$post = \Fusion\Objects\Post::get_by_post_id($post_id);
```

**Show**

```php
$post_id = $this->factory->post->create(array(
    'post_title' = > 'Video',
    'post_content' = > 'Post Content for Video',
    'post_date' = > '2014-10-01 17:28:00',
    'post_status' = > 'publish',
    'post_type' = > 'fusion_show',
    'post_author' = > $user_id, ));

$post = \Fusion\Objects\Post::get_by_post_id($post_id);
```

**Gallery**

```php
$post_id = $this->factory->post->create(array(
    'post_title' = > 'Video',
    'post_content' = > 'Post Content for Video',
    'post_date' = > '2014-10-01 17:28:00',
    'post_status' = > 'publish',
    'post_type' = > 'fusion_gallery',
    'post_author' = > $user_id, ));

$post = \Fusion\Objects\Post::get_by_post_id($post_id);
```
