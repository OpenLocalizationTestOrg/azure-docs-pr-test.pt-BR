## <a name="public-ip-address"></a><span data-ttu-id="c8e57-101">Endereço IP público</span><span class="sxs-lookup"><span data-stu-id="c8e57-101">Public IP address</span></span>
<span data-ttu-id="c8e57-102">Um recurso de endereço IP público fornece um endereço IP para Internet dinâmico ou reservado.</span><span class="sxs-lookup"><span data-stu-id="c8e57-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="c8e57-103">Embora você possa criar um endereço IP público como um objeto autônomo, você precisa tooassociate-tooanother objeto tooactually usar endereço hello.</span><span class="sxs-lookup"><span data-stu-id="c8e57-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="c8e57-104">Você pode associar um balanceador de carga do tooa de endereço IP público, o gateway de aplicativo ou uma NIC tooprovide Internet acessar toothose os recursos.</span><span class="sxs-lookup"><span data-stu-id="c8e57-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="c8e57-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c8e57-105">Property</span></span> | <span data-ttu-id="c8e57-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="c8e57-106">Description</span></span> | <span data-ttu-id="c8e57-107">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="c8e57-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8e57-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="c8e57-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="c8e57-109">Define se o endereço IP de saudação é *estático* ou *dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="c8e57-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="c8e57-110">estático, dinâmico</span><span class="sxs-lookup"><span data-stu-id="c8e57-110">static, dynamic</span></span> |
| <span data-ttu-id="c8e57-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="c8e57-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="c8e57-112">Define o limite de tempo ocioso hello, com um valor padrão de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="c8e57-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="c8e57-113">Se não há mais pacotes para uma determinada sessão for recebida dentro desse período, a sessão de saudação é encerrada.</span><span class="sxs-lookup"><span data-stu-id="c8e57-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="c8e57-114">qualquer valor entre 4 e 30</span><span class="sxs-lookup"><span data-stu-id="c8e57-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="c8e57-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="c8e57-115">**ipAddress**</span></span> |<span data-ttu-id="c8e57-116">Endereço IP atribuído tooobject.</span><span class="sxs-lookup"><span data-stu-id="c8e57-116">IP address assigned tooobject.</span></span> <span data-ttu-id="c8e57-117">Essa é uma propriedade somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c8e57-117">This is a read-only property.</span></span> |<span data-ttu-id="c8e57-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="c8e57-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="c8e57-119">Configurações DNS</span><span class="sxs-lookup"><span data-stu-id="c8e57-119">DNS settings</span></span>
<span data-ttu-id="c8e57-120">Endereços IP públicos tem um objeto filho chamado **dnsSettings** contendo Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8e57-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="c8e57-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c8e57-121">Property</span></span> | <span data-ttu-id="c8e57-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="c8e57-122">Description</span></span> | <span data-ttu-id="c8e57-123">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="c8e57-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8e57-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="c8e57-124">**domainNameLabel**</span></span> |<span data-ttu-id="c8e57-125">Host nomeado usado para resolução de nomes.</span><span class="sxs-lookup"><span data-stu-id="c8e57-125">Host named used for name resolution.</span></span> |<span data-ttu-id="c8e57-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="c8e57-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="c8e57-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="c8e57-127">**fqdn**</span></span> |<span data-ttu-id="c8e57-128">Nome totalmente qualificado para o IP público hello.</span><span class="sxs-lookup"><span data-stu-id="c8e57-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="c8e57-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="c8e57-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="c8e57-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="c8e57-130">**reverseFqdn**</span></span> |<span data-ttu-id="c8e57-131">Nome de domínio totalmente qualificado que resolve o endereço IP de toohello e está registrado no DNS como um registro PTR.</span><span class="sxs-lookup"><span data-stu-id="c8e57-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="c8e57-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c8e57-132">www.contoso.com.</span></span> |

<span data-ttu-id="c8e57-133">Endereço IP de público exemplo, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="c8e57-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="c8e57-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c8e57-134">Additional resources</span></span>
* <span data-ttu-id="c8e57-135">Obtenha mais informações sobre [endereços IP públicos](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c8e57-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="c8e57-136">Saiba mais sobre [endereços IP públicos em nível de instância](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c8e57-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="c8e57-137">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="c8e57-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

