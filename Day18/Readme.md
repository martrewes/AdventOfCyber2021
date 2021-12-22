# `[Cloud]` Playing With Containers

## Premise
>Grinch Enterprises has been gloating about their attack on an underground forum. We know they were specifically targeting organizations in a campaign they've themed "Advent of Cyber" (AOC) - what a frustrating coincidence. Tracing the user back over time - we also encountered a reference to using AWS Elastic Container Registry (ECR) to store container images they use as infrastructure in their attacks. Let's see if we can find out more about the attack tooling Grinch Enterprises is using.


### What command will list container images stored in your local container registry? `****** ******`

<details>
  <summary>Answer:</summary>

```
docker images
```
</details>

### What command will allow you to save a docker image as a tar archive? `****** ****`

<details>
  <summary>Answer:</summary>

```
docker save
```
</details>

### What is the name of the file (including file extension) for the configuration, repository tags, and layer hash values stored in a container image? `********.****`

<details>
  <summary>Answer:</summary>

```
manifest.json
```
</details>

### What is the token value you found for the bonus challenge? `********************************`

```sh
$ sudo pacman -S docker
$ sudo systemctl enable docker
$ sudo systemctl start docker
$ sudo docker ps
...
$ sudo docker pull public.ecr.aws/h0w1j9u3/grinch-aoc:latest
latest: Pulling from h0w1j9u3/grinch-aoc
7b1a6ab2e44d: Pull complete 
7181c3c4941b: Pull complete 
148b30b9ae2d: Pull complete 
6f5a7c388565: Pull complete 
ef099323cb4a: Pull complete 
de5bf7e2abf0: Pull complete 
455d5424d859: Pull complete 
b1ee65a7e02a: Pull complete 
a47021107475: Pull complete 
Digest: sha256:593c79eaaa1a905c533e389b0034022e074969da3936df648172c4efc8d421d8
Status: Downloaded newer image for public.ecr.aws/h0w1j9u3/grinch-aoc:latest
public.ecr.aws/h0w1j9u3/grinch-aoc:latest
$ sudo docker save -o aoc.tar public.ecr.aws/h0w1j9u3/grinch-aoc:latest
$ sudo chown martin:martin aoc.tar
$ tar -xf aoc.tar
$ cd aoc/4416e55edf1a706527e19102949972f4a8d89bbe2a45f917565ee9f3b08b7682/
$ cat root/envconsul/config.hcl | grep 'token'
  # This is the token to use when communicating with the Vault server.
  # assumption that you provide it with a Vault token; it does not have the
  # incorporated logic to generate tokens via Vault's auth methods.
  token = "7095b3e9300542edadbc2dd558ac11fa"
  # This tells Envconsul to load the Vault token from the contents of a file.
  # - by default Envconsul will not try to renew the Vault token, if you want it
  # to renew you will need to specify renew_token = true as below.
...
```

<details>
  <summary>Answer:</summary>

```
7095b3e9300542edadbc2dd558ac11fa
```
</details>
