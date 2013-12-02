# Heroku Buildpack SSH Key

This is a buildpack that allows you to add a private ssh key to the build
process so that you can clone private dependencies from GitHub.

## Usage

1. Enable the `user-env-compile` labs feature:

   ```bash
   $ heroku labs:enable user-env-compile
   ```

2. Add the SSH key to the app environment:

   ```
   $ heroku config:set SSH_KEY=$(cat ~/.ssh/id_rsa)
   ```
3. Ensure that your're app is using the [multi buildpack](https://github.com/ddollar/heroku-buildpack-multi):

   ```bash
   $ heroku config:set BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi
   ```

4. Add the buildpack to your `.buildpacks` file:

   ```
   https://github.com/ejholmes/heroku-buildpack-sshkey
   https://github.com/heroku/heroku-buildpack-ruby
   ```

Now you'll have access to your private repos on GitHub:

```ruby
source 'https://rubygems.org'

gem 'rake'
gem 'private-gem', github: 'ejholmes/private-gem'
```
