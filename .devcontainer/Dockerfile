FROM mcr.microsoft.com/devcontainers/typescript-node:20-bookworm

ADD install-vscode.sh /root/
RUN chmod +x /root/install-vscode.sh
RUN /root/install-vscode.sh

# Ensure post-create.sh is executable
ADD post-create.sh /root/
RUN chmod +x /root/post-create.sh
# RUN chmod +x post-create.sh

RUN git config --system codespaces-theme.hide-status 1

USER node
RUN npm install -g node-gyp
RUN NPM_CACHE="$(npm config get cache)" && rm -rf "$NPM_CACHE" && ln -s /vscode-dev/npm-cache "$NPM_CACHE"
RUN echo 'export DISPLAY="${DISPLAY:-:1}"' | tee -a ~/.bashrc >> ~/.zshrc

USER root
CMD chown node:node /vscode-dev && sudo -u node mkdir -p /vscode-dev/npm-cache && sleep inf
