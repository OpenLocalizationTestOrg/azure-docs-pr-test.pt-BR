---
title: "aaaAzure serviço de metadados de instância para VMs do Linux | Microsoft Docs"
description: "Interface rESTful tooget obter informações sobre de Linux VM computação, rede e eventos de manutenção futura."
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
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="4a97b-103">Serviço de metadados da instância do Azure para VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="4a97b-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="4a97b-104">saudação de serviço de metadados de instância do Azure fornece informações sobre instâncias de máquina virtual que podem ser usado toomanage e configurar as máquinas virtuais em execução.</span><span class="sxs-lookup"><span data-stu-id="4a97b-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="4a97b-105">Isso inclui informações como SKU, configuração de rede e eventos de manutenção futura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="4a97b-106">Para obter mais informações sobre o tipo de informação que está disponível, consulte [categorias de metadados](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="4a97b-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="4a97b-107">Serviço de metadados de instância do Azure é um ponto de extremidade REST tooall acessível IaaS VMs criada por meio do hello [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="4a97b-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="4a97b-108">ponto de extremidade Hello está disponível em um endereço IP não roteável conhecido (`169.254.169.254`) que podem ser acessados somente de dentro de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="4a97b-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a97b-109">Esse serviço é **disponível geralmente** em regiões do Azure globais.</span><span class="sxs-lookup"><span data-stu-id="4a97b-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="4a97b-110">Ele está em visualização pública para o governo, China e em nuvem alemã do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="4a97b-111">Regularmente, ele recebe atualizações tooexpose novas informações sobre instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a97b-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="4a97b-112">Esta página reflete Olá atualizada [categorias de dados](#instance-metadata-data-categories) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4a97b-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="4a97b-113">Disponibilidade do serviço</span><span class="sxs-lookup"><span data-stu-id="4a97b-113">Service availability</span></span>
<span data-ttu-id="4a97b-114">serviço de saudação está disponível em todas as regiões do Azure Global disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4a97b-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="4a97b-115">serviço de saudação está em visualização pública no hello governamentais, China, Alemanha regiões.</span><span class="sxs-lookup"><span data-stu-id="4a97b-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="4a97b-116">Regiões</span><span class="sxs-lookup"><span data-stu-id="4a97b-116">Regions</span></span>                                        | <span data-ttu-id="4a97b-117">Disponibilidade?</span><span class="sxs-lookup"><span data-stu-id="4a97b-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="4a97b-118">Todas as regiões globais do Azure disponíveis</span><span class="sxs-lookup"><span data-stu-id="4a97b-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="4a97b-119">Disponível</span><span class="sxs-lookup"><span data-stu-id="4a97b-119">Generally Available</span></span> 
[<span data-ttu-id="4a97b-120">Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="4a97b-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="4a97b-121">Na visualização</span><span class="sxs-lookup"><span data-stu-id="4a97b-121">In Preview</span></span> 
[<span data-ttu-id="4a97b-122">Azure China:</span><span class="sxs-lookup"><span data-stu-id="4a97b-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="4a97b-123">Na visualização</span><span class="sxs-lookup"><span data-stu-id="4a97b-123">In Preview</span></span>
[<span data-ttu-id="4a97b-124">Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="4a97b-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="4a97b-125">Na visualização</span><span class="sxs-lookup"><span data-stu-id="4a97b-125">In Preview</span></span>

<span data-ttu-id="4a97b-126">Esta tabela é atualizada quando o serviço Olá torna-se disponível em outras nuvens do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="4a97b-127">tootry out Olá instância metadados de serviço, criar uma VM do [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou hello [portal do Azure](http://portal.azure.com) em Olá acima regiões e siga Olá exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="4a97b-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="4a97b-128">Uso</span><span class="sxs-lookup"><span data-stu-id="4a97b-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="4a97b-129">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="4a97b-129">Versioning</span></span>
<span data-ttu-id="4a97b-130">Olá serviço de metadados de instância é com controle de versão.</span><span class="sxs-lookup"><span data-stu-id="4a97b-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="4a97b-131">As versões são obrigatórias e Olá a versão atual é `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="4a97b-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-132">Versões anteriores de visualização de eventos agendados suportados {mais recente} como Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="4a97b-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="4a97b-133">Esse formato não é mais suportado e será substituído em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="4a97b-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="4a97b-134">Como adicionamos versões mais recentes, as versões mais antigas ainda podem ser acessadas para fins de compatibilidade se os scripts tiverem dependências de formatos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="4a97b-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="4a97b-135">No entanto, observe que version(2017-03-01) de visualização atual Olá pode não estar disponível quando o serviço de saudação estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="4a97b-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="4a97b-136">Uso de cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="4a97b-136">Using headers</span></span>
<span data-ttu-id="4a97b-137">Quando você consulta Olá instância metadados de serviço, você deve fornecer o cabeçalho Olá `Metadata: true` solicitação de saudação tooensure não foi redirecionada acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="4a97b-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="4a97b-138">Configurando e recuperando os metadados</span><span class="sxs-lookup"><span data-stu-id="4a97b-138">Retrieving metadata</span></span>

<span data-ttu-id="4a97b-139">Os metadados de instância estão disponíveis para a execução de máquinas virtuais criadas/gerenciadas usando o [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="4a97b-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="4a97b-140">Acesse todas as categorias de dados para uma instância de máquina virtual usando Olá solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a97b-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="4a97b-141">Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4a97b-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="4a97b-142">Saída de dados</span><span class="sxs-lookup"><span data-stu-id="4a97b-142">Data output</span></span>
<span data-ttu-id="4a97b-143">Por padrão, Olá instância metadados de serviço retorna dados em formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="4a97b-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="4a97b-144">No entanto, diferentes APIs podem retornar dados em formatos diferentes, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="4a97b-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="4a97b-145">Olá tabela a seguir é uma referência de outros formatos de dados que pode oferecer suporte a APIs.</span><span class="sxs-lookup"><span data-stu-id="4a97b-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="4a97b-146">API</span><span class="sxs-lookup"><span data-stu-id="4a97b-146">API</span></span> | <span data-ttu-id="4a97b-147">Formato de dados padrão</span><span class="sxs-lookup"><span data-stu-id="4a97b-147">Default Data Format</span></span> | <span data-ttu-id="4a97b-148">Outros formatos</span><span class="sxs-lookup"><span data-stu-id="4a97b-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="4a97b-149">/instance</span><span class="sxs-lookup"><span data-stu-id="4a97b-149">/instance</span></span> | <span data-ttu-id="4a97b-150">json</span><span class="sxs-lookup"><span data-stu-id="4a97b-150">json</span></span> | <span data-ttu-id="4a97b-151">texto</span><span class="sxs-lookup"><span data-stu-id="4a97b-151">text</span></span>
<span data-ttu-id="4a97b-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="4a97b-152">/scheduledevents</span></span> | <span data-ttu-id="4a97b-153">json</span><span class="sxs-lookup"><span data-stu-id="4a97b-153">json</span></span> | <span data-ttu-id="4a97b-154">nenhum</span><span class="sxs-lookup"><span data-stu-id="4a97b-154">none</span></span>

<span data-ttu-id="4a97b-155">tooaccess um formato de resposta não padrão, especificar o formato solicitado hello como um parâmetro de querystring na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a97b-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="4a97b-156">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a97b-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="4a97b-157">Segurança</span><span class="sxs-lookup"><span data-stu-id="4a97b-157">Security</span></span>
<span data-ttu-id="4a97b-158">ponto de extremidade de serviço de metadados de instância de saudação é acessível somente dentro Olá executando a instância de máquina virtual em um endereço IP não roteável.</span><span class="sxs-lookup"><span data-stu-id="4a97b-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="4a97b-159">Além disso, qualquer solicitação com um `X-Forwarded-For` cabeçalho é rejeitado pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a97b-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="4a97b-160">Também precisamos solicitações toocontain um `Metadata: true` tooensure de cabeçalho que Olá solicitação real diretamente foi pretendido e não faz parte do redirecionamento não intencional.</span><span class="sxs-lookup"><span data-stu-id="4a97b-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="4a97b-161">Erro</span><span class="sxs-lookup"><span data-stu-id="4a97b-161">Error</span></span>
<span data-ttu-id="4a97b-162">Se houver um elemento de dados não encontrado ou uma solicitação incorreta, Olá instância metadados de serviço retorna erros HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="4a97b-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="4a97b-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a97b-163">For example:</span></span>

<span data-ttu-id="4a97b-164">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="4a97b-164">HTTP Status Code</span></span> | <span data-ttu-id="4a97b-165">Motivo</span><span class="sxs-lookup"><span data-stu-id="4a97b-165">Reason</span></span>
----------------|-------
<span data-ttu-id="4a97b-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="4a97b-166">200 OK</span></span> |
<span data-ttu-id="4a97b-167">400 Solicitação Inválida</span><span class="sxs-lookup"><span data-stu-id="4a97b-167">400 Bad Request</span></span> | <span data-ttu-id="4a97b-168">Faltando `Metadata: true` cabeçalho</span><span class="sxs-lookup"><span data-stu-id="4a97b-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="4a97b-169">404 Não Encontrado</span><span class="sxs-lookup"><span data-stu-id="4a97b-169">404 Not Found</span></span> | <span data-ttu-id="4a97b-170">Olá does't elemento solicitado existe</span><span class="sxs-lookup"><span data-stu-id="4a97b-170">hello requested element does't exist</span></span> 
<span data-ttu-id="4a97b-171">405 método não permitido</span><span class="sxs-lookup"><span data-stu-id="4a97b-171">405 Method Not Allowed</span></span> | <span data-ttu-id="4a97b-172">Somente as solicitações `GET` e `POST` são suportadas</span><span class="sxs-lookup"><span data-stu-id="4a97b-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="4a97b-173">429 Número excessivo de solicitações</span><span class="sxs-lookup"><span data-stu-id="4a97b-173">429 Too Many Requests</span></span> | <span data-ttu-id="4a97b-174">Olá API atualmente suporta um máximo de 5 consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="4a97b-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="4a97b-175">500 Erro do serviço</span><span class="sxs-lookup"><span data-stu-id="4a97b-175">500 Service Error</span></span>     | <span data-ttu-id="4a97b-176">Aguarde um pouco e tente novamente</span><span class="sxs-lookup"><span data-stu-id="4a97b-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="4a97b-177">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4a97b-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-178">Todas as respostas de API são cadeias de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="4a97b-178">All API responses are JSON strings.</span></span> <span data-ttu-id="4a97b-179">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="4a97b-180">Recuperação das informações de rede</span><span class="sxs-lookup"><span data-stu-id="4a97b-180">Retrieving network information</span></span>

<span data-ttu-id="4a97b-181">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="4a97b-182">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-183">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="4a97b-183">hello response is a JSON string.</span></span> <span data-ttu-id="4a97b-184">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-184">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="4a97b-185">Recuperação do endereço IP público</span><span class="sxs-lookup"><span data-stu-id="4a97b-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="4a97b-186">Recuperação de todos os metadados para uma instância</span><span class="sxs-lookup"><span data-stu-id="4a97b-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="4a97b-187">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="4a97b-188">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-189">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="4a97b-189">hello response is a JSON string.</span></span> <span data-ttu-id="4a97b-190">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-190">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="4a97b-191">Recuperação de metadados na máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="4a97b-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="4a97b-192">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-192">**Request**</span></span>

<span data-ttu-id="4a97b-193">Metadados de instância podem ser recuperados no Windows por meio de saudação do PowerShell utilitário `curl`:</span><span class="sxs-lookup"><span data-stu-id="4a97b-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="4a97b-194">Ou por meio de saudação `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4a97b-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="4a97b-195">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-196">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="4a97b-196">hello response is a JSON string.</span></span> <span data-ttu-id="4a97b-197">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-197">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="4a97b-198">Categorias de dados de metadados de instância</span><span class="sxs-lookup"><span data-stu-id="4a97b-198">Instance metadata data categories</span></span>
<span data-ttu-id="4a97b-199">Olá categorias de dados a seguir está disponível por meio de saudação instância metadados de serviço:</span><span class="sxs-lookup"><span data-stu-id="4a97b-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="4a97b-200">Dados</span><span class="sxs-lookup"><span data-stu-id="4a97b-200">Data</span></span> | <span data-ttu-id="4a97b-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="4a97b-201">Description</span></span>
-----|------------
<span data-ttu-id="4a97b-202">location</span><span class="sxs-lookup"><span data-stu-id="4a97b-202">location</span></span> | <span data-ttu-id="4a97b-203">Saudação de região do Azure VM está em execução</span><span class="sxs-lookup"><span data-stu-id="4a97b-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="4a97b-204">name</span><span class="sxs-lookup"><span data-stu-id="4a97b-204">name</span></span> | <span data-ttu-id="4a97b-205">Nome da saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-205">Name of hello VM</span></span> 
<span data-ttu-id="4a97b-206">oferta</span><span class="sxs-lookup"><span data-stu-id="4a97b-206">offer</span></span> | <span data-ttu-id="4a97b-207">Oferece informações para a imagem VM hello.</span><span class="sxs-lookup"><span data-stu-id="4a97b-207">Offer information for hello VM image.</span></span> <span data-ttu-id="4a97b-208">Esse valor só está presente para as imagens implantadas na Galeria de imagens do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="4a97b-209">publicador</span><span class="sxs-lookup"><span data-stu-id="4a97b-209">publisher</span></span> | <span data-ttu-id="4a97b-210">Editor de imagem de VM Olá</span><span class="sxs-lookup"><span data-stu-id="4a97b-210">Publisher of hello VM image</span></span>
<span data-ttu-id="4a97b-211">sku</span><span class="sxs-lookup"><span data-stu-id="4a97b-211">sku</span></span> | <span data-ttu-id="4a97b-212">SKU específica para a imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="4a97b-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="4a97b-213">version</span><span class="sxs-lookup"><span data-stu-id="4a97b-213">version</span></span> | <span data-ttu-id="4a97b-214">Versão da imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="4a97b-214">Version of hello VM image</span></span> 
<span data-ttu-id="4a97b-215">osType</span><span class="sxs-lookup"><span data-stu-id="4a97b-215">osType</span></span> | <span data-ttu-id="4a97b-216">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="4a97b-216">Linux or Windows</span></span> 
<span data-ttu-id="4a97b-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="4a97b-217">platformUpdateDomain</span></span> |  <span data-ttu-id="4a97b-218">[Domínio de atualização](manage-availability.md) Olá VM está em execução em</span><span class="sxs-lookup"><span data-stu-id="4a97b-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="4a97b-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="4a97b-219">platformFaultDomain</span></span> | <span data-ttu-id="4a97b-220">[Domínio de falha](manage-availability.md) Olá VM está em execução em</span><span class="sxs-lookup"><span data-stu-id="4a97b-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="4a97b-221">vmId</span><span class="sxs-lookup"><span data-stu-id="4a97b-221">vmId</span></span> | <span data-ttu-id="4a97b-222">[Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para Olá VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="4a97b-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="4a97b-223">vmSize</span></span> | [<span data-ttu-id="4a97b-224">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-224">VM size</span></span>](sizes.md)
<span data-ttu-id="4a97b-225">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="4a97b-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="4a97b-226">Endereço IPv4 local da saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="4a97b-227">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="4a97b-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="4a97b-228">Endereço IPv4 público da saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="4a97b-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="4a97b-229">subnet/address</span></span> | <span data-ttu-id="4a97b-230">Endereço de sub-rede de saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-230">Subnet address of hello VM</span></span>
<span data-ttu-id="4a97b-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="4a97b-231">subnet/prefix</span></span> | <span data-ttu-id="4a97b-232">Prefixo de sub-rede, exemplo 24</span><span class="sxs-lookup"><span data-stu-id="4a97b-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="4a97b-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="4a97b-233">ipv6/ipAddress</span></span> | <span data-ttu-id="4a97b-234">Endereço IPv6 local da saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="4a97b-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="4a97b-235">macAddress</span></span> | <span data-ttu-id="4a97b-236">Endereço mac da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4a97b-236">VM mac address</span></span> 
<span data-ttu-id="4a97b-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="4a97b-237">scheduledevents</span></span> | <span data-ttu-id="4a97b-238">No momento em Consulte de visualização pública [aventosagendados](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="4a97b-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="4a97b-239">Cenários de exemplo para uso</span><span class="sxs-lookup"><span data-stu-id="4a97b-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="4a97b-240">VM de controle em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4a97b-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="4a97b-241">Como um provedor de serviço, pode exigir o número de saudação do tootrack de VMs que executam o software ou tiver agentes que precisam tootrack exclusividade de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="4a97b-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="4a97b-242">toobe tooget capaz de uma ID exclusiva de uma VM, use Olá `vmId` campo do serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="4a97b-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="4a97b-243">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="4a97b-244">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="4a97b-245">Posicionamento de contêineres, partições de dados com base em domínio de falha/atualização</span><span class="sxs-lookup"><span data-stu-id="4a97b-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="4a97b-246">Para determinados cenários nos quais o posicionamento de réplicas diferentes é de vital importância.</span><span class="sxs-lookup"><span data-stu-id="4a97b-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="4a97b-247">Por exemplo, [posicionamento de réplica do HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou a colocação de contêiner por meio de um [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) pode exigir o hello tooknow `platformFaultDomain` e `platformUpdateDomain` Olá VM está em execução no.</span><span class="sxs-lookup"><span data-stu-id="4a97b-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="4a97b-248">Você pode consultar esses dados diretamente por meio de saudação serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="4a97b-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="4a97b-249">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="4a97b-250">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="4a97b-251">Obtendo mais informações sobre Olá VM durante o caso de suporte</span><span class="sxs-lookup"><span data-stu-id="4a97b-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="4a97b-252">Como um provedor de serviço, você pode obter uma chamada de suporte em que você deseja tooknow mais informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4a97b-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="4a97b-253">Solicitando Olá cliente tooshare Olá computação metadados podem fornecer informações básicas para tooknow profissional de suporte de saudação sobre o tipo de saudação do VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="4a97b-254">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="4a97b-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="4a97b-255">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="4a97b-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="4a97b-256">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="4a97b-256">hello response is a JSON string.</span></span> <span data-ttu-id="4a97b-257">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="4a97b-257">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="4a97b-258">Exemplos de como chamar o serviço de metadados usando linguagens diferentes dentro de saudação VM</span><span class="sxs-lookup"><span data-stu-id="4a97b-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="4a97b-259">idioma</span><span class="sxs-lookup"><span data-stu-id="4a97b-259">Language</span></span> | <span data-ttu-id="4a97b-260">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4a97b-260">Example</span></span> 
---------|----------------
<span data-ttu-id="4a97b-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="4a97b-261">Ruby</span></span>     | <span data-ttu-id="4a97b-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="4a97b-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="4a97b-263">Vá Lan</span><span class="sxs-lookup"><span data-stu-id="4a97b-263">Go Lan</span></span>   | <span data-ttu-id="4a97b-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="4a97b-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="4a97b-265">python</span><span class="sxs-lookup"><span data-stu-id="4a97b-265">python</span></span>   | <span data-ttu-id="4a97b-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="4a97b-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="4a97b-267">C++</span><span class="sxs-lookup"><span data-stu-id="4a97b-267">C++</span></span>      | <span data-ttu-id="4a97b-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="4a97b-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="4a97b-269">C#</span><span class="sxs-lookup"><span data-stu-id="4a97b-269">C#</span></span>       | <span data-ttu-id="4a97b-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="4a97b-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="4a97b-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4a97b-271">Javascript</span></span> | <span data-ttu-id="4a97b-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="4a97b-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="4a97b-273">Powershell</span><span class="sxs-lookup"><span data-stu-id="4a97b-273">Powershell</span></span> | <span data-ttu-id="4a97b-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="4a97b-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="4a97b-275">Bash</span><span class="sxs-lookup"><span data-stu-id="4a97b-275">Bash</span></span>       | <span data-ttu-id="4a97b-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="4a97b-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="4a97b-277">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4a97b-277">FAQ</span></span>
1. <span data-ttu-id="4a97b-278">Estou recebendo o erro de saudação `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="4a97b-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="4a97b-279">O que isso significa?</span><span class="sxs-lookup"><span data-stu-id="4a97b-279">What does this mean?</span></span>
   * <span data-ttu-id="4a97b-280">Olá instância metadados de serviço requer cabeçalho Olá `Metadata: true` toobe passado na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a97b-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="4a97b-281">Passar esse cabeçalho na chamada REST Olá permite acesso toohello serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="4a97b-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="4a97b-282">Por que não estou obtendo informações de computação para minha máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="4a97b-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="4a97b-283">Atualmente Olá instância metadados de serviço suporta apenas instâncias criadas com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="4a97b-284">Olá futuras, podemos pode adicionar suporte para VMs de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4a97b-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="4a97b-285">Criei minha máquina virtual com o Azure Resource Manager há algum tempo.</span><span class="sxs-lookup"><span data-stu-id="4a97b-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="4a97b-286">Por que não consigo ver as informações de metadados de computação?</span><span class="sxs-lookup"><span data-stu-id="4a97b-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="4a97b-287">Para todas as máquinas virtuais criadas depois de setembro de 2016, adicione um [marca](../../azure-resource-manager/resource-group-using-tags.md) toostart ver metadados de computação.</span><span class="sxs-lookup"><span data-stu-id="4a97b-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="4a97b-288">Para VMs mais antigas (criadas antes de setembro de 2016), adicionar ou remover extensões ou dados discos toohello VM toorefresh metadados.</span><span class="sxs-lookup"><span data-stu-id="4a97b-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="4a97b-289">Por que estou recebendo o erro de saudação `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="4a97b-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="4a97b-290">Repita a solicitação com base no sistema de retirada exponencial.</span><span class="sxs-lookup"><span data-stu-id="4a97b-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="4a97b-291">Se o problema de saudação persistir, contate o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a97b-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="4a97b-292">Onde posso publicar comentários/perguntas adicionais?</span><span class="sxs-lookup"><span data-stu-id="4a97b-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="4a97b-293">Envie seus comentários em http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="4a97b-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="4a97b-294">Isso funcionaria para Instância do Conjunto de Dimensionamento da Máquina Virtual?</span><span class="sxs-lookup"><span data-stu-id="4a97b-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="4a97b-295">Sim, o serviço de metadados está disponível para instâncias de conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="4a97b-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="4a97b-296">Como obter suporte para o serviço Olá?</span><span class="sxs-lookup"><span data-stu-id="4a97b-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="4a97b-297">suporte tooget para serviço hello, criar um problema de suporte no portal do Azure para Olá VM em que não é capaz de tooget metadados resposta após várias tentativas longo</span><span class="sxs-lookup"><span data-stu-id="4a97b-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Serviço de Metadados de Instância](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="4a97b-299">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a97b-299">Next steps</span></span>

- <span data-ttu-id="4a97b-300">Saiba mais sobre Olá [eventos agendados](scheduled-events.md) API **em visualização pública** fornecida pelo Olá metadados da instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="4a97b-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
