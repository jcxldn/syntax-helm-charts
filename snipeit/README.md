# helm-charts/snipeit
[Snipeit-IT](http://www.snipeitapp.com) is open source software. Transparency, security and oversight is at the heart of everything we do. No vendor lock-in again, ever.

## introduction
This helm chart uses for the database the bitnami mariadb database as dependency.

Also the official container image from snipe is used.

You dont need to generate the lavarel app key, at the first start a job generates it for you and store it as a secret. Upgrades dont overite it because a check prevents this.

You only need to overite the default values with your own values and youre done. 

## install 
- `helm repo add syntax3rror404  https://syntax3rror404.github.io/helm-charts/charts`
- `helm install snipeit syntax3rror404/snipeit -n snipeit --create-namespace`

## upgrade
- `helm upgrade snipeit syntax3rror404/snipeit -n snipeit`

## uninstall 
- `helm uninstall snipeit -n snipeit`
- `kubectl delete ns snipeit`

## customisation
Please note that a simple install only use default variables like example.com for the url or unsafe passwords for the database. Please create your own values file.

For all possible values please take a look to the values file.

Value    | Default  | Description
-------- | -------- | --------
mariadb.global.defaultStorageClass   | "longhorn"   | storage class for mariadb
mariadb.auth.rootPassword   | "adminsecret"   | root password to be generated for mariadb
mariadb.auth.database  | "snipeit"   | mariadb database name to be created for snipeit app
mariadb.auth.username  | "snipeit"   | mariadb database user to be created for snipeit app
mariadb.auth.password  | "snipeitdbsecret"   | mariadb database password to be created for snipeit app
snipeit.config.persistence.storageClass   | "longhorn"   | storage class for snipeit
snipeit.config.persistence.size   | "2Gi"   | storage space for snipeit
snipeit.config.url   | "http://snipeit.example.com"   | App url for snipeit 
snipeit.config.timezone   | "Europe/Berlin"   | App timezone
snipeit.config.locale   | "en"   | App locale
image.repository  | "docker.io/snipe/snipe-it"   | image repo for snipeit app
image.tag  | "v8.0.4-alpine"   | image tag for snipeit app
ingress.enabled   | "false"   | use ingress
ingress.className   | ""   | ingress name like nginx
ingress.annotations   | {}   | ingress annotations
ingress.hosts   | list   | list of hosts

### customisation example
For example this values file you can install it with:

- `helm install snipeit syntax3rror404/snipeit -n snipeit --create-namespace -f myvaules.yaml`


```yaml
# myvaules.yaml
---
mariadb:
  global:
    defaultStorageClass: "longhorn"
  auth:
    rootPassword: 12h5j3k5hjk2345h
    password: "23jk65h3jk643"

snipeit:
  config:
    url: https://snipeit.mycooldomain.com
  persistence:
    size: 20Gi
    storageClass: longhorn

ingress:
  enabled: true
  className: "nginx"
  annotations: {}
  hosts:
    - host: snipeit.mycooldomain.com
      paths:
        - path: /
          pathType: Prefix
  tls: 
    - secretName: snipeit-tls
      hosts:
        - snipeit.mycooldomain.com
```
