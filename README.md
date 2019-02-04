# Ansible Role: verify_artifact

An Ansible Role that helps to verify an artifact for Debian and OpenBSD.

There are four methods:
    - by retrieving the checksum file
    - by retrieving the signature of the artifact
    - by retrieving the checksum file with the signature
    - by retrieving the checksum file and the signature of the checksum file

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    verify_artifact_tmpdir: [mandatory]             # working directory
    
The working directory, where all files are downloaded first, has to be specified.
    
    verify_artifact_pgp_key: [mandatory]            # the pgp key

The PGP key must be supplied and thus should have been retrieved before executing the role.
    
    verify_artifact_download_url: [mandatory]       # the url of the artifact
    verify_artifact_download_timeout: 10            # the download timeout
    
This variable specifies the url of the artifact and the download timeout.
    
    verify_artifact_artifact_name: ''

This optional variable allows to create a readable path as the destination of the downloaded artifact.
Indeed, some urls completely obfuscate the real name of the artifact.

    verify_artifact_signature_url:                  # the url of the file containing the signature of the arifact
                                                    # or the url of the file containing the signature of the sum file
    verify_artifact_sum_url:                        # the url of the file containing the sum of the file
    verify_artifact_sum_and_sig_url:                # the url of the file containing the sum and signature of the file

According to the chosen method, this variable is url of the sum file or the signature file.
    
    verify_artifact_cksum_algo: sha26

In the case of a checksum file validation, the checksum algo has to be specified.

## Dependencies

None.

## Example Playbook

    - hosts: webservers
      roles:
        - role: t18s.fr_verify_artifact
          verify_artifact_pgp_key: xxxx
          verify_artifact_sum_url: https://yyyy/file_SHA256SUMS
          verify_artifact_signature_url: https://yyyy/file_SHA256SUMS.sig
          verify_artifact_download_url: https://yyyy/file
          verify_artifact_cksum_algo: sha256
          
## Todo

None.

## License

```
Copyright (c) 2018, 2019 Tristan Weil <titou@lab.t18s.fr>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
