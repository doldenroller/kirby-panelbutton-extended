# Kirby Panelbutton Extended Plugin

<img width="100%" height="auto" alt="Kirby CMS buttons field to open URLs in a new tab or trigger webhooks" src="screenshot.png" />

A custom Kirby Panel field that features a button. This button can be used to either open a URL in a new tab or to trigger a URL or a webhook, providing feedback on success or error.

The extensions adds a optional confirmation dialog before the action is triggered. Additionally you can add a redirect after a webhook.

## Installation

Requires PHP 8.1 and Kirby 4.0.0 or higher.

Just download/clone this repo into `site/plugins` of your Kirby project.

Currently there is no Composer.

## Usage

```yml
webhook_button:
    type: panelbutton
    label: Button
    text: Button Text # Button text
    url: {{page.url}}/my-webhook-route # url to call
    theme: positive # (default: null)
    fullwidth: true # (default: null)
    size: lg # (default: "lg")
    icon: lab # (default: null)
    help: Help text # (default: null)
    reload: true # trigger a page refresh on success to display updated data (default: false)
    redirect: some-page?tab=maintab
    dialog: true
    dialogtext: Use Webhook this Page (<strong>{{ page.title }}</strong>)?

link_button:
    type: panelbutton
    label: Refresh data
    text: Refresh
    url: https://example.com/ # url to open (default: false)
    open: true
    # disabled: true # (default: false)

multilang_support:
    type: panelbutton
    label: toolbar.button.code # translate by reference
    text: # provide exact translations
        en: Reset code
        de: Code Zurücksetzen
```

You can use all Icons from the Kirby UI. The themes are based on the Info section:

- info
- positive
- negative
- notice
- warning
- passive
- text
- dark
- code
- empty


## Development

1. Install a fresh Kirby StarterKit
2. `cd site/plugins`
3. `git clone` this repo
4. `cd` into this plugin folder

```
npm run dev
```

## Credit

This plugin is built upon [Kirby Panel Buttons Plugin](https://github.com/lemmon/kirby-panel-buttons) by Lemmon, whichis built upon [Kirby Panel Button Plugin](https://github.com/moritzebeling/kirby-panel-button) by Moritz Ebeling.

## License

[MIT](https://opensource.org/licenses/MIT)


It is discouraged to use this plugin in any project that promotes racism, sexism, homophobia animal abuse, violence or any other form of hate speech.
