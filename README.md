# Rogierslag.nl

Since my hosting provider does not support an ALIAS DNS record, I use Github pages to catch the root `rogierslag.nl` domain.
This is then redirected to www.rogierslag.nl which is properly handled by Cloudfront.

So all in all, this repo is not that interesting.

## Setup of Rogierslag.nl

1. A Medium user account
1. An AWS account
1. A TransIP account

First we create a completely empty S3 bucket.
Configure this as website hosting, and let it redirect everything to your Medium account.

In AWS, open certificate manager and create a certificate for the wanted domain names (also include the www version!)
After accepting the certificate, open Cloudfront, and create a distribution from the empty redirect bucket.
Change the URL to `<bucketname>.s3-website-eu-west-1.amazonaws.com` (the REST endpoint does not redirect)

Just accept HTTP and HTTPS (a redirect to the other is pointless, Medium will handle it anyhow).
Then set all domains you entered in the certificate step to the CNAME.
Pick your own certificate from the dropdown

Finally at TransIP, change your domain settings.

The `@` A record goes to GH pages with `192.30.252.153` and `192.30.252.154`.
Send the domain records to CNAME and pick the Cloudfront distribution name (ends with `cloudfront.net`).

