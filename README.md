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

    gitlab_buildpkg_tools__ppa_url

URL of the PPA.

    gitlab_buildpkg_tools__ppa_url_deb

URL of the PPA with Debian part.

    gitlab_buildpkg_tools__ppa_url_deb

URL of the PPA with CentOS part.

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

### Example to install packages **inside** of a CI  ###


  * `.gitlab-ci.yml`:

```yaml
variables:
  DEB_PACKAGES_NAME: "['apt-add-gitlab', 'gitlab-buildpkg-tools']"
  RPM_PACKAGES_NAME: "['yum-add-gitlab', 'gitlab-buildpkg-tools']"
  CI_PROJECT_NAME: gitlab-buildpkg-tools
  CI_PAGES_URL: http://orange-opensource.gitlab.io
```

Of course, if you use this playbook inside a pipeline where
`gitlab-buildpkg-tools` is used, you don't need to define `CI_PROJECT_NAME`
and `CI_PAGES_URL` variables.

  * example playbook: see [playbook.yml use for molecule tests](molecule/default/playbook.yml)


### Example to install packages with additional repos and keys ###

See [playbook-additional.yml use for molecule
tests](molecule/default/playbook-additional.yml).

License
-------

GPL-3.0

Author Information
------------------

Inverse inc <info@inverse.ca>
