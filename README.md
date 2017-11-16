# Introduction
```
> bundle install --path .bundle
> bundle exec msync --help
> bundle exec rake rubocop
```

# Performing a dry-run
```
> bundle exec msync update --noop
```


# Only want to update a single module?  Specify a filter
```
> bundle exec msync update -f <regex> --noop
```

# I want to update my fork with modulesync config from voxpopuli in order to cut a release
```
  > bundle exec msync update -f windowsfeature -n tragiccode -b release_prep -m "Preping for release"
```

# NOTE
If you have posh-git and Win32-OpenSSH Installed they will fight and not use the same version of ssh-agent and ssh-add.  Also be sure to start-sshagent if using posh git


# Deleting a file in a module repo that is in the module_sync config repo
Managing files may mean removing files. You can ensure a file is absent by marking it "delete". This is useful for purging nodesets.

To mark a file deleted, list it in .sync.yml with the value delete: true. For example,
```
---
spec/acceptance/nodesets/sles-11sp1-x64.yml
  delete: true
```
```
---
  .fixtures.yml:
    repositories:
      - module_name: 'powershell'
        module_git_url: 'https://github.com/puppetlabs/puppetlabs-powershell.git'
  Guardfile:
    delete: true
```


# Unmanaged Files

A file can be marked "unmanaged" in .sync.yml, in which case modulesync will not try to modify it. This is useful if, for example, the module has special Rake tasks in the Rakefile which is difficult to manage through a template.

To mark a file "unmanaged", list it in .sync.yml with the value unmanaged: true. For example,
```
---
spec/spec_helper.rb:
  unmanaged: true

```


# Creating a module Release

While this is technically not related to modulesync this seemed like the best place to put this.  Below are the following steps i currently take in order to release a module.

## Bump metadata.json using blacksmith
```
  > be rake module:bump:minor
```

## Generate Changelog
```
  > be rake changelog
```

## Commit changes and add release tag and push
```
  > git commit -am "Bump version to v0.2.0"
  > git tag v0.2.0
  > git push origin HEAD
```
## Build & Publish to forge using blacksmith
```
  > be rake build
  > be rake module:push
```
