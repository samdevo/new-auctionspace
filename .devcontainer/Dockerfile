FROM mcr.microsoft.com/devcontainers/base:jammy

# Set HOME environment variable explicitly
ENV HOME="/root"
ENV PATH="${HOME}/.cargo/bin:${HOME}/.local/share/solana/install/active_release/bin:${PATH}"

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    libssl-dev \
    curl

# Install Rust
RUN sh -c "$(curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs)" -- -y

# Persist Rust and Cargo PATH in bashrc
RUN echo 'export PATH="${HOME}/.cargo/bin:$PATH"' >> ~/.bashrc

# Verify Rust installation
RUN rustc --version

# Install Solana
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Persist Solana PATH in bashrc
RUN echo 'export PATH="${HOME}/.local/share/solana/install/active_release/bin:$PATH"' >> ~/.bashrc

# Verify Solana installation
RUN solana --version

# Install AVM (Anchor Version Manager)
RUN cargo install --git https://github.com/coral-xyz/anchor avm --force

# Install Solana CLI and Anchor CLI
RUN avm install latest && avm use latest

# Verify Anchor CLI installation
RUN anchor --version
