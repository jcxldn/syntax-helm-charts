# helm-charts/snipeit
[Snipeit-IT](http://www.snipeitapp.com) is open source software. Transparency, security and oversight is at the heart of everything we do. No vendor lock-in again, ever.

## introduction
This helm chart uses for the database the bitnami mariadb database as dependency.

Also the official container image from snipe is used.

You dont need to generate the lavarel app key, at the first start a job generates it for you and store it as a secret. Upgrades dont overite it because a check prevents this.

You only need to overite the default values with your own values and youre done. 

## install 
- helm repo add syntax3rror404  https://syntax3rror404.github.io/helm-charts/charts
- helm install snipeit syntax3rror404/snipeit -n snipeit --create-namespace

## upgrade
- helm upgrade snipeit syntax3rror404/snipeit -n snipeit

## uninstall 
- helm uninstall snipeit -n snipeit
- kubectl delete ns snipeit