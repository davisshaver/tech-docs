# ElasticSearch Integration

It looks like we have a couple options we can go for. 

1. Related articles
2. Search query from VIP

# Related articles

This is done via `https://developer.wordpress.com/docs/api/1.1/post/sites/%24site/posts/%24post/related/` which is a public api we can use. 

Example

```
$curl = curl_init( 'https://public-api.wordpress.com/oauth2/token' );
curl_setopt( $curl, CURLOPT_POST, true );
curl_setopt( $curl, CURLOPT_POSTFIELDS, array(
    	'client_id' => '$client_id',
    	'client_secret' => '$client_secret',
    	'grant_type' => 'password',
    	'username' => '$email',
    	'password' => '$password',
) );
curl_setopt( $curl, CURLOPT_RETURNTRANSFER, 1);
$auth = curl_exec( $curl );
$auth = json_decode($auth);
$access_key = $auth->access_token;

$options  = array (
  	'http' => 
  		array (
    			'ignore_errors' => true,
    			'method' => 'POST',
    			'header' => 
				array (
      					0 => 'authorization: Bearer ' . $access_key,
					1 => 'Content-Type: application/x-www-form-urlencoded',
    				),
    			'content' => http_build_query(   
      				array (
        				'size' => 5,
      				)
    			),
  		),
	);
 
$context  = stream_context_create( $options );
$response = file_get_contents(
	'https://public-api.wordpress.com/rest/v1/sites/73194874/posts/121641/related',
	false,
  	$context
);
$response = json_decode( $response );

```
If you're not familiar with OAuth please check https://developer.wordpress.com/docs/oauth2/ for more information. In the example I've used the password technique and this is for testing purposes only. This is also the downside of this technique which we need to authenticate the request and it makes local development a bit difficult.

# Search query from VIP

VIP offers us a low-level api which is [es_api_search_index](https://vip.wordpress.com/functions/es_api_search_index/)

Example

```
$args = array( 
	'blog_id' 		=> '$blod_id',
	'query'			=> '$search_query'
);
$results = wpcom_search_api_query($args);
var_dump($results['results']);

```

The source code of this function can be found here `plugins/vip-do-not-include-on-wpcom/wpcom-functions.php`line 186.

This gives us more flexibility which we can make our own query. However, Jetpack doesn't quite work locally. We need to hack the source code to make the test case works. Line 223 is checking `$jetpack_blog_id` we need to turn that off and that would work locally. 

```
if ( isset( $hit['fields']['blog_id'] ) ) { // && $hit['fields']['blog_id'] == $jetpack_blog_id ) {
	$response['results']['hits'][$key]['fields']['blog_id'] = $local_blog_id;
} 
```







