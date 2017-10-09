---
title: aaaUsing PowerShell toomanage Traffic Manager no Azure | Microsoft Docs
description: "Usando o PowerShell para o Gerenciador de Tráfego com o Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="74f03-103">Usando o PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="74f03-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="74f03-104">Gerenciador de recursos do Azure é a interface de gerenciamento preferencial de saudação para serviços no Azure.</span><span class="sxs-lookup"><span data-stu-id="74f03-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="74f03-105">Os perfis do Gerenciador de Tráfego do Azure podem ser gerenciados usando ferramentas e APIs baseadas no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74f03-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="74f03-106">Modelo de recursos</span><span class="sxs-lookup"><span data-stu-id="74f03-106">Resource model</span></span>

<span data-ttu-id="74f03-107">O Gerenciador de Tráfego do Azure é configurado usando um conjunto de configurações chamado de perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="74f03-108">Este perfil contém as configurações de DNS, configurações de roteamento de tráfego, configurações de monitoramento do ponto de extremidade e uma lista de tráfego de toowhich de pontos de extremidade do serviço é roteada.</span><span class="sxs-lookup"><span data-stu-id="74f03-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="74f03-109">Cada perfil do Gerenciador de Tráfego é representado por um recurso do tipo "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="74f03-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="74f03-110">Em Olá nível da API REST, Olá URI para cada perfil é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="74f03-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="74f03-111">Configurando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="74f03-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="74f03-112">Essas instruções usam o Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74f03-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="74f03-113">Olá seguinte artigo explica como tooinstall e configurar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74f03-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="74f03-114">Como tooinstall e configurar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f03-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="74f03-115">exemplos de saudação neste artigo presumem que você tenha um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="74f03-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="74f03-116">Você pode criar um grupo de recursos usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="74f03-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="74f03-117">O Azure Resource Manager requer que todos os grupos de recursos tenham um local.</span><span class="sxs-lookup"><span data-stu-id="74f03-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="74f03-118">Esse local é usado como saudação padrão para recursos criados nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74f03-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="74f03-119">No entanto, como os recursos de perfil do Traffic Manager são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto sobre o Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="74f03-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="74f03-120">Criar um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="74f03-121">toocreate um perfil do Gerenciador de tráfego, use Olá `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="74f03-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="74f03-122">Olá, a tabela a seguir descreve os parâmetros de saudação:</span><span class="sxs-lookup"><span data-stu-id="74f03-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="74f03-123">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="74f03-123">Parameter</span></span> | <span data-ttu-id="74f03-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="74f03-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74f03-125">Nome</span><span class="sxs-lookup"><span data-stu-id="74f03-125">Name</span></span> |<span data-ttu-id="74f03-126">nome de recurso de saudação de saudação recurso de perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="74f03-127">Perfis do hello mesmo grupo de recursos deve ter nomes exclusivos.</span><span class="sxs-lookup"><span data-stu-id="74f03-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="74f03-128">Esse nome é separado do nome DNS Olá usado para consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="74f03-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="74f03-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="74f03-129">ResourceGroupName</span></span> |<span data-ttu-id="74f03-130">nome de Olá do recurso de perfil do hello recurso grupo contentor hello.</span><span class="sxs-lookup"><span data-stu-id="74f03-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="74f03-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="74f03-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="74f03-132">Especifica o roteamento de tráfego da saudação método usado toodetermine qual ponto de extremidade é retornado na resposta de uma consulta DNS.</span><span class="sxs-lookup"><span data-stu-id="74f03-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="74f03-133">Os valores possíveis são “Desempenho”, “Ponderado” ou “Prioridade”.</span><span class="sxs-lookup"><span data-stu-id="74f03-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="74f03-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="74f03-134">RelativeDnsName</span></span> |<span data-ttu-id="74f03-135">Especifica a porção hostname de Olá Olá do nome de DNS fornecido por esse perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="74f03-136">Esse valor é combinado com o nome de domínio DNS Olá usado pelo Gerenciador de tráfego do Azure tooform Olá nome totalmente qualificado (FQDN) do perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="74f03-137">Por exemplo, definir o valor Olá 'contoso' torna-se 'contoso.trafficmanager.net'.</span><span class="sxs-lookup"><span data-stu-id="74f03-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="74f03-138">TTL</span><span class="sxs-lookup"><span data-stu-id="74f03-138">TTL</span></span> |<span data-ttu-id="74f03-139">Especifica a saudação DNS Time-to-Live (TTL), em segundos.</span><span class="sxs-lookup"><span data-stu-id="74f03-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="74f03-140">Este TTL informa os resolvedores de DNS Local hello e os clientes DNS quanto tempo toocache respostas DNS a esse perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="74f03-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="74f03-141">MonitorProtocol</span></span> |<span data-ttu-id="74f03-142">Especifica a integridade do ponto de extremidade do hello protocolo toouse toomonitor.</span><span class="sxs-lookup"><span data-stu-id="74f03-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="74f03-143">Os valores possíveis são “HTTP” e “HTTPS”.</span><span class="sxs-lookup"><span data-stu-id="74f03-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="74f03-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="74f03-144">MonitorPort</span></span> |<span data-ttu-id="74f03-145">Especifica a saudação a porta TCP usada toomonitor integridade do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="74f03-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="74f03-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="74f03-146">MonitorPath</span></span> |<span data-ttu-id="74f03-147">Especifica o nome de domínio de ponto de extremidade do hello caminho relativo toohello usado tooprobe para integridade do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="74f03-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="74f03-148">Olá cmdlet cria um perfil do Traffic Manager no Azure e retorna um tooPowerShell de objeto correspondente do perfil.</span><span class="sxs-lookup"><span data-stu-id="74f03-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="74f03-149">Neste ponto, o perfil de saudação não contém nenhum ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="74f03-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="74f03-150">Para obter mais informações sobre como adicionar o perfil do Gerenciador de tráfego de tooa de pontos de extremidade, consulte [adicionar pontos de extremidade do Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="74f03-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="74f03-151">Obter um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="74f03-152">tooretrieve um objeto de perfil do Gerenciador de tráfego existente, use Olá `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="74f03-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="74f03-153">Esse cmdlet retorna um objeto de perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="74f03-154">Atualizar um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="74f03-155">A modificação de perfis do Gerenciador de Tráfego segue um processo de 3 etapas:</span><span class="sxs-lookup"><span data-stu-id="74f03-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="74f03-156">Recuperar Olá perfil usando `Get-AzureRmTrafficManagerProfile` ou usar perfil Olá retornado por `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="74f03-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="74f03-157">Modificar o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-157">Modify hello profile.</span></span> <span data-ttu-id="74f03-158">Você pode adicionar e remover pontos de extremidade ou alterar ponto de extremidade ou parâmetros do perfil.</span><span class="sxs-lookup"><span data-stu-id="74f03-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="74f03-159">Essas alterações são operações offline.</span><span class="sxs-lookup"><span data-stu-id="74f03-159">These changes are off-line operations.</span></span> <span data-ttu-id="74f03-160">Somente você está alterando o objeto de saudação local na memória que representa o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="74f03-161">Confirmar as alterações usando Olá `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74f03-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="74f03-162">Todas as propriedades de perfil podem ser alteradas com exceção RelativeDnsName do perfil Olá.</span><span class="sxs-lookup"><span data-stu-id="74f03-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="74f03-163">toochange Olá RelativeDnsName, você deve excluir o perfil e um novo perfil com um novo nome.</span><span class="sxs-lookup"><span data-stu-id="74f03-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="74f03-164">saudação de exemplo a seguir demonstra como toochange Olá TTL do perfil:</span><span class="sxs-lookup"><span data-stu-id="74f03-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="74f03-165">Há três tipos de pontos de extremidade do Gerenciador de Tráfego:</span><span class="sxs-lookup"><span data-stu-id="74f03-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="74f03-166">Os **pontos de extremidade do Azure** são serviços hospedados no Azure</span><span class="sxs-lookup"><span data-stu-id="74f03-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="74f03-167">Os **pontos de extremidade externos** são serviços hospedados fora do Azure</span><span class="sxs-lookup"><span data-stu-id="74f03-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="74f03-168">**Aninhados pontos de extremidade** são hierarquias usadas tooconstruct aninhado de perfis de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="74f03-169">Os pontos de extremidade aninhados habilitam configurações avançadas de roteamento de tráfego para aplicativos complexos.</span><span class="sxs-lookup"><span data-stu-id="74f03-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="74f03-170">Em todos os três casos, os pontos de extremidade podem ser adicionados de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="74f03-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="74f03-171">Usando um processo de 3 etapas descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74f03-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="74f03-172">vantagem Olá desse método é que várias alterações de ponto de extremidade podem ser feitas em uma única atualização.</span><span class="sxs-lookup"><span data-stu-id="74f03-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="74f03-173">Usando Olá AzureRmTrafficManagerEndpoint novo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74f03-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="74f03-174">Esse cmdlet adiciona um perfil de Gerenciador de tráfego existente do ponto de extremidade tooan em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="74f03-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="74f03-175">Adicionando pontos de extremidade do Azure</span><span class="sxs-lookup"><span data-stu-id="74f03-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="74f03-176">Os pontos de extremidade do Azure fazem referência a serviços hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="74f03-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="74f03-177">Há suporte para dois tipos de pontos de extremidade do Azure:</span><span class="sxs-lookup"><span data-stu-id="74f03-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="74f03-178">Aplicativos Web do Azure </span><span class="sxs-lookup"><span data-stu-id="74f03-178">Azure Web Apps</span></span>
2. <span data-ttu-id="74f03-179">Recursos PublicIpAddress do Azure (que podem ser anexado tooa balanceador de carga ou uma NIC de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="74f03-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="74f03-180">Olá PublicIpAddress deve ter um nome DNS atribuído toobe usado no Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="74f03-181">Em cada caso:</span><span class="sxs-lookup"><span data-stu-id="74f03-181">In each case:</span></span>

* <span data-ttu-id="74f03-182">o serviço de saudação é especificado usando o parâmetro 'targetResourceId' hello `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="74f03-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="74f03-183">Olá 'Target' e 'EndpointLocation' são implicado Olá TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="74f03-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="74f03-184">A especificação de saudação 'Peso' é opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="74f03-185">Os pesos são usados somente se o perfil de saudação for método de roteamento de tráfego do toouse configurado hello 'Ponderado'.</span><span class="sxs-lookup"><span data-stu-id="74f03-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="74f03-186">Caso contrário, eles serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="74f03-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="74f03-187">Se especificado, o valor de saudação deve ser um número entre 1 e 1000.</span><span class="sxs-lookup"><span data-stu-id="74f03-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="74f03-188">valor padrão de saudação é '1'.</span><span class="sxs-lookup"><span data-stu-id="74f03-188">hello default value is '1'.</span></span>
* <span data-ttu-id="74f03-189">Olá especificando 'Priority' é opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="74f03-190">As prioridades são usadas somente se o perfil de Olá é o método de roteamento de tráfego do toouse configurado hello 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="74f03-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="74f03-191">Caso contrário, eles serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="74f03-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="74f03-192">Os valores válidos são de 1 too1000 com valores menores que indica uma prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="74f03-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="74f03-193">Se especificados para um ponto de extremidade, deverão ser especificados para todos os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="74f03-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="74f03-194">Se omitido, os valores padrão a partir de '1' são aplicados na ordem de saudação que pontos de extremidade de saudação são listados.</span><span class="sxs-lookup"><span data-stu-id="74f03-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="74f03-195">Exemplo 1: adicionar pontos de extremidade do aplicativo Web usando `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="74f03-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="74f03-196">Neste exemplo, podemos criar um perfil do Gerenciador de tráfego e adicionar dois pontos de extremidade do aplicativo Web usando Olá `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74f03-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="74f03-197">Exemplo 2: Adicionar um ponto de extremidade publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="74f03-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="74f03-198">Neste exemplo, um recurso de endereço IP público é adicionado toohello perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="74f03-199">endereço IP público de saudação deve ter um nome DNS configurado e pode ser vinculado ou toohello NIC um VM ou tooa do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="74f03-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="74f03-200">Adicionando pontos de extremidade externos</span><span class="sxs-lookup"><span data-stu-id="74f03-200">Adding External Endpoints</span></span>

<span data-ttu-id="74f03-201">Traffic Manager usa pontos de extremidade externos toodirect tráfego tooservices hospedado fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="74f03-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="74f03-202">Como com pontos de extremidade do Azure, pontos de extremidade externos podem ser adicionados usando `Add-AzureRmTrafficManagerEndpointConfig` seguido por `Set-AzureRmTrafficManagerProfile` ou `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="74f03-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="74f03-203">Ao especificar pontos de extremidade externos:</span><span class="sxs-lookup"><span data-stu-id="74f03-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="74f03-204">nome de domínio do ponto de extremidade Olá deve ser especificado usando o parâmetro de 'Target' hello</span><span class="sxs-lookup"><span data-stu-id="74f03-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="74f03-205">Se Olá método de roteamento de tráfego 'Desempenho' for usado, Olá 'EndpointLocation' é necessário.</span><span class="sxs-lookup"><span data-stu-id="74f03-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="74f03-206">Caso contrário, será opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-206">Otherwise it is optional.</span></span> <span data-ttu-id="74f03-207">Olá valor deve ser um [nome da região do Azure válida](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="74f03-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="74f03-208">Olá 'Peso' e 'Priority' é opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="74f03-209">Exemplo 1: adicionar pontos de extremidade externos usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="74f03-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="74f03-210">Neste exemplo, podemos criar um perfil do Gerenciador de tráfego, adicionar dois pontos de extremidade externos e confirmar as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="74f03-211">Exemplo 2: adicionar pontos de extremidade externos usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="74f03-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="74f03-212">Neste exemplo, vamos adicionar um perfil existente do ponto de extremidade externo tooan.</span><span class="sxs-lookup"><span data-stu-id="74f03-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="74f03-213">perfil de saudação é especificado usando os nomes de grupo de perfil e recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="74f03-214">Adicionando pontos de extremidade ‘aninhados’</span><span class="sxs-lookup"><span data-stu-id="74f03-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="74f03-215">Cada perfil do Gerenciador de Tráfego especifica um único método de roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="74f03-216">No entanto, há cenários que exigem mais sofisticadas roteamento de tráfego de roteamento Olá fornecido por um único perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="74f03-217">Você pode aninhar os benefícios de saudação do Gerenciador de tráfego perfis toocombine de mais de um método de roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="74f03-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="74f03-218">Perfis aninhados permitem que você toooverride saudação padrão do Traffic Manager comportamento toosupport maior e mais complexas implantações de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="74f03-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="74f03-219">Para obter mais exemplos, consulte [Perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="74f03-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="74f03-220">Pontos de extremidade aninhados são configurados no perfil de pai hello, usando um tipo de ponto de extremidade específico, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="74f03-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="74f03-221">Ao especificar pontos de extremidade aninhados:</span><span class="sxs-lookup"><span data-stu-id="74f03-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="74f03-222">ponto de extremidade Olá deve ser especificado usando o parâmetro de 'targetResourceId' hello</span><span class="sxs-lookup"><span data-stu-id="74f03-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="74f03-223">Se Olá método de roteamento de tráfego 'Desempenho' for usado, Olá 'EndpointLocation' é necessário.</span><span class="sxs-lookup"><span data-stu-id="74f03-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="74f03-224">Caso contrário, será opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-224">Otherwise it is optional.</span></span> <span data-ttu-id="74f03-225">Olá valor deve ser um [nome da região do Azure válida](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="74f03-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="74f03-226">Olá 'Peso' e 'Priority' é opcional, como pontos de extremidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="74f03-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="74f03-227">Olá 'MinChildEndpoints' parâmetro é opcional.</span><span class="sxs-lookup"><span data-stu-id="74f03-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="74f03-228">valor padrão de saudação é '1'.</span><span class="sxs-lookup"><span data-stu-id="74f03-228">hello default value is '1'.</span></span> <span data-ttu-id="74f03-229">Se o número de saudação de pontos de extremidade disponíveis cair abaixo desse limite, perfil pai de saudação considera o perfil filho Olá 'degradado' e desvia tráfego toohello outros pontos de extremidade no perfil do hello pai.</span><span class="sxs-lookup"><span data-stu-id="74f03-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="74f03-230">Exemplo 1: adicionar pontos de extremidade aninhados usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="74f03-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="74f03-231">Neste exemplo, podemos criar pai e filho do novo Gerenciador de tráfego perfis, Adicionar filho hello como um pai do ponto de extremidade aninhada toohello e confirmar as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="74f03-232">Para resumir, neste exemplo, não adicionamos quaisquer outros pontos de extremidade toohello filho ou pai perfis.</span><span class="sxs-lookup"><span data-stu-id="74f03-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="74f03-233">Exemplo 2: adicionar pontos de extremidade aninhados usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="74f03-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="74f03-234">Neste exemplo, adicionamos um perfil filho existente como um perfil de pai existente do ponto de extremidade aninhada tooan.</span><span class="sxs-lookup"><span data-stu-id="74f03-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="74f03-235">perfil de saudação é especificado usando os nomes de grupo de perfil e recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="74f03-236">Atualizar um Ponto de Extremidade do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="74f03-237">Há tooupdate de duas maneiras de um ponto de extremidade do Gerenciador de tráfego existente:</span><span class="sxs-lookup"><span data-stu-id="74f03-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="74f03-238">Obter o perfil do Gerenciador de tráfego de saudação usando `Get-AzureRmTrafficManagerProfile`, atualizar as propriedades de ponto de extremidade Olá no perfil de saudação e confirmar as alterações de saudação usando `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="74f03-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="74f03-239">Esse método tem a vantagem de saudação de ser capaz de tooupdate mais de um ponto de extremidade em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="74f03-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="74f03-240">Obter usando o ponto de extremidade do Traffic Manager Olá `Get-AzureRmTrafficManagerEndpoint`, atualizar as propriedades de ponto de extremidade hello e confirmar alterações hello usando `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="74f03-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="74f03-241">Esse método é mais simples, já que não exige a indexação em uma matriz de pontos de extremidade Olá no perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f03-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="74f03-242">Exemplo 1: atualizar pontos de extremidade usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="74f03-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="74f03-243">Neste exemplo, vamos modificar prioridade da saudação de dois pontos de extremidade em um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="74f03-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="74f03-244">Exemplo 2: atualizar um ponto de extremidade usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="74f03-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="74f03-245">Neste exemplo, vamos modificar peso de saudação de um ponto de extremidade em um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="74f03-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="74f03-246">Habilitando e desabilitando pontos de extremidade e perfis</span><span class="sxs-lookup"><span data-stu-id="74f03-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="74f03-247">O Traffic Manager permite toobe de pontos de extremidade individuais habilitados e desabilitados, além de permitir a habilitação e desabilitação de perfis de inteiros.</span><span class="sxs-lookup"><span data-stu-id="74f03-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="74f03-248">Essas alterações podem ser feitas pelos recursos de ponto de extremidade ou perfil Olá obtendo/Atualizar/configuração.</span><span class="sxs-lookup"><span data-stu-id="74f03-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="74f03-249">toostreamline essas operações comuns, eles também têm suporte por meio de cmdlets dedicados.</span><span class="sxs-lookup"><span data-stu-id="74f03-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="74f03-250">Exemplo 1: Habilitando e desabilitando um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="74f03-251">tooenable um perfil do Gerenciador de tráfego, use `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="74f03-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="74f03-252">perfil de saudação pode ser especificado usando um objeto de perfil.</span><span class="sxs-lookup"><span data-stu-id="74f03-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="74f03-253">Olá objeto de perfil pode ser passado por meio do pipeline de saudação ou usando Olá '-TrafficManagerProfile' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74f03-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="74f03-254">Neste exemplo, podemos especificar perfil Olá pelo nome do grupo de recursos e perfil hello.</span><span class="sxs-lookup"><span data-stu-id="74f03-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="74f03-255">toodisable um perfil do Gerenciador de tráfego:</span><span class="sxs-lookup"><span data-stu-id="74f03-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="74f03-256">Olá Disable-AzureRmTrafficManagerProfile cmdlet solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="74f03-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="74f03-257">Esse aviso pode ser suprimido Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74f03-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="74f03-258">Exemplo 2: Habilitando e desabilitando um ponto de extremidade do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="74f03-259">tooenable um ponto de extremidade do Traffic Manager, use `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="74f03-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="74f03-260">Não há ponto de extremidade Olá toospecify de duas maneiras</span><span class="sxs-lookup"><span data-stu-id="74f03-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="74f03-261">Usando um objeto TrafficManagerEndpoint passado por meio do pipeline de saudação ou Olá '-TrafficManagerEndpoint' parâmetro</span><span class="sxs-lookup"><span data-stu-id="74f03-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="74f03-262">Usando o nome do ponto de extremidade hello, tipo de ponto de extremidade, nome do perfil e nome do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="74f03-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="74f03-263">Da mesma forma, toodisable um ponto de extremidade do Gerenciador de tráfego:</span><span class="sxs-lookup"><span data-stu-id="74f03-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="74f03-264">Assim como acontece com `Disable-AzureRmTrafficManagerProfile`, Olá `Disable-AzureRmTrafficManagerEndpoint` cmdlet solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="74f03-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="74f03-265">Esse aviso pode ser suprimido Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74f03-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="74f03-266">Excluir um Ponto de Extremidade do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="74f03-267">tooremove pontos de extremidade individuais, use Olá `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="74f03-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="74f03-268">Esse cmdlet solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="74f03-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="74f03-269">Esse aviso pode ser suprimido Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74f03-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="74f03-270">Excluir um perfil do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="74f03-271">toodelete um perfil do Gerenciador de tráfego, use Olá `Remove-AzureRmTrafficManagerProfile` cmdlet, especificando nomes de grupo de recursos e perfil hello:</span><span class="sxs-lookup"><span data-stu-id="74f03-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="74f03-272">Esse cmdlet solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="74f03-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="74f03-273">Esse aviso pode ser suprimido Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74f03-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="74f03-274">Olá toobe de perfil excluída também pode ser especificada usando um objeto de perfil:</span><span class="sxs-lookup"><span data-stu-id="74f03-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="74f03-275">Essa sequência também pode ser transferida:</span><span class="sxs-lookup"><span data-stu-id="74f03-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="74f03-276">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74f03-276">Next steps</span></span>

[<span data-ttu-id="74f03-277">Monitoramento do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="74f03-278">Considerações sobre desempenho do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="74f03-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
