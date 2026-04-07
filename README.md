# Summary
`bash-backup` is an easy-to-use script for compressing and encrypting an arbitrary number of files and/or directories for efficient replication elsewhere. Optionally, it can automatically connect and copy to an S3 Bucket.

## Dependencies
- `tar`: compression
- `gnupg`: symmetric encryption with `gpg`
- `aws-cli-v2` (optional): required for copying to S3 Buckets

# Usage
To invoke from command line:
```sh
./bash-backup -k path/to/keyfile [-b s3-bucket-name file1] [file2 ... fileN]
```
Encryption is assumed and program will exit without specification of a file for use as a symmetric key.

After compression and encryption, the resulting encrypted archive is written to the working directory.

If `-b` is specified and the aws cli has been locally configured, the encrypted archive is copied to the specified Bucket.

# Security Precautions
Use a cryptographically secure string in the keyfile. To generate a 32-bit keyfile with `openssl`:
```sh
openssl rand -out path/to/output.key 32
```

Jealously guard your keyfile. When invoking `bash-backup` from a script or cronjob, never hardcode the keystring as plaintext.

