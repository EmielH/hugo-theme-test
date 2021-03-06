# Hugo Theme Test

A simple Hugo site that can be used to test your theme, e.g. in a CI-pipeline.

## Travis CI

An example `.travis.yml`:

```
env:
  - HUGO_VERSION="0.50"
  - HUGO_VERSION="0.51"
  - HUGO_VERSION="0.52"
  - HUGO_VERSION="0.53"
  - HUGO_VERSION="0.54.0"
  - HUGO_VERSION="0.55.0"

install:
  - wget https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
  - tar xf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
  - mv hugo ~/bin/
  - hugo version
  - gem install html-proofer
  - htmlproofer --version
  - git clone https://github.com/EmielH/hugo-theme-test.git

script:
  - cd hugo-theme-test
  - hugo -t tale-hugo --themesDir ../..
  - htmlproofer public --check-html --disable-external --allow-hash-href --checks-to-ignore LinkCheck
```
