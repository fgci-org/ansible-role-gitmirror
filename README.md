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

Default variables (that can be overriden with group\_vars etc.):

- gitmirror\_download\_url; The URL where to download the binary
  distribution. The default is version 0.1.0 for Linux x86\_64.  

- gitmirror\_archive\_binpath; The path of the git-mirror binary inside
  the archive file.

- gitmirror\_binpath: The path where the git-mirror binary will be
  installed.

- gitmirror\_basepath: The directory where the mirrored repositories
  will be stored. Also the home directory of the gitmirror user.

- gitmirror\_generate\_config: Whether to generate the config
  file. Disabling this can be useful if you have some other mechanism
  to generate the config file instead.

- gitmirror\_config: Path of the git-mirror config file.

- gitmirror\_repos: List of maps containing repositories to
  mirror. Each repository must have at least a key "origin" which
  describes the URL of the repo to mirror. If present, the "name" key
  will mirror the repository under that name.


Dependencies
------------

Does not depend on any other roles.

Example Playbook
----------------

The default parameters should mostly be Ok, with the exception of the
gitmirror\_repos variable which you probably want to override. E.g. a
playbook like

    - hosts: servers
      roles:
         - { role: ansible-role-gitmirror, tags: [ 'gitmirror' ] }

and then somewhere in your group\_vars:

    gitmirror\_repos:
        - origin: https://github.com/jabl/ansible-role-gitmirror.git
        - origin: https://example.com/foo/bar.git
          name: "bar2.git"

License
-------

MIT

Author Information
------------------

Janne Blomqvist  https://github.com/jabl
