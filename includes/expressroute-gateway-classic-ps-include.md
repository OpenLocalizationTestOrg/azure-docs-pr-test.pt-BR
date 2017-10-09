<span data-ttu-id="8fc35-101">Você deve criar uma rede virtual e uma sub-rede do gateway primeiro, antes de iniciar Olá tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8fc35-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="8fc35-102">Consulte o artigo Olá [configurar uma rede Virtual usando o portal clássico Olá](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8fc35-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="8fc35-103">Adicionar um gateway</span><span class="sxs-lookup"><span data-stu-id="8fc35-103">Add a gateway</span></span>
<span data-ttu-id="8fc35-104">Use o comando Olá abaixo toocreate um gateway.</span><span class="sxs-lookup"><span data-stu-id="8fc35-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="8fc35-105">Ser toosubstitute-se de que os valores para seus próprios.</span><span class="sxs-lookup"><span data-stu-id="8fc35-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="8fc35-106">Verifique se o gateway de saudação foi criado</span><span class="sxs-lookup"><span data-stu-id="8fc35-106">Verify hello gateway was created</span></span>
<span data-ttu-id="8fc35-107">Use Olá comando abaixo tooverify que Olá gateway foi criado.</span><span class="sxs-lookup"><span data-stu-id="8fc35-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="8fc35-108">Esse comando também recupera a ID de gateway hello, que é necessário para outras operações.</span><span class="sxs-lookup"><span data-stu-id="8fc35-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="8fc35-109">Redimensionar um gateway</span><span class="sxs-lookup"><span data-stu-id="8fc35-109">Resize a gateway</span></span>
<span data-ttu-id="8fc35-110">Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="8fc35-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="8fc35-111">Você pode usar Olá Olá do comando toochange SKU de Gateway a seguir a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="8fc35-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc35-112">Esse comando não funciona para o gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="8fc35-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="8fc35-113">toochange gateway gateway tooan UltraPerformance, primeiro remova Olá existente do gateway de rota expressa e, em seguida, criar um novo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="8fc35-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="8fc35-114">toodowngrade seu gateway de um gateway UltraPerformance, primeiro remova Olá UltraPerformance gateway e, em seguida, criar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="8fc35-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="8fc35-115">Remover um gateway</span><span class="sxs-lookup"><span data-stu-id="8fc35-115">Remove a gateway</span></span>
<span data-ttu-id="8fc35-116">Use o comando Olá abaixo tooremove um gateway</span><span class="sxs-lookup"><span data-stu-id="8fc35-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>