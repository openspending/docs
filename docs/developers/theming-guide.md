# Theming Guide

Some of our web-apps can be themed, i.e. some visual properties can be modified.
This might be useful when embedding parts of OpenSpending in a different website, or when deploying a separation installation of OpenSpending altogether.

The customisable visual elements include colours, logos, header and footer links etc.

We have a few built-in themes. Each theme is represented as a `json` file under `app/config/themes`.

By default, apps will use `default.json` (the default theme). If the URL contains `theme=dark` (`dark` is the name of the theme), we will try to use `dark.json` as the theme. In case it's not found, we will fall back to the default theme.

Themes always use `default.json` as a basis, so that you can override only part of the scheme (or even modify single list elements: use `{}` to use a list element unchanged and `false` to remove one).

In order to use your own theme, you might choose one of these implementation paths:

- Independent installs of our app will have a single point of modification for theming. Source installations can edit the file directly. Docker deployments can override `default.json` or add a new theme using Docker's ADD command.
- Partners can upload a new theme via a pull-request, and refer to it in the query parameters.

Sample `default.json` (might be a little different, depending on the app):

```json
{
  "colors": {
    "brand": "#3a99d9",
    "sidebar": "#2a2d34",
    "content": "#f5f5f5"
  },
  "header": {
    "links": [
      {
        "title": "Upload Data",
        "href": "/packager/"
      },
      {
        "title": "Explore Datasets",
        "href": "/explorer/"
      }
    ],
    "logo": {
      "icon": "assets/os.svg",
      "image": "assets/viewer.svg"
    }
  },
  "footer": {
    "projectLogo": {
      "image": "http://a.okfn.org/img/openspending/logo.svg"
    },
    "orgLogo": {
      "href": "http://okfn.org",
      "image": "http://a.okfn.org/img/oki/landscape-white-165x43.png"
    },
    "links": [
      {
        "title": "Privacy policy",
        "href": "https://okfn.org/privacy-policy/"
      },
      {
        "title": "IP policy",
        "href": "https://okfn.org/ip-policy/"
      },
      {
        "title": "Cookie policy",
        "href": "https://okfn.org/cookie-policy/"
      },
      {
        "title": "Terms of use",
        "href": "https://okfn.org/terms-of-use/"
      }
    ],
    "socialMedia": [
      {
        "href": "https://facebook.com/OKFNetwork",
        "icon": "https://raw.githubusercontent.com/thoughtbot/refills/master/source/images/facebook-logo-circle.png",
        "alt": "Facebook"
      },
      {
        "href": "https://twitter.com/okfn",
        "icon": "https://raw.githubusercontent.com/thoughtbot/refills/master/source/images/twitter-logo-circle.png",
        "alt": "Twitter"
      },
      {
        "href": "https://www.youtube.com/user/openknowledgefdn",
        "icon": "https://raw.githubusercontent.com/thoughtbot/refills/master/source/images/youtube-logo-circle.png",
        "alt": "YouTube"
      }
    ]
  }
}
```

