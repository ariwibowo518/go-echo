# test-argocd

# create a new namespace
kubectl create ns argo-app

# apply the changes
kubectl -n argo-app kustomize infra/ | kubectl -n argo-app apply -f -

# check all components are running
kubectl get all -n argo-app

# port forward to access health router
kubectl port-forward --address 0.0.0.0 service/argo-app -n argo-app 3000:3000


# install argocd

# Installing ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.8.4/manifests/install.yaml
kubectl get all -n argocd
kubectl port-forward svc/argocd-server -n argocd 8080:443

now lets go to browser with http://localhost:8080

# retrieve password from secret in argocd namespace

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

# the default login username is ```admin``` with the password we took above

# Create SSH KEY

ssh-keygen

Your identification has been saved in /Users/kowlon/.ssh/id_ed25519
Your public key has been saved in /Users/kowlon/.ssh/id_ed25519.pub

# insert pub key to your repo

https://github.com/<your-username>/<your-repo>/settings/keys
insert you private key