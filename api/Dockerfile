FROM registry.access.redhat.com/ubi8/ubi-minimal

ADD api/*.txt /lunch/

RUN microdnf install sqlite python3 shadow-utils \
    libxml2-devel libxslt-devel gcc python3-devel && microdnf clean all && \
    pip3 install -r /lunch/requirements.txt && \
    rm -rf /root/.cache

ENV TZ="Europe/Prague"
# apscheduler fix
RUN echo "Europe/Prague" > /etc/timezone

RUN adduser --gid 0 -d /lunch --no-create-home -c 'Lunch user' lunch

ADD api/*.py /lunch/
ADD api/*.yml /lunch/
ADD api/restaurants/*.py /lunch/restaurants/

USER lunch

EXPOSE 8001

ENV ENABLED_RESTAURANTS=asport,portoriko,nepal,purkynka,kotelna,padthai,spravnemisto,velorex,3opice

CMD python3 -m lunch.lunch
