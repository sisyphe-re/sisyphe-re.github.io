---
layout: default
---

# Presentation

The main goal of *sisyphe* is to provide a way to generate artifacts in an autonomous, repeatable and reproducible manner[^1]. To achieve this goal, *sisyphe* relies on multiple techniques or design principles which are presented in the companion paper of this project.

Long story short, *sisyphe* relies on reproducible package management through the use of  [Nix](https://nixos.org/), compartmentalisation with the help of virtual machines, and testbeds such as [FIT IoT-Lab](https://www.iot-lab.info/) to generate binaries (e.g firmwares), datasets, models, graphs, in an automated manner.

[^1]: We adopt the ACM [Artifact Review and Badging Version 1.1](https://www.acm.org/publications/policies/artifact-review-and-badging-current) terminology for the terms *repeatability*, *reproducibility* and *replicability*.


{:toc}

# FAQ

## Where is the source code for Sisyphe ?

The source code of the platform for Sisyphe is hosted under the [sisyphe github organization namespace](https://github.com/sisyphe-re). This source code is also backed-up by the [Software Heritage](https://www.softwareheritage.org/) project.

## What are the pre-requisites to use Sisyphe ?

The project makes good use of the [Nix package manager and NixOS distribution](https://nixos.org/). Therefore, to design experiments, fetch build artifacts or reproduce the results locally, you should have a working copy of the Nix package manager.

## How to download experiment artifacts from Sisyphe ?

Experiment artifacts are available directly on the [web interface of Sisyphe](https://sisyphe-api.grunblatt.org/), and you can download them using a browser or [curl](https://curl.se/).

## How to download build artifacts from Sisyphe ?

Build artifacts are made available for each run on specific subdomains of the form `https://<RUN_UUID>.cache.grunblatt.org/`, for example e.g. at [https://9c7341f9-95c5-48ea-ad95-670b0aff9698.cache.grunblatt.org/](https://9c7341f9-95c5-48ea-ad95-670b0aff9698.cache.grunblatt.org/) for the run `9c7341f9-95c5-48ea-ad95-670b0aff9698`.

You can browse and download the [NAR archives](https://nixos.org/guides/nix-pills/automatic-runtime-dependencies.html#idm140737320210464) manually, or you can use the run `store` as a binary cache, e.g:

    nix-store --realise /nix/store/qv1i4k82wjslgq1pbxaphh420ca2pxlp-gnrc_networking \
              --option extra-substituters https://9c7341f9-95c5-48ea-ad95-670b0aff9698.cache.grunblatt.org/ \
              --option require-sigs false

<!-- --option trusted-public-keys bincache.grunblatt.org:ktUnzmIdQUSVIyu3XcgdKP6LtocaDGbWrOpVBJ62T4A= -->

If the binary was available in the binary cache, it should now be present in the `/nix/store` hierarchy: 

        $ ls -alh /nix/store/qv1i4k82wjslgq1pbxaphh420ca2pxlp-gnrc_networking/
        total 11M
        dr-xr-xr-x    2 root root   4,0K  1 janv.  1970 .
        drwxrwxr-t 6975 root nixbld 7,5M  6 juil. 09:56 ..
        -r-xr-xr-x    1 root root   2,9M  1 janv.  1970 gnrc_networking.elf

<!-- The key signing those packages is either the cache.nixos.org key or the bincache.grunblatt.org key, whose public keys are:

- `cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=`
- `bincache.grunblatt.org:ktUnzmIdQUSVIyu3XcgdKP6LtocaDGbWrOpVBJ62T4A=` -->

## Can I propose some experiment to run on Sisyphe ?

Yes ! We plan to open the platform for any one in the coming weeks, but right now you can contact [Rémy](mailto:remy@grunblatt.org) for any specific information on how to do so.

## How to download the companion paper data ?

Due to its size, the experiment artifacts for the companion paper is hosted in a specific manner (torrent files). The torrent files are available here:
- [Emergency Response Scenario](static/emergency_response_262939.db3.zst.torrent)
- [HVAC Scenario](static/hvac_263685.db3.zst.torrent)
- [Ligthing Scenario](static/ligthing_263684.db3.zst.torrent)
- [Surveillance Scenario](static/surveillance_263711.db3.zst.torrent)
- [VoIP Scenario](static/VoIP_263714.db3.zst.torrent)
