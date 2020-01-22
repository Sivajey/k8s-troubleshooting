# Fixing the namespace which got stuck at terminating state

(
NAMESPACE=your-rogue-namespace
kubectl proxy &
kubectl get namespace $NAMESPACE -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize
)

ref: https://stackoverflow.com/a/53661717/9398070


# unable to retrieve the complete list of server APIs

kubectl get apiservice

if you see the AVAILABLE is false , delete them

ref: https://github.com/helm/helm/issues/6361#issuecomment-538220109