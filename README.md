# Introduction

> bundle install --path .bundle
> bundle exec msync --help
> bundle exec rake rubocop

# Performing a dry-run
> bundle exec msync update --noop


# Only want to update a single module?  Specify a filter
> bundle exec msync update -f <regex> --noop

# NOTE
If you have posh-git and Win32-OpenSSH Installed they will fight and not use the same version of ssh-agent and ssh-add.  Also be sure to start-sshagent if using posh git


# Common usecase examples
