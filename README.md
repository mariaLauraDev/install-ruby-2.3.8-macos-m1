# Install Ruby 2.x on macOS M1

This repository provides scripts and detailed instructions for installing older Ruby versions, such as Ruby 2.3.8, on macOS systems with M1 chips. It aims to ensure a smooth and optimized setup for Ruby development in this specific environment.

## Prerequisites

Understanding the macOS architecture and terminal environments is crucial:

- **ARM64**: The native Apple Silicon architecture, offering optimized performance.
- **x86_64 (Rosetta)**: An emulation layer for Intel-based applications, enabling them to run on Apple Silicon. Use the `arch x86_64` command with Rosetta for compatibility.

## Installation Steps

### Using Rosetta for Compatibility

Certain steps or applications may require running under the Intel architecture emulation provided by Rosetta, especially when dealing with older software versions or tools that have not yet been updated for ARM64 architecture. This is essential for ensuring compatibility and stable operation of software not natively supported by Apple Silicon.

For instance, when installing Ruby 2.3.8, you might encounter issues with native extensions or dependencies that were built for x86_64 architecture. In such cases, running the installation commands under Rosetta ensures these components can be compiled and executed as intended.

### Install Homebrew

Homebrew is a package manager for macOS. Install it by running:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install Git
```sh
brew install git
```

### Generate and Configure SSH Keys
For GitHub or GitLab, use the ed25519 algorithm to create SSH keys:

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Then, add the generated SSH keys to your SSH agent:

```sh
touch ~/.ssh/config
sudo nano ~/.ssh/config
```
In the ~/.ssh/config file, add:

```sh
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

### Install Development Tools
```sh
brew install asdf # follow asdf official steps!
brew install gpg gawk
xcode-select --install
brew install openssl@3 readline libyaml gmp
brew install openssl@1.1
```

### Install Ruby
Add asdf ruby plugin
```sh
asdf plugin add ruby
```
Use flags to install an older version of ruby
```sh
optflags=-Wno-error=implicit-function-declaration ASDF_RUBY_BUILD_VERSION=v20220630 asdf install ruby 2.3.8
```
Font: https://github.com/asdf-vm/asdf-ruby/issues/301#issuecomment-1934846430 
Set a ruby version 
```sh
asdf local ruby 2.3.8
```
Update the bundle directory after setting the ruby version
```sh
asdf reshim
```

### Install Bundler
For Ruby 2.3.8, you may need to install an older version of Bundler:

```sh
gem install bundler -v 1.17.3
```

### Verify Installation
Check if Rails is correctly installed and can download gems:

```sh
curl -o doctor.rb https://raw.githubusercontent.com/mislav/ssl-tools/8b3dec4/doctor.rb
ruby doctor.rb
```

###  Final Steps
After completing these steps, your system should be ready for Ruby development using older versions on macOS with M1 chips. For further assistance or troubleshooting, consult the documentation or open an issue in this repository.
