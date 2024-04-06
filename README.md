# Install Ruby 2.x on macOS M1

This repository provides scripts and detailed instructions for installing older Ruby versions, such as Ruby 2.3.8, on macOS systems with M1 chips. It aims to ensure a smooth and optimized setup for Ruby development in this specific environment.

## Prerequisites

When setting up software on Macs with the M1 chip, it's critical to grasp the macOS architecture and the terminal environments available. This is due to Apple's shift to M1 (ARM-based) chips, which introduced significant changes in how applications run compared to the traditional Intel chips. Here's a simplified overview:

### ARM64: Apple Silicon Architecture

- **What It Is**: ARM64 refers to the architecture used in Apple's M1, M1 Pro, and M1 Max chips, collectively known as Apple Silicon. This architecture is designed for energy efficiency and optimized performance, being lighter and faster compared to the traditional x86_64 architecture used in Intel chips.
- **Who It's For**: Ideal for all new applications and development, especially those designed or updated to leverage the capabilities of Apple Silicon chips. If you are developing, compiling, or running software that has been updated to support ARM64, you'll be operating at the maximum capacity of your Mac.

### x86_64 (Rosetta): An Emulation Layer for Intel-based Applications
- **What It Is**: x86_64, in the context of Apple Silicon Macs, refers to the emulation layer known as Rosetta 2. Rosetta allows applications built for Intel's x86_64 architecture to run on the newer ARM64 architecture of Apple Silicon. This is crucial for ensuring compatibility with older software not yet optimized for ARM64.
- **Why It Matters**: The transition to ARM64 architecture means not all applications will immediately work natively on M1 Macs. Rosetta 2 bridges this gap by translating Intel-based applications to run on ARM64. While there may be a slight performance overhead due to this translation, it ensures a broad range of software remains usable on the latest hardware.
-** Who It's For**: Users who need to run legacy or specific software that hasn't been updated for ARM64. This includes developers relying on certain tools, libraries, or environments that are yet to be ported over. By using Rosetta, you can continue your work uninterrupted, ensuring compatibility with a vast ecosystem of Intel-based applications while waiting for ARM64 updates.

Understanding these two key components of the macOS architecture ensures a smoother setup process, whether you're installing new software designed for ARM64 or navigating the complexities of running older, Intel-based applications on your M1 Mac.

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
