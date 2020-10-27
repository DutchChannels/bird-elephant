# Twitter Search PHP

Connect apps to the new Twitter API v2 search tweets and lookup endpoints, in PHP.

This package currently caters for **bearer token based app access only**. I plan to expand this as V2 matures.

Twitter [have stated](https://developer.twitter.com/en/docs/twitter-api/tweets/search/introduction) that they will release a full-archive version which will make the entire archive of public Tweets available soon. "The recent and full-archive search endpoints will share common design and features and are part of the Search Tweets group of endpoints" - this package will be expanded to include this as it becomes available.

To use this package you must have an approved developer account, and have activated the new developer portal.

Learn more about getting access to the Twitter API v2 endpoints:

[Twitter Getting Started Docs](https://developer.twitter.com/en/docs/twitter-api/getting-started/guide)

### API Reference

[Twitter Recent Search Endpoint API Reference](https://developer.twitter.com/en/docs/twitter-api/tweets/search/api-reference/get-tweets-search-recent)

[Lookup Multiple Tweets API Reference](https://developer.twitter.com/en/docs/twitter-api/tweets/lookup/api-reference/get-tweets)

[Lookup Single Tweets API Reference](https://developer.twitter.com/en/docs/twitter-api/tweets/lookup/api-reference/get-tweets-id)

Note that operator support is quite sparse at the moment which makes the use of tweets and media more than a little risky in some contexts - for example filtering NSFW content is not yet possible.

## Install:

Install via composer.

```bash
$ composer install coderjerk/twitter-search-php
```

## Examples:

Get the 14 most recent tweets relating to football and containing images.

```php
use Coderjerk\TwitterSearch\RecentSearch;

$params = [
    'query'        => 'football',
    'max_results'  => 14,
];

$search = new RecentSearch;
$result = $search->RecentSearchRequest($params);

$tweets = $result->data;

```

Retrieve media:

```php
use Coderjerk\TwitterSearch\RecentSearch;

$params = [
    'query' => 'dancing has:images ',
    'tweet.fields' => 'attachments,author_id,created_at',
    'expansions'   => 'attachments.media_keys',
    'media.fields' => 'public_metrics,type,url,width',
    'max_results'  => 10,

];

$search = new RecentSearch;
$result = $search->RecentSearchRequest($params);
$media = $result->includes->media;

```

Lookup details about multiple tweets by Id:

```php
$ids = [
    '1261326399320715264',
    '1278347468690915330'
];

$params = [
    'tweet.fields' => 'attachments,author_id,created_at,public_metrics,source'
];

$lookup = new TweetLookup;
$tweets = $lookup->getTweetsById($ids, $params);
```

## Contributing

This package is in early stages development, contributions most welcome.
