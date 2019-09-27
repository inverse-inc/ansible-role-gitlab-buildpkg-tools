# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Molecule tests to test this role on several OS
- Enable PPA only if running in a pipeline with
  `gitlab_buildpkg_tools__deb_ppa_enabled`
- Allow to install any repos or any GPG keys without any relation between them
- Simplify installation of repos

### Changed
- `gpgkey_url` renamed to `gpgkey`
- `gitlab_buildpkg_tools__deb_built_pkg` and
  `gitlab_buildpkg_tools__rpm_built_pkg` renamed to
  `gitlab_buildpkg_tools__deb_pkgs` and `gitlab_buildpkg_tools__rpm_pkgs`
- Documentation of variables

### Removed
- Variable `gitlab_buildpkg_tools__ppa`
- Variable `extra_path` and `pool`  for CentOS and Debian repos

### Fixed
- Role name in example playbook


[Unreleased]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v0.2.0...HEAD
