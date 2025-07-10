# overleaf-isolation
Concepts of hardening the Overleaf compilation. Since the community edition compiles as the www-data user, anyone could gain access to all files in that instance.

This solution only requires a minor modification to the container, so it should be easy to upgrade by swapping out the latexmk. This should work for all versions of Overleaf. It was tested in ```5.5.2```.

## Overview
- ```overleaf/Dockerfile```: Example Dockerfile to create sharelatex image with apptainer installation. Modify the content as needed.
- ```overleaf/latexmk```: This is a proof-of-concept python file, which you need to replace with the original ```/usr/local/bin/latexmk```
- ```overleaf/config/docker-compose.overrride.yml```: Shows the changes needed to make the Apptainer image work within your image.
- ```apptainer/latexmk-isolated.def```: This file defines how to build an isolated TeX image for Apptainer. Modify the content as needed.

## Status
Work in progress: Basically, it works like this: However, starting Docker in privileged mode opens other doors.

## How to
1. Build apptainer image: ```apptainer build /apptainer/images/latexmk-isolated.sif apptainer/latexmk-isolated.def```.
2. Build modified sharelatex+apptainer image: ```docker build -t sharelatex+apptainer:5.5.2 -f overleaf/Dockerfile .```.
3. Modify your ```overleaf/config/docker-compose.override.yml```.
4. Start overleaf

## See also
- Marcel Wunderlich' <a href="https://github.com/Deaddy/overleaf-hardening">overleaf-hardening</a> provides isolation via sidecar, allowing one to harden latexmk with podman for k8s.
- Oliver Cordes' <a href="https://github.com/ocordes/sharelatex-isolation">sharelatex-isolation</a> provides isolation via LD_PRELOAD, allowing one to harden latexmk without needing to use chroots or containers or different build hosts.

## Acknowledgements
Special thanks go to Marcel Wunderlich from the University of Münster for communicating between different universities and leading the project to harden Overleaf.