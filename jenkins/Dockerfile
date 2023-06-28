FROM jenkins/jenkins:2.401
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli

# Add the jenkins user to the docker group on the local machine to be able to access the docker socket (/var/run/docker.sock); 
# This will allow jenkins to use docker from the local machine (where the jenkins container is created by docker) in its container.
RUN groupadd -g 999 docker && usermod -aG docker jenkins
USER jenkins
RUN jenkins-plugin-cli --plugins "git matrix-auth workflow-aggregator docker-workflow credentials-binding blueocean docker-workflow"