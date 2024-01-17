# -*- mode: Python -*-
load('ext://namespace', 'namespace_create', 'namespace_inject')
namespace_create('mktplace-develop')

k8s_yaml(
  helm(
    'app', 
    name='mktplace', 
    namespace='mktplace-develop',
    values='values-develop.yaml'
  )
)

# The helm() call above is functionally equivalent to the following:
#
# k8s_yaml(local('helm template -f ./values-dev.yaml ./busybox'))
# watch_file('./busybox')
# watch_file('./values-dev.yaml')

# docker_build('k8s-develop', '.')

# 'busybox-deployment' is the name of the Kubernetes resource we're deploying.
k8s_resource(
  new_name='mktplace-configs', 
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services'],
  objects=[
    "mktplace-kafka:serviceaccount",
    "mktplace-develop:namespace",
    "mktplace-keycloak:serviceaccount",
    "mktplace-postgresql:serviceaccount",
    "mktplace-kafka:role",
    "mktplace-postgresql:role",
    "mktplace-kafka:rolebinding",
    "mktplace-postgresql:rolebinding",
    "mktplace-zookeeper-scripts:configmap",
    "mktplace-kafka-scripts:configmap",
    "mktplace-keycloak-env-vars:configmap",
    "keycloak-realm-import:configmap",
    "keycloak-ha-configmap:configmap",
    "postgresql-initdb:configmap",
    "mktplace-externaldb:secret",
    "mktplace-keycloak:secret",
    "mktplace-postgresql:secret",
    "keycloak-secret:secret",
    "mktplace-kafka-0-external:service",
    "mktplace-keycloak:ingress",
    "mktplace-ingress:ingress",
  ]
)
k8s_resource(
  'mktplace-zookeeper', 
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services']
)
k8s_resource(
  'mktplace-kafka', 
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services'],
  port_forwards='9094:9094'
)
k8s_resource(
  'mktplace-kafka-control-center',
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services'],
  port_forwards='9021:9021'
)
k8s_resource(
  'mktplace-postgresql',
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services'],
  port_forwards='54323:5432'
)
k8s_resource(
  'mktplace-keycloak',
  trigger_mode=TRIGGER_MODE_AUTO,
  labels=['helm-services']
)

