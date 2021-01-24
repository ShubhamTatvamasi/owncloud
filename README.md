# owncloud

Install owncloud:
```bash
kubectl create deployment owncloud --image=owncloud
kubectl expose deployment owncloud --port=80 --name=owncloud
```

Setup ingress:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: owncloud
spec:
  tls:
    - hosts:
      - owncloud.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: owncloud.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: owncloud
            servicePort: 80
EOF
```

Delete everything:
```bash
kubectl delete deploy/owncloud svc/owncloud ing/owncloud
```
