# Summary

GoLang http web server running on port 8080 used to illustrate GitHub Actions as Continuous Deployment pipeline for GoLang static binary and OCI-compatible image published to Docker Hub and Github Container Registry.

Image is based on busybox:1.32.1-glibc, is small (~11Mb) because it takes advantage of multi-stage building

docker hub: https://hub.docker.com/r/fabianlee/golang-github-action-example

# Makefile targets
* docker-build (builds image)
* docker-test-fg (runs container in foreground, ctrl-C to exit)
* docker-run-bg (runs container in background)
* k8s-apply (applies deployment to kubernetes cluster)
* k8s-delete (removes deployment on kubernetes cluster)

# Create Github release

Must have [Go Lang](https://fabianlee.org/2022/10/29/golang-installing-the-go-programming-language-on-ubuntu-22-04/) compiler and [Github CLI](https://fabianlee.org/2022/04/21/github-cli-tool-for-repository-operations/) installed on local host as prerequisite.

Github Actions will automatically build OCI image based on tags that look like semantic version.

# Creating tag

```
newtag=v1.0.1
git commit -a -m "changes for new tag $newtag" && git push
git tag $newtag && git push origin $newtag
```

# Deleting tag

```
todel=v1.0.1

# delete local tag, then remote
git tag -d $todel && git push origin :refs/tags/$todel
```

# Deleting release

```
todel=v1.0.1

# delete release and remote tag
gh release delete $todel --cleanup-tag -y

# delete local tag
git tag -d $todel
```




