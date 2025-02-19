# JavaScript library: `algoliasearchZendeskHC`

[![npm](https://img.shields.io/npm/v/algoliasearch.zendesk-hc.png)](https://www.npmjs.com/package/algoliasearch.zendesk-hc)

[![Dependency Status](https://david-dm.org/algolia/algoliasearch-zendesk.png?path=app)](https://david-dm.org/algolia/algoliasearch-zendesk?path=app)
[![devDependency Status](https://david-dm.org/algolia/algoliasearch-zendesk/dev-status.png?path=app)](https://david-dm.org/algolia/algoliasearch-zendesk?path=app#info=devDependencies)
[![peerDependency Status](https://david-dm.org/algolia/algoliasearch-zendesk/peer-status.png?path=app)](https://david-dm.org/algolia/algoliasearch-zendesk?path=app#info=peerDependencies)

[![GitHub license](https://img.shields.io/github/license/algolia/algoliasearch-zendesk.png)](../LICENSE)

This JavaScript library allows you to replace the default search of your Zendesk Help Center by Algolia. [Algolia](https://www.algolia.com) is a hosted full-text, numerical, and faceted search engine capable of delivering realtime results from the first keystroke.

To browse through the crawler, visit the [crawler/](../crawler/) folder.

## Documentation

<!--
  docs/documentation.md is generated from the content of the ## Documentation section of app/README.md
  To change its content, modify app/README.md, go to the app/ folder and run `npm install && npm run build:docs`
-->

### Synchronize Algolia with your Help Center

<div align="center">
  <img src="https://community.algolia.com/zendesk/img/algolia-zendesk.svg" alt="Data connection visualization" />
</div>

1. Create an [Algolia account](https://www.algolia.com/users/sign_up).
1. Follow the <a href="https://www.algolia.com/zendesk" rel="nofollow">Get Started</a> guide to connect your Zendesk Help Center with your Algolia account.

### Indexing

When you install our Zendesk integration, it creates what we call a connector in your Algolia account.
You can access it with the left sidebar in your dashboard.

This connector will every day take your public Help Center articles and put them inside an Algolia index.
In most cases, this should be enough to have an up-to-date search.

However, if you'd rather have it updated sooner, you can manually trigger a full reindex.
On this page, click the "Reindex" button in the bottom right corner. An indexing job will be pushed in our indexing queue. Depending on the load of the queue, it might take up to a few hours for your search index to be updated.

### Updating your Help Center theme

Once your data has been extracted to Algolia, you need to update your Help Center theme in order to replace the search feature by Algolia.

* Open the **Document Head** template in the **Theme Editor**:
  1. Head to your Zendesk Help Center
  1. Click **General > Customize the design** in the top bar
  1. In the **Theme** section, click on **Edit theme**
  1. In the top left corner dropdown, select the **Document Head** template

<div align="center">
  <img src="https://res.cloudinary.com/hilnmyskv/image/upload/v1522421354/Onboarding--First-Gif_wsuvrs.gif" alt="Document Head opening GIF" />
</div>

* Copy the **JavaScript** snippet & **Publish** changes:
  1. Paste the code we provide you while connecting your Zendesk Help Center with Algolia at the end of the template.
  1. Click **Save** and ensure everything is working using the preview on the right (if you have some small CSS issues, [read this part](#customizing-the-css))
  1. Click **Publish Changes**

<div align="center">
  <img src="https://res.cloudinary.com/hilnmyskv/image/upload/v1522421175/Onboarding--Second-Gif_y0i5pe.gif" alt="Document Head editing GIF" />
</div>

&nbsp;

### Available options

Here is a full breakdown of the available options for the JavaScript library:

```html
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/2/algoliasearch.zendesk-hc.min.css">
<script type="text/javascript" src="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/2/algoliasearch.zendesk-hc.min.js"></script>
<script type="text/javascript">
  algoliasearchZendeskHC({
    applicationId: '<YOUR APPLICATION_ID>',
    apiKey: '<YOUR SEARCH ONLY API KEY>',
    subdomain: '<YOUR ZENDESK APPLICATION NAME>',

    //
    // Optional configuration:
    //
    indexPrefix: 'zendesk_',              // or your custom <INDEX_PREFIX>
    analytics: true,                      // should queries be processed by Algolia analytics
    baseUrl: '/hc/',                      // the base URL of your Help Center
    poweredBy: true,                      // show the "Search by Algolia" link (required if you're on Algolia's FREE plan)
    clickAnalytics: false,                // whether or not to enable the clickAnalytics feature (available on the Enterprise plan)
    debug: false,                         // debug mode prevents the autocomplete to close when trying to inspect it
    color: '#158EC2',                     // main color (used for links)
    highlightColor: '#158EC2',            // highlight color to emphasize matching text
    responsive: true,                     // responsive instantsearch page
    autocomplete: {
      enabled: true,                      // is the autocomplete feature enabled?
      inputSelector: '#query',            // the DOM selector to select the search box
      hitsPerPage: 5                      // the number of suggestions to display
    }, 
    instantsearch: {
      enabled: true,                      // is the instantsearch feature enabled?
      hitsPerPage: 20,                    // the number of suggestions to display
      paginationSelector: '.pagination',  // the DOM selector for the current pagination (to hide it)
      reuseAutocomplete: false,           // do not add a search input for the instant-search page
      hideAutocomplete: true,             // whether or not to hide the autocomplete on the instantsearch page (ignored if reuseAutocomplete is used)
      selector: '.search-results',        // the DOM selector for the results container
      tagsLimit: 15,                      // maximum number of tags to display
      useEditedAt: false                  // show edited_at timestamp in search results
    },
    instantsearchPage,                    // function to check if we're on the search page
    templates: {                          // template objects (see the templates section)
      autocomplete: {},
      instantsearch: {}
    },
    translations: {}                      // translation strings
  });
</script>
```

### Customizing the CSS

It is definitely possible that, when you install the application, it doesn't exactly display as you expect.
No worries, these are usually just a few conflicting rules between your design and our integration.

You might also just want to change the look & feel of the search.

Either way, just follow the following steps:

- Ensure you read the [SCSS source file](https://github.com/algolia/algoliasearch-zendesk/blob/master/app/css/index.scss) to see all the rules we're using
- Add a `<style>` tag after the `<link>` tag you've already added in your **Document Head** template and add your custom CSS here

**Example:**

```html
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/CURRENT_VERSION/algoliasearch.zendesk-hc.min.css">
<style>
  .aa-dropdown-menu {
    background-color: #ccc;
  }
</style>
<script type="text/javascript" src="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/CURRENT_VERSION/algoliasearch.zendesk-hc.min.js"></script>
<script type="text/javascript">
  algoliasearchZendeskHC(/* ... */);
</script>
```

**Note:** You might have some trouble trying to customize the autocomplete menu because it automatically closes when you try to Inspect it.
Just set `debug: true` to avoid this behaviour.

### Supporting multiple languages

#### Description

This library supports out of the box Help Centers with multiple languages.

1. The results sent to the user are always limited to the ones in the currently selected locale.

2. Some constant strings like the ones used in the sentence "12 results found in 1ms" need to be translated.
   The library already supports these locales:

   - __ar__: العربية / Arabic
   - __ar-eg__: العربية (مصر) / Arabic (Egypt)
   - __bg__: Български / Bulgarian
   - __cs__: Čeština / Czech
   - __da__: Dansk / Danish
   - __de__: Deutsch / German
   - __de-at__: Deutsch (Österreich) / German (Austria)
   - __de-ch__: Deutsch (Schweiz) / German (Switzerland)
   - __el__: Ελληνικά / Greek
   - __en-au__: English (Australia)
   - __en-ca__: English (Canada)
   - __en-gb__: English (Great Britain)
   - __en-ie__: English (Ireland)
   - __en-us__: English (United States)
   - __en-150__: English (Europe)
   - __es__: Español / Spanish
   - __es-es__: Español (España) / Spanish (Spain)
   - __es-mx__: Español (Mexico) / Spanish (Mexico)
   - __es-419__: Español (Latinoamérica) / Spanish (Latin America)
   - __fi__: Suomi / Finnish
   - __fr__: Français / French
   - __fr-be__: Français (Belgique) / French (Belgium)
   - __fr-ca__: Français (Canada) / French (Canada)
   - __fr-ch__: Français (Suisse) / French (Switzerland)
   - __fr-fr__: Français (France) / French (France)
   - __hu__: Magyar / Hungarian
   - __id__: Bahasa Indonesia / Indonesian
   - __it__: Italiano / Italian
   - __ja__: 日本語 / Japanese
   - __ko__: 한국어 / Korean
   - __nl__: Nederlands / Dutch
   - __nl-be__: Nederlands (België) / Dutch (Belgium)
   - __no__: Norsk / Norwegian
   - __pl__: Polski / Polish
   - __pt__: Português / Portuguese
   - __pt-br__: Português do Brasil / Brazilian Portuguese
   - __ro__: Română / Romanian
   - __ru__: Русский / Russian
   - __sk__: Slovenčina / Slovak
   - __sv__: Svenska / Swedish
   - __th__: ไทย / Thai
   - __tr__: Türkçe / Turkish
   - __uk__: Українська / Ukrainian
   - __vi__: Tiếng Việt / Vietnamese
   - __zh-cn__: 简体中文 / Simplified Chinese
   - __zh-tw__: 繁體中文 / Traditional Chinese

   If you want to support another locale, please help us by [opening an issue on GitHub][locale_issue].

<!--
  In browser console edition of this link:

  var body = encodeURIComponent("\u003C!\u2212\u2212\n  To improve the extension, we need your help!\n  We only need to know how to write a few sentences in the language you want us to add.\n  Can you help us translate them? :)\n\u2212\u2212\u003E\n\nTranslations:\n\n```txt\nSearch in our articles: \nSearch by Algolia: \nNo result found for \"xxx\": \n\"change your query\" or \"clear your filters\": \n1 result found in XXXms: \n2,000 results found in XXXms: \nCategories: \nTags (in the \"Labels\" meaning): \nFilter results: \n```\n\nIs there more than 1 plural form? [Yes/No]\nHow do you write big numbers? [20,000]");
  var title = encodeURIComponent("Missing locale: [en-us]")
  "https://github.com/algolia/algoliasearch-zendesk/issues/new?title=" + title + "&body=" + body
-->

  [locale_issue]: https://github.com/algolia/algoliasearch-zendesk/issues/new?title=Missing%20locale%3A%20%5Ben-us%5D&body=%3C!%E2%88%92%E2%88%92%0A%20%20To%20improve%20the%20extension%2C%20we%20need%20your%20help!%0A%20%20We%20only%20need%20to%20know%20how%20to%20write%20a%20few%20sentences%20in%20the%20language%20you%20want%20us%20to%20add.%0A%20%20Can%20you%20help%20us%20translate%20them%3F%20%3A)%0A%E2%88%92%E2%88%92%3E%0A%0ATranslations%3A%0A%0A%60%60%60txt%0ASearch%20in%20our%20articles%3A%20%0ASearch%20by%20Algolia%3A%20%0ANo%20result%20found%20for%20%22xxx%22%3A%20%0A%22change%20your%20query%22%20or%20%22clear%20your%20filters%22%3A%20%0A1%20result%20found%20in%20XXXms%3A%20%0A2%2C000%20results%20found%20in%20XXXms%3A%20%0ACategories%3A%20%0ATags%20(in%20the%20%22Labels%22%20meaning)%3A%20%0AFilter%20results%3A%20%0A%60%60%60%0A%0AIs%20there%20more%20than%201%20plural%20form%3F%20%5BYes%2FNo%5D%0AHow%20do%20you%20write%20big%20numbers%3F%20%5B20%2C000%5D


#### Modifying translations

If some translations don't fit what you want, you can change them using this syntax:

```coffee
translations: {
  placeholder: {
    de: 'In unseren Help Center suchen',
    'en-us': 'Search in our Help Center',
    fr: 'Recherchez dans notre Help Center'
  }
}
```

For reference, here is the list of all the translations for the `en-us` locale:

```coffee
translations: {
  categories: {
    'en-us': 'Categories'
  },
  change_query: {
    'en-us': 'Change your query'
  },
  clear_filters: {
    'en-us': 'clear your filters'
  },
  format_number: {
    'en-us': function (n) { return n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ','); }
  },
  filter: {
    'en-us': 'Filter results'
  },
  nb_results: {
    'en-us': function (nb) {
      return this.format_number(nb) + ' result' + (nb > 1 ? 's' : '');
    }
  },
  no_result_for: {
    'en-us': function (query) {
      return 'No result found for ' + this.quoted(query);
    }
  },
  no_result_actions: {
    'en-us': function () {
      return this.change_query + ' or ' + this.clear_filters;
    }
  },
  placeholder: {
    'en-us': 'Search in our articles'
  },
  quoted: {
    'en-us': function (text) { return '"' + escapeHTML(text) + '"'; }
  },
  stats: {
    'en-us': function (nbHits, processing) {
      return this.nb_results(nbHits) + ' found in ' + processing + ' ms';
    }
  },
  search_by_algolia: {
    'en-us': function (algolia) { return 'Search by ' + algolia; }
  },
  tags: {
    'en-us': 'Tags'
  }
}
```

### Localized tags

You can index localized tags based on locales prefix (e.g. `en-us` or `en`).
If we detect a locale, we'll only index localized tags for this translation.
For instance, an article with those tags:

```coffee
[
  'Wow',
  'en:Awesome',
  'en-gb:Good',
  'fr:Incroyable'
]
```

For `fr` and `fr-*` locales, we'll index `{ "label_names": ["Incroyable"] }`.
For `en-au`, `en-ca` and `en-us` locales, we'll index `{ "label_names": ["Awesome"] }`.
For the `en-gb` locale, we'll index `{ "label_names": ["Good"] }`.
For all the other locales, we'll index `{ "label_names": ["Wow"] }`.

### Zendesk Community search

We do not index community forums for now. If you're using them, you'll probably want to disable `instantsearch` by setting `enabled: false` and just use the auto-complete feature.

### Indexing private articles

Since we're providing a front-end search, and we can't securely know which access a user has in Zendesk's templates, we have to limit our indexing to public articles only.
A public article is not a draft and is visible to Everybody.
If you're in such a scenario, we recommend you to disable `instantsearch` by setting `enabled: false` and just use the auto-complete feature.

### Removing specific articles from the search results

You can let our script know that you'd want for an article not to be indexed. For this, all you need to do is to add an `algolia-ignore` tag on your article.
After the next reindex, the article should not be searchable anymore.

### Excluding portions of article from indexing

To prevent certain specific portion of your article to be indexed to Algolia, you can wrap the html source code of these portion between `<!-- algolia-ignore --> <!-- /algolia-ignore -->` tags. This way, these portions of text won't be searchable. 

Example:
```html
<h1>This is a test article</h1>
<!-- algolia-ignore -->
<p>
  This paragraph won't be indexed to Algolia.
</p>
<!-- /algolia-ignore -->
<p>
  This paragraph will be indexed to Algolia.
</p>
```

### Analytics

The `analytics` parameter enables searches capturing, for reports about popular queries, searches without results, and more. It defaults to `true`.

The `clickAnalytics` parameter enables click capturing in search results, for reports about the click rate and average position of clicks for specific queries. It defaults to `false`, as this feature is only accessible on our Enterprise plan.

With `clickAnalytics` enabled, you can use `algoliasearchZendeskHC.trackConversion()` on an article page to capture a “conversion” if your articles include Calls To Action.

### Modifying templates

__WARNING__: We don't provide any guarantee that we won't change the templates between versions.
If you chose to modify a template, you'll need to lock your version to MAJOR.MINOR.PATCH instead of just MAJOR in

```html
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/2/algoliasearch.zendesk-hc.min.css">
<script type="text/javascript" src="//cdn.jsdelivr.net/algoliasearch.zendesk-hc/2/algoliasearch.zendesk-hc.min.js"></script>
```

The latest version is [![version](https://img.shields.io/npm/v/algoliasearch.zendesk-hc.png)](https://www.npmjs.com/package/algoliasearch.zendesk-hc).

With your version locked in place, you can now look at [`templates.js`](https://github.com/algolia/algoliasearch-zendesk/blob/master/app/src/templates.js) to know which keys you can override.
The code here is ES6, you'll need to rewrite your custom template using Vanilla JavaScript instead.
Also, some templates are using a `compile` function in this file. This function is internally calling the [`Hogan.js` template engine](http://mustache.github.io/mustache.5.html) with square brackets instead of braces (because Zendesk templates already use braces). This function is available using `algoliasearchZendeskHC.compile`.

### Whitelisting our IPs

In case you're using Zendesk's [IP restrictions feature](https://support.zendesk.com/hc/en-us/articles/203663706-Restricting-access-to-Zendesk-Support-and-your-Help-Center-using-IP-restrictions), you'll need to whitelist our IPs for our indexing to work.
Here are those IPs:
- `3.221.200.5`
- `52.204.20.39`
- `52.22.248.248`

## Development

The `package.json` holds multiple scripts:
- `build:css`: Compiles the CSS files to `dist/algoliasearch.zendesk-hc.css`
- `build:docs`: Extracts the documentation from this `README.md` to [`../docs/documentation.md`](../docs/documentation.md)
- `build:js`: Compiles the JS files to `dist/algoliasearch.zendesk-hc.js` and `dist-es5-module/*.js`
- `build`: Launches all 3 previous builds
- `clean`: Removes `dist/` and `dist-es5-module`
- `dev`: Launches `build` and `server`, and watches the files to rebuild them if needed
- `lint`: Lints the JS files
- `server`: Runs a simple HTTP server pointing to `dist/`
- `test:coverage`: Runs `test` with coverage enabled
- `test`: Runs the test suite

`build:js`, `build:css`, `build` and `dev` can be passed a `NODE_ENV` environment variable.
If set to production, it also creates minified files and map files.

`server` accepts a `PORT` environment variable to change on which port it will run.

### Example

```sh
$ PORT=3005 npm run dev

> algoliasearch.zendesk-hc@2.22.3 dev /Users/jerska/algolia/zendesk/app
> gulp dev

[13:59:53] Failed to load external module @babel/register
[13:59:53] Requiring external module babel-register
[13:59:56] Using gulpfile ~/algolia/zendesk/app/gulpfile.babel.js
[13:59:56] Starting 'build:js:watch'...
[13:59:56] Environment for 'build:js': NODE_ENV=development
[13:59:56] Starting 'build:css'...
[13:59:56] Environment for 'build:css': NODE_ENV=development
[13:59:56] Starting 'build:css:watcher'...
[13:59:56] Finished 'build:css:watcher' after 8.64 ms
[13:59:56] Starting 'build:docs'...
[13:59:56] Starting 'build:docs:watcher'...
[13:59:56] Finished 'build:docs:watcher' after 1.11 ms
[13:59:56] Starting 'server'...
[13:59:56] Finished 'server' after 42 ms
[13:59:56] Server started http://localhost:3005
[13:59:56] Finished 'build:docs' after 66 ms
[13:59:56] Starting 'build:docs:watch'...
[13:59:56] Finished 'build:docs:watch' after 40 μs
[13:59:56] Finished 'build:css' after 109 ms
[13:59:56] Starting 'build:css:watch'...
[13:59:56] Finished 'build:css:watch' after 3.4 μs
[14:00:00] Finished 'build:js:watch' after 4.05 s
[14:00:00] Starting 'dev'...
[14:00:00] Finished 'dev' after 2.68 μs
```

When running, you can then add this custom script to your Help Center, inside the Document Head template:

```html
<link rel="stylesheet" type="text/css" href="http://localhost:3005/dist/algoliasearch.zendesk-hc.css">
<script type="text/javascript" src="http://localhost:3005/dist/algoliasearch.zendesk-hc.js"></script>
<script type="text/javascript">
  algoliasearchZendeskHC({
    applicationId: 'FIXME',
    apiKey: 'FIXME',
    subdomain: 'FIXME',
  })
</script>
```

This might however not load, due to trying to load HTTP content on an HTTPS site.
Some browsers will prevent the connection and print warnings in your browser console.  
In this case, you'll need to authorize insecure loading.
This will most often be hidden behind a shield icon or the green lock icon in your location bar.  
For instance, on Firefox: click the lock icon in the location bar > Right arrow with label "Show connection details" > Disable protection for now

### Documentation

To update the documentation of the project, you only need to update this README.
To propagate the changes to the `docs/` website, you simply need to run:

```sh
npm run build:docs
```

## Contributing

We're considering any contribution and PR, please go ahead!

## License

This project is under the [MIT License](../LICENSE).
