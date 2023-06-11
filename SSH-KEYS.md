CRIE A CHAVE
```
 ssh-keygen -t rsa
 ```

ENTRE NO SERVIDOR E CRIE A PASTA
```
mkdir -p ~/.ssh
```

CRIE O ARQUIVO E INCLUA O TEXTO DA CHAVE ".pub"
```
nano ~/.ssh/authorized_keys
```

CONFIGURE AS PERMISSOES
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

AGORA PARA ABRIR SSH COM SUA CHAVE
```
ssh -i chave usuario@host
```
