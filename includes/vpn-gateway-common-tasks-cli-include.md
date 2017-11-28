### <a name="to-view-local-network-gateways"></a><span data-ttu-id="5dbc7-101">Para exibir os gateways de rede local</span><span class="sxs-lookup"><span data-stu-id="5dbc7-101">To view local network gateways</span></span>

<span data-ttu-id="5dbc7-102">Para exibir uma lista de gateways de rede local, use o comando [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list).</span><span class="sxs-lookup"><span data-stu-id="5dbc7-102">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a><span data-ttu-id="5dbc7-103">Para verificar os valores de chave compartilhados</span><span class="sxs-lookup"><span data-stu-id="5dbc7-103">To verify the shared key values</span></span>

<span data-ttu-id="5dbc7-104">Verifique se o valor de chave compartilhado é o mesmo valor usado para a configuração do dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="5dbc7-104">Verify that the shared key value is the same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="5dbc7-105">Caso contrário, execute a conexão novamente usando o valor do dispositivo ou atualize o dispositivo com o valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="5dbc7-105">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span></span> <span data-ttu-id="5dbc7-106">Os valores devem ser correspondentes.</span><span class="sxs-lookup"><span data-stu-id="5dbc7-106">The values must match.</span></span> <span data-ttu-id="5dbc7-107">Para exibir a chave compartilhada, use [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="5dbc7-107">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a><span data-ttu-id="5dbc7-108">Para exibir o endereço IP público do gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="5dbc7-108">To view the VPN gateway Public IP address</span></span>

<span data-ttu-id="5dbc7-109">Para localizar o endereço IP público do seu gateway de rede virtual, use o comando [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="5dbc7-109">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="5dbc7-110">Para facilitar a leitura, a saída para este exemplo é formatada para exibir a lista de IPs públicos em formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="5dbc7-110">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
