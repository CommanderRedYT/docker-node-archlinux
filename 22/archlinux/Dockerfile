FROM archlinux

ENV NODE_VERSION 22.3.0

ENV YARN_VERSION 1.22.22

RUN useradd -m -u 1000 -U node \
    && pacman -Syu --noconfirm \
    && pacman -S --noconfirm \
        gcc \
        make \
        python \
        git \
        npm \
    && npm install -g npm@latest \
    && npm install -g yarn@latest \
    && pacman -R --noconfirm gcc make python git \
    && rm -rf /var/cache/pacman/pkg/* \
    && node --version \
    && npm --version \
    && yarn --version

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]

CMD [ "node" ]
