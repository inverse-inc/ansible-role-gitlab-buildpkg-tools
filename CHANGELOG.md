# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Allow to enable/disable repositories in /etc/yum.repos.d for EL

## [1.0.0] - 2019-09-30

### Added
- Molecule tests to test this role on several OS
- Enable PPA only if running in a pipeline with
  `gitlab_buildpkg_tools__deb_ppa_enabled`
- Allow to install any repos or any GPG keys without any relation between them
- Simplify installation of repos
- Travis CI pipeline to test roles using `molecule`

### Changed
- `gpgkey_url` renamed to `gpgkey`
- `gitlab_buildpkg_tools__deb_built_pkg` and
  `gitlab_buildpkg_tools__rpm_built_pkg` renamed to
  `gitlab_buildpkg_tools__deb_pkgs` and `gitlab_buildpkg_tools__rpm_pkgs`
- Documentation of variables
- Use state `present` in place of `latest` for packages installations

### Removed
- Variable `gitlab_buildpkg_tools__ppa`
- Variable `extra_path` and `pool`  for CentOS and Debian repos

### Fixed
- Role name in example playbook


[Unreleased]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v0.2.0...v1.0.0
