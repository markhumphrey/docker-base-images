FROM python:2.7

WORKDIR /app

# add config files for front-end dependencies
ONBUILD ADD package.json /app/package.json
ONBUILD ADD bower.json /app/bower.json
ONBUILD ADD .bowerrc /app/.bowerrc

# install front-end dependencies
# TODO: this is not ideal, for now chaining together in one RUN instruction to reduce image size
# 1) install node and npm using apt-get
# 2) cleanup apt-get
# 3) handle debian naming the node binary nodejs by creating a symlink
# 4) npm install (should at least install bower)
# 5) bower install
# 6) remove npm and nodejs now that front-end dependencies have been pulled down
# 7) remove node symlink
ONBUILD RUN apt-get update && \
            apt-get install -y \
                    nodejs \
                    npm && \
            apt-get clean && \
            rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
            ln -s /usr/bin/nodejs /usr/bin/node && \
            npm install && \
            /app/node_modules/bower/bin/bower install --allow-root --config.interactive=false && \
            apt-get purge -y \
                    npm \
                    nodejs && \
            rm /usr/bin/node

# install python library requirements
ONBUILD RUN virtualenv /env
ONBUILD ADD requirements.txt /app/requirements.txt
ONBUILD RUN /env/bin/pip install -r /app/requirements.txt

ONBUILD ADD . /app

EXPOSE 8080
CMD []
ENTRYPOINT ["/env/bin/python", "main.py"]
