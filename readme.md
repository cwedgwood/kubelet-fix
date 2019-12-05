This was created via the following:

1) clone k8s repo, checking out the desired branch and pulling in the patch:
```
git clone https://github.com/kubernetes/kubernetes
cd ./kubernetes
git checkout release-1.16
git remote add other https://github.com/yutedz/kubernetes
git fetch other
git cherry-pick 4ff054e5031af404dc6d2d9344c4ee3bad45f481
```

2) build the updated kubelet
```
build/run.sh make kubelet
```

3) the output of that copied into this repo:

```
cp ../kubernetes/_output/dockerized/bin/linux/amd64/kubelet ./
```

4) a docker image built

```
docker build -t port/kubelet:1.16-patched .
docker push port/kubelet:1.16-patched
```