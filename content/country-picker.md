+++
date = "2019-01-04T15:59:11+00:00"
title = "Country Picker"

+++
# Flow Country Picker

The Flow country picker is a javascript module that can be loaded on any website. It exposes the function `window.flow.countryPicker.createCountryPicker` which takes in an options object that will define its behavior. By default the country picker module will utilize the local Flow session cached in the browser or API calls to determine a list of countries to display. These behaviors can be changed via options provided to the country picker module.

## Installation

There are 3 steps to install the Flow country picker:

1. Place this script tag somewhere in the head of your website `<script src="https://cdn.flow.io/country-picker/js/v0/country-picker.js"/>`
2. Download the css from [here](https://cdn.flow.io/country-picker/example.css) and add it to your website. Use this as a foundation upon which you can add further style customizations to the country picker.
3. Add the following code next to existing Flow integration code or add it in a new script tag toward the bottom of the HTML document.

```JS3
  window.flow.countryPicker.createCountryPicker(optionsObject);
```

## Options Object

The options object is passed into our country picker functions and defines the functionality for the country picker. The options object is as follows:

```JavaScript
{
  type: String,
  logo: Boolean,
  containerId: String,
  currentExperience: Country,
  countries: [Country],
  onSelection: Function,
  onSessionUpdate: Function
  modalTitle: String,
  isDestination: Boolean,
}
```

* type: Decides what kind of country picker to render, the two types are 'modal' and 'dropdown', it defaults to 'dropdown'.
* logo: Toggles whether or not to display the country flag logo, defaults to true.
* containerId: The element that will be the country picker container, defaults to country-picker.
* currentExperience: The experience that is currently selected, defaults to the country object in the Flow session, if that isn't available it defaults to 'Select your Experience'.
* countries: An array of countries you wish to display, it defaults to using the Flow API to determine countries based on defined experiences (see /:organization/countries).
* onSelection: A function that is executed on country selection, it takes in a country object and returns a [session_put_form](/type/session-put-form). When implementing this property if you do not want the country picker to update session using Flow's session API just return undefined instead of a session_put_form.
* onSessionUpdate(callback): A function that is executed after the session API is called and the local storage session is updated. It takes in (status, session) where `session` is the updated session from the API. It is recommended to call window.location.reload() at the end of the function as it will no longer be called automatically.
* modalTitle: Defines the title of the modal defaults to 'Current Experience'.
* isDestination: If set to `true` the country picker will display all destination countries for the organization. For example, an experience for World will result in displaying available countries to users. This option defaults to `false`.

## Country Object

The country object is what the dropdown uses to display and set data, it is as follows:

```JavaScript
{
  iso_3166_3: String,
  currency: String,
  name: String,
  label: String,
  language: String,
  logoUrl: String
}
```

* iso_3166_3: ISO 3166 3-character country code. See https://api.flow.io/reference/countries
* currency: ISO 4217 3-character currency code. See https://api.flow.io/reference/currencies
* label: What actually shows up in the country picker, if no label is passed in it defaults to: `country.name + '(' + country.currency + ')'`
* language: ISO 639 2-character language code. See https://api.flow.io/reference/languages
* logoUrl: Url to the country flag logo, if no logo url is passed in it defaults to: `'https://flowcdn.io/util/icons/flags/24/' + country.code + '.png'`

## Styling

We provide example css rules that are customizable to fit your styling needs .

You can download our default CSS code from [here](https://cdn.flow.io/country-picker/example.css).

## Examples

Here is an example of a dropdown country picker

```JavaScript
window.flow.countryPicker.createCountryPicker({
  containerId: 'country-picker',
  modalTitle: 'Select an Experience',
  countries: [
    {
      "iso_3166_3": "AUS",
      "currency": "AUD",
      "name": "Australia",
      "label": "Australia (AUD)",
      "language": "en",
      "logoUrl": "https://flowcdn.io/util/icons/flags/24/aus.png"
    },
    ...
  ]
});
```

![Dropdown](https://cdn.flow.io/docs/dropdown-country-picker.png)

Here is an example of a modal country picker

```JavaScript
window.flow.countryPicker.createCountryPicker({
  type: 'modal',
  containerId: 'country-picker',
  modalTitle: 'Select an Experience',
  countries: [
    {
      "iso_3166_3": "AUS",
      "currency": "AUD",
      "name": "Australia",
      "label": "Australia (AUD)",
      "language": "en",
      "logoUrl": "https://flowcdn.io/util/icons/flags/24/aus.png"
    },
    ...
  ]
});
```

![Modal](https://cdn.flow.io/docs/modal-country-picker.png)

## Some Other Title

blah blah blah