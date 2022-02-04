---
id: vDpJf8h65cx41A07HI2S8
title: Falcano
desc: ''
updated: 1643913976113
created: 1643909288755
---


## Docker Configuration

```
docker pull amazon/dynamodb-local:latest
docker run -p 8000:8000 amazon/dynamodb-local:latest
```

## Example

```python
import os
from falcano.model import Model
from falcano.attributes import UnicodeAttribute, MapAttribute

os.environ['DYNAMODB_TABLE'] = 'cloudops'
os.environ['AWS_DEFAULT_REGION'] = 'us-east-1'
os.environ['AWS_ACCESS_KEY_ID'] = 'my-access-key'
os.environ['AWS_SECRET_ACCESS_KEY'] = 'my-secret-key'
os.environ['AWS_SECURITY_TOKEN'] = 'my-session-token'

class AwsAccount(Model):
    '''
    A DynamoDB User
    '''
    class Meta(Model.Meta):
        table_name = 'cloudops'
        billing_mode = 'PAY_PER_REQUEST'
        host = 'http://localhost:8000'
    email = UnicodeAttribute(null=False)
    PK = UnicodeAttribute(range_key=True)
    SK = UnicodeAttribute(hash_key=True)
    Type = UnicodeAttribute(default='aws_account')
    name = UnicodeAttribute(null=False)
    status = MapAttribute(null=False)
    sso_email = UnicodeAttribute(null=False)
    sso_first_name = UnicodeAttribute(null=False)
    sso_last_name = UnicodeAttribute(null=False)
    ou_path = UnicodeAttribute(null=False)
    provider_boundary = UnicodeAttribute(null=False)
    creation_date = UnicodeAttribute(null=False)
    last_modified_date = UnicodeAttribute(null=False)
    tr_team = UnicodeAttribute(null=False)


AwsAccount.create_table()
account = AwsAccount('aws#12345',"account#details")

account.name = "spscloudopsprod"

account.save()

test = account.get("aws#12345","account#details")

print(test.name)

```
