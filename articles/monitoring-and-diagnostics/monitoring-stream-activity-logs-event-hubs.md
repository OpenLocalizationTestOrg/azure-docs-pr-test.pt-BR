---
title: "aaaStream Olá Log de atividades do Azure tooEvent Hubs | Microsoft Docs"
description: "Saiba como toostream Olá tooEvent do Log de atividades do Azure Hubs."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="1b5d1-103">Fluxo de tooEvent de Log de atividades do Azure Olá Hubs</span><span class="sxs-lookup"><span data-stu-id="1b5d1-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="1b5d1-104">Olá [ **o Log de atividades do Azure** ](monitoring-overview-activity-logs.md) pode ser transmitida em quase em tempo real tooany aplicativo usando a opção Olá interna "Exportar" no portal de hello, ou habilitando Olá Id de regra de barramento de serviço em um perfil de registro por meio de saudação Cmdlets do PowerShell do Azure ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="1b5d1-105">O que você pode fazer com hello Log de atividades e Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="1b5d1-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="1b5d1-106">Aqui estão algumas maneiras que você pode usar o hello streaming funcionalidade para Olá Log de atividades:</span><span class="sxs-lookup"><span data-stu-id="1b5d1-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="1b5d1-107">**Fluxo de sistemas de registro em log e telemetria toothird terceiros** – ao longo do tempo, streaming de Hubs de eventos se tornará Olá mecanismo toopipe o Log de atividades em SIEMs de terceiros e soluções de análise de log.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="1b5d1-108">**Criar uma plataforma de registro em log e telemetria personalizada** – se você já tem uma plataforma de telemetria personalizada ou estão pensando sobre como criar um, Olá altamente escalonável de publicação / assinatura natureza dos Hubs de eventos permite que você tooflexibly ingestão Olá log de atividades.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="1b5d1-109">Consulte toousing de guia de Dan Rosanova Hubs de eventos em uma plataforma de telemetria de escala global aqui.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="1b5d1-110">Habilitar o streaming de saudação Log de atividades</span><span class="sxs-lookup"><span data-stu-id="1b5d1-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="1b5d1-111">Você pode habilitar o streaming de hello atividade de Log programaticamente ou por meio do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="1b5d1-112">De qualquer forma, você escolhe um Namespace de barramento de serviço e uma política de acesso compartilhado para que o namespace e um Hub de eventos é criado no namespace quando ocorre Olá primeiro novo evento de Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="1b5d1-113">Se você não tem um Namespace de barramento de serviço, é necessário primeiro toocreate um.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="1b5d1-114">Se você tiver anteriormente transmitido toothis de eventos do Log de atividades Namespace de barramento de serviço, Olá Hub de eventos que foi criado anteriormente será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="1b5d1-115">política de acesso compartilhada de saudação define permissões de saudação com mecanismo de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="1b5d1-116">Atualmente, o streaming de Hubs de eventos tooan exige **gerenciar**, **enviar**, e **escutar** permissões.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="1b5d1-117">Você pode criar ou modificar políticas de acesso do Namespace de barramento de serviço compartilhado no portal clássico do hello na guia de "Configurar" Olá para o Namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="1b5d1-118">tooupdate Olá fluxo contínuo tooinclude de perfil do log de Log de atividades, usuário Olá Olá alteração deve ter permissão de ListKey Olá nessa regra de autorização do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="1b5d1-119">Olá namespace de hub de evento ou de barramento de serviço não tem toobe em Olá mesma assinatura que Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="1b5d1-120">Via Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1b5d1-120">Via Azure portal</span></span>
1. <span data-ttu-id="1b5d1-121">Navegue toohello **Log de atividades** folha usando o menu de saudação em Olá esquerda do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Navegue tooActivity Log no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="1b5d1-123">Clique em Olá **exportar** botão na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Botão Exportar no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="1b5d1-125">Na folha de saudação que aparece, você pode selecionar regiões Olá para o qual você gostaria que os eventos toostream e Olá Namespace de barramento de serviço em que você gostaria que um toobe de Hub de eventos criado para esses eventos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Folha Exportar Log de Atividades](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="1b5d1-127">Clique em **salvar** toosave essas configurações.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="1b5d1-128">configurações de saudação imediatamente são ser aplicada tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="1b5d1-129">Via Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b5d1-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="1b5d1-130">Se já existir um perfil de registro, é necessário primeiro tooremove esse perfil.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="1b5d1-131">Use `Get-AzureRmLogProfile` tooidentify se existe um perfil de registro</span><span class="sxs-lookup"><span data-stu-id="1b5d1-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="1b5d1-132">Nesse caso, use `Remove-AzureRmLogProfile` tooremove-lo.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="1b5d1-133">Use `Set-AzureRmLogProfile` toocreate um perfil:</span><span class="sxs-lookup"><span data-stu-id="1b5d1-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="1b5d1-134">Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: {ID de recurso do barramento de serviço} /authorizationrules/ {nome da chave}, por exemplo</span><span class="sxs-lookup"><span data-stu-id="1b5d1-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="1b5d1-135">Via CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1b5d1-135">Via Azure CLI</span></span>
<span data-ttu-id="1b5d1-136">Se já existir um perfil de registro, é necessário primeiro tooremove esse perfil.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="1b5d1-137">Use `azure insights logprofile list` tooidentify se existe um perfil de registro</span><span class="sxs-lookup"><span data-stu-id="1b5d1-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="1b5d1-138">Nesse caso, use `azure insights logprofile delete` tooremove-lo.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="1b5d1-139">Use `azure insights logprofile add` toocreate um perfil:</span><span class="sxs-lookup"><span data-stu-id="1b5d1-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="1b5d1-140">Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="1b5d1-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="1b5d1-141">Como consomem a dados de log de saudação dos Hubs de eventos?</span><span class="sxs-lookup"><span data-stu-id="1b5d1-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="1b5d1-142">[esquema Olá Olá Log de atividade está disponível aqui](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1b5d1-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="1b5d1-143">Cada evento é uma matriz de blobs JSON chamada "registros".</span><span class="sxs-lookup"><span data-stu-id="1b5d1-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b5d1-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b5d1-144">Next Steps</span></span>
* [<span data-ttu-id="1b5d1-145">Saudação de arquivamento conta de armazenamento do Log de atividades tooa</span><span class="sxs-lookup"><span data-stu-id="1b5d1-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="1b5d1-146">Ler visão geral de saudação do hello Log de atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="1b5d1-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="1b5d1-147">Configurar um alerta com base em um evento do Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="1b5d1-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

