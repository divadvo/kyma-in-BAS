# Kyma tooling setup in SAP Business Application Studio

Follow the [SAP Tutorial](https://developers.sap.com/tutorials/cp-kyma-download-cli.html) with some adjustments for BAS, described below.

Open Terminal in BAS: `Terminal > New Terminal`


## Step 1 from SAP tutorial


Follow [linked guide for Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/). Installation with curl.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

`sudo` can't be used in BAS. So install locally instead

```bash
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
```

Add this location to PATH in `.bashrc`

```bash
cd /home/user
nano .bashrc  (or vim .bashrc)
```

Add at the end of the file and save: 

```bash
export PATH=~/.local/bin:$PATH
```

Check install:

```bash
kubectl version --client
```


## Step 2 from SAP tutorial

First, install krew (kubectl plugin manager). Follow [guide for Linux, bash shell](https://krew.sigs.k8s.io/docs/user-guide/setup/install/)

```bash
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)
```

Add to PATH to .bashrc at the end of the file like before

```bash
nano .bashrc
Add: export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"

```

Install `oidc-login` plugin

```bash
kubectl krew install oidc-login
```


## Step 3 from SAP tutorial

Follow as is

## Step 4 from SAP tutorial

Follow as is


## Step 5 from SAP tutorial

Open folder `/home/user`

![Open folder](/images/01_open_folder.png)

Upload `kubeconfig.yaml` to BAS to that folder by right clicking in the file explorer

![Upload file](/images/02_upload_file.png)



```bash
export KUBECONFIG=/home/user/kubeconfig.yaml
```

Test:

```bash
kubectl config get-contexts
```