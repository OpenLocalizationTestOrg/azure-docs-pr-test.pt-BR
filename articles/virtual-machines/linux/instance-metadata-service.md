---
title: "Serviço de Metadados de Instância do Azure para VMs do Linux | Microsoft Docs"
description: "A Interface RESTful para obter informações sobre a computação, a rede e os eventos de manutenção futura da VM do Linux."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a61acbe0532ece3a6a26ceb366c12c69db4c304c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="236df-103">Serviço de metadados da instância do Azure para VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="236df-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="236df-104">O Serviço de metadados de instância do Azure fornece informações sobre instâncias da máquina virtual em execução que podem ser usadas para gerenciar e configurar suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="236df-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="236df-105">Isso inclui informações como SKU, configuração de rede e eventos de manutenção futura.</span><span class="sxs-lookup"><span data-stu-id="236df-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="236df-106">Para obter mais informações sobre o tipo de informação que está disponível, consulte [categorias de metadados](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="236df-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="236df-107">O serviço de metadados de instância do Azure é um ponto de extremidade REST disponível para todas as máquinas virtuais de IaaS criadas por meio [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="236df-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="236df-108">O ponto de extremidade está disponível em um endereço IP não roteável conhecido (`169.254.169.254`) que pode ser acessado somente de dentro da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="236df-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="236df-109">Esse serviço é **disponível geralmente** em regiões do Azure globais.</span><span class="sxs-lookup"><span data-stu-id="236df-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="236df-110">Ele está em visualização pública para o governo, China e em nuvem alemã do Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="236df-111">Regularmente, ele recebe atualizações para expor informações novas sobre instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="236df-111">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="236df-112">Esta página reflete as atualizadas [categorias de dados](#instance-metadata-data-categories) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="236df-112">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="236df-113">Disponibilidade do serviço</span><span class="sxs-lookup"><span data-stu-id="236df-113">Service availability</span></span>
<span data-ttu-id="236df-114">Esse serviço é disponível geralmente em regiões do Azure globais.</span><span class="sxs-lookup"><span data-stu-id="236df-114">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="236df-115">O serviço está em visualização pública nas regiões governamentais, China ou Alemanha.</span><span class="sxs-lookup"><span data-stu-id="236df-115">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="236df-116">Regiões</span><span class="sxs-lookup"><span data-stu-id="236df-116">Regions</span></span>                                        | <span data-ttu-id="236df-117">Disponibilidade?</span><span class="sxs-lookup"><span data-stu-id="236df-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="236df-118">Todas as regiões globais do Azure disponíveis</span><span class="sxs-lookup"><span data-stu-id="236df-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="236df-119">Disponível</span><span class="sxs-lookup"><span data-stu-id="236df-119">Generally Available</span></span> 
[<span data-ttu-id="236df-120">Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="236df-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="236df-121">Na visualização</span><span class="sxs-lookup"><span data-stu-id="236df-121">In Preview</span></span> 
[<span data-ttu-id="236df-122">Azure China:</span><span class="sxs-lookup"><span data-stu-id="236df-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="236df-123">Na visualização</span><span class="sxs-lookup"><span data-stu-id="236df-123">In Preview</span></span>
[<span data-ttu-id="236df-124">Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="236df-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="236df-125">Na visualização</span><span class="sxs-lookup"><span data-stu-id="236df-125">In Preview</span></span>

<span data-ttu-id="236df-126">Esta tabela é atualizada quando o serviço está disponível em outras nuvens do Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-126">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="236df-127">Para testar o serviço de metadados de instância, crie uma VM do [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou [portal do Azure](http://portal.azure.com) nas regiões acima e siga os exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="236df-127">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="236df-128">Uso</span><span class="sxs-lookup"><span data-stu-id="236df-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="236df-129">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="236df-129">Versioning</span></span>
<span data-ttu-id="236df-130">O Serviço de Metadados de Instância tem controle de versão.</span><span class="sxs-lookup"><span data-stu-id="236df-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="236df-131">As versões são obrigatórias e a versão atual é `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="236df-131">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-132">Versões de visualização anteriores de eventos agendados compatíveis {mais recentes} como a api-version.</span><span class="sxs-lookup"><span data-stu-id="236df-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="236df-133">Esse formato não é mais suportado e será substituído no futuro.</span><span class="sxs-lookup"><span data-stu-id="236df-133">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="236df-134">Como adicionamos versões mais recentes, as versões mais antigas ainda podem ser acessadas para fins de compatibilidade se os scripts tiverem dependências de formatos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="236df-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="236df-135">Entretanto, observe que a versão de visualização atual (2017-03-01) poderá não estar disponível quando o serviço estiver totalmente disponível.</span><span class="sxs-lookup"><span data-stu-id="236df-135">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="236df-136">Uso de cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="236df-136">Using headers</span></span>
<span data-ttu-id="236df-137">Ao consultar o Serviço de Metadados você deverá fornecer o cabeçalho `Metadata: true` para garantir que a solicitação não seja redirecionada de forma involuntária.</span><span class="sxs-lookup"><span data-stu-id="236df-137">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="236df-138">Configurando e recuperando os metadados</span><span class="sxs-lookup"><span data-stu-id="236df-138">Retrieving metadata</span></span>

<span data-ttu-id="236df-139">Os metadados de instância estão disponíveis para a execução de máquinas virtuais criadas/gerenciadas usando o [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="236df-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="236df-140">Acessar todas as categorias de dados para uma instância de máquina virtual usando a seguinte solicitação:</span><span class="sxs-lookup"><span data-stu-id="236df-140">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="236df-141">Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="236df-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="236df-142">Saída de dados</span><span class="sxs-lookup"><span data-stu-id="236df-142">Data output</span></span>
<span data-ttu-id="236df-143">Por padrão, o serviço de metadados de instância retorna dados em formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="236df-143">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="236df-144">No entanto, diferentes APIs podem retornar dados em formatos diferentes, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="236df-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="236df-145">A tabela a seguir é uma referência de outros formatos de dados que pode oferecer suporte a APIs.</span><span class="sxs-lookup"><span data-stu-id="236df-145">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="236df-146">API</span><span class="sxs-lookup"><span data-stu-id="236df-146">API</span></span> | <span data-ttu-id="236df-147">Formato de dados padrão</span><span class="sxs-lookup"><span data-stu-id="236df-147">Default Data Format</span></span> | <span data-ttu-id="236df-148">Outros formatos</span><span class="sxs-lookup"><span data-stu-id="236df-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="236df-149">/instance</span><span class="sxs-lookup"><span data-stu-id="236df-149">/instance</span></span> | <span data-ttu-id="236df-150">json</span><span class="sxs-lookup"><span data-stu-id="236df-150">json</span></span> | <span data-ttu-id="236df-151">texto</span><span class="sxs-lookup"><span data-stu-id="236df-151">text</span></span>
<span data-ttu-id="236df-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="236df-152">/scheduledevents</span></span> | <span data-ttu-id="236df-153">json</span><span class="sxs-lookup"><span data-stu-id="236df-153">json</span></span> | <span data-ttu-id="236df-154">nenhum</span><span class="sxs-lookup"><span data-stu-id="236df-154">none</span></span>

<span data-ttu-id="236df-155">Para acessar um formato de resposta não padrão, especifique o formato solicitado como um parâmetro querystring na solicitação.</span><span class="sxs-lookup"><span data-stu-id="236df-155">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="236df-156">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="236df-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="236df-157">Segurança</span><span class="sxs-lookup"><span data-stu-id="236df-157">Security</span></span>
<span data-ttu-id="236df-158">O ponto de extremidade de metadados de instância está acessível somente dentro da instância de máquina virtual em execução em um endereço IP não roteável.</span><span class="sxs-lookup"><span data-stu-id="236df-158">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="236df-159">Além disso, qualquer solicitação com `X-Forwarded-For`Cabeçalho é rejeitada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="236df-159">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="236df-160">Também exigimos que as solicitações contenham um `Metadata: true` cabeçalho para garantir que a solicitação real tenha sido desejada diretamente e não faça parte de um redirecionamento não intencional.</span><span class="sxs-lookup"><span data-stu-id="236df-160">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="236df-161">Erro</span><span class="sxs-lookup"><span data-stu-id="236df-161">Error</span></span>
<span data-ttu-id="236df-162">Se houver um elemento de dados não encontrado ou solicitações malformadas, o serviço de metadados da instância retornará o erro de HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="236df-162">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="236df-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="236df-163">For example:</span></span>

<span data-ttu-id="236df-164">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="236df-164">HTTP Status Code</span></span> | <span data-ttu-id="236df-165">Motivo</span><span class="sxs-lookup"><span data-stu-id="236df-165">Reason</span></span>
----------------|-------
<span data-ttu-id="236df-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="236df-166">200 OK</span></span> |
<span data-ttu-id="236df-167">400 Solicitação Inválida</span><span class="sxs-lookup"><span data-stu-id="236df-167">400 Bad Request</span></span> | <span data-ttu-id="236df-168">Faltando `Metadata: true` cabeçalho</span><span class="sxs-lookup"><span data-stu-id="236df-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="236df-169">404 Não Encontrado</span><span class="sxs-lookup"><span data-stu-id="236df-169">404 Not Found</span></span> | <span data-ttu-id="236df-170">O elemento solicitado não existe</span><span class="sxs-lookup"><span data-stu-id="236df-170">The requested element does't exist</span></span> 
<span data-ttu-id="236df-171">405 método não permitido</span><span class="sxs-lookup"><span data-stu-id="236df-171">405 Method Not Allowed</span></span> | <span data-ttu-id="236df-172">Somente as solicitações `GET` e `POST` são suportadas</span><span class="sxs-lookup"><span data-stu-id="236df-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="236df-173">429 Número excessivo de solicitações</span><span class="sxs-lookup"><span data-stu-id="236df-173">429 Too Many Requests</span></span> | <span data-ttu-id="236df-174">A API atualmente suporta um máximo de 5 consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="236df-174">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="236df-175">500 Erro do serviço</span><span class="sxs-lookup"><span data-stu-id="236df-175">500 Service Error</span></span>     | <span data-ttu-id="236df-176">Aguarde um pouco e tente novamente</span><span class="sxs-lookup"><span data-stu-id="236df-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="236df-177">Exemplos</span><span class="sxs-lookup"><span data-stu-id="236df-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-178">Todas as respostas de API são cadeias de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="236df-178">All API responses are JSON strings.</span></span> <span data-ttu-id="236df-179">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="236df-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="236df-180">Recuperação das informações de rede</span><span class="sxs-lookup"><span data-stu-id="236df-180">Retrieving network information</span></span>

<span data-ttu-id="236df-181">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="236df-182">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-183">A resposta é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="236df-183">The response is a JSON string.</span></span> <span data-ttu-id="236df-184">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="236df-184">The following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="236df-185">Recuperação do endereço IP público</span><span class="sxs-lookup"><span data-stu-id="236df-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="236df-186">Recuperação de todos os metadados para uma instância</span><span class="sxs-lookup"><span data-stu-id="236df-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="236df-187">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="236df-188">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-189">A resposta é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="236df-189">The response is a JSON string.</span></span> <span data-ttu-id="236df-190">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="236df-190">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="236df-191">Recuperação de metadados na máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="236df-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="236df-192">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-192">**Request**</span></span>

<span data-ttu-id="236df-193">Os metadados de instância podem ser recuperados no Windows por meio do utilitário do Powershell`curl`:</span><span class="sxs-lookup"><span data-stu-id="236df-193">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="236df-194">Ou por meio de `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="236df-194">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="236df-195">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-196">A resposta é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="236df-196">The response is a JSON string.</span></span> <span data-ttu-id="236df-197">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="236df-197">The following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="236df-198">Categorias de dados de metadados de instância</span><span class="sxs-lookup"><span data-stu-id="236df-198">Instance metadata data categories</span></span>
<span data-ttu-id="236df-199">As seguintes categorias de dados estão disponíveis por meio do serviço de metadados da instância:</span><span class="sxs-lookup"><span data-stu-id="236df-199">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="236df-200">Dados</span><span class="sxs-lookup"><span data-stu-id="236df-200">Data</span></span> | <span data-ttu-id="236df-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="236df-201">Description</span></span>
-----|------------
<span data-ttu-id="236df-202">location</span><span class="sxs-lookup"><span data-stu-id="236df-202">location</span></span> | <span data-ttu-id="236df-203">Região do Azure na qual a máquina virtual está sendo executada</span><span class="sxs-lookup"><span data-stu-id="236df-203">Azure Region the VM is running in</span></span>
<span data-ttu-id="236df-204">name</span><span class="sxs-lookup"><span data-stu-id="236df-204">name</span></span> | <span data-ttu-id="236df-205">Nome da VM</span><span class="sxs-lookup"><span data-stu-id="236df-205">Name of the VM</span></span> 
<span data-ttu-id="236df-206">oferta</span><span class="sxs-lookup"><span data-stu-id="236df-206">offer</span></span> | <span data-ttu-id="236df-207">Oferece informações para a imagem VM.</span><span class="sxs-lookup"><span data-stu-id="236df-207">Offer information for the VM image.</span></span> <span data-ttu-id="236df-208">Esse valor só está presente para as imagens implantadas na Galeria de imagens do Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="236df-209">publicador</span><span class="sxs-lookup"><span data-stu-id="236df-209">publisher</span></span> | <span data-ttu-id="236df-210">Publicador da imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-210">Publisher of the VM image</span></span>
<span data-ttu-id="236df-211">sku</span><span class="sxs-lookup"><span data-stu-id="236df-211">sku</span></span> | <span data-ttu-id="236df-212">SKU específica para a imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-212">Specific SKU for the VM image</span></span>  
<span data-ttu-id="236df-213">version</span><span class="sxs-lookup"><span data-stu-id="236df-213">version</span></span> | <span data-ttu-id="236df-214">Versão da imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-214">Version of the VM image</span></span> 
<span data-ttu-id="236df-215">osType</span><span class="sxs-lookup"><span data-stu-id="236df-215">osType</span></span> | <span data-ttu-id="236df-216">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="236df-216">Linux or Windows</span></span> 
<span data-ttu-id="236df-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="236df-217">platformUpdateDomain</span></span> |  <span data-ttu-id="236df-218">[Domínio de atualização](manage-availability.md) no qual a máquina virtual está sendo executada</span><span class="sxs-lookup"><span data-stu-id="236df-218">[Update domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="236df-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="236df-219">platformFaultDomain</span></span> | <span data-ttu-id="236df-220">[Domínio de falha](manage-availability.md) no qual a máquina virtual está sendo executada</span><span class="sxs-lookup"><span data-stu-id="236df-220">[Fault domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="236df-221">vmId</span><span class="sxs-lookup"><span data-stu-id="236df-221">vmId</span></span> | <span data-ttu-id="236df-222">[Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="236df-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="236df-223">vmSize</span></span> | [<span data-ttu-id="236df-224">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="236df-224">VM size</span></span>](sizes.md)
<span data-ttu-id="236df-225">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="236df-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="236df-226">Endereço IPv4 local da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-226">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="236df-227">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="236df-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="236df-228">Endereço IPv4 local da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-228">Public IPv4 address of the VM</span></span>
<span data-ttu-id="236df-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="236df-229">subnet/address</span></span> | <span data-ttu-id="236df-230">Endereço sub-rede da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-230">Subnet address of the VM</span></span>
<span data-ttu-id="236df-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="236df-231">subnet/prefix</span></span> | <span data-ttu-id="236df-232">Prefixo de sub-rede, exemplo 24</span><span class="sxs-lookup"><span data-stu-id="236df-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="236df-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="236df-233">ipv6/ipAddress</span></span> | <span data-ttu-id="236df-234">Endereço IPv6 local da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-234">Local IPv6 address of the VM</span></span>
<span data-ttu-id="236df-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="236df-235">macAddress</span></span> | <span data-ttu-id="236df-236">Endereço mac da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="236df-236">VM mac address</span></span> 
<span data-ttu-id="236df-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="236df-237">scheduledevents</span></span> | <span data-ttu-id="236df-238">No momento em Consulte de visualização pública [aventosagendados](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="236df-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="236df-239">Cenários de exemplo para uso</span><span class="sxs-lookup"><span data-stu-id="236df-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="236df-240">VM de controle em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="236df-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="236df-241">Como provedor de serviço, você talvez precise controlar o número de máquinas virtuais que executam o seu software ou ter agentes que precisam controlar a exclusividade da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="236df-241">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="236df-242">Para obter uma ID exclusiva de uma máquina virtual, use o `vmId` campo do serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="236df-242">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="236df-243">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="236df-244">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="236df-245">Posicionamento de contêineres, partições de dados com base em domínio de falha/atualização</span><span class="sxs-lookup"><span data-stu-id="236df-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="236df-246">Para determinados cenários nos quais o posicionamento de réplicas diferentes é de vital importância.</span><span class="sxs-lookup"><span data-stu-id="236df-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="236df-247">Por exemplo, o [posicionamento de réplica de HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou o posicionamento do contêiner por meio de um [organizador](https://kubernetes.io/docs/user-guide/node-selection/) podem exigir que você conheça os `platformFaultDomain` e `platformUpdateDomain` nas quais a máquina virtual está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="236df-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="236df-248">Você pode consultar esses dados diretamente por meio de serviço de metadados.</span><span class="sxs-lookup"><span data-stu-id="236df-248">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="236df-249">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="236df-250">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="236df-251">Obtendo mais informações sobre a máquina virtual durante a ocorrência de suporte</span><span class="sxs-lookup"><span data-stu-id="236df-251">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="236df-252">Como provedor de serviços, você poderá receber uma chamada de suporte na qual gostaria de ter mais informações sobre a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="236df-252">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="236df-253">Pedir ao cliente para informar os metadados de computação pode fornecer informações básicas para o profissional de suporte saber o tipo de VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-253">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="236df-254">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="236df-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="236df-255">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="236df-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="236df-256">A resposta é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="236df-256">The response is a JSON string.</span></span> <span data-ttu-id="236df-257">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="236df-257">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="236df-258">Exemplos de como chamar o serviço de metadados usando diferentes idiomas dentro da VM</span><span class="sxs-lookup"><span data-stu-id="236df-258">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="236df-259">Linguagem</span><span class="sxs-lookup"><span data-stu-id="236df-259">Language</span></span> | <span data-ttu-id="236df-260">Exemplo</span><span class="sxs-lookup"><span data-stu-id="236df-260">Example</span></span> 
---------|----------------
<span data-ttu-id="236df-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="236df-261">Ruby</span></span>     | <span data-ttu-id="236df-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="236df-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="236df-263">Vá Lan</span><span class="sxs-lookup"><span data-stu-id="236df-263">Go Lan</span></span>   | <span data-ttu-id="236df-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="236df-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="236df-265">python</span><span class="sxs-lookup"><span data-stu-id="236df-265">python</span></span>   | <span data-ttu-id="236df-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="236df-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="236df-267">C++</span><span class="sxs-lookup"><span data-stu-id="236df-267">C++</span></span>      | <span data-ttu-id="236df-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="236df-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="236df-269">C#</span><span class="sxs-lookup"><span data-stu-id="236df-269">C#</span></span>       | <span data-ttu-id="236df-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="236df-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="236df-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="236df-271">Javascript</span></span> | <span data-ttu-id="236df-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="236df-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="236df-273">Powershell</span><span class="sxs-lookup"><span data-stu-id="236df-273">Powershell</span></span> | <span data-ttu-id="236df-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="236df-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="236df-275">Bash</span><span class="sxs-lookup"><span data-stu-id="236df-275">Bash</span></span>       | <span data-ttu-id="236df-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="236df-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="236df-277">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="236df-277">FAQ</span></span>
1. <span data-ttu-id="236df-278">Estou recebendo o erro `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="236df-278">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="236df-279">O que isso significa?</span><span class="sxs-lookup"><span data-stu-id="236df-279">What does this mean?</span></span>
   * <span data-ttu-id="236df-280">O serviço de metadados de instância exige que o cabeçalho `Metadata: true` seja passado na solicitação.</span><span class="sxs-lookup"><span data-stu-id="236df-280">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="236df-281">Passar o cabeçalho na chamada de REST permite acessar o serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="236df-281">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="236df-282">Por que não estou obtendo informações de computação para minha máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="236df-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="236df-283">Atualmente o serviço de metadados de instância suporta apenas instâncias criadas com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-283">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="236df-284">No futuro, poderemos adicionar suporte para VMs de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="236df-284">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="236df-285">Criei minha máquina virtual com o Azure Resource Manager há algum tempo.</span><span class="sxs-lookup"><span data-stu-id="236df-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="236df-286">Por que não consigo ver as informações de metadados de computação?</span><span class="sxs-lookup"><span data-stu-id="236df-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="236df-287">Para todas as máquinas virtuais criadas depois de setembro de 2016, adicione uma [marca](../../azure-resource-manager/resource-group-using-tags.md) para começar a ver os metadados de computação.</span><span class="sxs-lookup"><span data-stu-id="236df-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="236df-288">Para máquinas virtuais mais antigas (criadas antes de setembro de 2016), adicione ou remova extensões ou dados de discos à máquina virtual para atualizar os metadados.</span><span class="sxs-lookup"><span data-stu-id="236df-288">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="236df-289">Por que estou recebendo o erro `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="236df-289">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="236df-290">Repita a solicitação com base no sistema de retirada exponencial.</span><span class="sxs-lookup"><span data-stu-id="236df-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="236df-291">Se o problema persistir, contate o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="236df-291">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="236df-292">Onde posso publicar comentários/perguntas adicionais?</span><span class="sxs-lookup"><span data-stu-id="236df-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="236df-293">Envie seus comentários em http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="236df-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="236df-294">Isso funcionaria para Instância do Conjunto de Dimensionamento da Máquina Virtual?</span><span class="sxs-lookup"><span data-stu-id="236df-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="236df-295">Sim, o serviço de metadados está disponível para instâncias de conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="236df-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="236df-296">Como posso obter suporte para o serviço?</span><span class="sxs-lookup"><span data-stu-id="236df-296">How do I get support for the service?</span></span>
   * <span data-ttu-id="236df-297">Para obter suporte para o serviço, crie um problema de suporte no portal do Azure para a máquina virtual na qual você não consegue obter resposta de metadados após várias tentativas</span><span class="sxs-lookup"><span data-stu-id="236df-297">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Serviço de Metadados de Instância](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="236df-299">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="236df-299">Next steps</span></span>

- <span data-ttu-id="236df-300">Saiba mais sobre a API dos [Eventos Agendados](scheduled-events.md) **em visualização pública** fornecida pelo serviço Metadados de Instância.</span><span class="sxs-lookup"><span data-stu-id="236df-300">Learn more about the [Scheduled Events](scheduled-events.md) API **in public preview** provided by the Instance Metadata service.</span></span>
