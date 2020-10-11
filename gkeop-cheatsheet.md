# GKE on-prem Cheat Sheet
GKE on-prem でよく使うコマンドライン集 (2020.10 版)

## gkeadm

### Admin Workstation 用 Config (admin-ws-config.yaml) の作成

```bash
gkeadm create config
```

### Admin Workstation 作成 (Service Accounts も自動的に作成)

```bash
gkeadm create admin-workstation --auto-create-service-accounts
```

### Admin Workstation アップグレード
[AW_CONFIG_FILE] に Admin Workstation の Config を指定
[INFO_FILE] にAdmin Workstation の Information File (gke-admin-ws-**** を指定)
```bash
gkeadm upgrade admin-workstation --config [AW_CONFIG_FILE] --info-file [INFO_FILE]
```

### 旧バージョンの Admin Workstation へのロールバック

```bash
gkeadm rollback admin-workstation
```

### Admin Workstation のリストア
Admin-Workstation アップグレード時のバックアップファイルからのリストア
```bash
gkeadm create admin-workstation --restore-from-backup [ADMIN-WORKSTATION-NAME]-backup.tar.gz
```

## gkectl

### Admin Cluster の Config チェック

```bash
gkectl check-config --config admin-cluster.yaml
```

### Node Image のアップロード

```bash
gkectl prepare --config admin-cluster.yaml --skip-validation-all
```

### Admin Cluster 用 LoadBalancerの作成

```bash
gkectl create loadbalancer --config admin-cluster.yaml
```

### Admin Cluster のインストール

```bash
gkectl create admin --config admin-cluster.yaml
```

### User Cluster の Config チェック

```bash
gkectl check-config --kubeconfig kubeconfig --config user-cluster.yaml 
```

### User Cluster 用 LoadBalancerの作成

```bash
gkectl create loadbalancer --config user-cluster.yaml --kubeconfig kubeconfig
```

### User Cluster のインストール

```bash
gkectl create cluster --config user-cluster.yaml --kubeconfig kubeconfig
```
