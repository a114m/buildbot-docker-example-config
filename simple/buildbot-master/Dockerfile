FROM buildbot/buildbot-master:master

# Required by GoogleAuth plugin
RUN pip install requests==2.18.4

# Add docker command
RUN apk update && apk add docker
