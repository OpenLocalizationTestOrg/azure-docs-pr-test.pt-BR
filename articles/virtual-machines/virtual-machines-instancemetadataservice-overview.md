---
title: "Visão geral do serviço de metadados de instância de aaaAzure | Microsoft Docs"
description: "Interface rESTful tooget obter informações sobre computação, rede e eventos de manutenção futura da VM."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="73f5a-103">Serviço de metadados de instância do Azure</span><span class="sxs-lookup"><span data-stu-id="73f5a-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="73f5a-104">saudação de serviço de metadados de instância do Azure fornece informações sobre instâncias de máquina virtual que podem ser usado toomanage e configurar as máquinas virtuais em execução.</span><span class="sxs-lookup"><span data-stu-id="73f5a-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="73f5a-105">Isso inclui informações como SKU, configuração de rede e eventos de manutenção futura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="73f5a-106">Para obter mais informações sobre o tipo de informação que está disponível, consulte [categorias de metadados](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="73f5a-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="73f5a-107">Serviço de metadados de instância do Azure é um ponto de extremidade REST tooall acessível IaaS VMs criada por meio do hello [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="73f5a-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="73f5a-108">ponto de extremidade Hello está disponível em um endereço IP não roteável conhecido (`169.254.169.254`) que podem ser acessados somente de dentro de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="73f5a-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="73f5a-109">Informações importantes</span><span class="sxs-lookup"><span data-stu-id="73f5a-109">Important information</span></span>

<span data-ttu-id="73f5a-110">Esse serviço é **disponível geralmente** em regiões do Azure globais.</span><span class="sxs-lookup"><span data-stu-id="73f5a-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="73f5a-111">Ele está em visualização pública para o governo, China e em nuvem alemã do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="73f5a-112">Regularmente, ele recebe atualizações tooexpose novas informações sobre instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="73f5a-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="73f5a-113">Esta página reflete Olá atualizada [categorias de dados](#instance-metadata-data-categories) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="73f5a-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="73f5a-114">Disponibilidade do serviço</span><span class="sxs-lookup"><span data-stu-id="73f5a-114">Service Availability</span></span>
<span data-ttu-id="73f5a-115">serviço de saudação está disponível em todas as regiões do Azure Global disponíveis.</span><span class="sxs-lookup"><span data-stu-id="73f5a-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="73f5a-116">serviço de saudação está em visualização pública no hello governamentais, China, Alemanha regiões.</span><span class="sxs-lookup"><span data-stu-id="73f5a-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="73f5a-117">Regiões</span><span class="sxs-lookup"><span data-stu-id="73f5a-117">Regions</span></span>                                        | <span data-ttu-id="73f5a-118">Disponibilidade?</span><span class="sxs-lookup"><span data-stu-id="73f5a-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="73f5a-119">Todas as regiões globais do Azure disponíveis</span><span class="sxs-lookup"><span data-stu-id="73f5a-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="73f5a-120">Disponível</span><span class="sxs-lookup"><span data-stu-id="73f5a-120">Generally Available</span></span> 
[<span data-ttu-id="73f5a-121">Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="73f5a-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="73f5a-122">Na visualização</span><span class="sxs-lookup"><span data-stu-id="73f5a-122">In Preview</span></span> 
[<span data-ttu-id="73f5a-123">Azure China:</span><span class="sxs-lookup"><span data-stu-id="73f5a-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="73f5a-124">Na visualização</span><span class="sxs-lookup"><span data-stu-id="73f5a-124">In Preview</span></span>
[<span data-ttu-id="73f5a-125">Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="73f5a-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="73f5a-126">Na visualização</span><span class="sxs-lookup"><span data-stu-id="73f5a-126">In Preview</span></span>

<span data-ttu-id="73f5a-127">Esta tabela é atualizada quando o serviço Olá torna-se disponível em outras nuvens do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="73f5a-128">tootry out Olá instância metadados de serviço, criar uma VM do [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou hello [portal do Azure](http://portal.azure.com) em Olá acima regiões e siga Olá exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="73f5a-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="73f5a-129">Uso</span><span class="sxs-lookup"><span data-stu-id="73f5a-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="73f5a-130">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="73f5a-130">Versioning</span></span>
<span data-ttu-id="73f5a-131">Olá serviço de metadados de instância é com controle de versão.</span><span class="sxs-lookup"><span data-stu-id="73f5a-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="73f5a-132">As versões são obrigatórias e Olá a versão atual é `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="73f5a-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-133">Versões anteriores de visualização de eventos agendados suportados {mais recente} como Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="73f5a-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="73f5a-134">Esse formato não é mais suportado e será substituído em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="73f5a-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="73f5a-135">Como adicionamos versões mais recentes, as versões mais antigas ainda podem ser acessadas para fins de compatibilidade se os scripts tiverem dependências de formatos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="73f5a-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="73f5a-136">No entanto, observe que version(2017-03-01) de visualização atual Olá pode não estar disponível quando o serviço de saudação estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="73f5a-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="73f5a-137">Usando cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="73f5a-137">Using Headers</span></span>
<span data-ttu-id="73f5a-138">Quando você consulta Olá instância metadados de serviço, você deve fornecer o cabeçalho Olá `Metadata: true` solicitação de saudação tooensure não foi redirecionada acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="73f5a-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="73f5a-139">Configurando e recuperando os metadados</span><span class="sxs-lookup"><span data-stu-id="73f5a-139">Retrieving metadata</span></span>

<span data-ttu-id="73f5a-140">Os metadados de instância estão disponíveis para a execução de máquinas virtuais criadas/gerenciadas usando o [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="73f5a-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="73f5a-141">Acesse todas as categorias de dados para uma instância de máquina virtual usando Olá solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="73f5a-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="73f5a-142">Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="73f5a-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="73f5a-143">Saída de dados</span><span class="sxs-lookup"><span data-stu-id="73f5a-143">Data output</span></span>
<span data-ttu-id="73f5a-144">Por padrão, Olá instância metadados de serviço retorna dados em formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="73f5a-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="73f5a-145">No entanto, diferentes APIs podem retornar dados em formatos diferentes, se solicitado.</span><span class="sxs-lookup"><span data-stu-id="73f5a-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="73f5a-146">Olá tabela a seguir é uma referência de outros formatos de dados que pode oferecer suporte a APIs.</span><span class="sxs-lookup"><span data-stu-id="73f5a-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="73f5a-147">API</span><span class="sxs-lookup"><span data-stu-id="73f5a-147">API</span></span> | <span data-ttu-id="73f5a-148">Formato de dados padrão</span><span class="sxs-lookup"><span data-stu-id="73f5a-148">Default Data Format</span></span> | <span data-ttu-id="73f5a-149">Outros formatos</span><span class="sxs-lookup"><span data-stu-id="73f5a-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="73f5a-150">/instance</span><span class="sxs-lookup"><span data-stu-id="73f5a-150">/instance</span></span> | <span data-ttu-id="73f5a-151">json</span><span class="sxs-lookup"><span data-stu-id="73f5a-151">json</span></span> | <span data-ttu-id="73f5a-152">texto</span><span class="sxs-lookup"><span data-stu-id="73f5a-152">text</span></span>
<span data-ttu-id="73f5a-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="73f5a-153">/scheduledevents</span></span> | <span data-ttu-id="73f5a-154">json</span><span class="sxs-lookup"><span data-stu-id="73f5a-154">json</span></span> | <span data-ttu-id="73f5a-155">nenhum</span><span class="sxs-lookup"><span data-stu-id="73f5a-155">none</span></span>

<span data-ttu-id="73f5a-156">tooaccess um formato de resposta não padrão, especificar o formato solicitado hello como um parâmetro de querystring na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="73f5a-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="73f5a-157">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73f5a-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="73f5a-158">Segurança</span><span class="sxs-lookup"><span data-stu-id="73f5a-158">Security</span></span>
<span data-ttu-id="73f5a-159">ponto de extremidade de serviço de metadados de instância de saudação é acessível somente dentro Olá executando a instância de máquina virtual em um endereço IP não roteável.</span><span class="sxs-lookup"><span data-stu-id="73f5a-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="73f5a-160">Além disso, qualquer solicitação com um `X-Forwarded-For` cabeçalho é rejeitado pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="73f5a-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="73f5a-161">Também precisamos solicitações toocontain um `Metadata: true` tooensure de cabeçalho que Olá solicitação real diretamente foi pretendido e não faz parte do redirecionamento não intencional.</span><span class="sxs-lookup"><span data-stu-id="73f5a-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="73f5a-162">Erro</span><span class="sxs-lookup"><span data-stu-id="73f5a-162">Error</span></span>
<span data-ttu-id="73f5a-163">Se houver um elemento de dados não encontrado ou uma solicitação incorreta, Olá instância metadados de serviço retorna erros HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="73f5a-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="73f5a-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73f5a-164">For example:</span></span>

<span data-ttu-id="73f5a-165">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="73f5a-165">HTTP Status Code</span></span> | <span data-ttu-id="73f5a-166">Motivo</span><span class="sxs-lookup"><span data-stu-id="73f5a-166">Reason</span></span>
----------------|-------
<span data-ttu-id="73f5a-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="73f5a-167">200 OK</span></span> |
<span data-ttu-id="73f5a-168">400 Solicitação Inválida</span><span class="sxs-lookup"><span data-stu-id="73f5a-168">400 Bad Request</span></span> | <span data-ttu-id="73f5a-169">Faltando `Metadata: true` cabeçalho</span><span class="sxs-lookup"><span data-stu-id="73f5a-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="73f5a-170">404 Não Encontrado</span><span class="sxs-lookup"><span data-stu-id="73f5a-170">404 Not Found</span></span> | <span data-ttu-id="73f5a-171">Olá does't elemento solicitado existe</span><span class="sxs-lookup"><span data-stu-id="73f5a-171">hello requested element does't exist</span></span> 
<span data-ttu-id="73f5a-172">405 método não permitido</span><span class="sxs-lookup"><span data-stu-id="73f5a-172">405 Method Not Allowed</span></span> | <span data-ttu-id="73f5a-173">Somente as solicitações `GET` e `POST` são suportadas</span><span class="sxs-lookup"><span data-stu-id="73f5a-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="73f5a-174">429 Número excessivo de solicitações</span><span class="sxs-lookup"><span data-stu-id="73f5a-174">429 Too Many Requests</span></span> | <span data-ttu-id="73f5a-175">Olá API atualmente suporta um máximo de 5 consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="73f5a-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="73f5a-176">500 Erro do serviço</span><span class="sxs-lookup"><span data-stu-id="73f5a-176">500 Service Error</span></span>     | <span data-ttu-id="73f5a-177">Aguarde um pouco e tente novamente</span><span class="sxs-lookup"><span data-stu-id="73f5a-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="73f5a-178">Exemplos</span><span class="sxs-lookup"><span data-stu-id="73f5a-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-179">Todas as respostas de API são cadeias de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73f5a-179">All API responses are JSON strings.</span></span> <span data-ttu-id="73f5a-180">Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="73f5a-181">Recuperação das informações de rede</span><span class="sxs-lookup"><span data-stu-id="73f5a-181">Retrieving network information</span></span>

<span data-ttu-id="73f5a-182">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="73f5a-183">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-184">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73f5a-184">hello response is a JSON string.</span></span> <span data-ttu-id="73f5a-185">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-185">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="73f5a-186">Recuperação do endereço IP público</span><span class="sxs-lookup"><span data-stu-id="73f5a-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="73f5a-187">Recuperação de todos os metadados para uma instância</span><span class="sxs-lookup"><span data-stu-id="73f5a-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="73f5a-188">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="73f5a-189">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-190">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73f5a-190">hello response is a JSON string.</span></span> <span data-ttu-id="73f5a-191">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-191">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="73f5a-192">Recuperação de metadados na máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="73f5a-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="73f5a-193">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-193">**Request**</span></span>

<span data-ttu-id="73f5a-194">Metadados de instância podem ser recuperados no Windows por meio de saudação do PowerShell utilitário `curl`:</span><span class="sxs-lookup"><span data-stu-id="73f5a-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="73f5a-195">Ou por meio de saudação `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="73f5a-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="73f5a-196">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-197">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73f5a-197">hello response is a JSON string.</span></span> <span data-ttu-id="73f5a-198">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-198">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="73f5a-199">Categorias de dados de metadados de instância</span><span class="sxs-lookup"><span data-stu-id="73f5a-199">Instance metadata data categories</span></span>
<span data-ttu-id="73f5a-200">Olá categorias de dados a seguir está disponível por meio de saudação instância metadados de serviço:</span><span class="sxs-lookup"><span data-stu-id="73f5a-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="73f5a-201">Dados</span><span class="sxs-lookup"><span data-stu-id="73f5a-201">Data</span></span> | <span data-ttu-id="73f5a-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="73f5a-202">Description</span></span>
-----|------------
<span data-ttu-id="73f5a-203">location</span><span class="sxs-lookup"><span data-stu-id="73f5a-203">location</span></span> | <span data-ttu-id="73f5a-204">Saudação de região do Azure VM está em execução</span><span class="sxs-lookup"><span data-stu-id="73f5a-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="73f5a-205">name</span><span class="sxs-lookup"><span data-stu-id="73f5a-205">name</span></span> | <span data-ttu-id="73f5a-206">Nome da saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-206">Name of hello VM</span></span> 
<span data-ttu-id="73f5a-207">oferta</span><span class="sxs-lookup"><span data-stu-id="73f5a-207">offer</span></span> | <span data-ttu-id="73f5a-208">Oferece informações para a imagem VM hello.</span><span class="sxs-lookup"><span data-stu-id="73f5a-208">Offer information for hello VM image.</span></span> <span data-ttu-id="73f5a-209">Esse valor só está presente para as imagens implantadas na Galeria de imagens do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="73f5a-210">publicador</span><span class="sxs-lookup"><span data-stu-id="73f5a-210">publisher</span></span> | <span data-ttu-id="73f5a-211">Editor de imagem de VM Olá</span><span class="sxs-lookup"><span data-stu-id="73f5a-211">Publisher of hello VM image</span></span>
<span data-ttu-id="73f5a-212">sku</span><span class="sxs-lookup"><span data-stu-id="73f5a-212">sku</span></span> | <span data-ttu-id="73f5a-213">SKU específica para a imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="73f5a-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="73f5a-214">version</span><span class="sxs-lookup"><span data-stu-id="73f5a-214">version</span></span> | <span data-ttu-id="73f5a-215">Versão da imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="73f5a-215">Version of hello VM image</span></span> 
<span data-ttu-id="73f5a-216">osType</span><span class="sxs-lookup"><span data-stu-id="73f5a-216">osType</span></span> | <span data-ttu-id="73f5a-217">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73f5a-217">Linux or Windows</span></span> 
<span data-ttu-id="73f5a-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="73f5a-218">platformUpdateDomain</span></span> |  <span data-ttu-id="73f5a-219">[Domínio de atualização](virtual-machines-windows-manage-availability.md) Olá VM está em execução em</span><span class="sxs-lookup"><span data-stu-id="73f5a-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="73f5a-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="73f5a-220">platformFaultDomain</span></span> | <span data-ttu-id="73f5a-221">[Domínio de falha](virtual-machines-windows-manage-availability.md) Olá VM está em execução em</span><span class="sxs-lookup"><span data-stu-id="73f5a-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="73f5a-222">vmId</span><span class="sxs-lookup"><span data-stu-id="73f5a-222">vmId</span></span> | <span data-ttu-id="73f5a-223">[Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para Olá VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="73f5a-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="73f5a-224">vmSize</span></span> | [<span data-ttu-id="73f5a-225">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="73f5a-226">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="73f5a-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="73f5a-227">Endereço IPv4 local da saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="73f5a-228">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="73f5a-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="73f5a-229">Endereço IPv4 público da saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="73f5a-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="73f5a-230">subnet/address</span></span> | <span data-ttu-id="73f5a-231">Endereço de sub-rede de saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-231">Subnet address of hello VM</span></span>
<span data-ttu-id="73f5a-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="73f5a-232">subnet/prefix</span></span> | <span data-ttu-id="73f5a-233">Prefixo de sub-rede, exemplo 24</span><span class="sxs-lookup"><span data-stu-id="73f5a-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="73f5a-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="73f5a-234">ipv6/ipAddress</span></span> | <span data-ttu-id="73f5a-235">Endereço IPv6 local da saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="73f5a-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="73f5a-236">macAddress</span></span> | <span data-ttu-id="73f5a-237">Endereço mac da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="73f5a-237">VM mac address</span></span> 
<span data-ttu-id="73f5a-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="73f5a-238">scheduledevents</span></span> | <span data-ttu-id="73f5a-239">No momento em Consulte de visualização pública [aventosagendados](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="73f5a-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="73f5a-240">Cenários de exemplo para uso</span><span class="sxs-lookup"><span data-stu-id="73f5a-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="73f5a-241">VM de controle em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="73f5a-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="73f5a-242">Como um provedor de serviço, pode exigir o número de saudação do tootrack de VMs que executam o software ou tiver agentes que precisam tootrack exclusividade de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="73f5a-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="73f5a-243">toobe tooget capaz de uma ID exclusiva de uma VM, use Olá `vmId` campo do serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="73f5a-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="73f5a-244">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="73f5a-245">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="73f5a-246">Posicionamento de contêineres, partições de dados com base em domínio de falha/atualização</span><span class="sxs-lookup"><span data-stu-id="73f5a-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="73f5a-247">Para determinados cenários nos quais o posicionamento de réplicas diferentes é de vital importância.</span><span class="sxs-lookup"><span data-stu-id="73f5a-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="73f5a-248">Por exemplo, [posicionamento de réplica do HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou a colocação de contêiner por meio de um [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) pode exigir o hello tooknow `platformFaultDomain` e `platformUpdateDomain` Olá VM está em execução no.</span><span class="sxs-lookup"><span data-stu-id="73f5a-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="73f5a-249">Você pode consultar esses dados diretamente por meio de saudação serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="73f5a-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="73f5a-250">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="73f5a-251">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="73f5a-252">Obtendo mais informações sobre Olá VM durante o caso de suporte</span><span class="sxs-lookup"><span data-stu-id="73f5a-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="73f5a-253">Como um provedor de serviço, você pode obter uma chamada de suporte em que você deseja tooknow mais informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="73f5a-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="73f5a-254">Solicitando Olá cliente tooshare Olá computação metadados podem fornecer informações básicas para tooknow profissional de suporte de saudação sobre o tipo de saudação do VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="73f5a-255">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="73f5a-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="73f5a-256">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="73f5a-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="73f5a-257">resposta de saudação é uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="73f5a-257">hello response is a JSON string.</span></span> <span data-ttu-id="73f5a-258">saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="73f5a-258">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="73f5a-259">Exemplos de como chamar o serviço de metadados usando linguagens diferentes dentro de saudação VM</span><span class="sxs-lookup"><span data-stu-id="73f5a-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="73f5a-260">idioma</span><span class="sxs-lookup"><span data-stu-id="73f5a-260">Language</span></span> | <span data-ttu-id="73f5a-261">Exemplo</span><span class="sxs-lookup"><span data-stu-id="73f5a-261">Example</span></span> 
---------|----------------
<span data-ttu-id="73f5a-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="73f5a-262">Ruby</span></span>     | <span data-ttu-id="73f5a-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="73f5a-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="73f5a-264">Vá Lan</span><span class="sxs-lookup"><span data-stu-id="73f5a-264">Go Lan</span></span>   | <span data-ttu-id="73f5a-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="73f5a-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="73f5a-266">python</span><span class="sxs-lookup"><span data-stu-id="73f5a-266">python</span></span>   | <span data-ttu-id="73f5a-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="73f5a-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="73f5a-268">C++</span><span class="sxs-lookup"><span data-stu-id="73f5a-268">C++</span></span>      | <span data-ttu-id="73f5a-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="73f5a-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="73f5a-270">C#</span><span class="sxs-lookup"><span data-stu-id="73f5a-270">C#</span></span>       | <span data-ttu-id="73f5a-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="73f5a-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="73f5a-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="73f5a-272">Javascript</span></span> | <span data-ttu-id="73f5a-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="73f5a-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="73f5a-274">Powershell</span><span class="sxs-lookup"><span data-stu-id="73f5a-274">Powershell</span></span> | <span data-ttu-id="73f5a-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="73f5a-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="73f5a-276">Bash</span><span class="sxs-lookup"><span data-stu-id="73f5a-276">Bash</span></span>       | <span data-ttu-id="73f5a-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="73f5a-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="73f5a-278">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="73f5a-278">FAQ</span></span>
1. <span data-ttu-id="73f5a-279">Estou recebendo o erro de saudação `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="73f5a-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="73f5a-280">O que isso significa?</span><span class="sxs-lookup"><span data-stu-id="73f5a-280">What does this mean?</span></span>
   * <span data-ttu-id="73f5a-281">Olá instância metadados de serviço requer cabeçalho Olá `Metadata: true` toobe passado na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="73f5a-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="73f5a-282">Passar esse cabeçalho na chamada REST Olá permite acesso toohello serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="73f5a-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="73f5a-283">Por que não estou obtendo informações de computação para minha máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="73f5a-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="73f5a-284">Atualmente Olá instância metadados de serviço suporta apenas instâncias criadas com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="73f5a-285">Olá futuras, podemos pode adicionar suporte para VMs de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="73f5a-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="73f5a-286">Criei minha máquina virtual com o Azure Resource Manager há algum tempo.</span><span class="sxs-lookup"><span data-stu-id="73f5a-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="73f5a-287">Por que não consigo ver as informações de metadados de computação?</span><span class="sxs-lookup"><span data-stu-id="73f5a-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="73f5a-288">Para todas as máquinas virtuais criadas depois de setembro de 2016, adicione um [marca](../azure-resource-manager/resource-group-using-tags.md) toostart ver metadados de computação.</span><span class="sxs-lookup"><span data-stu-id="73f5a-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="73f5a-289">Para VMs mais antigas (criadas antes de setembro de 2016), adicionar ou remover extensões ou dados discos toohello VM toorefresh metadados.</span><span class="sxs-lookup"><span data-stu-id="73f5a-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="73f5a-290">Por que estou recebendo o erro de saudação `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="73f5a-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="73f5a-291">Repita a solicitação com base no sistema de retirada exponencial.</span><span class="sxs-lookup"><span data-stu-id="73f5a-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="73f5a-292">Se o problema de saudação persistir, contate o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="73f5a-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="73f5a-293">Onde posso publicar comentários/perguntas adicionais?</span><span class="sxs-lookup"><span data-stu-id="73f5a-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="73f5a-294">Envie seus comentários em http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="73f5a-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="73f5a-295">Isso funcionaria para Instância do Conjunto de Dimensionamento da Máquina Virtual?</span><span class="sxs-lookup"><span data-stu-id="73f5a-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="73f5a-296">Sim, o serviço de metadados está disponível para instâncias de conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="73f5a-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="73f5a-297">Como obter suporte para o serviço Olá?</span><span class="sxs-lookup"><span data-stu-id="73f5a-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="73f5a-298">suporte tooget para serviço hello, criar um problema de suporte no portal do Azure para Olá VM em que não é capaz de tooget metadados resposta após várias tentativas longo</span><span class="sxs-lookup"><span data-stu-id="73f5a-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Serviço de Metadados de Instância](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="73f5a-300">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73f5a-300">Next Steps</span></span>

- <span data-ttu-id="73f5a-301">Saiba mais sobre Olá [scheduledevents](virtual-machines-scheduled-events.md) API **na visualização pública** fornecida pelo Olá serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="73f5a-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
