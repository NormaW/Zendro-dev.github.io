[ &larr; back](README.md)
<br/>
# Zendro Command Line Interface (CLI)
## Introduction
A CLI for ZendroStarterPack.

## Installation
A quick installation would be this command: `npm install -g Zendro-dev/zendro`.
However, if you would like to customize your Zendro CLI, you can set it up as the following:
```
$ git clone https://github.com/Zendro-dev/zendro.git
$ cd zendro
$ npm install
$ npm link
```
For example, you can customize the version of each repository by editing `zendro_dependencies.json` file in your local Zendro CLI repository.

## Commands
### Start a new zendro application:
```
zendro new <your_application_name>

  Usage: zendro new [options] <your_application_name>

  Options:
    -d, --dockerize: Keep Docker files (default: false).
```
Hints: 
1. If you don't have local database or you want to dockerize Zendro App, you can keep docker files. These are examples for dockerizing a Zendro App.
2. If you want to modify environment variables or database configuration, you can edit the following files:
* without docker setup: ./graphql-server/config/data_models_storage_config.json
* with docker setup: ./config/data_models_storage_config.json
* ./graphql-server/.env
* SPA in development mode: ./single-page-app/.env.development
* SPA in production mode: ./single-page-app/.env.production
* GraphiQL in development mode: ./graphql-server/.env.development 
* GraphiQL in production mode: ./graphql-server/.env.production

### Generate code for graphql-server:
```
zendro generate

  Usage: zendro generate [options]

  Options:
    -f, --data_model_definitions: Input directory or a JSON file (default: current directory path + "/data_model_definitions").
    -o, --output_dir: Output directory (default: current directory path + "/graphql_server").
    -m, --migrations: Generate migrations (default: false).
```

### Dockerize Zendro App with example docker files:
```
zendro dockerize

  Usage: zendro dockerize [options]

  Options:
    -u, --up: Start docker service (default: false).
    -d, --down: Stop docker service (default: false).
    -p, --production: start or stop GQS and SPA with production mode (default: false).
    -v, --volume: remove volumes (default: false).
```

### Start Zendro service:
```
zendro start [service...]

  Usage: zendro start [options] [service...]

  Options:
    -p, --production: start GQS and SPA with production mode (default: false).
```
Hints:
1. start all service by default
2. start specified service with the following abbreviations:
* gqs: graphql-server
* spa: single-page-app
* giql: graphiql
  
### Stop Zendro service:
```
zendro stop [service…]

  Usage: zendro stop [service…]

  Options:
  -p, --production: stop GQS and SPA with production mode (default: false).
```
Hints:
1. stop all service by default
2. stop specified service

### Generate migration code for graphql-server:
```
zendro migration:generate

  Usage: zendro migration:generate [options]

  Options: 
  -f, --data_model_definitions: Input directory or a JSON file (default: current directory path + "/../data_model_definitions").
  -o, --output_dir: Output directory (default: current directory path + "/migrations").
```
Note: all generated migrations would be stored in a directory called `migrations`.
### Execute migrations
```
zendro migration:up

  Usage: zendro migration:up
```
Note: execute migrations which are generated after the last executed migration. Moreover, the last executed migration is recorded in `zendro_migration_state.json` and the log of migrations is in the file `zendro_migration_log.json`.

### Drop the last executed migration
```
zendro migration:down

  Usage: zendro migration:down
```

### Upload a file
```
zendro bulk-create

  Usage: zendro bulk-create [options]

  Options: 
  -f, --file_path: File path. Supported file format: CSV, XLSX, JSON
  -n, --model_name: Model name.
  -s, --sheet_name: Sheet name for XLSX file. By default process the first sheet.
  -r, --remote_server: Upload to a remote server (default: false).
```
### Set up a quick sandbox
```
zendro set-up

  Usage: zendro set-up [options] <name>

  Options: 
  -d, --dockerize: Keep Docker files (default: false).
```

