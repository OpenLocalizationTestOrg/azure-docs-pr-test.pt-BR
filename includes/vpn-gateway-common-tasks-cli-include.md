### <a name="tooview-local-network-gateways"></a><span data-ttu-id="3686f-101">tooview gateways de rede local</span><span class="sxs-lookup"><span data-stu-id="3686f-101">tooview local network gateways</span></span>

<span data-ttu-id="3686f-102">tooview uma lista de gateways de rede local hello, use Olá [lista de gateway local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.</span><span class="sxs-lookup"><span data-stu-id="3686f-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="3686f-103">valores de chave tooverify Olá compartilhado</span><span class="sxs-lookup"><span data-stu-id="3686f-103">tooverify hello shared key values</span></span>

<span data-ttu-id="3686f-104">Verifique se o valor de chave Olá compartilhado é Olá mesmo valor que você usou para a sua configuração de dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="3686f-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="3686f-105">Se não estiver, execute conexão Olá novamente usando o valor de saudação do dispositivo hello ou atualizar dispositivo Olá com valor de saudação do hello retorno.</span><span class="sxs-lookup"><span data-stu-id="3686f-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="3686f-106">Olá valores devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="3686f-106">hello values must match.</span></span> <span data-ttu-id="3686f-107">Olá tooview compartilhado chave, use Olá [lista de conexão de vpn de rede az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="3686f-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="3686f-108">gateway VPN tooview Olá endereço IP público</span><span class="sxs-lookup"><span data-stu-id="3686f-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="3686f-109">toofind Olá endereço IP público do seu gateway de rede virtual, use Olá [lista de ip público de rede az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="3686f-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="3686f-110">Para facilitar a leitura, a saída de hello para este exemplo é formatado toodisplay lista de saudação de IPs públicos em formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="3686f-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
