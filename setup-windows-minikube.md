## Before Start
#### Make sure you have Choco installed
* https://community.chocolatey.org/
#### Make sure you have Minikube installed
* https://minikube.sigs.k8s.io/docs/start/

### First step
Install the wget for windows </br>
```choco install wget ```

### Second step
Install the sed for windows </br>
``` choco install sed ```

#### Tip:
If you have problems with ingress-nginx-controller-admission, execute this: </br>
``` kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission ```

### Third step
create a keycloak deployment as a service
```kubectl create -f https://raw.githubusercontent.com/keycloak/keycloak-quickstarts/latest/kubernetes-examples/keycloak.yaml```

### Fourth step
Start by createing an ingress for Keycloak </br>
``` wget -q -O - https://raw.githubusercontent.com/keycloak/keycloak-quickstarts/latest/kubernetes-examples/keycloak-ingress.yaml | \ ```
``` sed "s/KEYCLOAK_HOST/keycloak.$(minikube ip).nip.io/" | \ ```
``` kubectl create -f - ```

##### get url for Keycloak ingress </br>
``` KEYCLOAK_URL=https://keycloak.$(minikube ip).nip.io/auth && ```
``` echo "" && ```
``` echo "Keycloak:                 $KEYCLOAK_URL" && ```
``` echo "Keycloak Admin Console:   $KEYCLOAK_URL/admin" && ```
``` echo "Keycloak Account Console: $KEYCLOAK_URL/realms/myrealm/account" && ```
``` echo "" ```

##### get url for Keycloak without ingress
```KEYCLOAK_URL=http://$(minikube ip):$(kubectl get services/keycloak -o go-template='{{(index .spec.ports 0).nodePort}}')/auth &&```
```echo "" &&```
```echo "Keycloak:                 $KEYCLOAK_URL" &&```
```echo "Keycloak Admin Console:   $KEYCLOAK_URL/admin" &&```
```echo "Keycloak Account Console: $KEYCLOAK_URL/realms/myrealm/account" &&```
```echo ""```

##### Default login: admin
##### Default pw: admin
