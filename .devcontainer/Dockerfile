FROM mcr.microsoft.com/devcontainers/base:jammy

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    libssl-dev

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# Set environment variables for Rust and Cargo
ENV PATH="/root/.cargo/bin:${PATH}"

# Verify Rust installation
RUN rustc --version

# Install Solana
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)" && \
    export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH" && \
    solana --version

# Install AVM
RUN cargo install --git https://github.com/coral-xyz/anchor avm --force && \
    avm --version

# Install Solana CLI
RUN avm install latest && \
    avm use latest && \
    anchor --version
    