1) Установка prometheus
```
helm install moni-stack prometheus-community/kube-prometheus-stack -n monitoring
```

2) Все что связано с prometheus (ставил через helm)
```
g2xdimix2@cloudshell:~$ kubectl get all -n monitoring
NAME                                                         READY   STATUS    RESTARTS   AGE
pod/alertmanager-moni-stack-kube-prometheus-alertmanager-0   2/2     Running   0          3h33m
pod/moni-stack-grafana-775575b7bd-cjrvd                      3/3     Running   0          3h33m
pod/moni-stack-kube-prometheus-operator-7647956c96-7pnr7     1/1     Running   0          3h33m
pod/moni-stack-kube-state-metrics-6bf7984f77-b52kj           1/1     Running   0          3h33m
pod/moni-stack-prometheus-node-exporter-jbq5c                1/1     Running   0          3h33m
pod/moni-stack-prometheus-node-exporter-sjr2c                1/1     Running   0          3h33m
pod/moni-stack-prometheus-node-exporter-vch2n                1/1     Running   0          3h33m
pod/prometheus-moni-stack-kube-prometheus-prometheus-0       2/2     Running   0          3h33m

NAME                                              TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
service/alertmanager-operated                     ClusterIP   None          <none>        9093/TCP,9094/TCP,9094/UDP   3h34m
service/moni-stack-grafana                        ClusterIP   10.8.7.14     <none>        80/TCP                       3h33m
service/moni-stack-kube-prometheus-alertmanager   ClusterIP   10.8.2.228    <none>        9093/TCP                     3h33m
service/moni-stack-kube-prometheus-operator       ClusterIP   10.8.5.184    <none>        443/TCP                      3h33m
service/moni-stack-kube-prometheus-prometheus     ClusterIP   10.8.11.196   <none>        9090/TCP                     3h33m
service/moni-stack-kube-state-metrics             ClusterIP   10.8.14.45    <none>        8080/TCP                     3h33m
service/moni-stack-prometheus-node-exporter       ClusterIP   10.8.1.227    <none>        9100/TCP                     3h33m
service/prometheus-operated                       ClusterIP   None          <none>        9090/TCP                     3h34m

NAME                                                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/moni-stack-prometheus-node-exporter   3         3         3       3            3           <none>          3h33m

NAME                                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/moni-stack-grafana                    1/1     1            1           3h33m
deployment.apps/moni-stack-kube-prometheus-operator   1/1     1            1           3h33m
deployment.apps/moni-stack-kube-state-metrics         1/1     1            1           3h33m

NAME                                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/moni-stack-grafana-775575b7bd                    1         1         1       3h33m
replicaset.apps/moni-stack-kube-prometheus-operator-7647956c96   1         1         1       3h33m
replicaset.apps/moni-stack-kube-state-metrics-6bf7984f77         1         1         1       3h33m

NAME                                                                    READY   AGE
statefulset.apps/alertmanager-moni-stack-kube-prometheus-alertmanager   1/1     3h33m
statefulset.apps/prometheus-moni-stack-kube-prometheus-prometheus       1/1     3h33m

NAME                                                   COMPLETIONS   DURATION   AGE
job.batch/prome-1-kube-prometheus-st-admission-patch   1/1           5s         3h33m
```

3) Установка nginx через kubectl
  
4) Все что связано с nginx
```
Cg2xdimix2@cloudshell:~kubectl get all -n nginx
NAME                         READY   STATUS    RESTARTS   AGE
pod/nginx-5f6bbdbbfc-j8g2k   2/2     Running   0          95m
pod/nginx-5f6bbdbbfc-n2whr   2/2     Running   0          95m
pod/nginx-5f6bbdbbfc-zbptc   2/2     Running   0          95m

NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)           AGE
service/nginx   ClusterIP   10.8.5.73    <none>        80/TCP,9990/TCP   93m

NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx   3/3     3            3           95m

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-5f6bbdbbfc   3         3         3       95m
```

5) Проверка работоспособности Prometheus
`
kubectl port-forward service/moni-stack-kube-prometheus-prometheus -n monitoring 9090:909
`
```
g2xdimix2@cloudshell:~$ curl http://127.0.0.1:9090/targets
<!doctype html><html lang="en"><head><meta charset="utf-8"/><link rel="shortcut icon" href="./favicon.ico"/><meta name="viewport" content="width=device-width,initial-scale=1,shrink-to-fit=no"/><meta name="theme-color" content="#000000"/><script>const GLOBAL_CONSOLES_LINK="",GLOBAL_AGENT_MODE="false"</script><link rel="manifest" href="./manifest.json" crossorigin="use-credentials"/><title>Prometheus Time Series Collection and Processing Server</title><script defer="defer" src="./static/js/main.8ea0e5d3.js"></script><link href="./static/css/main.faad45b4.css" rel="stylesheet"></head><body class="bootstrap"><noscript>You need to enable JavaScript to run this app.</noscript><div id="root"></div></body></html>g2xdimix2@cloudshell:~$ curl http://127.0.0.1:9090/targets
```

6) Проверка работоспособности Grafana
`kubectl port-forward service/moni-stack-grafana -n monitoring 8000:80 `
```
g2xdimix2@cloudshell:~$ curl http://127.0.0.1:8000/targets
<a href="/login">Found</a>.
```
