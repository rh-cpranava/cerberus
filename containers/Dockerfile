# Dockerfile for cerberus

FROM quay.io/openshift/origin-tests:latest as origintests

FROM quay.io/centos/centos:7

MAINTAINER Red Hat OpenShift Performance and Scale

ENV KUBECONFIG /root/.kube/config

# Copy OpenShift CLI, Kubernetes CLI from origin-tests image
COPY --from=origintests /usr/bin/oc /usr/bin/oc
COPY --from=origintests /usr/bin/kubectl /usr/bin/kubectl

# Install dependencies
RUN yum install -y git python39 python3-pip gcc python3-devel zlib-devel libjpeg-devel

RUN git clone https://github.com/rh-cpranava/cerberus.git --branch main /root/cerberus && \
mkdir -p /root/.kube && cd /root/cerberus && pip3 install --upgrade pip && pip3 install -r requirements.txt

WORKDIR /root/cerberus

ENTRYPOINT python3 start_cerberus.py --config=config/config.yaml
