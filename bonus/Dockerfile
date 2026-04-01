FROM jenkins/jenkins:lts

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

ENV CASC_JENKINS_CONFIG="/var/jenkins_home/casc_configs"

# Workflow-aggregator, plain-credentials, ssh-credentials is for my_bonus job
RUN jenkins-plugin-cli --plugins \
    cloudbees-folder \
    configuration-as-code \
    credentials \
    plain-credentials \
    ssh-credentials \
    github \
    instance-identity \
    job-dsl \
    workflow-aggregator \
    script-security \
    structs \
    role-strategy \
    ws-cleanup

RUN mkdir -p /var/jenkins_home/casc_configs

COPY my_marvin.yml /var/jenkins_home/casc_configs/my_marvin.yml
COPY bonus/my_bonus.yml /var/jenkins_home/casc_configs/my_bonus.yml
COPY bonus/lambdananas /usr/local/bin/lambdananas

COPY job_dsl.groovy /var/jenkins_home/job_dsl.groovy

USER root
RUN apt-get update && apt-get install -y make gcc git docker.io && rm -rf /var/lib/apt/lists/*
RUN chmod +x /usr/local/bin/lambdananas
RUN chown -R jenkins:jenkins /var/jenkins_home/casc_configs /var/jenkins_home/job_dsl.groovy
USER jenkins
