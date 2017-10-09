Você pode verificar se a conexão foi bem-sucedida usando Olá [Mostrar de conexão vpn de rede az](/cli/azure/network/vpn-connection#show) comando. No exemplo hello, '-nome ' refere-se o nome de toohello de conexão de saudação que você deseja tootest. Quando a conexão hello está no processo de saudação do que está sendo estabelecida, seu status de conexão mostra 'Conexão'. Após o estabelecimento de conexão Olá Olá status é alterado too'Connected'.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

