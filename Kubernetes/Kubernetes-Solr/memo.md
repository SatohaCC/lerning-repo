# 教材
ゼロから学ぶKubernetes × Solr運用
https://techbookfest.org/product/1qmwHdDEFeDXzGsNn0TB5h?productVariantID=eyBAVkuk35cF0NdTfaFWU0

## Kubernetes

## kind
https://kind.sigs.k8s.io/docs/user/quick-start/#installation


## kubectl
https://kubernetes.io/ja/docs/tasks/tools/install-kubectl-windows/
kubectlは、Kubernetesクラスターを操作するためのコマンドラインツールです。

## Helm
https://helm.sh/ja/docs/intro/install/
Helm は Kubernetes の パッケージマネージャー

## command
- kubectl apply -f pod.yaml
  - pod.yamlファイルに定義されたリソースをクラスターに適用する
  - 新規作成または更新時に使用
- kubectl get pods
  - クラスター内の全てのPodの一覧を表示
  - 状態や名前、IPアドレスなどの基本情報を確認可能

- kubectl exec -it my-deployment-6b567cdb75-2gkb8 -- /bin/bash

## Podの停止方法

### 1. 特定のpodを停止
```bash
kubectl delete pod <pod-name> -n <namespace>
```

### 2. ラベル指定でpodを停止
```bash
kubectl delete pod -l <label-key>=<label-value> -n <namespace>
```

### 3. デプロイメントのpodを停止（スケールダウン）
```bash
kubectl scale deployment <deployment-name> --replicas=0 -n <namespace>
```

### 4. namespace内の全podを停止
```bash
kubectl delete pods --all -n <namespace>
```

注意事項：
- podを直接削除すると、デプロイメントやレプリカセットによって自動的に再作成される可能性があります
- 本番環境では慎重に実行してください
- `-n <namespace>`は省略可能です（デフォルトのnamespaceを使用する場合）
