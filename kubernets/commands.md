
1) Docker obrazni arm64 qlib kutarish? ```docker buildx create --use && docker buildx build --platform linux/arm64 -t flask-app:v1 --load .```
2) Docker obrazni Docker Hub ga yuborish? ```docker login -u fayozdevops && docker tag todo:v2 fayozdevops/todo:v2 && docker push fayozdevops/todo:v2```
                                        
                                        
                                        POD


1) Config yaml fayilni kubernetsga expose qilish?  ```export KUBECONFIG=/home/fayoz/config.yaml```
2) Kontekstlar ro'yxatini ko'rsatish?  ```kubectl config get-contexts```
3) Kubernetsda nodelar ruyxatini kurish? ```kubectl get nodes```
4) Kubernetsda namespacelar ruyxatini kurish? ```kubectl get namespaces```
5) O'zimning namespace imni yaratish ? ```kubectl create namespace f-absoatov```
6) Barcha podlarni json formatda kurish? ```kubectl get pods -o json```
7) Pod larni kengaytirilgan formadda kurish? ```kubectl get pods -o wide```
8) Pod larning holatini online holatini kurish ? ```kubectl get pods --watch```
9) Pod yaratish malum bir image yordamida uzimni ns imda nginx-fayoz?  ```kubectl run nginx-fayoz --image nginx:latest --port 80 -n f-absoatov```
10) Pod uchun manifest fayil generatsiya qilish ? ```kubectl run nginx-fayoz --image nginx:latest --port 80 --dry-run=client -o yaml -n f-absoatov > nginx-absoatov.yaml```
11) Pod ni generatsiya qilingan fayl orqali ishga tushirish? ```kubectl apply -f nginx-absoatov.yaml```
12) Pod ning loglarini kurish ? ``` kubectl logs my-pod ```
13) Localniy portni poni portiga yunaltirish ? ``` kubectl port-forward my-pod 8080:80 ```
14) Pod ni detallari bilan kursatish ? ``` kubectl describe pod <pod-name>```

                                     Deployment
1) Как запустить deployment под своим namespace-ом?  ```kubectl create deploy tic-tac-toe --image m2yy5eu3z/tic-tac-toe:arm64 --replicas 1 --port 3000 -n f-sadatov```
2) Как посмотреть список deployment? ```kubectl get deployment -n f-sadatov```
3) Как посмотреть список replicaset? ```kubectl get replicaset -n f-sadatov```
4) Как посмотреть список pod-ов? ```kubectl get pods -n f-sadatov```
5) Как увеличить количество реплик deployment? ```kubectl scale deploy tic-tac-toe --replicas 5 -n f-sadatov```
6) Как сгенирировать deployment файл и записать в yaml файл? ```kubectl create deploy tic-tac-toe --image m2yy5eu3z/tic-tac-toe:arm64 --replicas 1 --port 3000 -n f-sadatov --dry-run=client -o yaml > tic-tac-toe-deployment.yaml```
7) Как посмотреть статус pod-a? ```kubectl describe pod tic-tac-toe-7474ff488c-bsqzz -n f-sadatov```
8) Как опубликовать deployment через Service? ```kubectl expose deployment flask-app --port 80 --target-port 5000 -n f-sadatov```
9) Как посмотреть список Service? ```kubectl get service -n f-sadatov```
10) Как зайти внутрь pod-a ? ```kubectl -n f-sadatov exec -it nginx -- bash```
11) Как опубликовать deployment через NodePort? ```kubectl expose deployment nginx-arm --port 80 --target-port 80 --type NodePort -n f-sadatov```
13) Как изменить deployment файл напрямую из CLI? ```kubectl edit deployment/nginx-deploy```
14) Как обновить версию nginx через императивным способом? ```kubectl set image deployment/my-deployment my-container=nginx:1.19.2```

                                    Ingress
1) Как создать ingress? ```kubectl create ingress flaskapp-clusterip-ingress --rule="f-sadatov.sts404.uz/*=cluster-ip-service:80" --class nginx -n f-sadatov --dry-run=client -o yaml > ingress.yaml```
   Не забудь добавить добавить в поле spec следующий запись:   ingressClassName: nginx

                                     Check
1) Для проверки какого то запроса какой образ использовать ? ```kubectl run check-pod --image nicolaka/netshoot -n exam-farrukh -- sleep infinity```
