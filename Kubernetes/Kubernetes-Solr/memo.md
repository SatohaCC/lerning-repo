# Kubernetes × Solr運用メモ

## 参考教材
- ゼロから学ぶKubernetes × Solr運用
  - URL: https://techbookfest.org/product/1qmwHdDEFeDXzGsNn0TB5h?productVariantID=eyBAVkuk35cF0NdTfaFWU0

## 必要なツール

### kind
- Kubernetesクラスターをローカルで実行するためのツール
- インストール: https://kind.sigs.k8s.io/docs/user/quick-start/#installation

### kubectl
- Kubernetesクラスターを操作するためのコマンドラインツール
- インストール: https://kubernetes.io/ja/docs/tasks/tools/install-kubectl-windows/

### Helm
- Kubernetesのパッケージマネージャー
- インストール: https://helm.sh/ja/docs/intro/install/

## 基本的なコマンド

### リソースの適用
```bash
kubectl apply -f pod.yaml  # pod.yamlファイルに定義されたリソースをクラスターに適用
```

### リソースの確認
```bash
kubectl get pods  # クラスター内の全てのPodの一覧を表示
```

### Podへの接続
```bash
kubectl exec -it <pod-name> -- /bin/bash  # 指定したPodにシェルで接続
```

## Podの停止方法

### 1. 特定のPodを停止
```bash
kubectl delete pod <pod-name> -n <namespace>
```

### 2. ラベル指定でPodを停止
```bash
kubectl delete pod -l <label-key>=<label-value> -n <namespace>
```

### 3. デプロイメントのPodを停止（スケールダウン）
```bash
kubectl scale deployment <deployment-name> --replicas=0 -n <namespace>
```

### 4. namespace内の全Podを停止
```bash
kubectl delete pods --all -n <namespace>
```

## 注意事項
- Podを直接削除すると、デプロイメントやレプリカセットによって自動的に再作成される可能性があります
- 本番環境では慎重に実行してください
- `-n <namespace>`は省略可能です（デフォルトのnamespaceを使用する場合）
