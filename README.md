# zfs2gcp
`zfs2gcp` is a shell script that takes ZFS snapshots and sends them to Google Cloud Storage.

## Usage
### Prerequisite
Set the `$ZFS2GCP_BUCKET` environment variable to the name of the bucket that will be used for backups.
### Taking Snapshots and Sending Them
`# zfs2gcp backup zroot/dataset/to/backup`
This will create a snapshot and send the `zfs send` stream to the specified bucket.
### Listing Snapshots
`# zfs2gcp list`
This will list all snapshots stream files in the specified bucket. To show snapshots for a specific dataset
`# zfs2gcp list name/of/dataset`
The output will be in the format of `zroot/dataset/to/backup@zfs2gcp_1480840292`, where the number after `zfs2gcp_` is the time of snapshot creation in UNIX time.
### Restoring From Snapshots
`# zfs2gcp restore zroot/dataset/to/backup@zfs2gcp_<timestamp> dataset/to/write/to`
Replace `<timestamp>` with a valid timestamp.

## Current Problems
* Snapshot stream filenames will potentially clash if the same dataset name is used on different hosts, and backup is ran at the same time. 
* Currently exists no way of sending pre-existing snapshots.
