[![Build Status](https://travis-ci.org/souly1/ion-image-search.svg?branch=master)](https://travis-ci.org/souly1/ion-image-search)

# ion-image-search

An Ionic service for searching an image from the web with an endless scroll, similar to Whatsapps `Search web` feature when defining image for group.

# Install

npm: npm install ion-image-search
bower: bower install ion-image-search

# Demo:

[Plunker Demo Using Bing](http://plnkr.co/edit/ThyM5ooHWFzjZcc50hJ7?p=preview)

Demo can be seen in app:

[Fitness Meal Planner](http://www.fitnessmealplanner.com)

## Requirements

- Ionic 1.*

## ScreenShots

![alt tag](/screenshots/screenshot1.jpg)

## Usage

- You can either add the basic CSS and JS to the project and then each provider separately:

```html
<link rel="stylesheet" href="wherever-you-put-it/ionImageSearch.css">

<script type="text/javascript" src="wherever-you-put-it/searchProviders/*Provider.js"></script>
<script type="text/javascript" src="wherever-you-put-it/ionImageSearch.js"></script>
```

Or just add the minified version:

```html
<link rel="stylesheet" href="wherever-you-put-it/ionImageSearch.min.css">

<script type="text/javascript" src="wherever-you-put-it/ionImageSearch.min.js"></script>
```

- Add the configuration file required by providers and ionImageSearch:

```html
<script src="wherever-you-put-it/ionImageSearch.config.js"></script>
```

- Add dependencies on the `ion-image-search` AngularJS module:

```javascript
angular.module('myApp', ['ion-image-search']);
```

Inject $webImageSelector and call init to configure with custom configuration and/or scope
```javascript
$webImageSelector.init(configuration, scope);
```

The `init` method receives two optional parameters: configuration parameter and scope parameter

Then call `show` to display the modal view:
```javascript
$webImageSelector.show();
```

The `show` method returns an object with 2 fields: `image` and `searchString`

An additional method available is getSearchProviderOptions which returns all provider options available according to providers in configuration
## Return object

`image` - The image object selected, has property `url` which is url of the image
`searchString` - The search string used to retrieve the image
## Configuration Attributes

The configuration attributes and default values can be found in the `ionImageSearch.config.js` file

- `maxSuccessiveFails` - Maximum number of successive search fails till infinite scroll stops or moving to next service provider if array supplied (see below). default is `5`
- `imgSize` - the size of image we want. Default is `small`
- `fileType` - the image file extension. Default is `jpg`
- `searchProviders` - An array that Specifies search providers to use.
                                If more than one is supplied to the array than loads from each service provider in order if service provider failed successively the configuration value of `maxSuccessiveFails` number of times.
                                Default out of the box is set to use `Google, Bing, Flickr` in that order

## Extending the provider list

You're more than invited to extend the image provider list and even request a merge to inlarge our list of image providers with API.
It is recommended the provider will conform to the existing providers structure, but it is mandatory that it will have at least the following structure:

```javascript

* Constructor that will receive configuration explained above
* `query(searchText, startIndex)` - an async query method to be called to do the actual query which receives two parameters:
    * searchText - the text to actually do the search with
    * startIndex - the starting index for this search
* `getPageSize()` - a method which returns the number of items the query retrieves


```

## Notes

Don't forget to enter your own keys to the different search providers. you can request them at the following locations:

_Google_ -

_Bing_ - go to [azure](https://datamarket.azure.com/) and get a key. To get auth value take the app key previously aquired add ':' to the start and transform it into base64 with a leading. This value will be set using: 'Basic' authetication, e.g if your key is x set in the ionImageSearch.config.js file auth: 'basic x'. See (here)[http://stackoverflow.com/questions/27311286/what-are-the-ajax-authorization-headers-for-a-bing-api-request/27315449#27315449] for additional info

_Flickr_ -

## Testing

Karma & Jasmine

## License

As AngularJS itself, this module is released under the permissive [MIT license](http://revolunet.mit-license.org). Your contributions are always welcome.

