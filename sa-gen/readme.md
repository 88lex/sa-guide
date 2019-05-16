# sa-gen

Create up to 100 service accounts for a google project using gcloud SDK

_forked from DashLt at https://gist.github.com/DashLt/4c6ff6e9bde4e9bc4a9ed7066c4efba4_ and

_forked from mc2squared at https://gist.github.com/mc2squared/01c933a8172a26af88285610a0e5af8d_


requires gcloud command line tools; go to https://cloud.google.com/sdk/docs/quickstarts to get them

max 100 service accounts per project

run gcloud init --console-only first and select a project

Create a folder for your keys before running the script

KEYS_DIR=/opt/sa

If you want to create more than 100 jsons then increment COUNT for each batch.
For the first batch COUNT=1. Second batch COUNT=101. Third batch COUNT=201 ...
