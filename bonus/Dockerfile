FROM jenkins/jenkins:lts

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

ENV CASC_JENKINS_CONFIG="/var/jenkins_home/casc_configs/my_marvin.yml"

RUN jenkins-plugin-cli --plugins \
    cloudbees-folder \
    configuration-as-code \
    credentials \
    github \
    instance-identity \
    job-dsl \
    script-security \
    structs \
    role-strategy \
    ws-cleanup

RUN mkdir -p /var/jenkins_home/casc_configs

COPY my_marvin.yml /var/jenkins_home/casc_configs/my_marvin.yml

COPY job_dsl.groovy /var/jenkins_home/job_dsl.groovy

USER root
RUN apt-get update && apt-get install -y make gcc git && rm -rf /var/lib/apt/lists/*
RUN chown -R jenkins:jenkins /var/jenkins_home/casc_configs /var/jenkins_home/job_dsl.groovy
USER jenkins
