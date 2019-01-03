+++
date = "2019-01-03T22:44:39+00:00"
draft = true

+++
\# Flow Features

Flow allows organizations to create features whose values are determined by the country or experience of their customers. The values can either be a boolean (true or false) or a text string. Features can be created in \[Console\]([https://console.flow.io](https://console.flow.io "https://console.flow.io")) by following the **Features** link under **Organization Settings**.

\## Dynamically insert text based on the country or experience

Using string features in Flow implementors can easily associate text with a country or experience. Flow.js provides a specific html attribute for this purpose, \`flow-string-feature\`. The value of this attribute should be the key of a Flow string feature and upon localization the innerText of this element will be assigned the value feature based on the query for that user.

Let's look at an example. Given the following feature,

\`\`\`

{

  "name": "Shipping Messaging",

  "key": "shipping-message",

  "status": "active",

  "type": "string",

  "rules": \[

    {

      "query": "experience.key:canada",

      "value": "FREE SHIPPING ON ORDERS OVER $100 CAD"

    },

    {

      "query": "experience.key:eurozone",

      "value": "FREE SHIPPING ON ORDERS OVER €75"

    },

    {

      "query": "experience.key:china",

      "value": "FREE SHIPPING ON ORDERS OVER 888元"

    },

    {

      "query": "experience.key: world",

      "value": "Subscribe for 15% off your first order."

    }

  \]

}

\`\`\`

and the the following markup,

\`\`\`html

  <span flow-string-feature="shipping-message"></span>

\`\`\`

The \`innerText\` of the span will be replaced with the text that corresponds to the experience of the user. So if a user is visiting from France, the markup will be rendered as

\`\`\`html

  <span flow-string-feature="shipping-message">FREE SHIPPING ON ORDERS OVER €75</span>

\`\`\`