## A Quick Example for setting up a Zendro Sandbox

Please go to [Quickstart](quickstart.md) guide to set up a Zendro Sandbox. 

## A Detailed Example for setting up a Zendro Instance

Please go to [Getting started](setup_root.md) guide to set up a Zendro Instance. 

## Example for Migrations
If a user has new data model definitions, it is convinient to use Zendro CLI for dealing with migrations. And the following procedure shows how to generate, perform or drop migrations:
1. in `graphql-server` folder, execute `zendro migration:generate -f <data_model_definitions>`. The migrations are automatically generated in the `/graphql-server/migrations` folder. By default, every migration file has two functions, namely `up` and `down`. The `up` function creates a table, the `down` function deletes the existing table. Furthermore it is possible to customize the migration functions.
2. in `graphql-server` folder, it is possible to perform new generated migrations, which are generated after the last executed migration, by executing `zendro migration:up`. After that, the last executed migration and migration log are updated.
3. in `graphql-server` folder, the last executed migration can be dropped by executing `zendro migration:down`. This will update the latest successful migration and add the dropped operation to the migration log. If there are some remaining records and associations in the table, by default an error is thrown. To forcefully drop the table, in spite of remaining records, set the environment variable `DOWN_MIGRATION` to `true` in `/graphql-server/.env` file and re-execute this down-migration.

## Uploading a File
### Data format requirements
Data to populate each model in your schema must be in a separate CSV file, following the format requirements below:
1. Column names in the first row must correspond to model attributes.
2. Empty values should be represented as `"NULL"`.
3. All fields should be quoted by `"`. However, if field delimiter and array delimiter do not occur in fields with String type, namely characters could be split without ambiguity, then no quotes are necessary. For example, if the field delimiter is `,` and one String field is like `Zendro, excellent!`, then without the quotation mark, this field will be split as two fields. So in such case these String fields must be quoted.
4. Default configuration: BATCH_SIZE=20, RECORD_DELIMITER="\n", FIELD_DELIMITER=",", ARRAY_DELIMITER=";". They can be changed in the config file for environment variables.
5. Date and time formats must follow the [RFC 3339](https://tools.ietf.org/html/rfc3339) standard.

### Examples
There are two ways to upload a file via zendro CLI:
1. If the Zendro instance is on your local machine, you can directly go into the folder `graphql-server` and execute
`zendro bulk-create -f <filename> -n <modelname> -s <sheetname>`, e.g. `zendro bulk-create -f ./country.csv -n country`. Three formats are supported here, namely CSV, XLSX and JSON. And the paramter `sheetname` is only used for XLSX file. If it is empty, by default records in the first sheet would be imported. And the default configuration for delimiters and batch size, you can find them in `graphql-server/.env`.
2. If you want to upload a file to a remote Zendro server, it is also possible via Zendro CLI. All configuration could be modified in the file `zendro/.env.migration`. After the configuration, you can execute `zendro bulk-create -f <filename> -n <modelname> -s <sheetname> -r`, e.g. `zendro bulk-create -f ./country.csv -n country -r`.

## Download Records
In general, it is possible to download all data into CSV format in two ways, either using the Zendro CLI or the Zendro Single Page App. Here every attribute will be quoted to avoid ambiguity and enable seamless integration with the zendro bulk creation functionalities.

1. If the Zendro instance is installed locally, then user can execute the command in the `graphql-server` folder: `zendro bulk-download -f <filename> -n <modelname>`. To configure delimiters (`ARRAY_DELIMITER`, `FIELD_DELIMITER` and `RECORD_DELIMITER`) and record-limit (`LIMIT_RECORDS`), set the according environment variables in  `graphql-server/.env`

2. If the Zendro instance is accessible remotely, modify the `zendro/.env.migration` configuration file to map to the remote Zendro instance. After that, execute `zendro bulk-create -f <filename> -n <modelname> -r` to download the records to CSV.
