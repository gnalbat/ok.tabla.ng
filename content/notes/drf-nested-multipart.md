---
title: django-rest-framework multipart/form-data request body for nested serializers
date: 2025-01-31
tags:
  - webdev
  - django
  - drf
  - tech
---

I'm confused since [Github](https://github.com/encode/django-rest-framework/issues/7262) [issues](https://github.com/encode/django-rest-framework/issues/8910)  for DRF and some Stackoverflow and Reddit (ew!) threads seem to indicate that multipart/form data http requests are impossible. But on cases where you need file uploads on related models, it's like a troublesome task to write custom functions

But the BrowseableAPI is possible to do that! Of course nested serializers [require a custom .create() method](https://www.django-rest-framework.org/api-guide/serializers/#writable-nested-representations), so given that you already have one, then it should be possible to create the model instance.

Upon checking the BrowseableAPI's html form for POST requests, names for individual fields are just as follows:

```
field1
field2
field3
nestedserializer1.field1
nestedserializer1.field2
nestedserializer1.field3
nestedserializer2.field1
nestedserializer2.field2
nestedserializer2.field3
```

And it works! Am I just dumb or am I missing something here?
