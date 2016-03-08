# react-i18n-components
Simple i18n translation and localization components for React applications.

[![npm version](https://badge.fury.io/js/react-i18n-components.svg)](https://badge.fury.io/js/react-i18n-components)

## Preparation

To start using this library, first install the package:
```
npm i react-i18n-components --save
```

Next, load translations and set the locale to be used:
```javascript
var I18n = require('react-i18n-components').I18n;

I18n.setTranslations({
  en: {
    application: {
      title: 'Awesome app with i18n!',
      hello: 'Hello, %{name}!'
    },
    date: {
      long: 'MMMM Do, YYYY'
    }
  },
  nl: {
    application: {
      title: 'Toffe app met i18n!',
      hello: 'Hallo, %{name}!'
    },
    date: {
      long: 'D MMMM YYYY'
    }
  }
});

I18n.setLocale('nl');
```

Now you're all set up to start unleashing the power of `react-i18n-components`!

## Usage

### Translate

The prefered way to have translated texts in your app is by using the `Translate` component:
```javascript
var React = require('react');
var Translate = require('react-i18n-components').Translate;

var SomeComponent = React.createClass({
  render: function() {
    return (
      <div>
        <Translate value="application.title"/>
          // => returns '<span>Toffe app met i18n!</span>' for locale 'nl'
        <Translate value="application.hello" name="Aad"/>
          // => returns '<span>Hallo, Aad!</span>' for locale 'nl'
      </div>
    );
  }
});
```

If for some reason, you cannot use the component, you can use the `I18n.t` helper instead:
```javascript
var I18n = require('react-i18n-components').I18n;

I18n.t('application.title'); // => returns 'Toffe app met i18n!' for locale 'nl'
I18n.t('application.name', {name: 'Aad'}); // => returns 'Hallo, Aad!' for locale 'nl'
```

### Localize

This library supports the localization of both dates and numbers.

The prefered way of doing that is by using the `Localize` component:
```javascript
var React = require('react');
var Localize = require('react-i18n-components').Localize;

var SomeComponent = React.createClass({
  render: function() {
    return (
      <div>
        <Localize value="2015-09-03" dateFormat="date.long"/>
          // => returns '<span>3 september 2015</span> for locale 'nl'
        <Localize value={10/3} options={{style: 'currency', currency: 'EUR', minimumFractionDigits: 2, maximumFractionDigits: 2}}/>
          // => returns '<span>€ 3,33</span> for locale 'nl'
      </div>
    );
  }
});
```

Also here, If for some reason, you cannot use the component, there is the `I18n.l` helper to help you out:
```javascript
var I18n = require('react-i18n-components').I18n;

I18n.l(1385856000000, { dateFormat: 'date.long' }); // => returns '1 december 2013' for locale 'nl'
I18n.l(Math.PI, { maximumFractionDigits: 2 }); // => returns '3,14' for locale 'nl'
```

The localize component and helper support all date formatting options as provided by the Javascript `moment` library. For the full list of options, see http://momentjs.com/docs/#/displaying/format/.

For number formatting, the localize component and helper support all options  as provided by the Javascript built-in `Intl.NumberFormat` object. For the full list of options, see https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat.