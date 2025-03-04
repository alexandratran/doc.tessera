# Bootstrap node configuration file

To start Tessera as a bootstrap node:

- Set [`bootstrapNode`](SampleConfiguration.md#bootstrapnode) to `true`.
- Use the `CUSTOM` [encryptor type](SampleConfiguration.md#encryptor) to integrate a third party encryptor implementation.

!!! info

    Tessera bootstrap nodes function the same way [bootnodes](https://besu.hyperledger.org/en/stable/HowTo/Find-and-Connect/Bootnodes/)
    do for Hyperledger Besu.

## Example configuration file

```json
{
  "useWhiteList": "boolean",
  "bootstrapNode": "boolean",
  "jdbc": {
    "url": "String",
    "username": "String",
    "password": "String"
  },
  "serverConfigs": [
    {
      "app": "ENCLAVE",
      // Defines us using a remote enclave, leave out if using built-in enclave
      "serverAddress": "http://localhost:9081",
      //Where to find the remote enclave
      "communicationType": "REST"
    },
    {
      "app": "ThirdParty",
      "serverAddress": "http://localhost:9081",
      "bindingAddress": "String - url with port e.g. http://127.0.0.1:9081",
      "communicationType": "REST"
    },
    {
      "app": "Q2T",
      "serverAddress": "unix:/tmp/tm.ipc",
      "communicationType": "REST"
    },
    {
      "app": "P2P",
      "serverAddress": "http://localhost:9001",
      "bindingAddress": "String - url with port e.g. http://127.0.0.1:9001",
      "sslConfig": {
        "tls": "enum STRICT,OFF",
        "generateKeyStoreIfNotExisted": "boolean",
        "serverKeyStore": "Path",
        "serverTlsKeyPath": "Path",
        "serverTlsCertificatePath": "Path",
        "serverKeyStorePassword": "String",
        "serverTrustStore": "Path",
        "serverTrustCertificates": [
          "Path..."
        ],
        "serverTrustStorePassword": "String",
        "serverTrustMode": "Enumeration: CA, TOFU, WHITELIST, CA_OR_TOFU, NONE",
        "clientKeyStore": "Path",
        "clientTlsKeyPath": "Path",
        "clientTlsCertificatePath": "Path",
        "clientKeyStorePassword": "String",
        "clientTrustStore": "Path",
        "clientTrustCertificates": [
          "Path..."
        ],
        "clientTrustStorePassword": "String",
        "clientTrustMode": "Enumeration: CA, TOFU, WHITELIST, CA_OR_TOFU, NONE",
        "knownClientsFile": "Path",
        "knownServersFile": "Path"
      },
      "communicationType": "REST"
    }
  ],
  "peer": [
    {
      "url": "url e.g. http://127.0.0.1:9000/"
    }
  ],
  "keys": {
    "passwordFile": "Path",
    "keyVaultConfigs": [
      {
        "keyVaultType": "Enumeration: AZURE, HASHICORP, AWS",
        "properties": "Map[string]string"
      }
    ],
    "keyData": [
      {
        "config": {
          "data": {
            "aopts": {
              "variant": "Enum : id,d or i",
              "memory": "int",
              "iterations": "int",
              "parallelism": "int"
            },
            "bytes": "String",
            "snonce": "String",
            "asalt": "String",
            "sbox": "String",
            "password": "String"
          },
          "type": "Enum: argon2sbox or unlocked. If unlocked is defined then config data is required. "
        },
        "privateKey": "String",
        "privateKeyPath": "Path",
        "azureVaultPrivateKeyId": "String",
        "azureVaultPrivateKeyVersion": "String",
        "publicKey": "String",
        "publicKeyPath": "Path",
        "azureVaultPublicKeyId": "String",
        "azureVaultPublicKeyVersion": "String",
        "hashicorpVaultSecretEngineName": "String",
        "hashicorpVaultSecretName": "String",
        "hashicorpVaultSecretVersion": "Integer (defaults to 0 (latest) if not set)",
        "hashicorpVaultPrivateKeyId": "String",
        "hashicorpVaultPublicKeyId": "String"
      }
    ]
  },
  "alwaysSendTo": [
    "String..."
  ],
  "unixSocketFile": "Path",
  "features": {
    "enableRemoteKeyValidation": false
  },
  "encryptor": {
    "type": "Enumeration: NACL, EC, CUSTOM",
    "properties":{
      "symmetricCipher":"String (defaults to AES/GCM/NoPadding if type = EC)",
      "ellipticCurve": "String (defaults to secp256r1 if type = EC)",
      "nonceLength": "String (defaults to 24 if type = EC)",
      "sharedKeyLength": "String (defaults to 32 if type = EC)"
    }
  }
}
```
