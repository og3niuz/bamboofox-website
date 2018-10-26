# bamboofox-website

[![build status][travis-image]][travis-url]
[![Rawsec's CyberSecurity Inventory](https://inventory.rawsec.ml/img/badges/Rawsec-inventoried-FF5050_flat.svg)](https://inventory.rawsec.ml/ctf_platforms.html#bamboofox)
[![GitHub stars](https://img.shields.io/github/stars/bamboofox/bamboofox-website.svg)](https://github.com/bamboofox/bamboofox-website/stargazers)
[![GitHub license](https://img.shields.io/github/license/bamboofox/bamboofox-website.svg)](https://github.com/bamboofox/bamboofox-website/blob/master/LICENSE)

## Requirements

```bash
sudo apt install imagemagick
sudo apt install libmysqlclient-dev
```

## Ruby and Rails versions

Ruby 2.4.0 or newer
Rails 5.2.0 or newer

## Installation

```bash
bundle install
rake db:migrate
```

## Running

```bash
rails server
```

See on http://localhost:3000

## Deploy


### Setup application config

Reference `config/application.yml.example`

Create `config/application.yml`

`config/application.yml`

```
# rake secret
secret_key_base: 73fd0783500cc42096f163859b5062376ccb90416a9bf920c89e43981986493029d20b58e088fc04444d571829381aa5e246ce364b9c16830128eb10757e65a9
host: bamboofox.nctucs.net
mailer_sender: no-reply@bamboofox.nctucs.net
password: password
facebook_id: facebook_id
facebook_secret: facebook_secret
github_id: github_id
github_secret: github_secret
google_id: google_id
google_secret: google_secret
nctu_id: nctu_id
nctu_secret: nctu_secret
```

### Setup secret key

Remove `config/credentials.yml.enc`

Reference `config/application.yml.example`

Generate `config/master.key` and `config/credentials.yml.enc`

```bash
rm config/application.yml.enc
rails credentials:edit
```

`config/credentials.yml`

```
secret_key_base: <%= Figaro.env.secret_key_base %>
```

### Setup seed data and compile assets

```bash
bundle install
RAILS_ENV=production rake db:reset DISABLE_DATABASE_ENVIRONMENT_CHECK=1
RAILS_ENV=production rake assets:precompile
```

## Tests

### Run RuboCop

```bash
rake rubocop
```

### Auto-correct RuboCop offenses
```bash
rake rubocop:auto_correct
```

### Run Rails Best Practice

```bash
rake rails_best_practices
```

### Format erb files

```bash
find . -name '*.erb' | xargs htmlbeautifier
```

[travis-image]: https://travis-ci.org/bamboofox/bamboofox-website.svg?branch=master
[travis-url]: https://travis-ci.org/bamboofox/bamboofox-website
