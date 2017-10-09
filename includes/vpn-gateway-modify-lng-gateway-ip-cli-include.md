### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="f9ab1-101">gateway de rede local toomodify Olá 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="f9ab1-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="f9ab1-102">Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="f9ab1-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="f9ab1-103">endereço IP do gateway Olá pode ser alterado sem remover uma conexão de gateway VPN existente (se houver).</span><span class="sxs-lookup"><span data-stu-id="f9ab1-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="f9ab1-104">endereço de IP do gateway de saudação toomodify, substituir valores de saudação 'Site2' e 'TestRG1' com seu próprio usando Olá [atualização de gateway local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.</span><span class="sxs-lookup"><span data-stu-id="f9ab1-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="f9ab1-105">Verifique se o endereço IP de saudação está correto na saída de hello:</span><span class="sxs-lookup"><span data-stu-id="f9ab1-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```