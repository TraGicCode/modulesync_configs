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


# Deleting a file in a module repo that is in the module_sync config repo
Managing files may mean removing files. You can ensure a file is absent by marking it "delete". This is useful for purging nodesets.

To mark a file deleted, list it in .sync.yml with the value delete: true. For example,

---
spec/acceptance/nodesets/sles-11sp1-x64.yml
  delete: true


---
  .fixtures.yml:
    repositories:
      - module_name: 'powershell'
        module_git_url: 'https://github.com/puppetlabs/puppetlabs-powershell.git'
  Guardfile:
    delete: true

