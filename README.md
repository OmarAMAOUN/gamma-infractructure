# gamma-infrastructure
to use argocd:
kubectl -n argocd port-forward svc/argocd-server 80:80
get argocd password:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
connect to postgres:
kubectl -n keycloak-prod run psql --rm -it --image ongres/postgres-util:v13.2-build-6.2 --restart=Never -- psql -h keycloak-postgresql-ha-pgpool postgres postgres