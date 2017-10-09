### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>gateway de rede local toomodify Olá 'gatewayIpAddress'

Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram. endereço IP do gateway Olá pode ser alterado sem remover uma conexão de gateway VPN existente (se houver). endereço de IP do gateway de saudação toomodify, substituir valores de saudação 'Site2' e 'TestRG1' com seu próprio usando Olá [atualização de gateway local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Verifique se o endereço IP de saudação está correto na saída de hello:

```
"gatewayIpAddress": "23.99.222.170",
```