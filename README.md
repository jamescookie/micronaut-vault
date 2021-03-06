# micronaut-vault

Run vault in docker:

`docker run --cap-add=IPC_LOCK -e 'VAULT_DEV_ROOT_TOKEN_ID=myroot' -p 8200:8200 --name vault vault`

Access it:

`docker exec -it vault sh`

Set up kv secret v1:

```
export VAULT_ADDR='http://0.0.0.0:8200'
export VAULT_TOKEN='myroot'
vault secrets disable secret
vault secrets enable -version=1 -path=secret kv
vault kv put secret/application test=testing
```

Run this application:

`./gradlew run`

Then check the result:

`curl http://localhost:8080/test`

Should produce:

`{"vault-key-test":"testing"}`
