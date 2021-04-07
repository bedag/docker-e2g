<!-- - Copyright © 2021 Bedag Informatik AG Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License. -->

 # e2guardian Docker Image

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![docker-publish](https://github.com/bedag/docker-e2g/workflows/docker-publish/badge.svg) [![Dockerhub](https://img.shields.io/docker/pulls/bedag/e2g?style=plastic)](https://hub.docker.com/r/bedag/e2g)

![Bedag](https://www.bedag.ch/wGlobal/wGlobal/layout/images/logo.svg)

This is a docker project for [e2guardian](https://github.com/e2guardian/e2guardian/).

Find images on [dockerhub](https://hub.docker.com/repository/docker/bedag/e2g).

## Usage

Run the container like this:

```
docker run -v /usr/local/e2guardian/etc/e2guardian/:${PWD}/config bedag/e2g:<tag>
```

## Volumes

Make sure that all volumes are owned by nobody(65534).

Mountpoint                            | Description
------------------------------------- | ----------------------------------
/usr/local/e2guardian/var/log/        | log file for e2guardian
/usr/local/e2guardian/var/run/        | pid file for e2guardian
/usr/local/e2guardian/etc/e2guardian/ | configuration files for e2guardian

## Build

Docker builds are created with [bedag/image-build](https://github.com/bedag/image-build).

[musl compiler](https://www.musl-libc.org/how.html) is used to compile e2guardian.

`gcr.io/distroless/cc` are used because we do not need any common linux binaries, [here](https://github.com/GoogleContainerTools/distroless) you can find more information about distroless images. For troubleshooting we recommend to use our `-debug` images. For more information go to [Debug](#Debug) section.

Every Sunday(`0 0 * * SUN`) we automatically update all [supported tags](#Tags) with the current upstream image.

## Debug

In our production image there are no binaries for troubleshooting. Therefore if u like to troubleshoot you should use our debug image like this:

```
docker run -it bedag/e2g:latest-debug
docker run -it bedag/e2g:5-debug
```

In the debug image busybox is installed. You can find all busybox supported commands like this:

```
busybox --list
```

## Tags

Supported tags are:

- `latest`, `5`, `5.3`, `5.3.5`, `latest-debug`, `5-debug`, `5.3-debug`, `5.3.5-debug`
- `5.3.4`, `5.3.4-debug`
- `5.3.3`, `5.3.3-debug`
- `5.2`, `5.2.2`, `5.2-debug`, `5.2.2-debug`
- `5.1`, `5.1.2`, `5.1-debug`, `5.1.2-debug`
- `4`, `4.1`, `4.1.5`, `4-debug`, `4.1-debug`, `4.1.5-debug`

## Security notice

Security scans are performed via [trivy](https://github.com/aquasecurity/trivy) and reported in [github](./security). Scans are only performed to the `latest` tag, which should include all libs vulnerabilities from all possible tags.

## Contributing

We'd love to have you contribute! Please refer to our [contribution guidelines](CONTRIBUTING.md) for details.

**By making a contribution to this project, you agree to and comply with the [Developer's Certificate of Origin](./DCO).**

## License

[Apache 2.0 License](./LICENSE).
