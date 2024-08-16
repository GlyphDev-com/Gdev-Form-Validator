# Gdev Form Validator
## Overview

[![gdev](https://i.postimg.cc/90SKHP2w/removal-ai-68a74532-f4d0-4b18-87c3-ffe7a11deffe-screenshot-2024-06-20-075650-19-Z4-RR.png, "gdev")](https://gdev.com)
pour la version francaise de ce document, visite notre site [gdev.com](https://gdev.com/resources/gdev_form_validator)


Gdev Form Validator is a dynamic and customizable form validation package designed to make form validation easy and flexible for developers. It provides multiple methods to handle form validation, including auto-validation, specific form validation, and validation as the user types both in English and French.

`NOTE: Make sure you write your script in a module environment`

## Installation

### NPM

To install the package using npm, run:

```bash
npm install gdev_form_validator
```

### CDN

To use the package via CDN, include the following in your HTML:

```html
<!-- CSS for styling -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gdev_form_validator@latest/dist/style.css">

<!-- JavaScript for validation -->
<script src="https://cdn.jsdelivr.net/npm/gdev_form_validator@latest/dist/validator.bundle.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gdev_form_validator@latest/dist/autovalidate.bundle.js"></script>

```
## Validation Response
when validation is completed, the package returns the response as an object in its simplest form so the developer can foward users input to the backend as object `values:{}` very easily.
### onSuccess (if the validation rules have all been checked)
```json
  {
      "status": "true",
      "values": {
          "field1_name_as_specified_in_validation_rule": "value1",
          "field2_name_as_specified_in_validation_rule": "value2",
          "field3_name_as_specified_in_validation_rule": "value3"
      }
  }
  ```
  
  ### onError (if one of the validation rules failed)
```json
  {
      "status": "false",
      "values": {}
  }
  ```
  
  
## Usage

### Auto Validation

To automatically validate all forms on a page:

1. Include the auto-validator script in your HTML body:
    ```html
    <!-- CDN -->
    <script src="https://cdn.jsdelivr.net/npm/gdev_form_validator@latest/dist/autovalidate.js"></script>

    <!-- NPM -->
    <script src="path to the installed package ./dist/autovalidate.js"></script>
    ```
    make sure to provide unique id for each form to be validated and `Gdev-lang = "fr or en"` attribute for language to report errors.

2. The validator will scan through all forms on the page and validate them based on rules specified in the HTML.

3. To handle validation results, listen for the `onValidationComplete` event:

    ```javascript
    const form1 = document.getElementById('your-form-id');
    form1.addEventListener('onValidationComplete', e => {
      console.log(window.validationResponse.your-form-id);
    });
    ```

### Specific Form Validation

To validate a specific form:

1. Import the validator script:
    ```html
    <!-- CDN -->
    <script src="https://cdn.jsdelivr.net/npm/gdev_form_validator@latest/dist/validator.js"></script>

    <!-- NPM -->
    <script src="path to the installed package ./dist/validator.js"></script>
    ```

2. Create a validator instance and call the `validate` method:
    
    ```javascript
    
    import { FormValidation } from 'gdev_form_validator'; //Optiomal: import if your working on non-browser environments (like Node.js)

    const form = document.getElementById('yourFormId');
    const validator = new FormValidation(form, 'en'); // 'en' or 'fr' for language

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      const result = validator.validate();
      console.log(result);
    });
    ```

### Validate as User Types

To validate each input field as the user types:

1. Call the `validateEach()` method on your validator instance:

    ```javascript
    validator.validateEach();
    ```

## Validation Rules

Specify validation rules directly in your HTML using the `Gdev-props` attribute in plain English. Here are some examples:

### Text Input

```html
<div class="gdev-field-wrapper">
    <input type="text" Gdev-props='{"type":"text","name":"username",minchar":10,"minWord":3}' />
    <div class="gdev-error"></div>
</div>
```

### Password Input

```html
<div class="gdev-field-wrapper">
    <input type="password" Gdev-props='{"type":"password","name":"password", "confirmWith": "name of confirm field"}' />
    <div class="gdev-error"></div>
</div>
```

### Email Input

```html
<div class="gdev-field-wrapper">
    <input type="email" Gdev-props='{"type":"email","name":"email", "provider": ["gmail", "outlook"]}' />
    <div class="gdev-error"></div>
</div>
```

### Phone Input

```html
<div class="gdev-field-wrapper">
    <input type="tel" Gdev-props='{"type":"tel","name":"phone", "country": ["cameroon", "nigeria"]}' />
    <div class="gdev-error"></div>
</div>
```



### Number Input

```html
<div class="gdev-field-wrapper">
    <input type="tel" name="number" Gdev-props='{"type":"number","name":"number","range":[20, 500], "multipleOf": 9}' />
    <div class="gdev-error"></div>
</div>
```

## Documentation

For more detailed documentation and examples, visit [our website](https://your-website-link.com).

## License

This project is licensed under the MIT License.
