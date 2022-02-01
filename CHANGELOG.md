# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.3.3] - 2022-02-01
### Added
- Support for RockyLinux on old Ansible releases

## [1.3.2] - 2021-10-18
### Added
- Allow to override state of packages

## [1.3.1] - 2021-07-20
### Changed
- Switch from yum_repository module to template module

## [1.3.0] - 2021-06-29
### Added
- Update cache before installing packages (Debian)
- Allow to use `module_hotfixes` option in inventory (EL)

## [1.2.0] - 2021-06-09

### Added
- Allow to set a priority for yum repositories

## [1.1.0] - 2019-12-27

### Added
- Allow to enable/disable repositories in /etc/yum.repos.d for EL
- Support for Debian 10 (Buster) and EL8

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

[Unreleased]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.3.3...HEAD
[1.3.3]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.3.2...v1.3.3
[1.3.2]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.3.1...v1.3.2
[1.3.1]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.3.0...v1.3.1
[1.3.0]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/inverse-inc/ansible-role-gitlab-buildpkg-tools/compare/v0.2.0...v1.0.0
