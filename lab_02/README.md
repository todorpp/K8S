This is the same code from lab_02, but this time we will deploy it using a declarative approach. Instead of doing it manually with commands, we will create files that serve as a blueprint for our desired state.

The selector is a tool that binds different objects by correlating them using identifiers. All identifiers should match for the selector to apply correctly:
selector:
  app: second-app
  tier: backend
  
Activate the deployment by running:
kubectl apply -f deployment.yaml

When changes are needed, simply update the file and re-apply it.

This option will perform health checks:
livenessProbe:
            httpGet:
              path: /
              port: 8080
            periodSeconds: 15
            initialDelaySeconds: 5
