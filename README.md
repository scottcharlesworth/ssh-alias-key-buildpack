# Heroku Buildpack: SSH Alias Key

You can use this build pack to set multiple SSH aliases in your ~/.ssh/config file.
This is particularly useful to download a composer dependency stored in a private repository using deploy keys.

The buildpack takes environment variables, creates a SSH Config file, and adds each alias to a list of 
known hosts. 

## Usage

Add the buildpack to your application using the Heroku dashboard, or:

    $ heroku buildpacks:set --index 1 https://github.com/scottcharlesworth/ssh-alias-key-buildpack
It needs to be run before any other buildpack that may need SSH access.

Next you will need to set the following environment variables:

- `SSH_ALIAS` - a comma separated list of aliases
- `SSH_HOST` - a comma separated list of hostnames
- `SSH_USER` - a comma separated list of users

Each item in the above must be in the same order. In addition there must also be a key value, encoded in base64 format:

- `SSH_KEY_#` - (starting from 0) a key for each alias

The buildpack will check to make sure there are an equal number of aliases, hosts, users, and keys - and will not process
the variables if there is a different number.