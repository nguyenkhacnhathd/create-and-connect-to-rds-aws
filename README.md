**CREATE AND CONNECT TO RDS AWS**

**How to deploy to your server**

*Step 1: Go to bash of stack service and install packages*
```bash
$ docker-compose run --rm stack sh
$ npm install -D
```

*Step 2: Basic Template*
```bash
$ serverless deploy --parameter-overrides EnableSecurityGroup=false --parameter-overrides EnablePostgres=false --parameter-overrides EnableDBReplica=false
```

*Step 3: Enable Security Group*
```bash
$ serverless deploy --parameter-overrides EnableSecurityGroup=true
```

*Step 4: Enable Postgres* (This step takes a lot of time. Please wait until it is complete)
```bash
$ serverless deploy --parameter-overrides EnablePostgres=true
```

*Step 5: Enable Database Replica* (This step takes a lot of time. Please wait until it is complete)
```bash
$ serverless deploy --parameter-overrides EnableDBReplica=true
```

**Get host of database(MasterDBEndpoint, ReplicaDBEndpoint)**
```bash
$ serverless info --verbose
```

**How to connect to RDS Database**
```
$ docker run -v {path/to/file}:/tmp -it postgres bash
$ psql -h {MasterDBEndpoint} -p 5432 -U flowermeister -f {path/to/file} fm
```

- set default_transaction_read_only = Off to can update fm database in IDE when remote to rds aws
```
$ psql -h {MasterDBEndpoint} -p 5432 -U flowermeister fm
$ set default_transaction_read_only = off
```

**How to delete db stack**
```bash
$ serverless remove
```