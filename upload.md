# Uploading data on lincbrain.org
**Note:** The steps below require access to lincbrain.org, which is a private repository for LINC project investigators.

## Create a new dataset
A dataset refers to a collection of brains that have been processed and imaged in a similar way. It typically contains data from multiple brains or samples, possibly imaged with multiple modalities. Log into lincbrain.org and click on the `NEW DATASET` button at the top right of the page. Fill out the title, description, and license. (The license option exists only because lincbrain.org is a clone of DANDI. It has no effect here, as lincbrain.org is a private repository.) Click on the `REGISTER DATASET` button to create the new dataset.

## Install the lincbrain command-line interface (CLI)
On your local machine, install the [lincbrain CLI package](https://pypi.org/project/lincbrain-cli/) in a python environment:

`pip install lincbrain-cli`

## Copy your lincbrain API key
Log into lincbrain.org and click on the button with your initials at the top right of the page. Copy your API key and enter it in the following environment variable on your local machine:

`export LINCBRAIN_API_KEY=<CopyYourKeyHere>`

## Download your new (empty) dataset locally
Create a directory that you will use as a staging area for uploading data. Then download the dataset that you just created from lincbrain.org into this local directory:

```
cd /path/to/my/staging/area
lincbrain download https://lincbrain.org/dandiset/000003/draft
```

where the URL above should be replaced with the one of the dataset that you just created. The above example will create a directory called `/path/to/my/staging/area/000003` with a file called `dandiset.yaml` in it. Any data files that you want to upload to your new lincbrain.org dataset have to first be saved here, and organized according to the [Brain Imaging Data Structure (BIDS)](https://bids-specification.readthedocs.io/).

## Organize your data
... *coming soon* ...

## Upload your data
Upload the data from your local machine to lincbrain.org:

```
cd /path/to/my/staging/area/000003
lincbrain upload
```

Check the output in your terminal for validation errors. If there were no errors, your data files should now appear on lincbrain.org.
