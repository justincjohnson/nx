# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.166.1/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG VARIANT="bionic"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends build-essential automake autoconf m4 libncurses5-dev libssh-dev libncurses-dev erlang-dev

USER vscode

# Issues:
# - Erlang build failure, related to M1 or qemu?
# - Bazel failure in qemu, even with 4.0.0
# - Slow performance
RUN bash -c " \
  git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.0 && \
  . ~/.asdf/asdf.sh && \
  asdf plugin add erlang https://github.com/asdf-vm/asdf-erlang.git && \
  asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git && \
  asdf plugin-add bazel https://github.com/rajatvig/asdf-bazel.git && \
  echo \". \$HOME/.asdf/asdf.sh\" >> ~/.bashrc && \
  echo \". \$HOME/.asdf/completions/asdf.bash\" >> ~/.bashrc && \
  export KERL_CONFIGURE_OPTIONS=\"--disable-debug --without-javac\" && \
  asdf install erlang 24.0-rc2 && \
  asdf global erlang 24.0-rc2 && \
  asdf install elixir 1.12.0-rc.0-otp-24 && \
  asdf global elixir 1.12.0-rc.0-otp-24 && \
  asdf install bazel 3.1.0 && \
  asdf global bazel 3.1.0 && \
  mix local.hex --force && \
  mix local.rebar --force"

# cd /workspace && \
#   curl -o /workspace/libtorch.zip https://download.pytorch.org/libtorch/cu102/libtorch-shared-with-deps-1.8.1%2Bcu102.zip && \
#   unzip /workspace/libtorch.zip && \
#   echo \"export LIBTORCH_DIR=/workspace/libtorch\" >> ~/.bashrc && \