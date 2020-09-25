# Ansible Role: verify_artifact

An Ansible Role that helps to verify an artifact.

There are four methods:
    - by retrieving the checksum file
    - by retrieving the signature of the artifact
    - by retrieving the checksum file with the signature
    - by retrieving the checksum file and the signature of the checksum file

[![Actions Status](https://github.com/tristan-weil/ansible-role-verify_artifact/workflows/molecule/badge.svg?branch=master)](https://github.com/tristan-weil/ansible-role-verify_artifact/actions)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| verify_artifact_tmpdir   | the working directory |
| verify_artifact_pgp_key | the PGP key |
| verify_artifact_download_url | the url of the artifact |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| verify_artifact_download_timeout | 10 | the download timeout |
| verify_artifact_artifact_name |    | override the name of the artifact as some urls completely obfuscate the real name |
| verify_artifact_signature_url | | the url of the file containing the signature of the arifact or the url of the file containing the signature of the sum file
| verify_artifact_sum_url | | the url of the file containing the sum of the file
| verify_artifact_sum_and_sig_url | | the url of the file containing the sum and signature of the file
| verify_artifact_cksum_algo | sha26 | the checksum algo

## Example Playbook

    - hosts: 'webservers'
      tasks:
        - import_role: 
            name: 'ansible-role-verify_artifact'
          vars:
            verify_artifact_sum_url: 'https://releases.hashicorp.com/consul/1.7.2/consul_1.7.2_SHA256SUMS'
            verify_artifact_signature_url: 'https://releases.hashicorp.com/consul/1.7.2/consul_1.7.2_SHA256SUMS.sig'
            verify_artifact_download_url: 'https://releases.hashicorp.com/consul/1.7.2/consul_1.7.2_linux_amd64.zip'
            verify_artifact_cksum_algo: 'sha256'
            verify_artifact_tmpdir: '/tmp/consul'
            verify_artifact_pgp_key: |
              -----BEGIN PGP PUBLIC KEY BLOCK-----
              Version: GnuPG v1
              xxx
              -----END PGP PUBLIC KEY BLOCK-----

## Todo

None.

## Dependencies

None.

## Supported platforms

See [meta/main.yml](https://github.com/tristan-weil/ansible-role-verify_artifact/blob/master/meta/main.yml)

## License

See [LICENSE.md](https://github.com/tristan-weil/ansible-role-verify_artifact/blob/master/LICENSE.md)
