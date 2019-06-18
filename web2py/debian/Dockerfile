FROM python:3.7-slim-stretch
LABEL AUTHOR "Abhishek Bajpai <abhvajpayee@gmail.com>"

ENV WEB2PY_ROOT=/opt/web2py

# overridable environment variables
ENV WEB2PY_VERSION=
ENV WEB2PY_PASSWORD=
ENV WEB2PY_ADMIN_SECURITY_BYPASS=
ENV UWSGI_OPTIONS=

WORKDIR $WEB2PY_ROOT

RUN apt-get update && apt-get -y install \
    gcc \
    git \
    libpcre3-dev \
 && pip install uwsgi \
 && git clone --recursive https://github.com/web2py/web2py.git $WEB2PY_ROOT \
 && mv $WEB2PY_ROOT/handlers/wsgihandler.py $WEB2PY_ROOT \
 && groupadd -g 1000 web2py \
 && useradd -r -u 1000 -g web2py web2py \
 && chown -R web2py:web2py $WEB2PY_ROOT

RUN pip install uwsgi pymongo==3.0 pillow pandas numpy 
RUN pip install gevent 

COPY entrypoint.sh /usr/local/bin/

ENTRYPOINT [ "entrypoint.sh" ]
CMD [ "http" ]
USER web2py

EXPOSE 8080 9090
