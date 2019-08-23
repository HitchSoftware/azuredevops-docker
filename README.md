# azuredevops-docker

This was slightly adapted from https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops.

 

Build:

docker build --rm -t hitchsoftware/dockeragent:arm-latest .


Swarm CLI Service:

docker service create \
  --with-registry-auth \
  --name dockeragent \
  --network {MY-NETWORK} \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  -e AZP_URL=https://dev.azure.com/{ORG-NAME} \
  -e AZP_TOKEN={PAT TOKEN} \
  -e AZP_AGENT_NAME={{.Node.Hostname}}-{{.Task.Slot}} \
  -e AZP_POOL={POOL-NAME} \
  hitchsoftware/dockeragent:arm-latest




