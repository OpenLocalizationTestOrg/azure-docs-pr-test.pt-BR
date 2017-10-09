### <a name="tooview-local-network-gateways"></a>tooview gateways de rede local

tooview uma lista de gateways de rede local hello, use Olá [lista de gateway local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>valores de chave tooverify Olá compartilhado

Verifique se o valor de chave Olá compartilhado é Olá mesmo valor que você usou para a sua configuração de dispositivo VPN. Se não estiver, execute conexão Olá novamente usando o valor de saudação do dispositivo hello ou atualizar dispositivo Olá com valor de saudação do hello retorno. Olá valores devem corresponder. Olá tooview compartilhado chave, use Olá [lista de conexão de vpn de rede az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>gateway VPN tooview Olá endereço IP público

toofind Olá endereço IP público do seu gateway de rede virtual, use Olá [lista de ip público de rede az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando. Para facilitar a leitura, a saída de hello para este exemplo é formatado toodisplay lista de saudação de IPs públicos em formato de tabela.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
