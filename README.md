# envy
simple env tool

## Install
```
curl https://raw.githubusercontent.com/LeafChage/envy/main/envy > ./envy
chmod +x ./envy
```

## How to use
```sh
$ envy help

envy utility tool for environment argument

SUBCOMMAND:
  help    show usage
  json    convert to json
    ex) envy json .local.env
  load    load dotenv file
    ex) envy load .local.env sh -c 'echo "$PASSWORD"'

SUBCOMMAND:
  encrypt|enc   encrypt file
  decrypt|dec   decrypt file

  OPTION:
    -i | --input   [InputFile]
    -k             [KeyString]
```

## Example
```sh
$ cat .env
> DATABASE_USER=user
> DATABASE_DRIVER=mysql
> # TEST_PASSWORD=test_password
> #%SECRET
> DATABASE_PASSWORD=password

# Encrypt
$ ./envy enc -i .env -k password
> DATABASE_USER=user
> DATABASE_DRIVER=mysql
> #%SECRET
> DATABASE_PASSWORD=U2FsdGVkX1/gv2lk32CtTcBAPkFDTa3vlSwObNfhAek=

# Decrypt
$ ./envy enc -i .env -k password > .env.enc
$ ./envy dec -i .env.enc -k password
> DATABASE_USER=user
> DATABASE_DRIVER=mysql
> #%SECRET
> DATABASE_PASSWORD=password

# json
$ ./envy json ./.env | jq
> {
>   "DATABASE_USER": "user",
>   "DATABASE_DRIVER": "mysql",
>   "DATABASE_PASSWORD": "password"
> }
```
