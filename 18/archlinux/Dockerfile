FROM archlinux

ENV NODE_VERSION 18.20.3

ENV YARN_VERSION 1.22.22

RUN useradd -m -u 1000 -U node \
    && pacman -Syu --noconfirm \
    && pacman -S --noconfirm \
    $(if [[ "$NODE_VERSION" == 18.* ]]; then echo "nodejs-lts-hydrogen"; elif [[ "$NODE_VERSION" == 20.* ]]; then echo "nodejs-lts-iron"; else echo "nodejs"; fi) \
        npm \
    && npm install -g npm@latest \
    && npm install -g yarn@latest \
    && rm -rf /var/cache/pacman/pkg/* \
    && npm cache clean --force \
    && yarn cache clean --force

RUN echo "node --version: $(node --version)" \
    && echo "npm --version: $(npm --version)" \
    && echo "yarn --version: $(yarn --version)" \
    && INSTALLED_NODE_VERSION=$(node --version) \
    && INSTALLED_YARN_VERSION=$(yarn --version) \
    # check if node --version is the same as NODE_VERSION
    && if [ "v$NODE_VERSION" != "$INSTALLED_NODE_VERSION" ]; then echo "node --version does not match NODE_VERSION (should be v$NODE_VERSION but is $INSTALLED_NODE_VERSION)"; exit 1; fi \
    # check if yarn --version is the same as YARN_VERSION
    && if [ "$YARN_VERSION" != "$INSTALLED_YARN_VERSION" ]; then echo "yarn --version does not match YARN_VERSION (should be $YARN_VERSION but is $INSTALLED_YARN_VERSION)"; exit 1; fi

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]

CMD [ "node" ]
