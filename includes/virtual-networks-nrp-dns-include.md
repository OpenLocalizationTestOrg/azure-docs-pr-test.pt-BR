## <a name="azure-dns"></a><span data-ttu-id="765de-101">DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="765de-101">Azure DNS</span></span>
<span data-ttu-id="765de-102">O DNS do Azure é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="765de-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="765de-103">Propriedade</span><span class="sxs-lookup"><span data-stu-id="765de-103">Property</span></span> | <span data-ttu-id="765de-104">Descrição</span><span class="sxs-lookup"><span data-stu-id="765de-104">Description</span></span> | <span data-ttu-id="765de-105">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="765de-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="765de-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="765de-106">**DNSzones**</span></span> |<span data-ttu-id="765de-107">Registros DNS de toohost de informações da zona do domínio de um domínio específico</span><span class="sxs-lookup"><span data-stu-id="765de-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="765de-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="765de-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="765de-109">Conjuntos de registros DNS</span><span class="sxs-lookup"><span data-stu-id="765de-109">DNS record sets</span></span>
<span data-ttu-id="765de-110">As zonas DNS têm um objeto filho chamado conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="765de-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="765de-111">Conjuntos de registros são uma coleção de registros de host por tipo para uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="765de-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="765de-112">Os tipos de gravação são A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="765de-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="765de-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="765de-113">Property</span></span> | <span data-ttu-id="765de-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="765de-114">Description</span></span> | <span data-ttu-id="765de-115">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="765de-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="765de-116">Uma</span><span class="sxs-lookup"><span data-stu-id="765de-116">A</span></span> |<span data-ttu-id="765de-117">Tipo de registro do IPv4</span><span class="sxs-lookup"><span data-stu-id="765de-117">IPv4 record type</span></span> |<span data-ttu-id="765de-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="765de-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="765de-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="765de-119">AAAA</span></span> |<span data-ttu-id="765de-120">Tipo de registro do IPv6</span><span class="sxs-lookup"><span data-stu-id="765de-120">IPv6 record type</span></span> |<span data-ttu-id="765de-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="765de-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="765de-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="765de-122">CNAME</span></span> |<span data-ttu-id="765de-123">tipo de registro de nome canônico <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="765de-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="765de-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="765de-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="765de-125">MX</span><span class="sxs-lookup"><span data-stu-id="765de-125">MX</span></span> |<span data-ttu-id="765de-126">tipo de registro de email</span><span class="sxs-lookup"><span data-stu-id="765de-126">mail record type</span></span> |<span data-ttu-id="765de-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="765de-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="765de-128">NS</span><span class="sxs-lookup"><span data-stu-id="765de-128">NS</span></span> |<span data-ttu-id="765de-129">tipo de registro do servidor de nome</span><span class="sxs-lookup"><span data-stu-id="765de-129">name server record type</span></span> |<span data-ttu-id="765de-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="765de-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="765de-131">SOA</span><span class="sxs-lookup"><span data-stu-id="765de-131">SOA</span></span> |<span data-ttu-id="765de-132">Início do tipo de registro da Autoridade <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="765de-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="765de-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="765de-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="765de-134">SRV</span><span class="sxs-lookup"><span data-stu-id="765de-134">SRV</span></span> |<span data-ttu-id="765de-135">tipo de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="765de-135">service record type</span></span> |<span data-ttu-id="765de-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="765de-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="765de-137"><sup>1</sup> permite apenas um valor por conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="765de-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="765de-138"><sup>2</sup> permite apenas um SOA de tipo de registro por zona DNS.</span><span class="sxs-lookup"><span data-stu-id="765de-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="765de-139">Exemplo de zona DNS no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="765de-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="765de-140">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="765de-140">Additional resources</span></span>
<span data-ttu-id="765de-141">Saudação de leitura [documentação da API REST para zonas DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="765de-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="765de-142">Saudação de leitura [documentação da API REST para conjuntos de registros de DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="765de-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

