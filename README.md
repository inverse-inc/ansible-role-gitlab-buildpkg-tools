gitlab_buildpkg_tools role
==========================

Install a [gitlab-buildpkg-tools PPA](http://orange-opensource.gitlab.io/gitlab-buildpkg-tools/)
and packages built with [gitlab-buildpkg-tools](https://gitlab.com/Orange-OpenSource/gitlab-buildpkg-tools) in a pipeline.

This role supports also installing additional repositories, GPG keys or packages to meet
dependencies of built packages in pipeline.

Requirements
------------

Role designed to be launch in a GitLab pipeline. It can be called outside a
pipeline but you will need to set some variables by hand.

Role Variables
--------------

Available variables are listed below, check `defaults/main.yml` for defaults values:

    gitlab_buildpkg_tools__ppa_enabled

Controls whether PPA repo and key should be installed.

    gitlab_buildpkg_tools__deb_ppa

Debian PPA repo parameters.

    gitlab_buildpkg_tools__rpm_ppa

RPM PPA repo parameters.

    gitlab_buildpkg_tools__deb_deps_pkgs

List of Debian dependencies to install repos.

    gitlab_buildpkg_tools__deb_keys

List of GPG keys **URL**.

    gitlab_buildpkg_tools__deb_combined_keys

List of GPG keys to install (PPA + additional).

    gitlab_buildpkg_tools__deb_sources_dir

Debian directory to store repos files.

    gitlab_buildpkg_tools__deb_deps_repos

List of additional Debian repos.

    gitlab_buildpkg_tools__deb_combined_repos

List of Debian repos to install.

    gitlab_buildpkg_tools__deb_pkgs

List of Debian packages to install.

    gitlab_buildpkg_tools__rpm_deps_pkgs

List of CentOS dependencies to install repos.

    gitlab_buildpkg_tools__rpm_keys

List of GPG keys URL or files.

    gitlab_buildpkg_tools__rpm_combined_keys

List of GPG keys to install (PPA + additional).

    gitlab_buildpkg_tools__rpm_deps_repos

List of additional CentOS repos.

    gitlab_buildpkg_tools__rpm_combined_repos

List of CentOS repos to install.

    gitlab_buildpkg_tools__rpm_pkgs

List of CentOS packages to install.


Environment variables to set in a pipeline (see below):
* `CI_PROJECT_NAME`
* `CI_PAGES_URL`
* `DEB_PACKAGES_NAME`
* `RPM_PACKAGES_NAME`


Limitations
-----------

### Debian limitations ###

- GPG keys need to be added by URL
- Debian packages need to be installed by name

### Environment Variables in .gitlab-ci.yml  ###

In a `.gitlab-ci.yml` file, you can define environment variables like
`DEB_PACKAGES_NAME:` but theses variables can't be a pure YAML list or
dictionnary. Consequently, you need to use an inline YAML syntax.

Examples
--------

### Example playbook to install packages **inside** of a CI with additional repos ###


  * `.gitlab-ci.yml`:

```yaml
variables:
  DEB_PACKAGES_NAME: "['fingerbank', 'apt-add-gitlab', 'gitlab-buildpkg-tools']"
  RPM_PACKAGES_NAME: "['fingerbank', 'yum-add-gitlab', 'gitlab-buildpkg-tools']"
```

  * example playbook:

```yaml
- name: example usage of inverse_inc.gitlab_buildpkg_tools role
  hosts: all
  roles:
    - role: inverse_inc.gitlab_buildpkg_tools
      vars:
        gitlab_buildpkg_tools__rpm_deps_repos:
          - name: packetfence-devel
            baseurl: http://inverse.ca/downloads/PacketFence
            extra_path: devel
            gpgkey_url: https://packetfence.org/downloads/RPM-GPG-KEY-PACKETFENCE-CENTOS
          - name: gitlab-buildpkg-tools
            baseurl: https://orange-opensource.gitlab.io/gitlab-buildpkg-tools
            gpgkey_url: https://orange-opensource.gitlab.io/gitlab-buildpkg-tools/GPG_PUBLIC_KEY
        gitlab_buildpkg_tools__deb_deps_repos:
          - name: packetfence-devel
            baseurl: http://inverse.ca/downloads/PacketFence
            gpgkey_url: http://inverse.ca/downloads/APT-GPG-KEY-PACKETFENCE-DEBIAN
            extra_path: debian-devel
            pool: stretch
          - name: packetfence
            baseurl: http://inverse.ca/downloads/PacketFence
            gpgkey_url: http://inverse.ca/downloads/APT-GPG-KEY-PACKETFENCE-DEBIAN
            pool: stretch
          - name: gitlab-buildpkg-tools
            baseurl: https://orange-opensource.gitlab.io/gitlab-buildpkg-tools
            gpgkey_url: https://orange-opensource.gitlab.io/gitlab-buildpkg-tools/GPG_PUBLIC_KEY
```

License
-------

GPL-3.0

Author Information
------------------

Inverse inc <info@inverse.ca>
