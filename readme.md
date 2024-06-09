# Практика

## 1. Подготовка окружения

Убедитесь, что у студентов установлены `kubectl` и `minikube` (или другой кластер Kubernetes).

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.5.0/components.yaml
kubectl patch -n kube-system deployment metrics-server --type=json \
  -p '[{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-insecure-tls"}]'
```

## 2. Создание Deployment

Создадим Deployment для веб-приложения на основе Nginx.

## 3. Создание Service

Создадим Service для нашего Deployment.

## 4. Создание Ingress

Создадим Ingress для маршрутизации трафика к нашему Service. Настроим `/etc/hosts` для доступа к Ingress:

```sh
echo "$(minikube ip) my-nginx.local" | sudo tee -a /etc/hosts
```

## 5. Создание ConfigMap

Создадим ConfigMap для хранения конфигурации.

Обновим Deployment для использования ConfigMap:

```yaml
    volumeMounts:
    - name: nginx-config
        mountPath: /usr/share/nginx/html
        subPath: index.html
    volumes:
    - name: nginx-config
      configMap:
        name: nginx-config
        items:
        - key: index.html
        path: index.html
```
## 6. Создание Horizontal Pod Autoscaler (HPA)

Создадим HPA для автоматического масштабирования наших подов.

## 7. Создание Job
Создадим Job для выполнения однократной задачи.
