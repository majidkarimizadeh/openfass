# Faas-cli

#### Installing faas cli on Mac
```
brew install faas-cli
```

#### Browse available templates from the official store
```
faas-cli template store list
```

# Deploy openfass to a Kubernetes cluster
#### Install arkade
```
brew install arkade
```

#### Install openfaas
```
arkade install openfaas
```

#### Get openfaas info
```
arkade info openfaas
```

#### Forward the gateway to your machine
```
kubectl rollout status -n openfaas deploy/gateway
kubectl port-forward -n openfaas svc/gateway 8080:8080
```

####  If basic auth is enabled, you can now log into your gateway:
```
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
echo -n $PASSWORD | faas-cli login --username admin --password-stdin
```

# Create and deploy function

#### Generate a function
```shell
# faas-cli new <FUNCTION_NAME> --lang <TEMPLATE>
faas-cli new node-hello-world --lang node12
```
> Make sure in the `node-hello-world.yml` file you changed the `image` attribute and pointed it to the correct registry path.

#### Build the function
```shell
# faas-cli build -f <FUNCTION_NAME>.yml
faas-cli build -f node-hello-world.yml
```

#### Push the function to the registry
```shell
# faas-cli push -f <FUNCTION_NAME>.yml
faas-cli push -f node-hello-world.yml
```

#### Deploy the function
```shell
# faas-cli deploy -f <FUNCTION_NAME>.yml
faas-cli deploy -f node-hello-world.yml
```

#### Alternative command for build, push and deploy
```shell
# faas-cli up -f <FUNCTION_NAME>.yml
faas-cli up -f node-hello-world.yml
```

#### Remove function 
```shell
# faas-cli rm -f <FUNCTION_NAME>.yml
faas-cli rm -f node-hello-world.yml
```

https://www.openfaas.com/

https://chaoscodes.github.io/2019/06/11/My-first-try-in-OpenFass/
