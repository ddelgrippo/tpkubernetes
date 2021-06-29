# tpkubernetes
# En el archivo "TP Kubernetes.doc" adjunto esta el paso a paso con imagenes y referencias mas concretas.

# Creacion del nuevo directorio
  $ mkdir drupal

# Ingresamos al directorio
  $ cd drupal

# SecretGenerator
  $  microk8s kubectl apply -k .

# Listamos el SecretGenerator
  $ microk8s kubectl get secrets
  
# Creamos Volumenes Locales
  $ microk8s kubectl apply -f drupal-pv.yaml
  $ microk8s kubectl apply -f mysql-pv.yaml

# Creamos los ClaimVolume
  $ microk8s kubectl apply -f drupal-pvc.yaml
  $ microk8s kubectl apply -f mysql-pvc.yaml

# Creamos los Deployments
  $ microk8s kubectl apply -f mysql.yaml
  $ microk8s kubectl apply -f drupal.yaml

# Verificamos la creacion de los objetos
  $ microk8s kubectl get pv
  $ microk8s kubectl get pvc
  $ microk8s kubectl get pod
  $ microk8s kubectl get deployment

# Verificamos los servicios
  $ microk8s kubectl get svc

# Se procede via web con la instalacion de Drupal y una vez que la misma finaliza se pueden aplicar los siguientes comandos:
  
  $ microk8s kubectl set image deployment drupal drupal=drupal:8.9 --all   # para hacer update de la app
  
  $ microk8s kubectl rollout undo deployment/drupal # para volver a la version anterior
  
# Redireccion de puertos
  $ microk8s kubectl port-forward deployment/drupal 8080:80 --address 0.0.0.0

  
  


