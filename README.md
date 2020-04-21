# gcp-cloud-build-local

## Introduction

Local Builder runs Google Cloud Build locally, allowing easier debugging, execution of builds on your own hardware, and integration into local build and test workflows.

The simplest way to describe the contents of cloudbuild.yaml is this: “You are specifying a list of arbitrary container images to be executed”.

```bash
docker run --rm $image-name $arg1 $arg2 $arg3 ...
docker run --rm $image-name $arg1 $arg2 $arg3 ...
docker run --rm $image-name $arg1 $arg2 $arg3 ...
```

## Run the tool locally

Download and extract the latest binaries available in the official Google Cloud Storage bucket.

```bash
curl https://storage.googleapis.com/local-builder/cloud-build-local_latest.tar.gz --output cloud-build-local_latest.tar.gz
mkdir cloud-build-local
tar -xf cloud-build-local_latest.tar.gz -C ./cloud-build-local/
```

Note: Run the build on a different platform using the following template

```bash
./cloud-build-local/cloud-build-local_{linux,darwin}_{386,amd64}-v0.5.0 --dryrun=false --config=cloudbuild.yaml --no-source
```

## Examples

Hello World - bash

```bash
./cloud-build-local/cloud-build-local_darwin_amd64-v0.5.0 --dryrun=false --config=examples/hello-world-bash.yaml --no-source --substitutions _MESSAGE='Hello World!'
```

```output
Using default tag: latest
latest: Pulling from cloud-builders/metadata
Digest: sha256:ab2c3c51dbd142d623c436627dad8e61db5afa5fbef3ad376af8fc2e10d5f4c6
Status: Image is up to date for gcr.io/cloud-builders/metadata:latest
gcr.io/cloud-builders/metadata:latest
2020/04/20 23:49:30 Started spoofed metadata server
2020/04/20 23:49:30 Build id = localbuild_52b1f50f-2a2e-41d3-9734-2996e68c2ee7
2020/04/20 23:49:30 status changed to "BUILD"
BUILD
: Already have image (with digest): ubuntu
: Hello World!
2020/04/20 23:49:30 Step  finished
2020/04/20 23:49:30 status changed to "DONE"
DONE
```

Hello World - Powershell

```bash
./cloud-build-local/cloud-build-local_darwin_amd64-v0.5.0 --dryrun=false --config=examples/hello-world-pwsh.yaml --no-source  --substitutions _MESSAGE='Hello World!'
```

```output
Using default tag: latest
latest: Pulling from cloud-builders/metadata
aad63a933944: Already exists 
139adc73af5f: Pull complete 
Digest: sha256:57690ba84e9b512fefaed96f50c5b3be9904208edd85abd8bcb0f972a1335aeb
Status: Downloaded newer image for gcr.io/cloud-builders/metadata:latest
gcr.io/cloud-builders/metadata:latest
2020/04/21 09:19:28 Started spoofed metadata server
2020/04/21 09:19:28 Build id = localbuild_60d5b9d9-c072-41fd-9c3e-105fbca5c92e
2020/04/21 09:19:28 status changed to "BUILD"
BUILD
: Pulling image: mcr.microsoft.com/powershell
: Using default tag: latest
: latest: Pulling from powershell
: 5bed26d33875: Already exists
: f11b29a9c730: Already exists
: 930bda195c84: Already exists
: 78bf9a5ad49e: Already exists
: 3183894b4ae2: Pulling fs layer
: 3183894b4ae2: Verifying Checksum
: 3183894b4ae2: Download complete
: 3183894b4ae2: Pull complete
: Digest: sha256:3c8fa7e4d1c2487287a8e3ad9748a74109ad6bd6133775d6f059f5a2338fce09
: Status: Downloaded newer image for mcr.microsoft.com/powershell:latest
: mcr.microsoft.com/powershell:latest
: Hello, World!
2020/04/21 09:19:37 Step  finished
2020/04/21 09:19:37 status changed to "DONE"
DONE
```

CURL

```bash
./cloud-build-local/cloud-build-local_darwin_amd64-v0.5.0 --dryrun=false --config=examples/curl.yaml --no-source  --substitutions _URL='https://api.ipify.org?format=json'
```

Output 

```output
2020/04/20 23:12:13 Warning: The server docker version installed (19.03.8) is different from the one used in GCB (18.09.0)
2020/04/20 23:12:13 Warning: The client docker version installed (19.03.8) is different from the one used in GCB (18.09.0)
Using default tag: latest
latest: Pulling from cloud-builders/metadata
Digest: sha256:ab2c3c51dbd142d623c436627dad8e61db5afa5fbef3ad376af8fc2e10d5f4c6
Status: Image is up to date for gcr.io/cloud-builders/metadata:latest
gcr.io/cloud-builders/metadata:latest
2020/04/20 23:12:23 Started spoofed metadata server
2020/04/20 23:12:23 Build id = localbuild_eca10e3a-590c-4e89-8cba-b4f271578afc
2020/04/20 23:12:23 status changed to "BUILD"
BUILD
: Already have image (with digest): gcr.io/cloud-builders/curl
: {"ip":"73.139.2.127"}
2020/04/20 23:12:24 Step  finished
2020/04/20 23:12:24 status changed to "DONE"
DONE
```

## Limitation

* Only one build can be run at a time on a given host.
* The tool works on the following platforms:
  * Linux
  * macOS

## References

* [Local Builder Github Repository](https://github.com/GoogleCloudPlatform/cloud-build-local)

## License

MIT - See [LICENSE](LICENSE) for more information.
