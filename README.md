# guia-gpg

Um guia prático para manusear chaves gpg

## Criação da chave

```
gpg --full-gen-key
-> RSA and RSA (default)
-> What keysize do you want?  2048
-> 0 = key does not expire
-> Real name: (nome completo)
-> Email address: (e-mail)
-> Comment: (opcional)

gpg --gen-key
-> Real name: (nome completo)
-> Email address: (e-mail)
-> Comment: (opcional)
```

### Listar chaves

```
gpg --list-key
gpg --list-secret-keys
```

### Fazer backup

```
gpg -a --export > mypubkeys.asc
gpg -a --export-secret-keys >myprivatekeys.asc
gpg --export-secret-keys --armor email@exemplo.org > nome-privkey.asc #E-mail da chave que deseja realizar backup
gpg --export --armor email@exemplo.org > nome-pubkey.asc
gpg --export-ownertrust > otrust.txt
```

### Remover chaves

```
gpg --delete-keys CHAVE
gpg --delete-secret-keys CHAVE
ou: gpg –delete-secret-and-public-keys  CHAVE
```

### Revogação de chaves

```
gpg --gen-revoke email@exemplo.org   #E-mail da chave que deseja realizar revogação
```

### Enviar no server

```
gpg --send-key CHAVE   #server padrão
gpg --keyserver pgp.mit.edu --send-key CHAVE
gpg --keyserver pgp.key-server.io --send-key CHAVE
gpg --keyserver keyserver.ubuntu.com --send-key CHAVE   #server Ubuntu
```

### Editar chave

```
gpg --edit-key CHAVE
```

### Importar as chaves públicas de outras pessoas

SERVER = qualquer server que esteja a chave (por exemplo os listados acima)
PARÂMETRO_PESQUISA = CHAVE, e-mail, nome, etc
```
local:    gpg --import nome_do_arquivo_chave_pub.asc
server:  gpg --keyserver SERVER --search-keys PARÂMETRO_PESQUISA
```

### Assinando a chave alheia

```
gpg --sign-key email@exemplo.org   # E-mail da pessoa que deseja assinar
```

### Listar assinaturas em chaves

```
gpg --list-sigs
```

### Criptografar arquivos

```
gpg --output arquivo.txt.gpg --encrypt --recipient <email_do_destinatario> arquivo.txt
```

### Descriptografando arquivos

```
gpg -d encrypted.asc
```

### Conceder Permissão

Conceder à pessoa que você assinou a chave as vantagens da vossa relação de confiança enviando à ela a chave assinada

```
gpg --export --armor email@exemplo.org   #E-mail da pessoa que deseja conceder as vantagens
Quando a pessoa receber a chave: gpg --import nome_do_arquivo_chave_pub_atualizado
```

### Atualizar repositório de chaves

```
local: gpg --refresh-keys
server: gpg --keyserver SERVER --refresh-keys
```
