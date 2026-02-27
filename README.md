# Fluxer Conda Package

[![Build and Publish](https://github.com/nandi-conda/fluxer/actions/workflows/build-and-publish.yml/badge.svg)](https://github.com/nandi-conda/fluxer/actions/workflows/build-and-publish.yml)

Conda package for [Fluxer](https://fluxer.app) desktop application.

## Installation

Install from the nandi-conda channel:

```bash
conda install -c nandi-conda fluxer
```

Or with mamba:

```bash
mamba install -c nandi-conda fluxer
```

## Supported Platforms

- **Linux x86_64** (linux-64)
- **Linux aarch64** (linux-aarch64)

## Dependencies

- gtk3
- nss
- alsa-lib

## Development

### Building Locally

To build the package locally using rattler-build:

```bash
# Install rattler-build
mamba install -c conda-forge rattler-build

# Build for current platform
rattler-build build --recipe recipe.yaml

# Build for specific platform
rattler-build build --recipe recipe.yaml --target-platform linux-64
rattler-build build --recipe recipe.yaml --target-platform linux-aarch64
```

### Testing the package

```bash
# Install the built package
conda install ./output/fluxer-*.tar.bz2

# Test
fluxer --version
```

## CI/CD

This repository uses GitHub Actions to:

1. Build conda packages for both x86_64 and aarch64 platforms
2. Publish packages to the nandi-conda channel on prefix.dev
3. Create GitHub releases when tags are pushed

### Secrets

The following secret must be configured in the repository:

- `PREFIX_API_KEY`: API key for uploading to prefix.dev (nandi-conda channel)

To set up the secret:
1. Go to repository Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `PREFIX_API_KEY`
4. Value: Your prefix.dev API token (get it from https://prefix.dev/channels/nandi-conda/settings)

## License

AGPL-3.0

## Maintainer

[nandi-conda](https://github.com/nandi-conda)
