Você deve criar uma rede virtual e uma sub-rede do gateway primeiro, antes de iniciar Olá tarefas a seguir. Consulte o artigo Olá [configurar uma rede Virtual usando o portal clássico Olá](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obter mais informações.   

## <a name="add-a-gateway"></a>Adicionar um gateway
Use o comando Olá abaixo toocreate um gateway. Ser toosubstitute-se de que os valores para seus próprios.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Verifique se o gateway de saudação foi criado
Use Olá comando abaixo tooverify que Olá gateway foi criado. Esse comando também recupera a ID de gateway hello, que é necessário para outras operações.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Redimensionar um gateway
Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Você pode usar Olá Olá do comando toochange SKU de Gateway a seguir a qualquer momento.

> [!IMPORTANT]
> Esse comando não funciona para o gateway UltraPerformance. toochange gateway gateway tooan UltraPerformance, primeiro remova Olá existente do gateway de rota expressa e, em seguida, criar um novo gateway UltraPerformance. toodowngrade seu gateway de um gateway UltraPerformance, primeiro remova Olá UltraPerformance gateway e, em seguida, criar um novo gateway. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Remover um gateway
Use o comando Olá abaixo tooremove um gateway

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>