---


copyright:
  years: 2016, 2019
lastupdated: "2019-10-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

Helm is a powerful and flexible package-management and operations tool for Kubernetes. Generally, this default helm installation applies no security configurations.
Our CFEE service didn't enable `secure tiller` before 4.0.0 release, so if you use the release before 4.0.0 and then maybe you can ignore this document. But if you want upgrade to 4.0.0 version or deploy CFEE 4.0.0 or higher version release, this document may help you to run helm commands with `tiller tls` enabled.

# How could you run a helm command with secure tiller enabled?
### confirm your environment is enabled secure tiller or not:
```
kubectl get secret helm-secret -n kube-system
```
Run above command, if it returns nothing, it means that the secure tiller is not enabled on your environment. Or the environment is enabled with secure tiller.

### Get helm cert, helm key and ca cert to connect tiller
In enabled secure tiller environment, if you want to connect tiller server with helm cli, you need to get helm cert, helm key and ca cert, first. Then when you run a helm command , `tls_params` (tls-ca-cert, tls-cert, tls-key) should be added.

* Get private CA and certs/keys
```
kubectl get secret helm-secret -n kube-system -o json | jq -r '.data."helm.cert"' | base64 --decode > "${HELM_SECRET_DIR}"/helm.cert.pem
kubectl get secret helm-secret -n kube-system -o json | jq -r '.data."helm.key"' | base64 --decode > "${HELM_SECRET_DIR}"/helm.key.pem
kubectl get secret helm-secret -n kube-system -o json | jq -r '.data."ca.cert"' | base64 --decode > "${HELM_SECRET_DIR}"/ca.cert.pem
```
```{HELM_SECRET_DIR}``` is the path where you want to save these files.
Note: `jq` command should be installed in your machine.

* Add tls parameters
```
helm_cert_path="${HELM_SECRET_DIR}/helm.cert.pem"
helm_key_path="${HELM_SECRET_DIR}/helm.key.pem"
ca_cert_path="${HELM_SECRET_DIR}/ca.cert.pem"
tls_params="--tls --tls-ca-cert ${ca_cert_path} --tls-cert ${helm_cert_path} --tls-key ${helm_key_path}"
```

Now, you can run your helm commands with `tls_params` , such as `helm list` on environment where secure tiller enabled, it should be changed as below:
```
helm list ${tls_params}
```

Actually, if you think it's so tedious to add ${tls_params} every time. You can move the key, cert, and CA into $HELM_HOME:
```
cp ca.cert.pem $(helm home)/ca.pem
cp helm.cert.pem $(helm home)/cert.pem
cp helm.key.pem $(helm home)/key.pem
``` 
Then you can simply run `helm list --tls`.