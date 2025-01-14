- Thiết lập kuberconfig
  doctl kubernetes cluster kubeconfig save be78db94-e760-4dcb-b5af-14b0df05788d

- Tạo Secret cho Docker Registry (DigitalOcean)
  kubectl create secret docker-registry regcred --docker-server=registry.digitalocean.com --docker-username=mailyhai --docker-password=<secret-key> --docker-email=mailyhai814@gmail.com

- Cài đặt metric server để lấy thông tin tài nguyên phục vụ cho autoscale
  kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

- Tạo deployment.yaml để cho k8s biết cần deploy gì
- Tạo service dể expose ứng dụng
- Tạo ConfigMap để lưu trữ các cấu hình dạng key-value cho service
- Tạo hpa.yaml để cấu hình hpa

- Triển khai các file yaml
  kubectl apply -f configmap.yaml
  kubectl apply -f deployment.yaml
  kubectl apply -f services.yaml
  kubectl apply -f hpa.yaml

- Kiểm tra trạng thái
  kubectl get pods
  kubectl get services
  kubectl get hpa

- Kiểm tra thông tin chi tiết dịch vụ
  kubectl describe service thda-app-service
- Lấy ra tên các deployments
  kubectl get deployments
- Update image khi build bản mới
  kubectl set image deployment/<Tên deployment> <Tên container>=<Tên image>:latest
  kubectl set image deployment/thda-app-deployment thda-app=registry.digitalocean.com/thda/thda-app:latest

- Restart pod
  kubectl rollout restart deployment/<Tên deployment>
  kubectl rollout restart deployment/thda-app-deployment
- Xóa 1 pod trong cluster
  kubectl delete pod thda-app-deployment-6ffbcf5645-rw4m7

- Giảm số lượng replicas thủ công
  kubectl scale deployment thda-app-deployment --replicas=2
