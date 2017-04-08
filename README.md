# api documentation for  [i18n (v0.8.3)](http://github.com/mashpie/i18n-node)  [![npm package](https://img.shields.io/npm/v/npmdoc-i18n.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-i18n) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-i18n.svg)](https://travis-ci.org/npmdoc/node-npmdoc-i18n)
#### lightweight translation module with dynamic json storage

[![NPM](https://nodei.co/npm/i18n.png?downloads=true)](https://www.npmjs.com/package/i18n)

[![apidoc](https://npmdoc.github.io/node-npmdoc-i18n/build/screenCapture.buildNpmdoc.browser.%252Fhome%252Ftravis%252Fbuild%252Fnpmdoc%252Fnode-npmdoc-i18n%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-i18n/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-i18n/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-i18n/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Marcus Spiegel",
        "email": "marcus.spiegel@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/mashpie/i18n-node/issues"
    },
    "dependencies": {
        "debug": "*",
        "make-plural": "^3.0.3",
        "math-interval-parser": "^1.1.0",
        "messageformat": "^0.3.1",
        "mustache": "*",
        "sprintf-js": ">=1.0.3"
    },
    "description": "lightweight translation module with dynamic json storage",
    "devDependencies": {
        "async": "*",
        "cookie-parser": "^1.4.1",
        "express": "^4.13.4",
        "jshint": "*",
        "mocha": "*",
        "should": "*",
        "sinon": "*",
        "url": "^0.11.0",
        "zombie": "*"
    },
    "directories": {
        "lib": "."
    },
    "dist": {
        "shasum": "2d8cf1c24722602c2041d01ba6ae5eaa51388f0e",
        "tarball": "https://registry.npmjs.org/i18n/-/i18n-0.8.3.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "gitHead": "523fa8e6f41850b793120c63c8392049b94f3e49",
    "homepage": "http://github.com/mashpie/i18n-node",
    "keywords": [
        "template",
        "i18n",
        "l10n"
    ],
    "license": "MIT",
    "main": "./index",
    "maintainers": [
        {
            "name": "mashpie",
            "email": "marcus.spiegel@gmail.com"
        }
    ],
    "name": "i18n",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/mashpie/i18n-node.git"
    },
    "scripts": {
        "jshint": "jshint --verbose .",
        "test": "npm run jshint && make test",
        "test-ci": "npm run jshint && istanbul cover ./node_modules/mocha/bin/_mocha"
    },
    "version": "0.8.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module i18n](#apidoc.module.i18n)
1.  [function <span class="apidocSignatureSpan">i18n.</span>__ (phrase)](#apidoc.element.i18n.__)
1.  [function <span class="apidocSignatureSpan">i18n.</span>__h (phrase)](#apidoc.element.i18n.__h)
1.  [function <span class="apidocSignatureSpan">i18n.</span>__l (phrase)](#apidoc.element.i18n.__l)
1.  [function <span class="apidocSignatureSpan">i18n.</span>__mf (phrase)](#apidoc.element.i18n.__mf)
1.  [function <span class="apidocSignatureSpan">i18n.</span>__n (singular, plural, count)](#apidoc.element.i18n.__n)
1.  [function <span class="apidocSignatureSpan">i18n.</span>addLocale (locale)](#apidoc.element.i18n.addLocale)
1.  [function <span class="apidocSignatureSpan">i18n.</span>configure (opt)](#apidoc.element.i18n.configure)
1.  [function <span class="apidocSignatureSpan">i18n.</span>getCatalog (object, locale)](#apidoc.element.i18n.getCatalog)
1.  [function <span class="apidocSignatureSpan">i18n.</span>getLocale (request)](#apidoc.element.i18n.getLocale)
1.  [function <span class="apidocSignatureSpan">i18n.</span>getLocales ()](#apidoc.element.i18n.getLocales)
1.  [function <span class="apidocSignatureSpan">i18n.</span>init (request, response, next)](#apidoc.element.i18n.init)
1.  [function <span class="apidocSignatureSpan">i18n.</span>removeLocale (locale)](#apidoc.element.i18n.removeLocale)
1.  [function <span class="apidocSignatureSpan">i18n.</span>setLocale (object, locale, skipImplicitObjects)](#apidoc.element.i18n.setLocale)
1.  object <span class="apidocSignatureSpan">i18n.</span>locales
1.  string <span class="apidocSignatureSpan">i18n.</span>version



# <a name="apidoc.module.i18n"></a>[module i18n](#apidoc.module.i18n)

#### <a name="apidoc.element.i18n.__"></a>[function <span class="apidocSignatureSpan">i18n.</span>__ (phrase)](#apidoc.element.i18n.__)
- description and source-code
```javascript
function i18nTranslate(phrase) {
  var msg;
  var argv = parseArgv(arguments);
  var namedValues = argv[0];
  var args = argv[1];

  // called like __({phrase: "Hello", locale: "en"})
  if (typeof phrase === 'object') {
    if (typeof phrase.locale === 'string' && typeof phrase.phrase === 'string') {
      msg = translate(phrase.locale, phrase.phrase);
    }
  }
  // called like __("Hello")
  else {
    // get translated message with locale from scope (deprecated) or object
    msg = translate(getLocaleFromObject(this), phrase);
  }

  // postprocess to get compatible to plurals
  if (typeof msg === 'object' && msg.one) {
    msg = msg.one;
  }

  // in case there is no 'one' but an 'other' rule
  if (typeof msg === 'object' && msg.other) {
    msg = msg.other;
  }

  // head over to postProcessing
  return postProcess(msg, namedValues, args);
}
```
- example usage
```shell
...

'''js
i18n.configure({
    locales:['en', 'de'],
    directory: __dirname + '/locales'
});
'''
now you are ready to use a global 'i18n.__('Hello')'.

## Example usage in global scope

In your cli, when not registered to a specific object:

'''js
var greeting = i18n.__('Hello');
...
```

#### <a name="apidoc.element.i18n.__h"></a>[function <span class="apidocSignatureSpan">i18n.</span>__h (phrase)](#apidoc.element.i18n.__h)
- description and source-code
```javascript
function i18nTranslationHash(phrase) {
  var translations = [];
  Object.keys(locales).sort().forEach(function(l) {
    var hash = {};
    hash[l] = i18n.__({ phrase: phrase, locale: l });
    translations.push(hash);
  });
  return translations;
}
```
- example usage
```shell
...
app.get( __l('/:locale/products/:id?'), function (req, res) {
    // guess what you might use req.params.locale for?
});
'''

> i18n.__ln() to get plurals will come up in another release...

### i18n.__h()

Returns a hashed list of translations for a given phrase in each language.

'''js
i18n.__h('Hello'); // --> [ { de: 'Hallo' }, { en: 'Hello' } ]
'''
...
```

#### <a name="apidoc.element.i18n.__l"></a>[function <span class="apidocSignatureSpan">i18n.</span>__l (phrase)](#apidoc.element.i18n.__l)
- description and source-code
```javascript
function i18nTranslationList(phrase) {
  var translations = [];
  Object.keys(locales).sort().forEach(function(l) {
    translations.push(i18n.__({ phrase: phrase, locale: l }));
  });
  return translations;
}
```
- example usage
```shell
...

* Simple Variable Replacement (similar to mustache placeholders)
* SelectFormat (ie. switch msg based on gender)
* PluralFormat (see above and [ranges](#ranged-interval-support))

Combinations of those give superpower, but should get tested well (contribute your use case, please!) on integration.

### i18n.__l()

Returns a list of translations for a given phrase in each language.

'''js
i18n.__l('Hello'); // --> [ 'Hallo', 'Hello' ]
'''
...
```

#### <a name="apidoc.element.i18n.__mf"></a>[function <span class="apidocSignatureSpan">i18n.</span>__mf (phrase)](#apidoc.element.i18n.__mf)
- description and source-code
```javascript
function i18nMessageformat(phrase) {
  var msg, mf, f;
  var targetLocale = defaultLocale;
  var argv = parseArgv(arguments);
  var namedValues = argv[0];
  var args = argv[1];

  // called like __({phrase: "Hello", locale: "en"})
  if (typeof phrase === 'object') {
    if (typeof phrase.locale === 'string' && typeof phrase.phrase === 'string') {
      msg = phrase.phrase;
      targetLocale = phrase.locale;
    }
  }
  // called like __("Hello")
  else {
    // get translated message with locale from scope (deprecated) or object
    msg = phrase;
    targetLocale = getLocaleFromObject(this);
  }

  msg = translate(targetLocale, msg);
  // --- end get msg

  // now head over to Messageformat
  // and try to cache instance
  if (MessageformatInstanceForLocale[targetLocale]) {
    mf = MessageformatInstanceForLocale[targetLocale];
  } else {
    mf = new Messageformat(targetLocale);
    mf.compiledFunctions = {};
    MessageformatInstanceForLocale[targetLocale] = mf;
  }

  // let's try to cache that function
  if (mf.compiledFunctions[msg]) {
    f = mf.compiledFunctions[msg];
  } else {
    f = mf.compile(msg);
    mf.compiledFunctions[msg] = f;
  }

  return postProcess(f(namedValues), namedValues, args);
}
```
- example usage
```shell
...
__n('%s cat', 5); // --> 5 кошек
__n('%s cat', 6); // --> 6 кошек
__n('%s cat', 21); // --> 21 кошка
'''

> __Note__ i18n.__n() will add a blueprint ("one, other" or "one, few, other" for eaxmple) for each locale to your json on updateFiles
 in a future version.

### i18n.__mf()

Supports the advanced MessageFormat as provided by excellent [messageformat module](https://www.npmjs.com/package/messageformat).
You should definetly head over to [messageformat.github.io](https://messageformat.github.io) for a guide to MessageFormat. i18n
takes care of 'new MessageFormat('en').compile(msg);' with the current 'msg' loaded from it's json files and cache that complied
 fn in memory. So in short you might use it similar to '__()' plus extra object to accomblish MessageFormat's formating. Ok, some
 examples:

'''js
// assume res is set to german
res.setLocale('de');
...
```

#### <a name="apidoc.element.i18n.__n"></a>[function <span class="apidocSignatureSpan">i18n.</span>__n (singular, plural, count)](#apidoc.element.i18n.__n)
- description and source-code
```javascript
function i18nTranslatePlural(singular, plural, count) {
  var msg, namedValues, targetLocale, args = [];

  // Accept an object with named values as the last parameter
  if (argsEndWithNamedObject(arguments)) {
    namedValues = arguments[arguments.length - 1];
    args = arguments.length >= 5 ? Array.prototype.slice.call(arguments, 3, -1) : [];
  } else {
    namedValues = {};
    args = arguments.length >= 4 ? Array.prototype.slice.call(arguments, 3) : [];
  }

  // called like __n({singular: "%s cat", plural: "%s cats", locale: "en"}, 3)
  if (typeof singular === 'object') {
    if (
      typeof singular.locale === 'string' &&
      typeof singular.singular === 'string' &&
      typeof singular.plural === 'string'
    ) {
      targetLocale = singular.locale;
      msg = translate(singular.locale, singular.singular, singular.plural);
    }
    args.unshift(count);

    // some template engines pass all values as strings -> so we try to convert them to numbers
    if (typeof plural === 'number' || parseInt(plural, 10) + '' === plural) {
      count = plural;
    }

    // called like __n({singular: "%s cat", plural: "%s cats", locale: "en", count: 3})
    if (typeof singular.count === 'number' || typeof singular.count === 'string') {
      count = singular.count;
      args.unshift(plural);
    }
  } else {
    // called like  __n('cat', 3)
    if (typeof plural === 'number' || parseInt(plural, 10) + '' === plural) {
      count = plural;

      // we add same string as default
      // which efectivly copies the key to the plural.value
      // this is for initialization of new empty translations
      plural = singular;

      args.unshift(count);
      args.unshift(plural);
    }
    // called like __n('%s cat', '%s cats', 3)
    // get translated message with locale from scope (deprecated) or object
    msg = translate(getLocaleFromObject(this), singular, plural);
    targetLocale = getLocaleFromObject(this);
  }

  if (count === null) count = namedValues.count;

  // enforce number
  count = parseInt(count, 10);

  // find the correct plural rule for given locale
  if (typeof msg === 'object') {
    var p;
    // create a new Plural for locale
    // and try to cache instance
    if (PluralsForLocale[targetLocale]) {
      p = PluralsForLocale[targetLocale];
    } else {
      // split locales with a region code
      var lc = targetLocale.toLowerCase().split(/[_-\s]+/)
        .filter(function(el){ return true && el; });
      // take the first part of locale, fallback to full locale
      p = new MakePlural(lc[0] || targetLocale);
      PluralsForLocale[targetLocale] = p;
    }

    // fallback to 'other' on case of missing translations
    msg = msg[p(count)] || msg.other;
  }

  // head over to postProcessing
  return postProcess(msg, namedValues, args, count);
}
```
- example usage
```shell
...

// passing specific locale
__({phrase: 'Hello', locale: 'fr'}); // Salut
__({phrase: 'Hello %s', locale: 'fr'}, 'Marcus'); // Salut Marcus
__({phrase: 'Hello function <span class="apidocSignatureSpan">i18n.</span>__n', locale: 'fr'}, { name: 'Marcus' }); // Salut Marcus
'''

### i18n.__n()

Plurals translation of a single phrase. Singular and plural forms will get added to locales if unknown. Returns translated parsed
 and substituted string based on last 'count' parameter.

'''js
// short syntax is best suited for reading
// --> writes '%s cat' to both 'one' and 'other' plurals
__n('%s cat', 1) // --> 1 Katze
...
```

#### <a name="apidoc.element.i18n.addLocale"></a>[function <span class="apidocSignatureSpan">i18n.</span>addLocale (locale)](#apidoc.element.i18n.addLocale)
- description and source-code
```javascript
function i18nAddLocale(locale) {
  read(locale);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.i18n.configure"></a>[function <span class="apidocSignatureSpan">i18n.</span>configure (opt)](#apidoc.element.i18n.configure)
- description and source-code
```javascript
function i18nConfigure(opt) {

  // reset locales
  locales = {};

  // Provide custom API method aliases if desired
  // This needs to be processed before the first call to applyAPItoObject()
  if (opt.api && typeof opt.api === 'object') {
    for (var method in opt.api) {
      if (opt.api.hasOwnProperty(method)) {
        var alias = opt.api[method];
        if (typeof api[method] !== 'undefined') {
          api[method] = alias;
        }
      }
    }
  }

  // you may register i18n in global scope, up to you
  if (typeof opt.register === 'object') {
    register = opt.register;
    // or give an array objects to register to
    if (Array.isArray(opt.register)) {
      register = opt.register;
      register.forEach(function(r) {
        applyAPItoObject(r);
      });
    } else {
      applyAPItoObject(opt.register);
    }
  }

  // sets a custom cookie name to parse locale settings from
  cookiename = (typeof opt.cookie === 'string') ? opt.cookie : null;

  // query-string parameter to be watched - @todo: add test & doc
  queryParameter = (typeof opt.queryParameter === 'string') ? opt.queryParameter : null;

  // where to store json files
  directory = (typeof opt.directory === 'string') ?
    opt.directory : path.join(__dirname, 'locales');

  // permissions when creating new directories
  directoryPermissions = (typeof opt.directoryPermissions === 'string') ?
    parseInt(opt.directoryPermissions, 8) : null;

  // write new locale information to disk
  updateFiles = (typeof opt.updateFiles === 'boolean') ? opt.updateFiles : true;

  // sync locale information accros all files
  syncFiles = (typeof opt.syncFiles === 'boolean') ? opt.syncFiles : false;

  // what to use as the indentation unit (ex: "\t", "  ")
  indent = (typeof opt.indent === 'string') ? opt.indent : '\t';

  // json files prefix
  prefix = (typeof opt.prefix === 'string') ? opt.prefix : '';

  // where to store json files
  extension = (typeof opt.extension === 'string') ? opt.extension : '.json';

  // setting defaultLocale
  defaultLocale = (typeof opt.defaultLocale === 'string') ? opt.defaultLocale : 'en';

  // auto reload locale files when changed
  autoReload = (typeof opt.autoReload === 'boolean') ? opt.autoReload : false;

  // enable object notation?
  objectNotation = (typeof opt.objectNotation !== 'undefined') ? opt.objectNotation : false;
  if (objectNotation === true) objectNotation = '.';

  // read language fallback map
  fallbacks = (typeof opt.fallbacks === 'object') ? opt.fallbacks : {};

  // setting custom logger functions
  logDebugFn = (typeof opt.logDebugFn === 'function') ? opt.logDebugFn : debug;
  logWarnFn = (typeof opt.logWarnFn === 'function') ? opt.logWarnFn : warn;
  logErrorFn = (typeof opt.logErrorFn === 'function') ? opt.logErrorFn : error;

  // when missing locales we try to guess that from directory
  opt.locales = opt.locales || guessLocales(directory);

  // implicitly read all locales
  if (Array.isArray(opt.locales)) {

    opt.locales.forEach(function(l) {
      read(l);
    });

    // auto reload locale files when changed
    if (autoReload) {

      // watch changes of locale files (it's called twice because fs.watch is still unstable)
      fs.watch(directory, function(event, filename) {
        var localeFromFile = guessLocaleFromFile(filename);

        if (localeFromFile && opt.locales.indexOf(localeFromFile) > -1) {
          logDebug('Auto reloading locale file "' + filename + '".');
          read(localeFromFile);
        }

      });
    }
  }
}
```
- example usage
```shell
...
'''

## Configure

Minimal example, just setup two locales and a project specific directory

'''js
i18n.configure({
    locales:['en', 'de'],
    directory: __dirname + '/locales'
});
'''
now you are ready to use a global 'i18n.__('Hello')'.

## Example usage in global scope
...
```

#### <a name="apidoc.element.i18n.getCatalog"></a>[function <span class="apidocSignatureSpan">i18n.</span>getCatalog (object, locale)](#apidoc.element.i18n.getCatalog)
- description and source-code
```javascript
function i18nGetCatalog(object, locale) {
  var targetLocale;

  // called like i18n.getCatalog(req)
  if (typeof object === 'object' && typeof object.locale === 'string' && locale === undefined) {
    targetLocale = object.locale;
  }

  // called like i18n.getCatalog(req, 'en')
  if (!targetLocale && typeof object === 'object' && typeof locale === 'string') {
    targetLocale = locale;
  }

  // called like req.getCatalog('en')
  if (!targetLocale && locale === undefined && typeof object === 'string') {
    targetLocale = object;
  }

  // called like req.getCatalog()
  if (!targetLocale &&
    object === undefined &&
    locale === undefined &&
    typeof this.locale === 'string'
  ) {
    if (register && register.GLOBAL) {
      targetLocale = '';
    } else {
      targetLocale = this.locale;
    }
  }

  // called like i18n.getCatalog()
  if (targetLocale === undefined || targetLocale === '') {
    return locales;
  }

  if (!locales[targetLocale] && fallbacks[targetLocale]) {
    targetLocale = fallbacks[targetLocale];
  }

  if (locales[targetLocale]) {
    return locales[targetLocale];
  } else {
    logWarn('No catalog found for "' + targetLocale + '"');
    return false;
  }
}
```
- example usage
```shell
...

'''js
getLocale(); // --> de
getLocale(req); // --> de
req.getLocale(); // --> de
'''

### i18n.getCatalog()

Returns a whole catalog optionally based on current scope and locale.

'''js
getCatalog(); // returns all locales
getCatalog('de'); // returns just 'de'
...
```

#### <a name="apidoc.element.i18n.getLocale"></a>[function <span class="apidocSignatureSpan">i18n.</span>getLocale (request)](#apidoc.element.i18n.getLocale)
- description and source-code
```javascript
function i18nGetLocale(request) {

  // called like i18n.getLocale(req)
  if (request && request.locale) {
    return request.locale;
  }

  // called like req.getLocale()
  return this.locale || defaultLocale;
}
```
- example usage
```shell
...

or disable inheritance by passing true as third parameter:

'''js
i18n.setLocale(res, 'ar', true); // --> req: Hallo res: مرحبا res.locals: Hallo
'''

### i18n.getLocale()

Getting the current locale (ie.: 'en') from current scope or globally.

'''js
getLocale(); // --> de
getLocale(req); // --> de
req.getLocale(); // --> de
...
```

#### <a name="apidoc.element.i18n.getLocales"></a>[function <span class="apidocSignatureSpan">i18n.</span>getLocales ()](#apidoc.element.i18n.getLocales)
- description and source-code
```javascript
function i18nGetLocales() {
  return Object.keys(locales);
}
```
- example usage
```shell
...
    * __fixed__: typos, missing and wrong docs, plural bugs like: #210, #191, #190
* 0.7.0:
    * __improved__: 'i18n.setLocale()' and 'i18n.init()' refactored to comply with most common use cases, much better test coverage
 and docs
    * __new__: options: 'autoReload', 'directoryPermissions', 'register', 'queryParameter', read locales from filenames with empty
 'locales' option (#134)
    * __fixed__: typos, missing and wrong docs, issues related to 'i18n.setLocale()'
* 0.6.0:
    * __improved__: Accept-Language header parsing to ICU, delimiters with object notation, jshint, package.json, README;
    * __new__: prefix for locale files, 'i18n.getLocales()', custom logger, fallback[s];
    * __fixed__: typos, badges, plural (numbers), 'i18n.setLocale()' for 'req' _and_ 'res'
* 0.5.0: feature release; added {{mustache}} parsing by #85, added "object.notation" by #110, fixed buggy req.__() implementation
 by #111 and closed 13 issues
* 0.4.1: stable release; merged/closed: #57, #60, #67 typo fixes; added more examples and new features: #53, #65, #66 - and some
 more api reference
* 0.4.0: stable release; closed: #22, #24, #4, #10, #54; added examples, clarified concurrency usage in different template engines
, added 'i18n.getCatalog'
* 0.3.9: express.js usage, named api, jscoverage + more test, refactored configure, closed: #51, #20, #16, #49
* 0.3.8: fixed: #44, #49; merged: #47, #45, #50; added: #33; updated: README
* 0.3.7: tests by mocha.js, added 'this.locale' to '__' and '__n'
...
```

#### <a name="apidoc.element.i18n.init"></a>[function <span class="apidocSignatureSpan">i18n.</span>init (request, response, next)](#apidoc.element.i18n.init)
- description and source-code
```javascript
function i18nInit(request, response, next) {
  if (typeof request === 'object') {

    // guess requested language/locale
    guessLanguage(request);

    // bind api to req
    applyAPItoObject(request);

    // looks double but will ensure schema on api refactor
    i18n.setLocale(request, request.locale);
  } else {
    return logError('i18n.init must be called with one parameter minimum, ie. i18n.init(req)');
  }

  if (typeof response === 'object') {
    applyAPItoObject(response);

    // and set that locale to response too
    i18n.setLocale(response, request.locale);
  }

  // head over to next callback when bound as middleware
  if (typeof next === 'function') {
    return next();
  }
}
```
- example usage
```shell
...

In case of cookie you will also need to enable cookies for your application. For express this done by adding 'app.use(express.cookieParser
())'). Now use the same cookie name when setting it in the user preferred language, like here:

'''js
res.cookie('yourcookiename', 'de', { maxAge: 900000, httpOnly: true });
'''

After this and until the cookie expires, 'i18n.init()' will get the value of the cookie to set that language instead of default
for every page.

#### Some words on 'register' option

Esp. when used in a cli like scriptyou won't use any 'i18n.init()' to guess language settings from your user. Thus 'i18n' won't
bind itself to any 'res' or 'req' object and will work like a static module.

'''js
var anyObject = {};
...
```

#### <a name="apidoc.element.i18n.removeLocale"></a>[function <span class="apidocSignatureSpan">i18n.</span>removeLocale (locale)](#apidoc.element.i18n.removeLocale)
- description and source-code
```javascript
function i18nRemoveLocale(locale) {
  delete locales[locale];
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.i18n.setLocale"></a>[function <span class="apidocSignatureSpan">i18n.</span>setLocale (object, locale, skipImplicitObjects)](#apidoc.element.i18n.setLocale)
- description and source-code
```javascript
function i18nSetLocale(object, locale, skipImplicitObjects) {

  // when given an array of objects => setLocale on each
  if (Array.isArray(object) && typeof locale === 'string') {
    for (var i = object.length - 1; i >= 0; i--) {
      i18n.setLocale(object[i], locale, true);
    }
    return i18n.getLocale(object[0]);
  }

  // defaults to called like i18n.setLocale(req, 'en')
  var targetObject = object;
  var targetLocale = locale;

  // called like req.setLocale('en') or i18n.setLocale('en')
  if (locale === undefined && typeof object === 'string') {
    targetObject = this;
    targetLocale = object;
  }

  // consider a fallback
  if (!locales[targetLocale] && fallbacks[targetLocale]) {
    targetLocale = fallbacks[targetLocale];
  }

  // now set locale on object
  targetObject.locale = locales[targetLocale] ? targetLocale : defaultLocale;

  // consider any extra registered objects
  if (typeof register === 'object') {
    if (Array.isArray(register) && !skipImplicitObjects) {
      register.forEach(function(r) {
        r.locale = targetObject.locale;
      });
    } else {
      register.locale = targetObject.locale;
    }
  }

  // consider res
  if (targetObject.res && !skipImplicitObjects) {

    // escape recursion
    // @see  - https://github.com/balderdashy/sails/pull/3631
    //       - https://github.com/mashpie/i18n-node/pull/218
    if (targetObject.res.locals) {
      i18n.setLocale(targetObject.res, targetObject.locale, true);
      i18n.setLocale(targetObject.res.locals, targetObject.locale, true);
    } else {
      i18n.setLocale(targetObject.res, targetObject.locale);
    }
  }

  // consider locals
  if (targetObject.locals && !skipImplicitObjects) {

    // escape recursion
    // @see  - https://github.com/balderdashy/sails/pull/3631
    //       - https://github.com/mashpie/i18n-node/pull/218
    if (targetObject.locals.res) {
      i18n.setLocale(targetObject.locals, targetObject.locale, true);
      i18n.setLocale(targetObject.locals.res, targetObject.locale, true);
    } else {
      i18n.setLocale(targetObject.locals, targetObject.locale);
    }
  }

  return i18n.getLocale(targetObject);
}
```
- example usage
```shell
...
var anyObject = {};

i18n.configure({
  locales: ['en', 'de'],
  register: anyObject
});

anyObject.setLocale('de');
anyObject.__('Hallo'); // --> Hallo'
'''

Cli usage is a special use case, as we won't need to maintain any transaction / concurrency aware setting of locale, so you could
 even choose to bind 'i18n' to _global_ scope of node:

'''js
i18n.configure({
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
