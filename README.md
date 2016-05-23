# Systemapic API scripts
_Scripts in Bash and NodeJS for interacting with the Systemapic API_

### Install
1. Clone this repository to your localhost: `git clone https://github.com/systemapic/api-scripts.git`
2. Enter folder: `cd api-scripts`
3. Run `./install.sh` script. This will install dependencies and copy the [config template](https://github.com/systemapic/api-scripts/blob/master/config.json.template). You'll also be prompted to add your credentials to the config. The config should end with the message: `You're now ready to use the Systemapic API!`

----

### Upload datasets

Create your own `datacube.json` file from [`datacube.json.template`](https://github.com/systemapic/api-scripts/blob/master/datacube.json.template):

```javascript
{
    "folder" : "/home/test-snow/", 	// absolute path of folder containing .tiff's
    "title" : "Snow raster 11" 		// name of cube
}
```

**Then run script:**   
`./upload_datacube.sh datacube.json`.

This will do the following:  
1. Create a cube  
2. Upload all rasters in folder  
3. Add all rasters to cube  
4. Create a project  
5. Add cube layer to project  


### Replace datasets

You can replace datasets in a cube, by using the `./replace_datasets.sh` script with the `replace_datasets.json` configuration:

```json
{
    "folder" : "/home/ftp_globesar/2016_02/",
    "cube_id" : "cube-535a0ec3-8705-4215-8c94-8786b9680598",
    "granularity" : "day"
}
```

Simply add the `cube_id` for the cube which you would like to replace datasets in, and the folder from which to upload data. The `granularity` option is used when comparing dates of datasets (see below for more info on date parsing). `'day'` is appropriate for daily rasters.

To get the `cube_id`:  

### Date parsing
Dates are added to metadata from filename. 

Currently with [these helper functions](https://github.com/systemapic/api-scripts/blob/master/lib/upload_rasters_to_cube.js#L20-L38), where `SCF_MOD_2014_001.tif` is parsed to `Jan 01 2014`.

It's possible to implement your own date parser, and change [this function call](https://github.com/systemapic/api-scripts/blob/master/lib/upload_rasters_to_cube.js#L113).

----

#### Dependencies:
- Git: https://git-scm.com/download/
- NodeJS: https://nodejs.org/en/download/