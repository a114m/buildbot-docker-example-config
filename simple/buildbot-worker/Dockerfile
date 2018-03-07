FROM buildbot/buildbot-worker:master

# Switch to root
USER root

# Docker command dependencies
RUN apt-get update && apt-get install -y libltdl7


ARG DOCKER_GID
RUN if [ ! -z "$DOCKER_GID" ]\
; then\
  addgroup --gid $DOCKER_GID docker || true &&\
  addgroup buildbot `awk -v GID=$DOCKER_GID -F':' '$3 == GID {print $1}' /etc/group`\
; else\
  apt-get install sudo &&\
  echo "buildbot ALL=(ALL) NOPASSWD: /usr/bin/docker" >> /etc/sudoers &&\
  echo "buildbot ALL=(ALL) NOPASSWD: /usr/local/bin/docker-compose" >> /etc/sudoers &&\
  echo "alias docker='sudo docker'" >> /etc/profile.d/custom.sh &&\
  echo "alias docker-compose='sudo docker-compose'" >> /etc/profile.d/custom.sh\
; fi


RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# Fall back to buildbot user
USER buildbot
