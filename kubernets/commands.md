
1) Docker obrazni Kubernetsda arm64 qlib kutarish? ```docker buildx create --use && docker buildx build --platform linux/arm64 -t flask-app:v1 --load .```
2) Docker obrazni Docker Hub ga yuborish? ```docker login -u fayozdevopser && docker tag todo:v2 fayozdevops/todo:v2 && docker push fayozdevopser/todo:v2```
                                        
                                        
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
1) Deploymentni ishga tushirish uzimning namespace imda arm64 archtictureda?  ```kubectl create deploy tic-tac-toe --image m2yy5eu3z/tic-tac-toe:arm64 --replicas 1 --port 3000 -n f-absoatov```
2) Deploymentlar ruyxatini kurish? ```kubectl get deployment -n f-absoatov```
3) Replicasetlar ruyxatini kurish? ```kubectl get replicaset -n f-sadatov```
4) Pod lar ruyxatini kurish? ```kubectl get pods -n f-absoatov```
5) Replica larning sonini scale orqali kupaytirish? ```kubectl scale deploy tic-tac-toe --replicas 5 -n f-absoatov```
6) Deployment yaml faylni generatsiya qilish va yaml fayilga yozib quyish? ```kubectl create deploy tic-tac-toe --image m2yy5eu3z/tic-tac-toe:arm64 --replicas 1 --port 3000 -n f-absoatov --dry-run=client -o yaml > tic-tac-toe-deployment.yaml```
8) Как опубликовать deployment через Service? ```kubectl expose deployment flask-app --port 80 --target-port 5000 -n f-absoatov```
9) Service lar ruyxatini kurish? ```kubectl get service -n f-absoatov```
10) Pod ichiga kirish  ? ```kubectl -n f-absoatv exec -it nginx -- bash```
11) Как опубликовать deployment через NodePort? ```kubectl expose deployment nginx-arm --port 80 --target-port 80 --type NodePort -n f-absoatov```
13) Как изменить deployment файл напрямую из CLI? ```kubectl edit deployment/nginx-deploy```
14) Obnavit qilish nginx imperativniy usulda ? ```kubectl set image deployment/my-deployment my-container=nginx:1.19.2```
Imperativ yangilash — bu siz tizimga “ana shuni bajar” deb aniq ko'rsatma berasiz.
``` kubectl set image deployment/my-app my-app=nginx:1.19 ```
15) Deklarativ yangilash — bu siz “mana bunday holatga yet” deb aytasiz, tizim o'zi qanday bajarishni aniqlaydi.
``` kubectl apply -f deployment.yaml ```

                                    Ingress
1) Ingress yaratish va yaml fayl ga yozish ? ```kubectl create ingress flaskapp-clusterip-ingress --rule="f-absoatov.sts404.uz/*=cluster-ip-service:80" --class nginx -n f-absoatov --dry-run=client -o yaml > ingress.yaml```
   Unutmang spec polyasiga qushish kerak quyidagini :   ingressClassName: nginx

                                     Check
1) Для проверки какого то запроса какой образ использовать ? ```kubectl run check-pod --image nicolaka/netshoot -n fayoz-final -- sleep infinity```
