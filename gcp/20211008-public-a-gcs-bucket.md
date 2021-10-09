---
title: Make a Cloud Storage bucket public
date: 2021-10-08
tags:
- gcs
- CloudStorage
categories:
- Google Cloud Platform
---

We need 3 configurations to make a bucket public to everyone.

## 1. Remove public access prevention

A bucket cannot be accessed by public as the default. So we need to remove public access prevention.

1. Go to the `Bucket details` > `Permissions` tab > `Public access` section
1. Click `Remove public access prevention` and confirm

## 2. Add permission for `allUsers` (e.g. to view objects)

1. Go to the `Bucket details` > `Permissions` tab > `Permissions` section
1. Click `Add` and fill in the following information, then click `Save`
   1. New principals: `allUsers` or `allAuthenticatedUsers`
   1. Select a role: `Storage Object Viewer`

## 3. Change `Access control` to `Fine-grained`

1. Go to the `Bucket details` > `Configuration` tab > `Permissions`
1. Edit `Access control` field to `Fine-grained`

## References

https://cloud.google.com/storage/docs/access-control/making-data-public#buckets