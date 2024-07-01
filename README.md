# bootstrap-alert-confirm-prompt

Drop-in (await) replacement for JavaScript's native `alert`, `confirm`, and `prompt` functions using Bootstrap 5 modals.
It allows for better customization and styling, making use of Bootstrap's components and utilities.

## Features

- Replacement for browser's native `alert`, `confirm`, and `prompt`.
- Customizable titles, icons, and CSS classes.
- Support for HTML content in alerts.
- Configurable buttons with custom text, classes, and return values.
- Focus management for buttons and input fields.
- Additional options for modal size and background customization.

![image](https://github.com/osalabs/bootstrap-alert-confirm-prompt/assets/1141095/eeb438fb-5250-4139-be27-e0636f56d1ae)

![image](https://github.com/osalabs/bootstrap-alert-confirm-prompt/assets/1141095/19ac2112-675d-4959-9eb3-4a4cc809952c)

![image](https://github.com/osalabs/bootstrap-alert-confirm-prompt/assets/1141095/36287df2-7ab1-4bbf-8b9c-2af3409e6a9f)


## Installation

1. Include CSS and JS for Bootstrap 5 and Bootstrap Icons in your HTML file:
    ```html
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    ```

2. Include the `bootstrap-alert-confirm-prompt.js` script in your HTML file:
    ```html
    <script src="path/to/bootstrap-alert-confirm-prompt.js"></script>
    ```

## Usage

### Basic Examples

```javascript
// Basic Alert
alert('This is a basic alert!');

// Basic Confirm
confirm('Are you sure?').then(result => console.log('Confirm result:', result));

// Basic Prompt
prompt('What is your name?').then(result => console.log('Prompt result:', result));
```

## Options

All modals accept an options object with the following properties:

- `title`: The title of the modal.
- `icon`: The icon class to display next to the message (Bootstrap Icons).
- `html`: Whether to render the message as HTML (default is `false`).
- `class`: Additional classes to apply to the modal.
- `classDialog`: Additional classes to apply to the modal dialog (e.g., `modal-lg`, `modal-xl`).
- `classContent`: Additional classes to apply to the modal content (e.g., `bg-danger`, `bg-primary`).

### Confirm and Prompt Specific Options

- `buttons`: An array of button definitions. Each button can have:
  - `text`: The button text.
  - `class`: Additional classes to apply to the button.
  - `value`: The value to return when the button is clicked.

### Confirm Specific Options

- `focus`: The index of the button to focus on when the modal is shown.


### Defaults:

```
alert('Text', {
    title: 'Alert',
    icon: 'bi-exclamation-triangle-fill text-warning',
    html: false,
    class: '',
    classDialog: '',
    classContent: ''
});

let result = await confirm('Text', {
    title: 'Confirmation',
    icon: 'bi-question-circle-fill text-primary',
    buttons: [
        { text: 'OK', class: 'btn-primary', value: true },
        { text: 'Cancel', class: 'btn-secondary', value: false }
    ],
    focus: 0, // index of the button to focus on, default is 0 (first button)
    class: '',
    classDialog: '',
    classContent: ''
});

let result = await prompt('Text', '', {
    title: 'Prompt',
    icon: 'bi-pencil-square text-secondary',
    buttons: [
        { text: 'OK', class: 'btn-primary', value: 'ok' },
        { text: 'Cancel', class: 'btn-secondary', value: 'cancel' }
    ],
    focus: 0, // index of the button to focus on, default is 0 (first button)
    class: '',
    classDialog: '',
    classContent: ''
});

```

### Advanced Examples

```javascript
// Alert with options
alert('This is an alert with a custom title and icon!', {
    title: 'Custom Alert',
    icon: 'bi-info-circle-fill text-info'
});

// Confirm with custom buttons
confirm('Do you want to proceed?', {
    title: 'Proceed?',
    icon: 'bi-question-diamond-fill text-warning',
    buttons: [
        { text: 'Yes', class: 'btn-success', value: true },
        { text: 'No', class: 'btn-danger', value: false },
        { text: 'Maybe', class: 'btn-secondary', value: 'maybe' }
    ]
}).then(result => console.log('Confirm result with custom buttons:', result));

// Prompt with custom title and icon
prompt('Please enter your email:', '', {
    title: 'Email Input',
    icon: 'bi-envelope-fill text-primary',
    class: 'custom-prompt-class'
}).then(result => console.log('Prompt result with custom title and icon:', result));

// Prompt with custom buttons and classes
prompt('Please enter your username:', 'user123', {
    title: 'Username',
    icon: 'bi-person-fill text-secondary',
    classDialog: 'modal-lg',
    classContent: 'bg-warning',
    buttons: [
        { text: 'Submit', class: 'btn-primary', value: 'submit' },
        { text: 'Cancel', class: 'btn-danger', value: 'cancel' }
    ]
}).then(result => console.log('Prompt result with custom buttons and classes:', result));
```


### Usage with await

```javascript
async function runAsyncExamples() {
    // Confirm with await
    const confirmResult = await confirm('Do you want to continue?');
    console.log('Async Confirm result:', confirmResult);

    // Prompt with await and custom buttons
    const promptResult = await prompt('What is your age?', '25', {
        title: 'Age Input',
        icon: 'bi-calendar-fill text-primary',
        buttons: [
            { text: 'Submit', class: 'btn-primary', value: 'submit' },
            { text: 'Cancel', class: 'btn-danger', value: 'cancel' }
        ]
    });
    console.log('Async Prompt result with custom buttons:', promptResult);

    // Prompt with await, HTML content, and custom class
    const htmlPromptResult = await prompt('Enter your <b>bold</b> text:', '', {
        title: 'Bold Input',
        icon: 'bi-fonts text-danger',
        classDialog: 'modal-sm',
        classContent: 'bg-light',
        buttons: [
            { text: 'OK', class: 'btn-primary', value: 'ok' },
            { text: 'Cancel', class: 'btn-danger', value: 'cancel' }
        ],
        html: true
    });
    console.log('Async Prompt result with HTML content:', htmlPromptResult);
}

runAsyncExamples();
```

