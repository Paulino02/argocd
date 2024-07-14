# Argo CD project
## Comandos
create a namespace 
-> kubectl create -ns argocd

instalando o argocd dentro do cluster
-> kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

getting initial admin password
-> kubectl get secret -n argocd argocd-initial-admin-secret -o yaml
-> kubectl get secret -n argocd argocd-initial-admin-secret -o yaml | grep 'password:' | awk '{print $2}' | base64 --decode | xargs echo

accessing argocd server
-> kubectl port-forward svc/argocd-server -n argocd 8080:443
-> open browser https://localhost:8080/
