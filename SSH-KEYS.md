Create the key in your pc
```
 ssh-keygen -t rsa
 ```

Now enter the remote server and create that directory
```
mkdir -p ~/.ssh
```

Create the fle with the string from ".pub" created
```
nano ~/.ssh/authorized_keys
```

SET the permissions
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

To open now with your key
```
ssh -i chave usuario@host
```
