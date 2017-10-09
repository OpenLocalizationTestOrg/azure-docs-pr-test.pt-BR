## <a name="traffic-manager-profile"></a><span data-ttu-id="9adec-101">Perfil de Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="9adec-101">Traffic Manager Profile</span></span>
<span data-ttu-id="9adec-102">O traffic manager e seus recursos de ponto de extremidade filho habilitar tooendpoints de roteamento de DNS no Azure e fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="9adec-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="9adec-103">Essa distribuição de tráfego é controlada por métodos de política de roteamento.</span><span class="sxs-lookup"><span data-stu-id="9adec-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="9adec-104">Traffic manager também permite toobe de integridade do ponto de extremidade é monitorado e tráfego desviado adequadamente com base na integridade de saudação de um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9adec-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="9adec-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9adec-105">Property</span></span> | <span data-ttu-id="9adec-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="9adec-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9adec-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="9adec-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="9adec-108">os valores possíveis são *Desempenho*, *Ponderado* e *Prioridade*</span><span class="sxs-lookup"><span data-stu-id="9adec-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="9adec-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="9adec-109">**dnsConfig**</span></span> |<span data-ttu-id="9adec-110">FQDN para o perfil de saudação</span><span class="sxs-lookup"><span data-stu-id="9adec-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="9adec-111">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="9adec-111">**Protocol**</span></span> |<span data-ttu-id="9adec-112">protocolo de monitoramento, os valores possíveis são *HTTP* e *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="9adec-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="9adec-113">**Porta**</span><span class="sxs-lookup"><span data-stu-id="9adec-113">**Port**</span></span> |<span data-ttu-id="9adec-114">porta de monitoramento</span><span class="sxs-lookup"><span data-stu-id="9adec-114">monitoring port</span></span> |
| <span data-ttu-id="9adec-115">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="9adec-115">**Path**</span></span> |<span data-ttu-id="9adec-116">caminho de monitoramento</span><span class="sxs-lookup"><span data-stu-id="9adec-116">monitoring path</span></span> |
| <span data-ttu-id="9adec-117">**Pontos de extremidade**</span><span class="sxs-lookup"><span data-stu-id="9adec-117">**Endpoints**</span></span> |<span data-ttu-id="9adec-118">contêiner para recursos de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="9adec-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="9adec-119">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="9adec-119">Endpoint</span></span>
<span data-ttu-id="9adec-120">Um ponto de extremidade é um recurso de filho de um perfil de Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="9adec-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="9adec-121">Representa um serviço ou tráfego de usuário de toowhich de ponto de extremidade da web é distribuído com base na política de saudação configurada no hello recurso de perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="9adec-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="9adec-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9adec-122">Property</span></span> | <span data-ttu-id="9adec-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="9adec-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9adec-124">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="9adec-124">**Type**</span></span> |<span data-ttu-id="9adec-125">Olá tipo de ponto de extremidade hello, os valores possíveis são *Azure ponto*, *ponto de extremidade externo*, e *aninhados ponto de extremidade*</span><span class="sxs-lookup"><span data-stu-id="9adec-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="9adec-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="9adec-126">**targetResourceId**</span></span> |<span data-ttu-id="9adec-127">endereço IP público de um ponto de extremidade de serviço ou da Web.</span><span class="sxs-lookup"><span data-stu-id="9adec-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="9adec-128">Isso pode ser um ponto de extremidade do Azure ou externo.</span><span class="sxs-lookup"><span data-stu-id="9adec-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="9adec-129">**Peso**</span><span class="sxs-lookup"><span data-stu-id="9adec-129">**Weight**</span></span> |<span data-ttu-id="9adec-130">peso de ponto de extremidade usado no gerenciamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="9adec-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="9adec-131">**Prioridade**</span><span class="sxs-lookup"><span data-stu-id="9adec-131">**Priority**</span></span> |<span data-ttu-id="9adec-132">prioridade de ponto de extremidade Olá toodefine usado uma ação de failover</span><span class="sxs-lookup"><span data-stu-id="9adec-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="9adec-133">Exemplo do Gerenciador de Tráfego no formato Json:</span><span class="sxs-lookup"><span data-stu-id="9adec-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="9adec-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9adec-134">Additional resources</span></span>
<span data-ttu-id="9adec-135">Leia a [documentação da API REST para o Gerenciador de Tráfego](https://msdn.microsoft.com/library/azure/mt163664.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="9adec-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

