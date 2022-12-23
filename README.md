# DSEI Exhibitors Dashboard

This repository is both a notebook for interacting with a list of DSEI exhibitors from CAAT's [arms fair data](https://github.com/caatdata/arms-and-security-fair-exhibitors), and a playground for [Meltano](https://meltano.com/)/[DVC](https://dvc.org/)/[Dagshub](https://dagshub.com/)

## Usage

1. `git clone https://dagshub.com/wheresalice/dsei-exhibitors.git` to get the code
2. `python3 -m venv venv && source venv/bin/activate` to setup a virtual environment (optional)
3. `pip3 install -r requirements.txt` to install dependencies
4. `dvc pull -r origin` to pull the data

You should now be able to work with the [notebook](notebook/exhibitors.ipynb) locally

## Adding a new year

1. Update meltano.yml to add the new stream to tap-rest-api-msdk
2. `meltano elt tap-rest-api-msdk target-parquet` to generate the data
3. `dvc add parquet && dvc push -r origin` to push the data to dvc

## Related Projects

* https://github.com/andrewcstewart/ds4fnp - This repository was the primary starting point for this project. It uses Postgresql in docker though, which makes it hard to share the data
* https://github.com/Resistance-Lab/resistancelab_data - This was an older project that @wheresalice worked on, storing the data locally within GitHub. The data is small enough that this works.  The ingest and processing of the data is Python scripts controlled by Makefiles, this is awkward to work with and involves a lot of code but given the nature of the data sources it's hard to do anything else
* https://github.com/caatdata/arms-and-security-fair-exhibitors - The source data for this repository. The code to generate this data is not available. The source data is provided in JSON format, with tools to convert to other formats including CSV.
