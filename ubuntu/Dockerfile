FROM ubuntu:22.04

RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y --no-install-recommends \
  sudo \
  ca-certificates \
  vim \
  curl \
  wget \
  build-essential \
  automake \
  cmake \
  bash-completion \
  software-properties-common \
  && \
  rm -rf /var/lib/apt/lists/*

RUN groupadd -g 10001 nosotros && \
  useradd -ms /bin/bash --uid 10001 --gid 10001 sysadmin && \
  echo "sysadmin ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/10-sysadmin

USER sysadmin
WORKDIR /home/sysadmin

RUN mkdir -p ~/.cargo/bin && \
  wget --progress=dot:giga https://github.com/starship/starship/releases/download/v1.20.0/starship-x86_64-unknown-linux-gnu.tar.gz && \
  tar xvzf starship-x86_64-unknown-linux-gnu.tar.gz && \
  rm starship-x86_64-unknown-linux-gnu.tar.gz && \
  mv starship ~/.cargo/bin/

RUN mkdir -p ~/.config && \
  touch ~/.config/starship.toml && \
  echo 'export PATH=~/.cargo/bin:~/.local/bin:$PATH' >> ~/.bashrc && \
  echo 'eval "$(starship init bash)"' >> ~/.bashrc && \
  /home/sysadmin/.cargo/bin/starship preset pastel-powerline -o ~/.config/starship.toml

CMD [ "/bin/bash" ]
