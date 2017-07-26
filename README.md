# Serverless S3 Sync [![npm](https://img.shields.io/npm/v/serverless-s3-sync.svg)]()

> A plugin to sync local directories and S3 prefixes for Serverless Framework :zap: .

## Use Case

- Static Website ( `serverless-s3-sync` ) & Contact form backend ( `serverless` ) .
- SPA ( `serverless` ) & assets ( `serverless-s3-sync` ) .

## Install

Run `npm install` in your Serverless project.

```sh
$ npm install --save serverless-s3-sync
```

Add the plugin to your serverless.yml file

```yaml
plugins:
  - serverless-s3-sync
```

## Setup

```yaml
custom:
  s3Sync:
    - bucketName: my-static-site-assets # required
      bucketPrefix: assets/ # optional
      localDir: dist/assets # required
    - bucketName: my-other-site
      localDir: path/to/other-site

resources:
  Resources:
    AssetsBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: my-static-site-assets
    OtherSiteBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: my-other-site
        AccessControl: PublicRead
        WebsiteConfiguration:
          IndexDocument: index.html
          ErrorDocument: error.html
```

## Usage

Run `sls deploy`, local directories and S3 prefixes are synced.

Run `sls remove`, S3 objects in S3 prefixes are removed.