---
title: "filtros de conexão de IP de Hub IoT aaaAzure | Microsoft Docs"
description: "Como endereços IP de toouse tooblock conexões de IP específica de filtragem para tooyour Azure IoT hub. Você pode bloquear conexões de endereços IP individuais ou de intervalos de endereços IP."
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
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="6acce-104">Usar filtros IP</span><span class="sxs-lookup"><span data-stu-id="6acce-104">Use IP filters</span></span>

<span data-ttu-id="6acce-105">A segurança é um aspecto importante de qualquer solução de IoT com base no Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="6acce-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="6acce-106">Às vezes você precisa tooexplicitly especificar endereços IP de saudação do qual o dispositivo pode se conectar como parte da configuração de segurança.</span><span class="sxs-lookup"><span data-stu-id="6acce-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="6acce-107">Olá _filtro IP_ recurso permite que as regras de tooconfigure para rejeitar ou aceitar tráfego de endereços IPv4 específicos.</span><span class="sxs-lookup"><span data-stu-id="6acce-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="6acce-108">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="6acce-108">When toouse</span></span>

<span data-ttu-id="6acce-109">Há dois casos de uso específicos quando se trata de pontos de extremidade de Hub IoT Olá de tooblock úteis para determinados endereços IP:</span><span class="sxs-lookup"><span data-stu-id="6acce-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="6acce-110">O Hub IoT deve receber tráfego somente de um intervalo específico de endereços IP e rejeitar todo o resto.</span><span class="sxs-lookup"><span data-stu-id="6acce-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="6acce-111">Por exemplo, você está usando o hub IoT com [rota expressa do Azure] toocreate de conexões privadas entre um hub IoT e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="6acce-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="6acce-112">É necessário tooreject tráfego de endereços IP que foram identificados como suspeita pelo administrador de hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="6acce-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="6acce-113">Como são aplicadas as regras de filtro</span><span class="sxs-lookup"><span data-stu-id="6acce-113">How filter rules are applied</span></span>

<span data-ttu-id="6acce-114">regras de filtro IP Hello são aplicadas em Olá nível de serviço de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6acce-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="6acce-115">Portanto regras de filtro IP hello aplicam tooall conexões de dispositivos e aplicativos de back-end usando qualquer protocolo com suporte.</span><span class="sxs-lookup"><span data-stu-id="6acce-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="6acce-116">Todas as tentativas de conexão de um endereço IP que corresponde a uma regra IP de rejeição em seu Hub IoT recebem um código de status 401 não autorizado e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="6acce-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="6acce-117">mensagem de resposta de saudação não mencionar a regra de IP hello.</span><span class="sxs-lookup"><span data-stu-id="6acce-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="6acce-118">Configuração padrão</span><span class="sxs-lookup"><span data-stu-id="6acce-118">Default setting</span></span>

<span data-ttu-id="6acce-119">Por padrão, Olá **filtro IP** grade no portal de saudação para um hub IoT está vazio.</span><span class="sxs-lookup"><span data-stu-id="6acce-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="6acce-120">Essa configuração padrão significa que o hub aceita conexões de qualquer endereço IP.</span><span class="sxs-lookup"><span data-stu-id="6acce-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="6acce-121">Essa configuração padrão é a regra de tooa equivalente que aceita o intervalo de endereços IP hello 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="6acce-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Configurações de filtro IP padrão do Hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="6acce-123">Adicionar ou editar uma regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="6acce-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="6acce-124">Quando você adiciona uma regra de filtro IP, você será solicitado para Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="6acce-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="6acce-125">Um **nome de regra de filtro IP** que deve ser uma cadeia de caracteres exclusiva, diferencia maiusculas de minúsculas, alfanumérica backup too128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6acce-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="6acce-126">Somente caracteres alfanuméricos de saudação ASCII de 7 bits mais `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` são aceitas.</span><span class="sxs-lookup"><span data-stu-id="6acce-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="6acce-127">Selecione um **rejeitar** ou **aceitar** como Olá **ação** para regra de filtro IP hello.</span><span class="sxs-lookup"><span data-stu-id="6acce-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="6acce-128">Forneça um endereço IPv4 único ou um bloco de endereços IP na notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="6acce-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="6acce-129">Por exemplo, CIDR notação 192.168.100.0/22 representa os endereços IPv4 Olá 1024 de 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="6acce-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Adicionar um hub IoT do IP filtro regra tooan][img-ip-filter-add-rule]

<span data-ttu-id="6acce-131">Depois de salvar regra Olá, verá um alerta, notificando que essa atualização Olá estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="6acce-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Notificação sobre como salvar uma regra de filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="6acce-133">Olá **adicionar** opção é desabilitada quando você atingir o máximo de saudação de 10 regras de filtro IP.</span><span class="sxs-lookup"><span data-stu-id="6acce-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="6acce-134">Você pode editar uma regra existente clicando duas vezes em linha hello que contém a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="6acce-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="6acce-135">Rejeitar IP endereços podem impedir que outros serviços do Azure (como o Stream Analytics do Azure, máquinas virtuais do Azure ou Olá Gerenciador de dispositivo no portal de saudação) interagir com o hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="6acce-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="6acce-136">Se você usar mensagens de tooread de análise de fluxo do Azure (ASA) de um hub IoT com a filtragem de IP habilitado, use o nome de Hub de eventos-compatível com de Olá e ponto de extremidade do seu IoT Hub em Olá cadeia de caracteres de conexão ASA.</span><span class="sxs-lookup"><span data-stu-id="6acce-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="6acce-137">Excluir uma regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="6acce-137">Delete an IP filter rule</span></span>

<span data-ttu-id="6acce-138">toodelete uma regra de filtro IP, selecione uma ou mais regras no hello grade e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="6acce-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Excluir uma regra de filtro IP de Hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="6acce-140">Avaliação da regra de filtro IP</span><span class="sxs-lookup"><span data-stu-id="6acce-140">IP filter rule evaluation</span></span>

<span data-ttu-id="6acce-141">Regras de filtro IP são aplicadas na ordem e a primeira regra de saudação que corresponde ao endereço IP de saudação determina Olá aceitar ou rejeitar a ação.</span><span class="sxs-lookup"><span data-stu-id="6acce-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="6acce-142">Por exemplo, se você quiser tooaccept endereços Olá intervalo 192.168.100.0/22 e rejeitar tudo, a primeira regra Olá na grade de saudação deve aceitar Olá endereço intervalo 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="6acce-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="6acce-143">próxima regra do Hello deve rejeitar todos os endereços usando o intervalo de saudação 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="6acce-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="6acce-144">Você pode alterar a ordem de saudação as regras de filtro IP na grade de saudação clicando em três pontos verticais Olá no início de saudação de uma linha e usando arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="6acce-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="6acce-145">filtro de seu novo IP toosave ordem de regras, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6acce-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Alterar a ordem das regras de filtro de IP de Hub IoT Olá][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="6acce-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6acce-147">Next steps</span></span>

<span data-ttu-id="6acce-148">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="6acce-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="6acce-149">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6acce-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="6acce-150">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6acce-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[rota expressa do Azure]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md