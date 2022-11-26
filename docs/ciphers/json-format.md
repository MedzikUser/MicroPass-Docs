# Cipher JSON format

The Cipher is a JSON object that contains the following fields:

## Parameters

- `id` - The unique identifier of the cipher. This is a UUID.
- `favorite` - Whether or not the cipher is a favorite. This is a boolean.
- `dir` - The directory of the cipher. This is a string. It can be null.
- `data` - The data of the cipher. This is a [Cipher Data type](#cipher-data).
- `attachments` - The attachments of the cipher. This is an array of strings (Attachment UUIDs).

### Example Cipher

```json
{
    "id": "aa770bed-e199-41f1-90b1-c4578104e22b",
    "favorite": false,
    "dir": "622e5baf-f4b4-427b-b1dd-d54cded668e3", // maybe null
    "data": {
        "type": 1,
        "name": "Example",
        "favorite": true,
        "fields": {
            "user": {
                "typ": -1, // -1 for default field (built-in email field)
                "val": "medzik@example.com"
            }, // maybe null
            "pass": {
                "typ": -1, // -1 for default field (built-in password field)
                "val": "$ecretP@ssw0rd"
            }, // maybe null
            "totp": {
                "typ": -1, // -1 for default field (built-in OTP field)
                "val": "otpauth://totp/medzik@example.com?secret=JBSWY3DPEHPK3PXP&issuer=example.com"
            }, // maybe null
            "url": {
                "typ": -1, // -1 for default field (built-in URL field)
                "val": "https://example.com"
            }, // maybe null
            "note": {
                "typ": -1, // -1 for default field (built-in note field)
                "val": "my note about this cipher"
            }, // maybe null
            "Custom Field": {
                "typ": 0, // 0 for text field
                "val": "This is a text in your custom field"
            }, // custom field
            "Custom Secret Field": {
                "typ": 1, // 1 for hidden text field
                "val": "This is a secret text in your secret custom field"
            } // custom field
        }
    },
    "attachments": [] // not implemented yet
}
```

## Cipher Data

### Parameters

-  `type` is the type of the cipher. It is an integer. The possible values are:
    -  `1` for login
    -  `2` for secure note (not implemented yet)
    -  `3` for card (not implemented yet)
    -  `4` for identity (not implemented yet)
- `name` is the name of the cipher. It is a string.
- `favorite` is a boolean indicating if the cipher is a favorite.
- `note` is the note of the cipher. It is a string. It can be null.
- `fields` is a list of fields. Each field is an object with the following properties:
    - `val` is the value of the field. It is a string.
    - `typ` is the type of the field. It is an integer. The possible values are:
        - `-1` for default fields
        - `0` for text
        - `1` for hidden

### Fields

#### Example

```json
{
    // ...
    "fields": {
        "field name": { // "field name" is the name of the field
            "typ": 0, // type of the field
            "val": "field value" // value of the field
        }
    },
    // ...
}
```

#### Login Field Type

For login ciphers, the following fields may be used:

- `user` is the username of the cipher. It is a string. It can be null.
- `pass` is the password of the cipher. It is a string. It can be null.
- `totp` is the otpauth of the cipher. It is a string. It can be null.
- `url` is the url of the cipher. It is a string. It can be null.
- and may contain more custom fields

##### Example

```json
{
    // ...
    "fields": {
        "user": {
            "typ": -1,
            "val": "medzik@example.com"
        },
        "pass": {
            "typ": -1,
            "val": "123456"
        },
        "url": {
            "typ": -1,
            "val": "https://example.com"
        }
    },
    // ...
}
```

#### Secure Note Field Type

For secure note ciphers, the following fields may be used:

- `note` is the note of the cipher. It is a string.
- and may contain more custom fields

##### Example

```json
{
    // ...
    "fields": {
        "note": {
            "typ": -1,
            "val": "This is my secure note"
        },
        "Something": {
            "typ": 0,
            "val": "any value"
        }
    },
    // ...
}
```

#### Other types of ciphers are not implemented yet.
