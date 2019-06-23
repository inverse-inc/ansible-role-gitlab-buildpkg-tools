gitlab_buildpkg_tools role
==========================

Install packages from a gitlab-buildpkg-tools PPA.

Requirements
------------

Role designed to be launch in a GitLab pipeline but can be called outside a
pipeline to install packages.

Role Variables
--------------

| Variable                                     | Default                                                      | Comments (type)                                       |
| ---                                          | ---                                                          | ---                                                   |
| `gitlab_buildpkg_tools__apt_sources_dir`     | `/etc/apt/sources.list.d`                                    | Directory to store gitlab-pages.list                  |
| `gitlab_buildpkg_tools__deb_pkgs`            | `['apt-transport-https','gnupg']`                            | List of Debian dependencies to install built packages |
| `gitlab_buildpkg_tools__deb_pkgs`            | `['gnupg2']`                                                 | List of CentOS dependencies to install built packages |
| `gitlab_buildpkg_tools__ci_pages_url`        | `'{{ lookup("env"), "CI_PAGES_URL" }}'`                      | URL of PPA created by gitlab-buildpkg-tools           |
| `gitlab_buildpkg_tools__ci_pages_gpgkey_url` | `"{{ gitlab_buildpkg_tools__ci_pages_url }}/GPG_PUBLIC_KEY"` | URL of GPG key used to sign built packages            |
| `gitlab_buildpkg_tools__ci_project_name`     | `'{{ lookup("env"), "CI_PROJECT_NAME" }}'`                   | Name of repo in GitLab                                |
| `gitlab_buildpkg_tools__ci_built_pkg`        | `'{{ lookup("env"), "PACKAGES_NAME" }}'`                     | Packages to install                                   |


All variables that contains `ci` in their name should be defined in pipeline.

Limitations
-----------

In GitLab, you can define environment variables like `PACKAGES_NAME:` but
theses variables can't be a YAML list or dictionnary. Consequently,
`gitlab_buildpkg_tools__ci_built_pkg` is a scalar. This should work because
`yum` and `apt` module support installing several packages from a scalar.

Examples
--------

### Example to install packages **inside** a CI ###

  * `.gitlab-ci.yml`:

```yaml
variables:
  PACKAGES_NAME: fingerbank
```

  * example playbook:

```yaml
- name: example usage of inverse-inc.gitlab_buildpkg_tools role
  hosts: all
  roles:
    - inverse-inc.gitlab_buildpkg_tools
```


### Example playbook to install packages **outside** of a CI ###


```yaml
- name: example usage of inverse-inc.gitlab_buildpkg_tools role
  hosts: all
  roles:
    - role: inverse-inc.gitlab_buildpkg_tools
      vars:
        gitlab_buildpkg_tools__ci_pages_url: https://orange-opensource.gitlab.io/gitlab-buildpkg-tools
        gitlab_buildpkg_tools__ci_project_name: gitlab-buildpkg-tools
        gitlab_buildpkg_tools__ci_built_pkg: gitlab-buildpkg-tools
```

License
-------

GPL-3.0

Author Information
------------------

Inverse inc <info@inverse.ca>
