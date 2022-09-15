---
teaser:
  text: Allows you to create forms to submit input fields in an SPZ document.
---

# spz-form

## Usage

The `spz-form` extension allows you to create forms (`<form>`) to submit input fields in an spz document. The `spz-form` extension also provides [polyfills](#polyfills) for some missing behaviors in browsers.

[tip type="important"]

If you're submitting data in your form, your server endpoint must implement the requirements for [CORS security]

[/tip]

Before creating a `<form>`, you must include the required script for the `<spz-form>` extension, otherwise your document will be invalid. If you're using `input` tags for purposes other than submitting their values (e.g., inputs not inside a `<form>`), you do not need to load the `spz-form` extension.

[example preview="inline" playground="true" imports="spz-form" template="spz-mustache"]

```html
<form method="post"
    action-xhr="https://example.com/subscribe"{% if not format=='email'%}
    target="_top"{% endif %}>
    <fieldset>
      <label>
        <span>Name:</span>
        <input type="text"
          name="name"
          required>
      </label>
      <br>
      <label>
        <span>Email:</span>
        <input type="email"
          name="email"
          required>
      </label>
      <br>
      <input type="submit"
        value="Subscribe">
    </fieldset>
    <div submit-success>
      <template type="spz-mustache">
        Subscription successful!
      </template>
    </div>
    <div submit-error>
      <template type="spz-mustache">
        Subscription failed!
      </template>
    </div>
  </form>
```

[/example]

### Inputs and fields

#### Allowed

[filter formats="websites, ads"]

-   Other form-related elements, including: `<textarea>`, `<select>`, `<option>`, `<fieldset>`, `<label>`, `<input type=text>`, `<input type=submit>`, and so on.
-   `<input type=password>` and `<input type=file>` inside of `<form method=POST action-xhr>`.
-   [`spz-selector`](https://spz.dev/documentation/components/spz-selector)

[/filter]<!-- formats="websites, ads" -->

[filter formats="email"]

-   Other form-related elements, including: `<textarea>`, `<select>`, `<option>`, `<fieldset>`, `<label>`, `<input type=text>`, `<input type=submit>`, and so on.
-   [`spz-selector`](https://spz.dev/documentation/components/spz-selector)

[/filter]<!-- formats="email" -->

#### Not Allowed

[filter formats="websites, ads"]

-   `<input type=button>`, `<input type=image>`
-   Most of the form-related attributes on inputs including: `form`, `formaction`, `formtarget`, `formmethod` and others.

[/filter]<!-- formats="websites, ads" -->

[filter formats="email"]

-   `<input type=button>`, `<input type=image>`
-   `<input type=password>` and `<input type=file>`
-   Most of the form-related attributes on inputs including: `form`, `formaction`, `formtarget`, `formmethod` and others.

[/filter]<!-- formats="email" -->

(Relaxing some of these rules might be reconsidered in the future - [please let us know] if you require these and provide use cases).

For details on valid inputs and fields, see [spz-form rules]) in the spz validator specification.

### Success and error response rendering

You can render success or error responses in your form by using [spz-mustache](../spz-mustache/spz-mustache.md), or success responses through data binding with [spz-bind](../spz-bind/spz-bind.md) and the following response attributes:

[filter formats="websites, ads"]

| Response attribute | Description                                                                                                                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `submit-success`   | Can be used to display a success message if the response is successful (i.e., has a status of `2XX`).                                                                                                                                                                  |
| `submit-error`     | Can be used to display a submission error if the response is unsuccessful (i.e., does not have a status of `2XX`).                                                                                                                                                     |
| `submitting`       | Can be used to display a message when the form is submitting. The template for this attribute has access to the form's input fields for any display purposes. Please see the [full form example below](#example-submitting) for how to use the `submitting` attribute. |

[/filter]<!-- formats="websites, ads" -->

[filter formats="email"]

| Response attribute | Description                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `submit-success`   | Can be used to display a success message if the response is successful (i.e., has a status of `2XX`).                                                                  |
| `submit-error`     | Can be used to display a submission error if the response is unsuccessful (i.e., does not have a status of `2XX`).                                                     |
| `submitting`       | Can be used to display a message when the form is submitting. Please see the [full form example below](#example-submitting) for how to use the `submitting` attribute. |

[/filter]<!-- formats="email" -->

#### To render responses with templating:

-   Apply a response attribute to any descendant of the `<form>` element.
-   Render the response in the child element by including a template via `<template></template>` or `<script type="text/plain"></script>` tag inside it or by referencing a template with a `template="id_of_other_template"` attribute.
-   Provide a valid JSON object for responses to `submit-success` and `submit-error`. Both success and error responses should have a `Content-Type: application/json` header.

[tip type="note"]
When using `<spz-form>` in tandem with another templating spz component, such as `<spz-list>`, note that templates may not nest in valid spz documents. In this case a valid workaround is to provide the template by `id` via the `template` attribute. Learn more about [nested templates in `<spz-mustache>`](https://spz.dev/documentation/components/spz-mustache/#nested-templates).
[/tip]

<a id="example-submitting"></a>

In the following example, the responses are rendered in an inline template inside the form.

[filter formats="websites, ads"]

```html
<form ...>
  <fieldset>
    <input type="text" name="firstName" />
    ...
  </fieldset>
  <div submitting>
    <template type="spz-mustache">
      Form submitting... Thank you for waiting {{name}}.
    </template>
  </div>
  <div submit-success>
    <template type="spz-mustache">
      Success! Thanks {{name}} for subscribing! Please make sure to check your
      email {{email}} to confirm! After that we'll start sending you weekly
      articles on {{#interests}}<b>{{name}}</b> {{/interests}}.
    </template>
  </div>
  <div submit-error>
    <template type="spz-mustache">
      Oops! {{name}}, {{message}}.
    </template>
  </div>
</form>
```

[/filter]<!-- formats="websites, ads" -->

[filter formats="email"]

```html
<form ...>
  <fieldset>
    <input type="text" name="firstName" />
    ...
  </fieldset>
  <div submitting>
    Form submitting... Thank you for waiting.
  </div>
  <div submit-success>
    <template type="spz-mustache">
      Success! Thanks {{name}} for subscribing! Please make sure to check your
      email {{email}} to confirm! After that we'll start sending you weekly
      articles on {{#interests}}<b>{{name}}</b> {{/interests}}.
    </template>
  </div>
  <div submit-error>
    <template type="spz-mustache">
      Oops! {{name}}, {{message}}.
    </template>
  </div>
</form>
```

[/filter]<!-- formats="email" -->

The publisher's `action-xhr` endpoint returns the following JSON responses:

On success:

```json
{
  "name": "Jane Miller",
  "interests": [
    {"name": "Basketball"},
    {"name": "Swimming"},
    {"name": "Reading"}
  ],
  "email": "email@example.com"
}
```

On error:

```json
{
  "name": "Jane Miller",
  "message": "The email (email@example.com) you used is already subscribed."
}
```

You can render the responses in a referenced template defined earlier in the document by using the template's id as the value of the `template` attribute, set on the elements with the `submit-success` and `submit-error` attributes.

```html
<template type="spz-mustache" id="submit_success_template">
  Success! Thanks {{name}} for subscribing! Please make sure to check your email
  {{email}} to confirm! After that we'll start sending you weekly articles on
  {{#interests}}<b>{{name}}</b> {{/interests}}.
</template>
<template type="spz-mustache" id="submit_error_template">
  Oops! {{name}}, {{message}}.
</template>

<form ...>
  <fieldset>
    ...
  </fieldset>
  <div submit-success template="submit_success_template"></div>
  <div submit-error template="submit_error_template"></div>
</form>
```

See the [full example here](../../examples/forms.spz.html).

### To render a successful response with data binding

-   Use the [on attribute](https://spz.dev/documentation/guides-and-tutorials/learn/spz-actions-and-events) to bind the form _submit-success_ attribute to [`spz.setState()`](<https://spz.dev/documentation/components/spz-bind#updating-state-with-spz.setstate()>).
-   Use the `event` property to capture the response data.
-   Add the state attribute to the desired element to bind the form response.

The following example demonstrates a form `submit-success` response with [`spz-bind`](../spz-bind/spz-bind.md):

```html
<p [text]="'Thanks, ' + subscribe +'! You have successfully subscribed.'">
  Subscribe to our newsletter
</p>
<form
  method="post"
  action-xhr="/components/spz-form/submit-form-input-text-xhr"
  target="_top"
  on="submit-success: spz.setState({'subscribe': event.response.name})"
>
  <div>
    <input type="text" name="name" placeholder="Name..." required />
    <input type="email" name="email" placeholder="Email..." required />
  </div>
  <input type="submit" value="Subscribe" />
</form>
```

When the form is submitted successfully it will return a JSON response similar to the following:

```json
{
  "name": "Jane Miller",
  "email": "email@example.com"
}
```

Then `spz-bind` updates the `<p>` element's text to match the `subscibe` state:

```html
...
<p [text]="'Thanks, ' + subscribe +'! You have successfully subscribed.'">
  Thanks Jane Miller! You have successfully subscribed.
</p>
...
```

[filter formats="websites, ads"]

#### Redirecting after a submission

You can redirect users to a new page after a successful form submission by setting the `spz-Redirect-To` response header and specifying a redirect URL. The redirect URL must be a HTTPS URL, otherwise spz will throw an error and redirection won't occur. HTTP response headers are configured via your server.

Make sure to update your `Access-Control-Expose-Headers` response header to include `spz-Redirect-To` to the list of allowed headers. Learn more about these headers in [CORS Security in spz](https://www.ampproject.org/docs/fundamentals/spz-cors-requests#cors-security-in-spz).

_Example response headers:_

```text
spz-Redirect-To: https://example.com/forms/thank-you
Access-Control-Expose-Headers: spz-Redirect-To
```

{% call callout('Tip', type='success') %}
Check out spz By Example's [Form Submission with Update](https://spz.dev/documentation/examples/components/spz-form/#form-submission-with-page-update) and [Product Page](https://spz.dev/documentation/examples/e-commerce/product_page/#product-page) that demonstrate using redirection after a form submission.
{% endcall %}

### Custom validations

The `spz-form` extension allows you to build your own custom validation UI by using the `custom-validation-reporting` attribute along with one the following reporting strategies: `show-first-on-submit`, `show-all-on-submit` or `as-you-go`.

To specify custom validation on your form:

1. Set the `custom-validation-reporting` attribute on your `form` to one of the [validation reporting strategies](#reporting-strategies).
2. Provide your own validation UI marked up with special attributes. spz will discover the special attributes and report them at the right time depending on the reporting strategy you specified.

Here's an example:

[example preview="inline" playground="true" imports="spz-form"]

```html
<form method="post"
    action-xhr="https://example.com/subscribe"
    custom-validation-reporting="show-all-on-submit"{% if not format=='email'%}
    target="_blank"{% endif %}>
    <fieldset>
      <label>
        <span>Name:</span>
        <input type="text"
          name="name"
          id="name5"
          required
          pattern="\w+\s\w+">
        <span visible-when-invalid="valueMissing"
          validation-for="name5"></span>
        <span visible-when-invalid="patternMismatch"
          validation-for="name5">
          Please enter your first and last name separated by a space (e.g. Jane Miller)
        </span>
      </label>
      <br>
      <label>
        <span>Email:</span>
        <input type="email"
          name="email"
          id="email5"
          required>
        <span visible-when-invalid="valueMissing"
          validation-for="email5"></span>
        <span visible-when-invalid="typeMismatch"
          validation-for="email5"></span>
      </label>
      <br>
      <input type="submit"
        value="Subscribe">
    </fieldset>
  </form>
```

[/example]

For validation messages, if your element contains no text content inside, spz will fill it out with the browser's default validation message. In the example above, when the `name5` input is empty and validation is kicked off (i.e., user tried to submit the form) spz will fill `<span visible-when-invalid="valueMissing" validation-for="name5"></span>` with the browser's validation message and show that `span` to the user.

{% call callout('Important', type='caution') %}
You must provide your own validation UI for each kind of invalid state that the input could have. If these are not present, users will not see any `custom-validation-reporting` for the missing error state. The validity states can be found in the [official W3C HTML validation reporting documentation](https://www.w3.org/TR/html50/forms.html#validitystate).
{% endcall %}

#### Reporting strategies

Specify one of the following reporting options for the `custom-validation-reporting` attribute:

##### Show First on Submit

The `show-first-on-submit` reporting option mimics the browser's default behavior when default validation kicks in. It shows the first validation error it finds and stops there.

##### Show All on Submit

The `show-all-on-submit` reporting option shows all validation errors on all invalid inputs when the form is submitted. This is useful if you'd like to show a summary of validations.

##### As You Go

The `as-you-go` reporting option allows your user to see validation messages as they're interacting with the input. For example, if the user types an invalid email address, the user will see the error right away. Once they correct the value, the error goes away.

##### Interact and Submit

The `interact-and-submit` reporting option combines the behavior of `show-all-on-submit` and `as-you-go`. Individual fields will show any errors immediately after interactions, and on submit the form will show errors on all invalid fields.

### Verification

HTML5 validation gives feedback based only on information available on the page, such as if a value matches a certain pattern. With `spz-form` verification you can give the user feedback that HTML5 validation alone cannot. For example, a form can use verification to check if an email address has already been registered. Another use-case is verifying that a city field and a zip code field match each other.

Here's an example:

```html
<h4>Verification example</h4>
<form
  method="post"
  action-xhr="/form/verify-json/post"
  verify-xhr="/form/verify-json/post"{% if not format=='email'%}
  target="_blank"{% endif %}
>
    <fieldset>
        <label>
            <span>Email</span>
            <input type="text" name="email" required>
        </label>
        <label>
            <span>Zip Code</span>
            <input type="tel" name="zip" required pattern="[0-9]{5}(-[0-9]{4})?">
        </label>
        <label>
            <span>City</span>
            <input type="text" name="city" required>
        </label>
        <label>
            <span>Document</span>
            <input type="file" name="document" no-verify>
        </label>
        <div class="spinner"></div>
        <input type="submit" value="Submit">
    </fieldset>
    <div submit-success>
        <template type="spz-mustache">
            <p>Congratulations! You are registered with {{email}}</p>
        </template>
    </div>
    <div submit-error>
        <template type="spz-mustache">
            {{#verifyErrors}}
                <p>{{message}}</p>
            {{/verifyErrors}}
            {{^verifyErrors}}
                <p>Something went wrong. Try again later?</p>
            {{/verifyErrors}}
        </template>
    </div>
</form>
```

The form sends a `__amp_form_verify` field as part of the form data as a hint to
the server that the request is a verify request and not a formal submit.
This is helpful so the server knows not to store the verify request if the same
endpoint is used for verification and for submit.

Here is how an error response should look for verification:

```json
{
  "verifyErrors": [
    {"name": "email", "message": "That email is already taken."},
    {"name": "zip", "message": "The city and zip do not match."}
  ]
}
```

To remove a field from the `verify-xhr` request, add the `no-verify` attribute
to the input element.

For more examples, see [examples/forms.spz.html](../../examples/forms.spz.html).

### Variable substitutions

The `spz-form` extension allows [platform variable substitutions](../../docs/spec/spz-var-substitutions.md) for inputs that are hidden and that have the `data-spz-replace` attribute. On each form submission, `spz-form` finds all `input[type=hidden][data-spz-replace]` inside the form and applies variable substitutions to its `value` attribute and replaces it with the result of the substitution.

You must provide the variables you are using for each substitution on each input by specifying a space-separated string of the variables used in `data-spz-replace` (see example below). spz will not replace variables that are not explicitly specified.

Here's an example of how inputs are before and after substitutions (note that you need to use platform syntax of variable substitutions and not analytics ones):

```html
<!-- Initial Load -->
<form ...>
  <input
    name="canonicalUrl"
    type="hidden"
    value="The canonical URL is: CANONICAL_URL - RANDOM - CANONICAL_HOSTNAME"
    data-spz-replace="CANONICAL_URL RANDOM"
  />
  <input
    name="clientId"
    type="hidden"
    value="CLIENT_ID(myid)"
    data-spz-replace="CLIENT_ID"
  />
  ...
</form>
```

Once the user tries to submit the form, spz will try to resolve the variables and update the fields' `value` attribute of all fields with the appropriate substitutions. For XHR submissions, all variables are likely to be substituted and resolved. However, in non-XHR GET submissions, values that requires async-resolution might not be available due to having not been resolved previously. `CLIENT_ID` for example would not resolve if it wasn't resolved and cached previously.

```html
<!-- User submits the form, variables values are resolved into fields' value -->
<form ...>
  <input
    name="canonicalUrl"
    type="hidden"
    value="The canonical URL is: https://example.com/hello - 0.242513759125 - CANONICAL_HOSTNAME"
    data-spz-replace="CANONICAL_URL RANDOM"
  />
  <input
    name="clientId"
    type="hidden"
    value="spz:asqar893yfaiufhbas9g879ab9cha0cja0sga87scgas9ocnas0ch"
    data-spz-replace="CLIENT_ID"
  />
  ...
</form>
```

Note how `CANONICAL_HOSTNAME` above did not get replaced because it was not in the allowlist through `data-spz-replace` attribute on the first field.

Substitutions will happen on every subsequent submission. Read more about [variable substitutions in spz](../../docs/spec/spz-var-substitutions.md).

[/filter]<!-- formats="websites, ads" -->

### Autoexpand

spz Form provides an `autoexpand` attribute to `<textarea>` elements. This allows the textarea
to expand and shrink to accomodate the user's rows of input, up to the field's maximum size. If the user manually resizes the field, the autoexpand behavior will be removed.

```html
<textarea autoexpand></textarea>
```

### Polyfills

The `spz-form` extension provide polyfills for behaviors and functionality missing from some browsers or being implemented in the next version of CSS.

#### Invalid submit blocking and validation message bubble

Browsers that use webkit-based engines currently (as of August 2016) do not support invalid form submissions. These include Safari on all platforms, and all iOS browsers. The `spz-form` extension polyfills this behavior to block any invalid submissions and shows validation message bubbles on invalid inputs.

#### User-interaction pseudo-classes

The `:user-invalid` and `:user-valid` pseudo classes are part of the [future CSS Selectors 4 spec](https://drafts.csswg.org/selectors-4/#user-pseudos) and are introduced to allow better hooks for styling invalid/valid fields based on a few criteria.

One of the main differences between `:invalid` and `:user-invalid` is when are they applied to the element. The `:user-invalid` class is applied after a significant interaction from the user with the field (e.g., the user types in a field, or blurs from the field).

The `spz-form` extension provides [classes](#classes-and-css-hooks) to polyfill these pseudo-classes. The `spz-form` extension also propagates these to the ancestor `form`. However, `fieldset` elements are only ever set to have class 'user-valid' to be consistent with browser behaviour.

#### `<textarea>` validation

Regular expression matching is a common validation feature supported natively on most input elements, except for `<textarea>`. We polyfill this functionality and support the `pattern` attribute on `<textarea>` elements.

### Security considerations

#### Protecting against XSRF

In addition to following the details in the [spz CORS spec](https://spz.dev/documentation/guides-and-tutorials/learn/spz-caches-and-cors/spz-cors-requests), please pay extra attention to the section on ["Processing state changing requests" ](https://www.ampproject.org/docs/fundamentals/spz-cors-requests.html#processing-state-changing-requests) to protect against [XSRF attacks](https://en.wikipedia.org/wiki/Cross-site_request_forgery) where an attacker can execute unauthorized commands using the current user session without the user knowledge.

In general, keep in mind the following points when accepting input from the user:

-   Only use POST for state changing requests.
-   Use non-XHR GET for navigational purposes only (e.g. search).
    -   Non-XHR GET requests are will not receive accurate origin/headers and backends won't be able to protect against XSRF with the above mechanism.
    -   In general, use XHR/non-XHR GET requests for navigational or information retrieval only.
-   Non-XHR POST requests are not allowed in spz documents. This is due to inconsistencies of setting `Origin` header on these requests across browsers, and the complications supporting it would introduce in protecting against XSRF. This might be reconsidered and introduced later &mdash; please file an issue if you think this is needed.

## Attributes

[filter formats="websites, ads"]

### `target`

Indicates where to display the form response after submitting the form. The value must be `_blank` or `_top`.

### `action`

Specifies a server endpoint to handle the form input. The value must be an `https` URL (absolute or relative) and must not be a link to a CDN.

-   For `method=GET`: use this attribute or [`action-xhr`](#action-xhr).
-   For `method=POST`: use the [`action-xhr`](#action-xhr) attribute.

[tip type="note"]
The `target` and `action` attributes are only used for non-xhr GET requests. The spz runtime will use `action-xhr` to make the request and will ignore `action` and `target`. When `action-xhr` is not provided, spz makes a GET request to the `action` endpoint and uses `target` to open a new window (if `_blank`). The spz runtime might also fall back to using `action` and `target` in cases where the `spz-form` extension fails to load.
[/tip][/filter] <!-- formats="websites, ads" -->

### `action-xhr`

Specifies a server endpoint to handle the form input and submit the form via XMLHttpRequest (XHR). An XHR request (sometimes called an AJAX request) is where the browser would make the request without a full load of the page or opening a new page. Browsers will send the request in the background using the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) when available and fall back to [XMLHttpRequest API](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) for older browsers.

{% call callout('Important', type='caution') %}
Your XHR endpoint must implement the requirements for [CORS security](https://www.ampproject.org/docs/fundamentals/spz-cors-requests#cors-security-in-spz).
{% endcall %}

This attribute is required for `method=POST`, and is optional for `method=GET`.

The value for `action-xhr` can be the same or a different endpoint than `action` and has the same `action` requirements above.

[filter formats="websites, ads"]

To learn about redirecting the user after successfully submitting the form, see the [Redirecting after a submission](#redirecting-after-a-submission) section below.

### `enctype`

The enctype attribute specifies how form-data should be encoded before sending it to the server via the `method=POST` submission. The default encoding is set to `multipart/form-data`. This and `application/x-www-form-urlencoded` encoding types are currently supported.

Summary of enctype values:

-   `application/x-www-form-urlencoded` - Sets the encoding type to `application/x-www-form-urlencoded`.
-   `multipart/form-data` - Sets the encoding type to `multipart/form-data`.
-   `any value` or unspecified - Setting the `enctype` attribute to a value not specified above or not setting the attribute at all will result in the default encoding type of `multipart/form-data`.

### `data-initialize-from-url`

Initializes form fields from the window URL's search string, where the query parameter name matches the field's name. When this attribute is present, `<input>`, `<select>`, and `<textarea>` fields can optionally be initialized.

Individual fields are opted-in if they contain attribute `data-allow-initialization`. On page load, if the URL contains a query parameter with name matching an opted-in field's `name` attribute, the value or checked-state of that field will be updated based on the value of that query parameter. For example, `<input type="search" name="q" data-allow-initialization>` would display "my search" if the spz page is visited with URL `https://example.com/search?q=my+search`.

Sample:

```html
<form data-initialize-from-url
    method="get"
    action="https://example.com/search"{% if not format=='email'%}
    target="_top"{% endif %}>
  <label>Search: <input type="search" name="q" data-allow-initialization></label>
</form>
<!-- display search results using spz-list -->
```

Limitations:

-   Supported `<input>` types include `checkbox`, `color`, `date`, `datetime-local`, `email`, `hidden`, `month`, `number`, `radio`, `range`, `search`, `tel`, `text`, `time`, `url`, and `week`.

### `xssi-prefix`

Specifies that a prefix should be stripped prior to parsing the fetched json from the `action-xhr` endpoint. If the prefix is not present in the response, then this attribute will have no effect.
This can be useful for APIs that include [security prefixes](http://patorjk.com/blog/2013/02/05/crafty-tricks-for-avoiding-xssi/) like `)]}` to help prevent cross site scripting attacks.

[/filter] <!-- formats="websites, ads" -->

### Other form attributes

All other [form attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) are optional.

[filter formats="websites, ads"]

### `custom-validation-reporting`

This is an optional attribute that enables and selects a custom validation reporting strategy. Valid values are one of: `show-first-on-submit`, `show-all-on-submit` or `as-you-go`.

See the [Custom Validation](#custom-validations) section for more details.

[/filter] <!-- formats="websites, ads" -->

[filter formats="email"]

### Invalid spz email attributes

The spz for Email spec disallows the use of the following attributes on the spz email format.

-   `action`
-   `name`
-   `target`
-   `verify-xhr`

[/filter]<!-- formats="email" -->

## Actions

The `spz-form` element exposes the following actions.

### `submit`

Allows you to trigger the form submission on a specific action, for example, tapping a link, or [submitting a form on input change](#input-events).

### `clear`

Empties the values from each input in the form. This can allow users to quickly fill out forms a second time.

## Events

Use `spz-form` events with the [`on` attribute]
The following example listens to both the `submit-success` and `submit-error` events and shows different lightboxes depending on the event:

```html
<form
  ...
  on="submit-success:success-lightbox;submit-error:error-lightbox"
  ...
></form>
```

### `submit`

The form is submitted and before the submission is complete.

### `submit-success`

The form submission is done and the response is a success.

### `submit-error`

The form submission is done and the response is an error.

[filter formats="websites, ads"]

### `verify`

Asynchronous verification is initiated.

### `verify-error`

Asynchronous verification is done and the response is an error.

### `valid`

The form's validation state changes to "valid" (in accordance with its [reporting strategy](#reporting-strategies)).

### `invalid`

The form's validation state to "invalid" (in accordance with its [reporting strategy](#reporting-strategies)).
[/filter]<!-- formats="websites, ads" -->

### Input events

spz exposes `change` and `input-debounced` events on child `<input>` elements. This allows you to use the [`on` attribute](https://www.ampproject.org/docs/fundamentals/spec#on) to execute an action on any element when an input value changes.

For example, a common use case is to submit a form on input change (selecting a radio button to answer a poll, choosing a language from a `select` input to translate a page, etc.).

[example preview="inline" playground="true" imports="spz-form"]

```html
<form id="myform"
    method="post"
    action-xhr="https://example.com/myform"{% if not format=='email'%}
    target="_blank"{% endif %}>
    <fieldset>
      <label>
        <input name="answer1"
          value="Value 1"
          type="radio"
          on="change:myform.submit">Value 1
      </label>
      <label>
        <input name="answer1"
          value="Value 2"
          type="radio"
          on="change:myform.submit">Value 2
      </label>
    </fieldset>
  </form>
```

[/example]

[filter formats="websites, ads"]
## Styling

### Classes and CSS hooks

The `spz-form` extension provides classes and CSS hooks for publishers to style their forms and inputs.

The following classes can be used to indicate the state of the form submission:

-   `.spz-form-initial`
-   `.spz-form-verify`
-   `.spz-form-verify-error`
-   `.spz-form-submitting`
-   `.spz-form-submit-success`
-   `.spz-form-submit-error`

The following classes are a [polyfill for the user interaction pseudo classes](#user-interaction-pseudo-classes):

-   `.user-valid`
-   `.user-invalid`

Publishers can use these classes to style their inputs and fieldsets to be responsive to user actions (e.g., highlighting an invalid input with a red border after user blurs from it).

See the [full example here](../../examples/spz-form.html) on using these.

## Validation

See [spz-form rules](validator-spz-form.protoascii) in the spz validator specification.
