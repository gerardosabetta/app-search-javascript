# Javascript client for the Swiftype App Search Api

**Note: Swiftype App Search is currently in beta**

## Getting Started
### Install from a CDN

The easiest way to install this client is to simply include the built distribution from the [jsDelivr](https://www.jsdelivr.com/) CDN.

```html
<script src="https://cdn.jsdelivr.net/npm/swiftype-app-search-javascript@1.0.3"></script>
```

This will make the client available globally at:

```javascript
window.SwiftypeAppSearch
```

### Install from NPM

This package can also be installed with `npm` or `yarn`.

```
npm install --save swiftype-app-search-javascript
```

The client could then be included into your project like follows:

```javascript
// CommonJS
var SwiftypeAppSearch = require('swiftype-app-search-javascript')

// ES
import * as SwiftypeAppSearch from 'swiftype-app-search-javascript'
```

## Usage

### Setup: Configuring the client and authentication

Using this client assumes that you have already created an [App Search](https://swiftype.com/app-search) account, and subsequently created an Engine. You'll need to configure the client with the name of your Engine and your authentication credentials, which can be found here: https://app.swiftype.com/as/credentials.

- accountHostKey -> Your "Account Key", should start with `host-`
- apiKey -> A read-only "API Key" *

```javascript
var client = SwiftypeAppSearch.createClient({
  accountHostKey: 'host-c5s2mj',
  apiKey: 'search-mu75psc5egt9ppzuycnc2mc3',
  engineName: 'favorite-videos'
})
```

\* Please note that you should only ever use a read-only API Key within Javascript code on the browser. By default, your account should have a Key prefixed with `search-` that is read-only. More information can be found here: https://swiftype.com/documentation/app-search/understanding-api-authentication.

### Searching

```javascript
var options = {
  search_fields: {title: {}},
  result_fields: {id: {raw: {}}, title: {raw: {}}}
}

client.search('cat', options).then((resultList) => {
  resultList.results.forEach((result) => {
    console.log(`id: ${result.getRaw('id')} raw: ${result.getRaw('title')}`)
  })
}).catch((error) => {
  console.log(`error: ${error}`)
})
```

Note that `options` supports all options listed here: https://swiftype.com/documentation/app-search/guides/searching.

## Build

```bash
yarn install
yarn build
```

## Contributions

  To contribute code to this gem, please fork the repository and submit a pull request.
