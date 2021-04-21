Before Start
Make sure you Choco installed
- https://community.chocolatey.org/
Make sure you have Minikube installed
- https://minikube.sigs.k8s.io/docs/start/

First step
Install the wget for windows
choco install wget

Second step
Install the sed for windows: https://community.chocolatey.org/packages/sed
choco install sed

Tip:
If you have problems with ingress-nginx-controller-admission, execute this:
kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission

Third step
Start by createing an ingress for Keycloak
wget -q -O - https://raw.githubusercontent.com/keycloak/keycloak-quickstarts/latest/kubernetes-examples/keycloak-ingress.yaml | \
sed "s/KEYCLOAK_HOST/keycloak.$(minikube ip).nip.io/" | \
kubectl create -f -

get url for Keycloak
KEYCLOAK_URL=https://keycloak.$(minikube ip).nip.io/auth &&
echo "" &&
echo "Keycloak:                 $KEYCLOAK_URL" &&
echo "Keycloak Admin Console:   $KEYCLOAK_URL/admin" &&
echo "Keycloak Account Console: $KEYCLOAK_URL/realms/myrealm/account" &&
echo ""

Default login: admin
Default pw: admin