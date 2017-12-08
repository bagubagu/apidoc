# Chynge API

Chynge public API is at [http://chynge-api-doc-js.s3-website-ap-southeast-1.amazonaws.com](http://chynge-api-doc-js.s3-website-ap-southeast-1.amazonaws.com/)

When you use the interactive API documentation, most of the endpoints will
give 'not authorized' message unless you are authorized.

To become authorized, copy `access_token` as the api_key input in the 'Authorize'
before you do the 'try it out'. See how to get `access_token` by reading the 
[authentication chapter](authentication.md).

## Developer's API key and secret

Chynge sends out API key (`client_id`) and Secret key (`client_secret`) to
developers manually. Please send email to info@chynge.com to request access.

The initial API key is to be used with a sandbox. The sandbox comes with a 
preloaded sample database.

When developer is ready to deploy to production, please send email
to info@chynge.com and we will give you a production API and Secret key.
