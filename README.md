# iuse-bluebuild-btw

[![build-ublue](https://github.com/duhdugg/iuse-bluebuild-btw/actions/workflows/build.yml/badge.svg)](https://github.com/duhdugg/iuse-bluebuild-btw/actions/workflows/build.yml)

This project is using [BlueBuild](https://blue-build.org/) and [blue-build/template](https://github.com/blue-build/template).

## Installation

> **Warning**  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

Until ISO hosting is available, the best way to install is by first installing an
existing atomic Fedora OS, and then following steps 1-4:

1. First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/duhdugg/iuse-bluebuild-btw:latest
  ```
2. Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
3. Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/duhdugg/iuse-bluebuild-btw:latest
  ```
4. Reboot again to complete the installation
  ```
  systemctl reboot
  ```
The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

This is currently being used on a machine that started with an [Aurora Developer
Edition](https://getaurora.dev/) ISO installation.

## ISO (TODO)

Instructors for generating an offline iso [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/duhdugg/iuse-bluebuild-btw
```
