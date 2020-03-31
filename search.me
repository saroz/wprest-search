#### Step 1: Search Field
We begin with the search filed *HTML*. 

``` html
<input
	name="global_search"
	class="search-autocomplete"
	type="text"
	placeholder="Start typing..."
>
```

#### Step 2: Search Template (partial template)

``` html
<div class="search-container">
	<span class="search-heading">Search Results</span>
	<div  class="search-results">
	</div>
</div>

```
#### Step 3: Link search template

Link your search template with your website
e.g. `header.php` or `page.php`

``` php
<?php
	get_template_part( 'template-parts/search.php' );
?>
```

#### Step 4: Style.css
Make `.search-container` container hidden fist, after user finished search something and we will make visible container.

``` scss
.search {
	display: none;
}
```

#### Step 5: Enqueue jquery-ui-autocomplete and search.js & pass query parameters to the script

This small piece of code allows you to pass the according parameters to the script that’s why the button can work on any page – tags, categories, custom post type archives, search etc. You can also use it for WooCommerce to load more products.

``` php
add_action('wp_enqueue_scripts', function () {
	global  $wp_query;
	wp_enqueue_script( 'jquery-ui-autocomplete' );
	wp_register_script( 'my_search', get_stylesheet_directory_uri() . '/search.js', array('jquery') );
	$ajax_params  =  array(
		// our search api
		'search_api'  =>  home_url( 'wp-json/wfg/v1/search' )
		'security'  =>  wp_create_nonce('search_api'),
	);
	wp_localize_script( 'my_search', 'custom_apis', $ajax_params);
}, 100);

```

#### Step 6: PHP code to Process the Request 

This code is fully based on `WP_Query`
Helper function which will help to show searched data on `search.php` template.
You can write this code on `function.php` or create different file and link on `function.php` file.


``` php
/**
* WP REST API register custom endpoints
*/

add_action( 'rest_api_init', function  wfg_rest_api_register_routes() {
	register_rest_route( 'wfg/v1', '/search', array(
		'methods'  =>  'GET',
		'callback'  =>  __NAMESPACE__  .  '\\wfg_rest_api_search',
	));
});

```

``` php
/**
* callback function for rest route
* WP REST API search results.
* @param  object $request
*/

function  wfg_rest_api_search( $request ) {
	if ( empty( $request['global_search'] ) ) { // search field name `global_search`
		return;
	}

	$time		=  microtime(true);
	$return		=  '';
	$term		=  $request['global_search'];
	$skey		=  isset ( $term['term'] ) &&  !empty( $term['term'] ) ? $term['term'] :  '';
	$keys		=  isset ( $skey ) ?  explode(" ", $skey) :  '';
	$per_page  	=  -1;

}

/*
* Argument for search people
* postype: staff, officer
* search: post_title
* Custom Field searched: designation, department etc
* WP_Query
* CPT(staff) searched : title (name of staff)
*/

$args  =  array(
	'post_type'  => [ staff, officer ], // 'staff' (for one post type)
	'suppress_filters'  =>  false,
	'_meta_or_title'  =>  $skey,
	'post_status'  =>  'publish',
	'meta_query'  => [
		'relation'  =>  'OR',
		[
			'key'  =>  'designation',
			'value'  =>  $skey,
			'compare'  =>  'LIKE'
		],
		[
			'key'  =>  'department',
			'value'  =>  $skey,
			'compare'  =>  'LIKE'
		]
	],
	'posts_per_page'  =>  $per_page
);
$peoples  =  new WP_Query($args);

// 
if ( $peoples->have_posts()) :
	$response = '<div class="people">
					<span class="title">People</span>
					<ul>';
	while ( $peoples->have_posts() ) : $peoples->the_post();
		$id  		=  $peoples->post->ID;
		$title  	=  $peoples->post->post_title;
		$title  	=  preg_replace('/('.implode('|', $keys) .')/iu', '<span>\0</span>', $title);
		$permalink  =  get_permalink($id);

		//designation (to query)
		$designation	=  get_post_meta($id, 'designation', true);
		$designation 	=  preg_replace('/('.implode('|', $keys) .')/iu', '<span>\0</span>', $designation);

		//department (to query)
		$department		=  get_post_meta($id, 'department', true);
		$department 	=  preg_replace('/('.implode('|', $keys) .')/iu', '<span>\0</span>', $designation);

		//avatar (to show for design purpose)
		$avatar			=  get_post_meta($id, 'avatar', true);
		$avatar			=  $avatar ? $avatar : get_the_post_thumbnail_url($id);

		$response .= '
			<li>
				<figure>
					<a href="'.$permalink.'" title="'.get_the_title().'">
						<img src="'.$avatar.'" alt="Profile Picture">
					</a>
				</figure>
				<div class="info">
					<a href="'.$permalink.'"><p>'.$title.'</p></a>
					<p>'.$designation.'/'.$department.'</p>
				</div>
			</li>';

	endwhile;
	wp_reset_postdata();
	$response .= '</ul></div>';
else:
	$response =	'<div class="people">
					<span class="title">People</span>
					<span class="message">No result found</span>
				</div>';
endif;

```

#### Step 4: jQuery script to Send a Request and to Receive Result Data
We added a file `search.js` on **Step 5**. We will be write this code on that JavaScript file.



``` js

$('.search-autocomplete').autocomplete({
	source:  function (searchItem) {
		if (searchItem.term.length  >=  4) {
			$('body').find('.results-wrap').html('');
			$('.search-container).append('<div class="loader active"><div class="loading" role="status"></div></div>');
			$('.search-results').fadeIn();

			// custom_apis.search_api (from Enqueue jQuery)
			// global_search (search field name)
			const  wpRestAPI  =  window.custom_apis.search_api || false;
			$.get(wpRestAPI, { global_search:  searchItem }, function (res) {
				if (res.status) {
					$('.search-results').fadeIn();
					$('body').find('.search-container').html(res.content);
				} else {
					$('body').find('.search-container').html('<span class="message">Something is wrong, please try again later ...</span>');
				}
			});
		} else {
			$('.search-results').fadeOut();
		}
	},
});

```
