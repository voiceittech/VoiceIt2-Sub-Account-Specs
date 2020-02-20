# Sub-Accounts HTTP Specification

Sub accounts are fully independent developer accounts which have access to all of the same API calls as the master accounts that create them.
The difference is that the funds used are subtracted from the master account. They are created and deleted via API calls to API 2.
Since they are full accounts, they can log into all VoiceIt related websites like [voiceit.io](voiceit.io) and [dashboard.voiceit.io](dashboard.voiceit.io).

---

## Create Sub-Account

HTTP POST to `https://api.voiceit.io/subaccount/managed`

### Optional Parameters

| Parameter | Explanation |
| -- | -- |
| firstName | Will be cryptographically generated if none is supplied |
| lastName | Will be cryptographically generated if none is supplied |
| email | Will be cryptographically generated if none is supplied |
| password | Will be cryptographically generated if none is supplied |
| contentLanguage | Will inherit from the master account's default content language if none is supplied |

### `curl`

```
curl -u "[MASTER API KEY]:[MASTER API TOKEN]" -F "firstName=John" -F "lastName=Doe" -F "email=someemail@domain.com" -F "password=thisisapassword" -F "contentLanguage=en-US" -X POST https://api.voiceit.io/subaccount/managed
```

### Example JSON response
```json
{
	"timeTaken": "0.082s",
	"password": "thisisapassword",
	"apiToken": "tok_7ea49bdea43f45a4a58d9109fbdbd471",
	"apiKey": "key_bd3ed09bbcca462b8bd89bd127efd632",
	"contentLanguage": "en-US",
	"message": "Created new managed sub-account with apiKey : key_bd3ed09bbcca462b8bd89bd127efd632",
	"email": "someemail@domain.com",
	"responseCode": "SUCC",
	"status": 201
}
```

### Cost
$0

---

## Usage

### Create User (`curl`)

```
curl -u "[SUB ACCOUNT API KEY]:[SUB ACCOUNT API TOKEN]" -X POST "https://api.voiceit.io/users"
```

### Cost
same as normal calls done under the master account but charged to the master account (see [our pricing page](https://voiceit.io/pricing))

---

## Regenerate Sub-Account API Token

### `curl`

```
curl -u "[MASTER API KEY]:[MASTER API TOKEN]" -X POST https://api.voiceit.io/subaccount/managed/key_bd3ed09bbcca462b8bd89bd127efd632
```

### Example JSON response

```json
{
	"timeTaken": "0.091s",
	"apiToken": "tok_c7ca6c5cb951414db0291d4c8965cc95",
	"message": "Regenerated apiToken : tok_c7ca6c5cb951414db0291d4c8965cc95 for sub-account with apiKey : key_bd3ed09bbcca462b8bd89bd127efd632",
	"responseCode": "SUCC",
	"status": 200
}
```

### Cost
Same as Other call type (see [our pricing page](https://voiceit.io/pricing))

---

## Delete Sub-Account

### `curl`

```
curl -u "[MASTER API KEY]:[MASTER API TOKEN]" -X DELETE https://api.voiceit.io/subaccount/managed/key_bd3ed09bbcca462b8bd89bd127efd632
```

### Example JSON response
```json
{
	"timeTaken": "0.315s",
	"message": "Deleted managed sub-account with apiKey : key_bd3ed09bbcca462b8bd89bd127efd632",
	"responseCode": "SUCC",
	"status": 200
}
```

### Cost
Same as Other call type (see [our pricing page](https://voiceit.io/pricing))
