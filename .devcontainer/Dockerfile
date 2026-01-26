FROM alpine:latest

RUN apk add --no-cache \
    curl \
    git \
    ca-certificates \
    direnv \
    bash \
    bash-completion \
    util-linux \
    helix \
    github-cli \
    mdbook \
    mdbook-bash-completion \
    jujutsu \
    jujutsu-bash-completion \
    git-bash-completion

# Create regular user
RUN adduser -D -s /bin/bash dd

# Install mise for root
RUN curl https://mise.run | sh

# Install mise for dd user
RUN su - dd -c 'curl https://mise.run | sh'

ENV PATH="/root/.local/bin:${PATH}"

# Enable direnv globally
RUN echo 'eval "$(direnv hook bash)"' >> /etc/bash.bashrc
RUN echo 'eval "$(direnv hook bash)"' >> /home/dd/.bashrc

# Enable mise globally
RUN echo 'eval "$(mise activate bash)"' >> /etc/bash.bashrc
RUN echo 'eval "$(mise activate bash)"' >> /home/dd/.bashrc

# Ensure dd user owns its home directory
RUN chown -R dd:dd /home/dd
