load('.tanzu/tanzu_tilt_extensions.py', 'tanzu_k8s_yaml')


SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", default='gcr.io/dap-local-workstation/sample-app-java-exe-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')

custom_build('gcr.io/dap-local-workstation/sample-app-java-exe',
    "tanzu apps workload apply -f config/workload.yaml --live-update \
      --local-path " + LOCAL_PATH + " --source-image " + SOURCE_IMAGE + " --yes && \
    .tanzu/wait.sh sample-app-java-exe",
  ['pom.xml', './target/classes'],
  live_update = [
    sync('./target/classes', '/workspace')
  ],
  skips_local_docker=True
)

tanzu_k8s_yaml('sample-app-java-exe', 'gcr.io/dap-local-workstation/sample-app-java-exe', './config/workload.yaml')
