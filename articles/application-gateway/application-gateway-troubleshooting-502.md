---
title: erros de Gateway incorreto de Gateway de aplicativo do Azure (502) aaaTroubleshoot | Microsoft Docs
description: Saiba como erros tootroubleshoot 502 de Gateway do aplicativo
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="349e7-103">Solução de problemas de erros de gateway incorreto no Application Gateway</span><span class="sxs-lookup"><span data-stu-id="349e7-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="349e7-104">Saiba como erros (502) de gateway incorreto tootroubleshoot recebeu ao usar o gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="349e7-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="349e7-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="349e7-105">Overview</span></span>

<span data-ttu-id="349e7-106">Depois de configurar um gateway de aplicativo, um dos erros de saudação que os usuários podem encontrar é "Erro de servidor: 502 - o servidor Web recebeu uma resposta inválida enquanto agia como um gateway ou servidor proxy".</span><span class="sxs-lookup"><span data-stu-id="349e7-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="349e7-107">Este erro pode ocorrer devido a seguir toohello motivos principais:</span><span class="sxs-lookup"><span data-stu-id="349e7-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="349e7-108">O [pool de back-end do Gateway de Aplicativo do Azure não está configurado ou está vazio](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="349e7-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="349e7-109">Nenhum dos Olá VMs ou instâncias em [conjunto de escala de VM estão íntegros](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="349e7-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="349e7-110">Máquinas virtuais ou instâncias do conjunto de escala de VM back-end são [não está respondendo investigação de integridade padrão toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="349e7-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="349e7-111">Configuração inválida ou incorreta [de investigações de integridade personalizadas](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="349e7-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="349e7-112">[Tempo limite de solicitação ou problemas de conectividade](#request-time-out) com solicitações de usuário.</span><span class="sxs-lookup"><span data-stu-id="349e7-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="349e7-113">BackendAddressPool vazio</span><span class="sxs-lookup"><span data-stu-id="349e7-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="349e7-114">Causa</span><span class="sxs-lookup"><span data-stu-id="349e7-114">Cause</span></span>

<span data-ttu-id="349e7-115">Se Olá Application Gateway não tem nenhuma VM ou conjunto de escala configurado no pool de endereços de back-end do hello, ele não pode rotear qualquer solicitação de cliente e gerará um erro de gateway incorreto.</span><span class="sxs-lookup"><span data-stu-id="349e7-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="349e7-116">Solução</span><span class="sxs-lookup"><span data-stu-id="349e7-116">Solution</span></span>

<span data-ttu-id="349e7-117">Certifique-se de que o pool de endereços de back-end de saudação não está vazio.</span><span class="sxs-lookup"><span data-stu-id="349e7-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="349e7-118">Isso pode ser feito por meio do PowerShell, da CLI ou do portal.</span><span class="sxs-lookup"><span data-stu-id="349e7-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="349e7-119">saída Olá Olá precede o cmdlet deve conter o pool de endereços de back-end não vazio.</span><span class="sxs-lookup"><span data-stu-id="349e7-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="349e7-120">A seguir há um exemplo em que são retornados dois pools que estão configurados com endereços FQDN ou IP para VMs de back-end.</span><span class="sxs-lookup"><span data-stu-id="349e7-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="349e7-121">Olá, estado de provisionamento da saudação BackendAddressPool deve ser 'êxito'.</span><span class="sxs-lookup"><span data-stu-id="349e7-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="349e7-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="349e7-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="349e7-123">Instâncias não íntegras em BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="349e7-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="349e7-124">Causa</span><span class="sxs-lookup"><span data-stu-id="349e7-124">Cause</span></span>

<span data-ttu-id="349e7-125">Se todas as instâncias de saudação do BackendAddressPool estiverem não íntegros, Application Gateway não teria qualquer solicitação de usuário tooroute de back-end.</span><span class="sxs-lookup"><span data-stu-id="349e7-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="349e7-126">Isso também pode ser o caso de Olá quando instâncias de back-end estão íntegros, mas não tem o aplicativo hello necessário implantado.</span><span class="sxs-lookup"><span data-stu-id="349e7-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="349e7-127">Solução</span><span class="sxs-lookup"><span data-stu-id="349e7-127">Solution</span></span>

<span data-ttu-id="349e7-128">Certifique-se de que as instâncias de saudação estejam íntegros e aplicativo hello está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="349e7-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="349e7-129">Verifique se capaz de toorespond tooa ping de outra VM em instâncias de back-end de saudação Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="349e7-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="349e7-130">Se configurado com um ponto de extremidade público, certifique-se de que um aplicativo da web do navegador solicitação toohello está operacional.</span><span class="sxs-lookup"><span data-stu-id="349e7-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="349e7-131">Problemas com a investigação de integridade padrão</span><span class="sxs-lookup"><span data-stu-id="349e7-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="349e7-132">Causa</span><span class="sxs-lookup"><span data-stu-id="349e7-132">Cause</span></span>

<span data-ttu-id="349e7-133">502 erros também podem ser frequentes indicadores que Olá investigação de integridade padrão é não é possível tooreach VMs de back-end.</span><span class="sxs-lookup"><span data-stu-id="349e7-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="349e7-134">Quando uma instância do Application Gateway é provisionada, ele automaticamente configura uma tooeach de investigação de integridade padrão BackendAddressPool usando as propriedades do hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="349e7-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="349e7-135">Nenhum usuário de entrada é necessária tooset essa investigação.</span><span class="sxs-lookup"><span data-stu-id="349e7-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="349e7-136">Especificamente, quando uma regra de balanceamento de carga é configurada, é feita uma associação entre BackendHttpSetting e BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="349e7-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="349e7-137">Uma investigação de padrão é configurada para cada uma dessas associações e inicia uma instância de tooeach integridade periódicas verificação de conexão no hello BackendAddressPool Olá porta especificada no elemento de BackendHttpSetting Olá a Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="349e7-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="349e7-138">Tabela a seguir lista os valores de saudação associados a investigação de integridade saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="349e7-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="349e7-139">Propriedades da investigação</span><span class="sxs-lookup"><span data-stu-id="349e7-139">Probe property</span></span> | <span data-ttu-id="349e7-140">Valor</span><span class="sxs-lookup"><span data-stu-id="349e7-140">Value</span></span> | <span data-ttu-id="349e7-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="349e7-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="349e7-142">URL de investigação</span><span class="sxs-lookup"><span data-stu-id="349e7-142">Probe URL</span></span> |<span data-ttu-id="349e7-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="349e7-143">http://127.0.0.1/</span></span> |<span data-ttu-id="349e7-144">Caminho da URL</span><span class="sxs-lookup"><span data-stu-id="349e7-144">URL path</span></span> |
| <span data-ttu-id="349e7-145">Intervalo</span><span class="sxs-lookup"><span data-stu-id="349e7-145">Interval</span></span> |<span data-ttu-id="349e7-146">30</span><span class="sxs-lookup"><span data-stu-id="349e7-146">30</span></span> |<span data-ttu-id="349e7-147">Intervalo da investigação em segundos</span><span class="sxs-lookup"><span data-stu-id="349e7-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="349e7-148">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="349e7-148">Time-out</span></span> |<span data-ttu-id="349e7-149">30</span><span class="sxs-lookup"><span data-stu-id="349e7-149">30</span></span> |<span data-ttu-id="349e7-150">Tempo limite da investigação em segundos</span><span class="sxs-lookup"><span data-stu-id="349e7-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="349e7-151">Limite não íntegro</span><span class="sxs-lookup"><span data-stu-id="349e7-151">Unhealthy threshold</span></span> |<span data-ttu-id="349e7-152">3</span><span class="sxs-lookup"><span data-stu-id="349e7-152">3</span></span> |<span data-ttu-id="349e7-153">Contagem de repetições da investigação.</span><span class="sxs-lookup"><span data-stu-id="349e7-153">Probe retry count.</span></span> <span data-ttu-id="349e7-154">servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello.</span><span class="sxs-lookup"><span data-stu-id="349e7-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="349e7-155">Solução</span><span class="sxs-lookup"><span data-stu-id="349e7-155">Solution</span></span>

* <span data-ttu-id="349e7-156">Verifique se um site padrão está configurado e está escutando em 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="349e7-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="349e7-157">Se BackendHttpSetting Especifica uma porta diferente de 80, o site padrão de saudação deve ser toolisten configurado na porta.</span><span class="sxs-lookup"><span data-stu-id="349e7-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="349e7-158">Olá toohttp://127.0.0.1:port de chamada deve retornar um código de resultado HTTP de 200.</span><span class="sxs-lookup"><span data-stu-id="349e7-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="349e7-159">Isso deve ser retornado dentro do período de tempo limite de 30 segundos hello.</span><span class="sxs-lookup"><span data-stu-id="349e7-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="349e7-160">Certifique-se de que a porta configurada está aberta e que não existem regras de firewall ou grupos de segurança de rede do Azure, que bloquear o tráfego de entrada ou de saída na porta de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="349e7-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="349e7-161">Se as VMs clássicas do Azure ou serviço de nuvem é usado com o FQDN ou IP público, certifique-se de que Olá correspondente [ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) é aberto.</span><span class="sxs-lookup"><span data-stu-id="349e7-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="349e7-162">Se Olá VM é configurada por meio do Gerenciador de recursos do Azure e está fora da saudação redes em que o Gateway de aplicativo é implantado, [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) deve ser configurado tooallow acesso Olá desejado de porta.</span><span class="sxs-lookup"><span data-stu-id="349e7-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="349e7-163">Problemas com a investigação de integridade personalizada</span><span class="sxs-lookup"><span data-stu-id="349e7-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="349e7-164">Causa</span><span class="sxs-lookup"><span data-stu-id="349e7-164">Cause</span></span>

<span data-ttu-id="349e7-165">Investigações de integridade personalizados permitem que o padrão de toohello flexibilidade adicional investigando o comportamento.</span><span class="sxs-lookup"><span data-stu-id="349e7-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="349e7-166">Ao usar testes personalizados, os usuários podem configurar o intervalo de sondagem hello, Olá URL e tootest de caminho e quantos tooaccept de respostas com falha antes de marcar a instância de pool de back-end hello como não íntegro.</span><span class="sxs-lookup"><span data-stu-id="349e7-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="349e7-167">Olá propriedades adicionais a seguir é adicionado.</span><span class="sxs-lookup"><span data-stu-id="349e7-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="349e7-168">Propriedades da investigação</span><span class="sxs-lookup"><span data-stu-id="349e7-168">Probe property</span></span> | <span data-ttu-id="349e7-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="349e7-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="349e7-170">Nome</span><span class="sxs-lookup"><span data-stu-id="349e7-170">Name</span></span> |<span data-ttu-id="349e7-171">Nome do teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="349e7-171">Name of hello probe.</span></span> <span data-ttu-id="349e7-172">Esse nome é usado toorefer toohello investigação em configurações de HTTP de back-end.</span><span class="sxs-lookup"><span data-stu-id="349e7-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="349e7-173">Protocolo</span><span class="sxs-lookup"><span data-stu-id="349e7-173">Protocol</span></span> |<span data-ttu-id="349e7-174">Protocolo usado toosend investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="349e7-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="349e7-175">investigação de saudação usa o protocolo de saudação definido nas configurações de HTTP de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="349e7-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="349e7-176">Host</span><span class="sxs-lookup"><span data-stu-id="349e7-176">Host</span></span> |<span data-ttu-id="349e7-177">Investigação de saudação do toosend do nome de host.</span><span class="sxs-lookup"><span data-stu-id="349e7-177">Host name toosend hello probe.</span></span> <span data-ttu-id="349e7-178">Aplicável somente quando vários sites são configurados no Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="349e7-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="349e7-179">Isso é diferente do nome de host de VM.</span><span class="sxs-lookup"><span data-stu-id="349e7-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="349e7-180">Caminho</span><span class="sxs-lookup"><span data-stu-id="349e7-180">Path</span></span> |<span data-ttu-id="349e7-181">Caminho relativo da investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="349e7-181">Relative path of hello probe.</span></span> <span data-ttu-id="349e7-182">caminho válido Olá começa com '/'.</span><span class="sxs-lookup"><span data-stu-id="349e7-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="349e7-183">teste de saudação é enviado muito\<protocolo\>://\<host\>:\<porta\>\<caminho\></span><span class="sxs-lookup"><span data-stu-id="349e7-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="349e7-184">Intervalo</span><span class="sxs-lookup"><span data-stu-id="349e7-184">Interval</span></span> |<span data-ttu-id="349e7-185">Intervalo de investigação em segundos.</span><span class="sxs-lookup"><span data-stu-id="349e7-185">Probe interval in seconds.</span></span> <span data-ttu-id="349e7-186">Este é o intervalo de tempo de saudação entre duas investigações consecutivos.</span><span class="sxs-lookup"><span data-stu-id="349e7-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="349e7-187">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="349e7-187">Time-out</span></span> |<span data-ttu-id="349e7-188">Tempo limite da investigação em segundos.</span><span class="sxs-lookup"><span data-stu-id="349e7-188">Probe time-out in seconds.</span></span> <span data-ttu-id="349e7-189">Se uma resposta válida não for recebida dentro desse período de tempo limite, investigação hello está marcada como falha.</span><span class="sxs-lookup"><span data-stu-id="349e7-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="349e7-190">Limite não íntegro</span><span class="sxs-lookup"><span data-stu-id="349e7-190">Unhealthy threshold</span></span> |<span data-ttu-id="349e7-191">Contagem de repetições da investigação.</span><span class="sxs-lookup"><span data-stu-id="349e7-191">Probe retry count.</span></span> <span data-ttu-id="349e7-192">servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello.</span><span class="sxs-lookup"><span data-stu-id="349e7-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="349e7-193">Solução</span><span class="sxs-lookup"><span data-stu-id="349e7-193">Solution</span></span>

<span data-ttu-id="349e7-194">Valide que Olá que investigação de integridade personalizado está configurado corretamente como Olá anterior da tabela.</span><span class="sxs-lookup"><span data-stu-id="349e7-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="349e7-195">Além disso toohello anterior etapas, solução de problemas também Certifique-se de seguir hello:</span><span class="sxs-lookup"><span data-stu-id="349e7-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="349e7-196">Certifique-se de que esse teste hello está especificado corretamente de acordo com a saudação [guia](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="349e7-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="349e7-197">Se o Gateway do aplicativo está configurado para um único site, por saudação padrão Host nome deve ser especificado como '127.0.0.1', a menos que o contrário configurada na investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="349e7-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="349e7-198">Certifique-se de que uma chamada toohttp: / /\<host\>:\<porta\>\<caminho\> retorna um código de resultado HTTP de 200.</span><span class="sxs-lookup"><span data-stu-id="349e7-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="349e7-199">Certifique-se de que o intervalo de tempo limite e UnhealtyThreshold estão dentro dos intervalos aceitáveis hello.</span><span class="sxs-lookup"><span data-stu-id="349e7-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="349e7-200">Se usar um HTTPS investigação, certifique-se de que servidor de back-end Olá não requer SNI Configurando um certificado de fallback no próprio servidor de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="349e7-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="349e7-201">Certifique-se de que o intervalo de tempo limite e UnhealtyThreshold estão dentro dos intervalos aceitáveis hello.</span><span class="sxs-lookup"><span data-stu-id="349e7-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="349e7-202">Tempo limite de solicitação</span><span class="sxs-lookup"><span data-stu-id="349e7-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="349e7-203">Causa</span><span class="sxs-lookup"><span data-stu-id="349e7-203">Cause</span></span>

<span data-ttu-id="349e7-204">Quando uma solicitação de usuário é recebida, o Application Gateway aplica Olá configurado regras toohello solicitação e encaminha tooa instância de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="349e7-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="349e7-205">Ele espera um intervalo configurável de tempo para uma resposta da instância de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="349e7-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="349e7-206">Por padrão, o intervalo é de **30 segundos**.</span><span class="sxs-lookup"><span data-stu-id="349e7-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="349e7-207">Se o Gateway de Aplicativo não receber uma resposta do aplicativo de back-end nesse intervalo, a solicitação de usuário obterá um erro 502.</span><span class="sxs-lookup"><span data-stu-id="349e7-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="349e7-208">Solução</span><span class="sxs-lookup"><span data-stu-id="349e7-208">Solution</span></span>

<span data-ttu-id="349e7-209">Application Gateway permite que usuários tooconfigure essa definição via BackendHttpSetting, que pode ser então aplicadas toodifferent pools.</span><span class="sxs-lookup"><span data-stu-id="349e7-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="349e7-210">Os pools de back-end diferentes podem ter BackendHttpSetting diferentes e, assim, um tempo limite de solicitação diferente configurado.</span><span class="sxs-lookup"><span data-stu-id="349e7-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="349e7-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="349e7-211">Next steps</span></span>

<span data-ttu-id="349e7-212">Se hello etapas anteriores não resolverem o problema de saudação, abra um [tíquete de suporte](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="349e7-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

