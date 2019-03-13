---
layout: default
title: Django Note
comments: true
---

## Static files
A template containing an image, for example, would be rendered the following way:

- Having the image located at assets/my_app/examples.jpg
- The settings.py file should have the configuration

```
STATIC_URL = "/static/"

STATICFILES_DIRS = (
    os.path.join(BASE_DIR, "assets"),
)
```

- The static template tag should be loaded and used to build the images URL

```
<img src="{% static "my_app/example.jpg" %}" alt="My image"/>
```

- The HTML should be rendered as

```
<img src="/static/my_app/example.jpg" alt="My image">
```

## Settings.py file
`[project]/settings.py` ; `INSTALLED_APPS`;

`TEMPLATES` add `        'DIRS': [os.path.join(BASE_DIR, 'templates')],
`

 `STATICFILES_DIRS` add
 `    os.path.join(BASE_DIR, 'assets'),
`

## Reference
https://medium.com/labcodes/configuring-django-with-react-4c599d1eae63

https://www.valentinog.com/blog/tutorial-api-django-rest-react/#Django_REST_with_React_what_you_will_learn