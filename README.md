# Concourse play store review resource

Checks for new app store reviews in the google play store using [market_bot](https://github.com/chadrem/market_bot/)


## Resource Configuration

```yaml
resource_types:
- name: market_bot
  type: docker-image
  source:
    repository: arwineap/concourse-playstore-review-resource
    tag: latest
```

## Resource Configuration

* app_name

### Example
```yaml
- name: facebook_app
  type: market_bot
  source:
    app_name: 'com.facebook.katana'
```


## Behavior

### `check`: Check for new google play review
Gets a new google play review, drops a json, and a msg (formatted for slack)


#### Examples
```yaml
jobs:
- name: app_reviews
  plan:
  - get: facebook_app
    trigger: true
  - put: slack
    params:
      channel: '#general'
      text_file: facebook_app/slack.msg
resource_types:
- name: market_bot
  type: docker-image
  source:
    repository: arwineap/concourse-playstore-review-resource
    tag: latest
resources:
- name: facebook_app
  type: market_bot
  source:
    app_name: 'com.facebook.katana'

```


