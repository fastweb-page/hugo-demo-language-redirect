---
title: Home (EN)
---

This is a Hugo demo on Netlify, demonstrating a multi-lingual project with base URL redirects by browser language and translated 404 error pages.

## config/_default/hugo.yaml

- https://gohugo.io/content-management/multilingual/

```yaml
# Language configuration
defaultContentLanguage: en
defaultContentLanguageInSubdir: true # Because the base URL gets redirected by language (otherwise switching to EN home would cause issues)
languages:
  en:
    contentDir: content/en
    languageName: English
    weight: 1
  de:
    contentDir: content/de
    languageName: Deutsch
    weight: 2
  fr:
    contentDir: content/fr
    languageName: Français
    weight: 3
```

## Netlify redirects config:

- https://docs.netlify.com/routing/redirects/redirect-options/#redirect-by-country-or-language
- https://docs.netlify.com/routing/redirects/redirect-options/#custom-404-page-handling


```shell
# Redirect base URL by language
# We use HTTP status code 302 because it's dynamic and might change in future requests
# We use force (!) because Hugo generates an alias in public/index.html tot redirect to the default language when defaultContentLanguageInSubdir is true
/ /de/ 302! Language=de
/ /fr/ 302! Language=fr
/ /en/ 302!

# Custom 404 error pages
/de/* /de/404.html 404
/fr/* /fr/404.html 404
/* /en/404.html 404
```