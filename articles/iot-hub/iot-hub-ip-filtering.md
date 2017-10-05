---
title: "Filtros IP de conexão do Hub IoT do Azure | Microsoft Docs"
description: "Como usar a filtragem de IP para bloquear conexões de endereços IP específicos para seu Hub IoT do Azure. Você pode bloquear conexões de endereços IP individuais ou de intervalos de endereços IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="66ab5-104">Usar filtros IP</span><span class="sxs-lookup"><span data-stu-id="66ab5-104">Use IP filters</span></span>

<span data-ttu-id="66ab5-105">A segurança é um aspecto importante de qualquer solução de IoT com base no Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="66ab5-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="66ab5-106">Às vezes você precisa especificar explicitamente os endereços IP dos quais o dispositivo pode se conectar como parte da sua configuração de segurança.</span><span class="sxs-lookup"><span data-stu-id="66ab5-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="66ab5-107">O recurso _filtro IP_ permite que você configure regras para rejeitar ou aceitar tráfego de endereços IPv4 específicos.</span><span class="sxs-lookup"><span data-stu-id="66ab5-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="66ab5-108">Quando usar</span><span class="sxs-lookup"><span data-stu-id="66ab5-108">When to use</span></span>

<span data-ttu-id="66ab5-109">Há dois casos de uso específicos em que é útil bloquear os pontos de extremidade do Hub IoT para determinados endereços IP:</span><span class="sxs-lookup"><span data-stu-id="66ab5-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="66ab5-110">O Hub IoT deve receber tráfego somente de um intervalo específico de endereços IP e rejeitar todo o resto.</span><span class="sxs-lookup"><span data-stu-id="66ab5-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="66ab5-111">Por exemplo, caso você esteja usando o Hub IoT com o [Azure ExpressRoute] para criar conexões privadas entre um Hub IoT e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="66ab5-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="66ab5-112">Você precisa rejeitar tráfego de endereços IP que foram identificados como suspeitos pelo administrador do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="66ab5-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="66ab5-113">Como são aplicadas as regras de filtro</span><span class="sxs-lookup"><span data-stu-id="66ab5-113">How filter rules are applied</span></span>

<span data-ttu-id="66ab5-114">As regras de filtro IP são aplicadas no nível do serviço Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="66ab5-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="66ab5-115">Portanto, as regras de filtro IP se aplicam a todas as conexões de dispositivos e aplicativos de back-end que usam qualquer protocolo com suporte.</span><span class="sxs-lookup"><span data-stu-id="66ab5-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="66ab5-116">Todas as tentativas de conexão de um endereço IP que corresponde a uma regra IP de rejeição em seu Hub IoT recebem um código de status 401 não autorizado e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="66ab5-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="66ab5-117">A mensagem de resposta não menciona a regra IP.</span><span class="sxs-lookup"><span data-stu-id="66ab5-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="66ab5-118">Configuração padrão</span><span class="sxs-lookup"><span data-stu-id="66ab5-118">Default setting</span></span>

<span data-ttu-id="66ab5-119">Por padrão, a grade **Filtro IP** no portal de Hub IoT fica vazia.</span><span class="sxs-lookup"><span data-stu-id="66ab5-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="66ab5-120">Essa configuração padrão significa que o hub aceita conexões de qualquer endereço IP.</span><span class="sxs-lookup"><span data-stu-id="66ab5-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="66ab5-121">Essa configuração padrão é equivalente a uma regra que aceita o intervalo de endereços IP 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="66ab5-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![Configurações de filtro IP padrão do Hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="66ab5-123">Adicionar ou editar uma regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="66ab5-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="66ab5-124">Quando você adiciona uma regra de filtro IP, os seguintes valores são solicitados:</span><span class="sxs-lookup"><span data-stu-id="66ab5-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="66ab5-125">Um **nome de regra de filtro IP** que deve ser uma cadeia de caracteres alfanumérica exclusiva com até 128 caracteres que diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="66ab5-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="66ab5-126">Somente são aceitos caracteres alfanuméricos ASCII de 7 bits mais `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`.</span><span class="sxs-lookup"><span data-stu-id="66ab5-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="66ab5-127">Selecione **rejeitar** ou **aceitar** como a **ação** para a regra de filtro IP.</span><span class="sxs-lookup"><span data-stu-id="66ab5-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="66ab5-128">Forneça um endereço IPv4 único ou um bloco de endereços IP na notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="66ab5-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="66ab5-129">Por exemplo, uma notação CIDR 192.168.100.0/22 representa os 1024 endereços IPv4 de 192.168.100.0 a 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="66ab5-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Adicionar uma regra de filtro IP a um Hub IoT][img-ip-filter-add-rule]

<span data-ttu-id="66ab5-131">Depois de salvar a regra, você verá um alerta informando que a atualização está em andamento.</span><span class="sxs-lookup"><span data-stu-id="66ab5-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notificação sobre como salvar uma regra de filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="66ab5-133">A opção **Adicionar** é desabilitada quando você atinge o máximo de dez regras de filtro IP.</span><span class="sxs-lookup"><span data-stu-id="66ab5-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="66ab5-134">Você pode editar uma regra existente clicando duas vezes na linha que contém a regra.</span><span class="sxs-lookup"><span data-stu-id="66ab5-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="66ab5-135">Rejeitar endereços IP pode impedir que outros serviços do Azure (como Stream Analytics do Azure, Máquinas Virtuais do Azure ou o Explorer de dispositivos no portal) interajam com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="66ab5-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="66ab5-136">Se você usar o ASA (Azure Stream Analytics) para ler mensagens de um hub IoT com a filtragem de IP habilitada, use o nome compatível com o Hub-de Eventos e o ponto de extremidade do Hub IoT na cadeia de conexão ASA.</span><span class="sxs-lookup"><span data-stu-id="66ab5-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="66ab5-137">Excluir uma regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="66ab5-137">Delete an IP filter rule</span></span>

<span data-ttu-id="66ab5-138">Para excluir uma regra de filtro IP, selecione uma ou mais regras na grade e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="66ab5-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Excluir uma regra de filtro IP de Hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="66ab5-140">Avaliação da regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="66ab5-140">IP filter rule evaluation</span></span>

<span data-ttu-id="66ab5-141">As regras de filtro IP são aplicadas na ordem e a primeira regra que corresponde ao endereço IP determina a ação de aceitar ou rejeitar.</span><span class="sxs-lookup"><span data-stu-id="66ab5-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="66ab5-142">Por exemplo, se você quiser aceitar endereços no intervalo 192.168.100.0/22 e rejeitar todo o resto, a primeira regra na grade deverá aceitar o intervalo de endereços 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="66ab5-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="66ab5-143">A próxima regra deve rejeitar todos os endereços usando o intervalo 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="66ab5-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="66ab5-144">Você pode alterar a ordem de suas regras de filtro IP na grade clicando nos três pontos verticais no início de uma linha e usando arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="66ab5-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="66ab5-145">Para salvar a nova ordem das regras de filtro IP, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66ab5-145">To save your new IP filter rule order, click **Save**.</span></span>

![Alterar a ordem de suas regras de filtro IP de Hub IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="66ab5-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66ab5-147">Next steps</span></span>

<span data-ttu-id="66ab5-148">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="66ab5-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="66ab5-149">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="66ab5-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="66ab5-150">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="66ab5-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="66ab5-151">[Azure ExpressRoute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="66ab5-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md