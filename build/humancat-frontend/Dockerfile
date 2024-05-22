FROM python:3.10

ENV PYTHONUNBUFFERED=1
ENV PORT 80
ENV SRC_DIR /opt/gitops
ENV PKG_TMP_DIR /tmp
COPY pip_requirements.txt ${PKG_TMP_DIR}/

RUN apt-get update
RUN apt-get install -y apache2 libapache2-mod-wsgi-py3 && apt-get clean

RUN pip install --upgrade pip && \
    pip install -r ${PKG_TMP_DIR}/pip_requirements.txt

COPY apache/000-default.conf /etc/apache2/sites-available/000-default.conf
RUN echo "ServerName 127.0.0.1" >> /etc/apache2/apache2.conf

RUN mkdir -p ${SRC_DIR}
COPY ./gitops ${SRC_DIR}/
WORKDIR ${SRC_DIR}

EXPOSE ${PORT}

ENTRYPOINT ["apachectl"]
CMD ["-D", "FOREGROUND"]