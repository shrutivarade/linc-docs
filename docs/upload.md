# Uploading data to lincbrain.org
**Note:** The steps below require access to https://lincbrain.org, which is a private repository for LINC project investigators.

## Create a new dataset or contribute to an existing dataset
A dataset refers to a collection of brains that have been processed and imaged in a similar way. It typically contains data from multiple brains or samples, possibly imaged with multiple modalities.

1. Create a new dataset
    1. Log into the [LINC Data Platform](https://lincbrain.org).
    1. Click on the `NEW DATASET` button at the top right of the page.
    1. Fill out the title, description, and license. (The license option exists only because lincbrain.org is a clone of DANDI. It has no effect here, as lincbrain.org is a private repository.)
    1. Click on the `REGISTER DATASET` button to create the new dataset.
1. Contribute to an existing dataset
    1. Log into the [LINC Data Platform](lincbrain.org).
    1. Browse the existing datasets under the [SHARED DATASETS](https://lincbrain.org/dandiset) tab.
    1. Contact the `Owner` by email requesting that they add you as an `Owner` of the dataset.

## Install the lincbrain command-line interface (CLI)
On your local machine, install the [lincbrain CLI package](https://pypi.org/project/lincbrain-cli/) in a python environment:

`pip install lincbrain-cli`

## Copy your lincbrain API key
Log into lincbrain.org and click on the button with your initials at the top right of the page. Copy your API key and enter it in the following environment variable on your local machine:

`export LINCBRAIN_API_KEY=<EnterYourKeyHere>`

## Download your new (empty) dataset locally
You can find the command that you need to run to download a specific dataset by navigating to the dataset landing page on lincbrain.org, clicking on the `DOWNLOAD` drop-down menu that you'll see at the top right corner of that page, and copying the `lincbrain download ...` command that you see when you click on that menu. 

On your local machine, create a directory that you will use as a staging area for uploading data. Then cd into this directory, and run the download command that you copied above. For example:
```
cd /path/to/my/staging/area
lincbrain download https://lincbrain.org/dandiset/101010/draft
```

The above example will create a directory called `/path/to/my/staging/area/101010` with a file called `dandiset.yaml` in it. Any data files that you want to upload to your new lincbrain.org dataset have to first be saved here, and organized according to the [Brain Imaging Data Structure (BIDS)](https://bids-specification.readthedocs.io/).

## Organize your data
An example of how to organize a dataset that includes dMRI and histology data from two brains is shown below:

```
101010/
  dataset_description.json
  participants.tsv
  rawdata/
    sub-Ken1/
      dwi/
        sub-Ken1_acq-DSI_dwi.bval
        sub-Ken1_acq-DSI_dwi.bvec
        sub-Ken1_acq-DSI_dwi.json
        sub-Ken1_acq-DSI_dwi.nii.gz
      micr/
        samples.tsv
        sub-Ken1_sample-slice0001_photo.json
        sub-Ken1_sample-slice0001_photo.tif
        sub-Ken1_sample-slice0001_stain-Nissl_BF.json
        sub-Ken1_sample-slice0001_stain-Nissl_BF.tif
        sub-Ken1_sample-slice0002_photo.json
        sub-Ken1_sample-slice0002_photo.tif
        sub-Ken1_sample-slice0002_stain-LY_DF.json
        sub-Ken1_sample-slice0002_stain-LY_DF.tif
        sub-Ken1_sample-slice0009_photo.json
        sub-Ken1_sample-slice0009_photo.tif
        sub-Ken1_sample-slice0009_stain-Nissl_BF.json
        sub-Ken1_sample-slice0009_stain-Nissl_BF.tif
        sub-Ken1_sample-slice0010_photo.json
        sub-Ken1_sample-slice0010_photo.tif
        sub-Ken1_sample-slice0010_stain-LY_DF.json
        sub-Ken1_sample-slice0010_stain-LY_DF.tif
    sub-Ken2/  
      dwi/
        sub-Ken2_acq-DSI_dwi.bval
        sub-Ken2_acq-DSI_dwi.bvec
        sub-Ken2_acq-DSI_dwi.json
        sub-Ken2_acq-DSI_dwi.nii.gz
        sub-Ken2_acq-MulShellMulTE_dwi.bval
        sub-Ken2_acq-MulShellMulTE_dwi.bvec
        sub-Ken2_acq-MulShellMulTE_dwi.json
        sub-Ken2_acq-MulShellMulTE_dwi.nii.gz
      micr/
        samples.tsv
        sub-Ken2_sample-slice0001_photo.json
        sub-Ken2_sample-slice0001_photo.tif
        sub-Ken2_sample-slice0001_stain-Nissl_BF.json
        sub-Ken2_sample-slice0001_stain-Nissl_BF.tif
        sub-Ken2_sample-slice0002_photo.json
        sub-Ken2_sample-slice0002_photo.tif
        sub-Ken2_sample-slice0002_stain-LY_DF.json
        sub-Ken2_sample-slice0002_stain-LY_DF.tif
        sub-Ken2_sample-slice0003_photo.json
        sub-Ken2_sample-slice0003_photo.tif
        sub-Ken2_sample-slice0003_stain-FR_DF.json
        sub-Ken2_sample-slice0003_stain-FR_DF.tif
        sub-Ken2_sample-slice0009_photo.json
        sub-Ken2_sample-slice0009_photo.tif
        sub-Ken2_sample-slice0009_stain-Nissl_BF.json
        sub-Ken2_sample-slice0009_stain-Nissl_BF.tif
        sub-Ken2_sample-slice0010_photo.json
        sub-Ken2_sample-slice0010_photo.tif
        sub-Ken2_sample-slice0010_stain-LY_DF.json
        sub-Ken2_sample-slice0010_stain-LY_DF.tif
        sub-Ken2_sample-slice0011_photo.json
        sub-Ken2_sample-slice0011_photo.tif
        sub-Ken2_sample-slice0011_stain-FR_DF.json
        sub-Ken2_sample-slice0011_stain-FR_DF.tif
```

The files and subdirectories in this example dataset are described in detail below.

### dataset_description.json
This text file is [described in detail in the BIDS specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files.html#dataset_descriptionjson). A minimal `dataset_description.json` would look like this:

```
{
	"Name": "Seminal post mortem dMRI and histology dataset from the laboratory of Dr. Barbara Millicent Roberts",
	"BIDSVersion": "1.9.0"
}
```

### participants.tsv
This text file is [described in detail in the BIDS specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files.html#participants-file). For this dataset, the `participants.tsv` might look like this:

```
participant_id age sex diagnosis
sub-Ken1 43 M healthy
sub-Ken2 61 M hypertension
```

### rawdata
This directory contains one subdirectory for each brain, which contain one subdirectory for each modality, which in turn contain raw image data files named according to the BIDS specification.

### dwi
This directory contains dMRI data files [as described in detail in the BIDS specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetic-resonance-imaging-data.html#diffusion-imaging-data). 

In this example the data include images (`.nii.gz`), b-value tables (`.bval`), gradient tables (`.bvec`), and metadata (`.json`). Data from Ken1 were acquired with a DSI scheme, whereas data from Ken2 were acquired both with a DSI scheme and with a multi-shell, multi-echo scheme.

### micr
This directory contains microscopy data files [as described in detail in the BIDS specification](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html).

In this example the data include images (`.tif`) and metadata (`.json`) from multiple brain sections. For each section there is a blockface photo (`_photo`) and a histological stain (`_stain`). Sections from Ken1 and Ken2 were either processed with a Nissl stain and imaged under brightfield microscopy (`_BF`), or processed for the fluorescent tracer Lucifer Yellow (`LY`) and imaged under darkfield microscopy (`_DF`). Additional sections from Ken2 were processed for the fluorescent tracer Fluoro-Ruby (`FR`) and imaged under darkfield microscopy (`_DF`).

### samples.tsv
This text file is [described in detail in the BIDS specification](https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files.html#samples-file). For Ken1, the `samples.tsv` would look like this:

```
participant_id sample_id sample_type
sub-Ken1 sample-slice0001 tissue
sub-Ken1 sample-slice0002 tissue
sub-Ken1 sample-slice0009 tissue
sub-Ken1 sample-slice0010 tissue
```

## Upload your data
Upload the data from your local machine to lincbrain.org:

```
cd /path/to/my/staging/area/101010
lincbrain upload
```

Check the output in your terminal for validation errors. If there were no errors, your data files should now appear on lincbrain.org.

## Delete data files or directories
Individual data files can be deleted on lincbrain.org by clicking on the trashcan icon next to each file. Alternatively, directories or files can be deleted from the command line.

This example deletes a directory named "horses" both on the local machine and on lincbrain.org:
```
lincbrain delete /path/to/my/staging/area/101010/rawdata/Ken2/horses
```

This example deletes a directory named "horses" on lincbrain.org:
```
lincbrain delete https://lincbrain.org/dandiset/101010/draft/files?location=rawdata%2Fsub-Ken2%2Fhorses
```
