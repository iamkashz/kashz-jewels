# awscli

## Install

```bash
sudo apt install awscli

# configure creds in ~/.aws/
aws configure
```

## help

```bash
aws [COMMAND] [SUB-COMMAND] help
```

## s3

```bash
aws s3 --endpoint-url DOMAIN COMMAND [PARAMS]

# upload file to s3
aws s3 --endpoint-url DOMAIN cp FILE s3://PATH/
```

## dynamoDb

```bash
aws dynamodb --endpoint-url DOMAIN COMMAND [PARAMS]

# COMMANDS:
list-tables
scan --table-name TABLE
create-table
```

### create-table

```json
{
    "TableName": "kashz",
    "KeySchema": [
      { "AttributeName": "title", "KeyType": "HASH" },
      { "AttributeName": "data", "KeyType": "RANGE" }
    ],
    "AttributeDefinitions": [
      { "AttributeName": "title", "AttributeType": "S" },
      { "AttributeName": "data", "AttributeType": "S" }
    ],
    "ProvisionedThroughput": {
      "ReadCapacityUnits": 10,
      "WriteCapacityUnits": 5
    }
}
# aws dynamodb --endpoint-url DOMAIN create-table --cli-input-json file://create-table.json
```

```bash
var params = {
    "TableName": "kashz",
    "KeySchema": [
      { "AttributeName": "ATTRIBUTE1", "KeyType": "HASH" },
      { "AttributeName": "ATTRIBUTE2", "KeyType": "RANGE" }
    ],
    "AttributeDefinitions": [
      { "AttributeName": "ATTRIBUTE1", "AttributeType": "S" },
      { "AttributeName": "ATTRIBUTE2", "AttributeType": "S" }
    ],
    "ProvisionedThroughput": {
      "ReadCapacityUnits": 10,
      "WriteCapacityUnits": 5
    }
};
dynamodb.createTable(params, function(err, data) {
    if (err) ppJson(err); // an error occurred
    else ppJson(data); // successful response
});
```

### put-item

```bash
aws dynamodb --endpoint-url DOMAIN put-item --table-name TABLE --item '{"ATTRIBUTE1":{"S":"STRING_DATA"},"ATTRIBUTE2":{"S":"STRING_DATA"}}'
```

```bash
var params = {
    TableName: 'kashz',
    Item: {
        "title": "ransomware",
        "data": "/root/root.txt",
    },
};
docClient.put(params, function(err, data) {
    if (err) ppJson(err); // an error occurred
    else ppJson(data); // successful response
});
```