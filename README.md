# post
The Andremyid Post package.

## Installation

* Add the following to your `Composer JSON` file
```
"andremyid/page": "~0.0"
```
* Run Composer
```
$ composer update
```
* Add the following to 'Andremyid/Framework-Core' => 'ServiceProvider'
```
Andremyid\Page\PageServiceProvider
```
* Run the migration

You can use database from WordPress, or copy from sample database migrate manually (you can modify as you like of the sample)
```
// first, optional
$ composer dump-autoload
// and then
$ php andre migrate
```
## Usage

### Extending

* Sample Backend Page

```php
<?php

use Andremyid\Page\SampleBackendPage;
use Andremyid\Page\BackendPageTrait;

class YourControllerBackendName extends SampleBackendPage {

    use BackendPageTrait;

    public function post_index()
	{
		return $this->index(); // use sample backend page
	}
	
	// uncomment below to replace sample backend page
	// protected funtion index()
	// {
	//    return $this->viewModule($this->module, "Title Backend Module");
	// }

}
```

* Sample Frontend Page

```php
<?php

use Andremyid\Page\SampleFrontendPage;
use Andremyid\Page\FrontendPageTrait;

class YourControllerFrontendName extends SampleFrontendPage {

    use FrontendPageTrait;

    public function post_index()
	{
		return $this->index(); // use sample frontend page
	}
	
	// uncomment below to replace sample frontend page
	// protected funtion index()
	// {
	//    $post = Post::model()->ofPublish();
	//    return $this->view($this->themes . 'index' , $post);
	// }

}
```

## Model
### Posts Table
* `Post::model();` to call back new Model Post (`wp_posts`)
* `Post::findSlug('sample-post-name')` return array data from query where `wp_posts.post_name = $slug`
* `Post::find($id);` to get `wp_posts` where `id = $id`
* `Post::create($data);` to create `wp_posts`
```php
    // sample create post manually
    Post::setCategory(array('uncategorized');
    Post::setStatus('publish'); // auto-draft, inherit, publish
    Post::setType('post');      // default 'post'

    $data = array(
        'post_author'  => $user_id,
        'post_content' => 'Sample Content',
        'post_title'   => 'Sample Title',
        'post_name'    => Post::makeSlug('Sample Title'),
    );
    Post::create($data);
    
```
* `Post::update($id);` to update `wp_post` where `id = $id`
* `Post::delete($id);` to delete `wp_post` where `id = $id`

### Terms Table
* `Term::model();` to call back new Model Term (`wp_terms`)
* `Term::findSlug('sample-slug')` return data from query where `wp_terms.name = $slug`
* `Term::find($id);` to get `wp_terms` where `term_id = $id`
* `Term::create($data);` to create `wp_terms`
* `Term::update($id);` to update `wp_terms` where `id = $id`
* `Term::delete($id);` to delete `wp_terms` where `id = $id`

## Credits

It's inspired by [WordPress](https://github.com/WordPress/WordPress)
