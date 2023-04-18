# website
Antón Morant's Personal Website

## Setup
- Using [rvm](https://rvm.io/) for Ruby Version Management.
- Run `bundle install`.

## Troubleshooting
**eventmachine can't find openssl**
With Apple M1, I encountered an error during installation where the gem `eventmachine` fails to find openssl.
Fix: Install the gem first with the line below (use the right version if what jekyll needs has changed), then run `bundle install` again.
```bash
gem install eventmachine -v '1.2.7' -- --with-openssl-dir=$(brew --prefix openssl)
```
