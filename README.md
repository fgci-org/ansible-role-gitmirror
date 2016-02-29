gitmirror
=========

This role installs and sets up a git mirror server (
https://github.com/beefsack/git-mirror )

Requirements
------------

This module has only been developed and tested on CentOS 7. It ought
to work on any Linux distro that uses systemd.

Role Variables
--------------

Default variables (that can be overriden with group_vars etc.):

- gitmirror_download_url; The URL where to download the binary
  distribution. The default is version 0.1.0 for Linux x86_64.  

- gitmirror_archive_binpath; The path of the git-mirror binary inside
  the archive file.

- gitmirror_binpath: The path where the git-mirror binary will be
  installed.

- gitmirror_basepath: The directory where the mirrored repositories
  will be stored. Also the home directory of the gitmirror user.

- gitmirror_config: Path of the git-mirror config file.

- gitmirror_repos: List of maps containing repositories to
  mirror. Each repository must have at least a key "origin" which
  describes the URL of the repo to mirror. If present, the "name" key
  will mirror the repository under that name.


Dependencies
------------

Does not depend on any other roles.

Example Playbook
----------------

The default parameters should mostly be Ok, with the exception of the
gitmirror_repos variable which you probably want to override. E.g. a
playbook like

    - hosts: servers
      roles:
         - { role: ansible-role-gitmirror, tags: [ 'gitmirror' ] }

and then somewhere in your group_vars:

    gitmirror_repos:
	- origin: https://github.com/jabl/ansible-role-gitmirror.git
	- origin: https://example.com/foo/bar.git
	  name: "bar2.git"

License
-------

MPL-2.0

Author Information
------------------

Janne Blomqvist  https://github.com/jabl
