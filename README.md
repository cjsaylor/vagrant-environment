# LAMP + Java, NodeJS, and MongoDB

The purpose of this project is to have a development environment up and running in the quickest amount of time.

## Dependencies

* Vagrant (1.22+)
* VirtualBox (4.2+)
* Ruby (1.87+)

## Installation

Once all dependencies have been installed, run `./setup.rb` to initialize the vagrant environment.

The script will do the following:

1. Configure your shared directory.
1. Update any attached submodules (cookbooks)
1. Install dependent vagrant plugins.

Then, run `vagrant up`.

## Using the environment

#### Accessing apache locations

In your mapped directory, the project directory must conform to your hostname. On vagrant, if you wanted to access `http://boxmeup.c.dev` from the browser,
then in the vagrant shared directory, the directory structure needs to be: `/home/vagrant/shared/boxmeup.c.dev/`. This is provided that your configured hostname is `c.dev` in the `config.yml`.


## Known Issues

* Due to an upstream bug in the opswords/php cookbook, pear installs fail when provisioning. https://github.com/opscode-cookbooks/php/pull/54. To fix, apply the following diff:

```diff
diff --git a/providers/pear.rb b/providers/pear.rb
index ca473b5..db90e17 100644
--- a/providers/pear.rb
+++ b/providers/pear.rb
@@ -258,13 +258,13 @@ def pecl?
   @pecl ||= begin
               # search as a pear first since most 3rd party channels will report pears as pecls!
               search_cmd = "#{node['php']['pear']} -d"
-              search_cmd << " preferred_state=#{can_haz(@new_resource, preferred_state)}"
+              search_cmd << " preferred_state=#{can_haz(@new_resource, "preferred_state")}"
               search_cmd << " search#{expand_channel(can_haz(@new_resource, "channel"))} #{@new_resource.package_name}"

               if grep_for_version(shell_out(search_cmd).stdout, @new_resource.package_name).nil?
                 # fall back and search as a pecl
                 search_cmd = "#{node['php']['pecl']} -d"
-                search_cmd << " preferred_state=#{can_haz(@new_resource, preferred_state)}"
+                search_cmd << " preferred_state=#{can_haz(@new_resource, "preferred_state")}"
                 search_cmd << " search#{expand_channel(can_haz(@new_resource, "channel"))} #{@new_resource.package_name}"
               else
                 false
```
