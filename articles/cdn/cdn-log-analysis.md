---
title: "análise de aaaLog para CDN do Azure | Microsoft Docs"
description: "O cliente pode habilitar a análise de log para a CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="60c5b-103">Logs de Diagnóstico para a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="60c5b-104">Depois de habilitar CDN para o seu aplicativo, você provavelmente deseja uso da CDN toomonitor Olá, verificar a integridade de saudação de sua entrega e solucionar possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="60c5b-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="60c5b-105">A CDN do Azure fornece esses recursos com a [Análise de Núcleo de CDN](cdn-analyze-usage-patterns.md) e os [Logs de Diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="60c5b-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="60c5b-106">Análise de Núcleo de CDN</span><span class="sxs-lookup"><span data-stu-id="60c5b-106">CDN Core Analytics</span></span>
<span data-ttu-id="60c5b-107">Como um usuário atual do Azure CDN Verizon padrão ou perfil de premium, você já está tooview capaz de análise de núcleo no portal suplementar da saudação acessível por meio da opção de "Gerenciar" hello da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c5b-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="60c5b-108">Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="60c5b-109">Azure Com esse novo recurso, você pode exibir a análise de núcleo e salvá-la em um ou mais destinos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="60c5b-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="60c5b-110">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-110">Azure Storage account</span></span>
 - <span data-ttu-id="60c5b-111">Hubs de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="60c5b-112">Repositório do OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="60c5b-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="60c5b-113">Este recurso está disponível para todos os pontos de extremidade CDN pertencentes tooVerizon (Standard e Premium) e perfis de CDN do Akamai (padrão).</span><span class="sxs-lookup"><span data-stu-id="60c5b-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="60c5b-114">Logs de diagnóstico permitem tooexport métricas de uso básico de sua variedade de tooa de ponto de extremidade CDN de fontes para que você pode consumi-los de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="60c5b-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="60c5b-115">Por exemplo, você pode fazer Olá seguintes tipos de exportação de dados:</span><span class="sxs-lookup"><span data-stu-id="60c5b-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="60c5b-116">Exportar armazenamento tooblob de dados, exportar tooCSV e gerar gráficos no excel.</span><span class="sxs-lookup"><span data-stu-id="60c5b-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="60c5b-117">Exportar hubs tooevent de dados e correlacionar com dados de outros serviços do azure.</span><span class="sxs-lookup"><span data-stu-id="60c5b-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="60c5b-118">Exportar dados toolog análise e exibir os dados em seu próprio espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="60c5b-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="60c5b-119">Hello figura a seguir mostra uma exibição de análise de núcleo de CDN típica em dados.</span><span class="sxs-lookup"><span data-stu-id="60c5b-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="60c5b-121">*Figura 1 – exibição de Análise de Núcleo de CDN*</span><span class="sxs-lookup"><span data-stu-id="60c5b-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="60c5b-122">Olá seguindo as instruções passo a passo passa pelo esquema de saudação do dados de análise de núcleo hello, etapas envolvidas na habilitação do recurso hello e entregá-los toovarious destinos e consumo desses destinos.</span><span class="sxs-lookup"><span data-stu-id="60c5b-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="60c5b-123">Habilitar registro em log com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="60c5b-124">Olá logs de diagnóstico estão ativados **off** por padrão.</span><span class="sxs-lookup"><span data-stu-id="60c5b-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="60c5b-125">Siga as próximas etapas, Olá tooenable registro em log com a análise de núcleo de CDN:</span><span class="sxs-lookup"><span data-stu-id="60c5b-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="60c5b-126">Entrar toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60c5b-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="60c5b-127">Se você ainda não tiver a CDN habilitada para o fluxo de trabalho, [Habilite a CDN do Azure](cdn-create-new-endpoint.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="60c5b-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="60c5b-128">No portal de hello, navegue até muito**perfil CDN**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="60c5b-129">Selecione um perfil CDN e selecione o ponto de extremidade CDN Olá que você deseja tooenable **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="60c5b-131">Vá muito**Logs de diagnóstico** folha sob **monitoramento** seção, em seguida, alterar o status de saudação muito**em**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="60c5b-133">Habilitar registro em log com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="60c5b-134">logs de saudação toostore do armazenamento do Azure toouse, selecione **tooa conta de armazenamento de arquivos**, selecione os dias de retenção e clique em **CoreAnalytics** em **Log**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="60c5b-136">*Figura 2 – Registro em log com o Armazenamento do Azure*</span><span class="sxs-lookup"><span data-stu-id="60c5b-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="60c5b-137">Registro em log com o OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="60c5b-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="60c5b-138">logs de saudação toostore de análise de logs do OMS toouse, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="60c5b-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="60c5b-139">De saudação **Logs de diagnóstico** folha sob **monitoramento**, selecione **enviar tooLog análise** de</span><span class="sxs-lookup"><span data-stu-id="60c5b-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="60c5b-141">Configure o log de análise de Log Olá clicando em configurar.</span><span class="sxs-lookup"><span data-stu-id="60c5b-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="60c5b-142">Isso leva tooa caixa de diálogo onde você pode selecionar um espaço de trabalho anterior ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="60c5b-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="60c5b-144">Clique em **Criar Novo Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-144">Click **Create New Workspace**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="60c5b-146">Em seguida, você deve selecionar um novo nome de espaço de trabalho, uma assinatura existente, um grupo de recursos (novo ou existente), um local e um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="60c5b-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="60c5b-147">Você tem a opção de saudação de Fixar este painel de tooyour de configuração.</span><span class="sxs-lookup"><span data-stu-id="60c5b-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="60c5b-148">Clique em configuração de saudação toocomplete Okey.</span><span class="sxs-lookup"><span data-stu-id="60c5b-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="60c5b-149">Em seguida, você verá seu espaço de trabalho com os nomes do grupo de recursos e do Espaço de Trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="60c5b-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="60c5b-150">Os nomes devem ser exclusivos e podem usar apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="60c5b-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="60c5b-151">Espaços e sublinhados não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="60c5b-151">Spaces and underscores are not allowed.</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="60c5b-153">Em seguida receber uma mensagem curta informando que seu espaço de trabalho foi criado e você retornará tooyour tela de configuração de log.</span><span class="sxs-lookup"><span data-stu-id="60c5b-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="60c5b-154">Você pode confirmar o nome de saudação do seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="60c5b-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="60c5b-156">Depois de ter definido a configuração de análise de Log hello, certifique-se de que conferir caixa CoreAnalytics Olá log CDN.</span><span class="sxs-lookup"><span data-stu-id="60c5b-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="60c5b-157">Se tudo estiver tooyour preferência, clique em Olá **salvar** botão na parte superior de saudação da caixa de diálogo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="60c5b-159">Olá **salvar** botão não está mais ativa e que Olá no/fora botão agora é ON, mas azul, em vez de roxo.</span><span class="sxs-lookup"><span data-stu-id="60c5b-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="60c5b-160">Se você quiser toosee seu novo espaço de trabalho do OMS, vá tooyour portal do Azure painel, clique em nome de saudação do seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="60c5b-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="60c5b-161">Em seguida, você verá seu espaço de trabalho (certifique-se de que o espaço de trabalho do OMS é realçado Olá esquerda).</span><span class="sxs-lookup"><span data-stu-id="60c5b-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="60c5b-162">Clique em Olá Portal do OMS bloco toosee seu espaço de trabalho no repositório do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="60c5b-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="60c5b-164">O repositório do OMS agora está pronto toolog dados.</span><span class="sxs-lookup"><span data-stu-id="60c5b-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="60c5b-165">Em ordem tooconsume dados, você deve usar um [solução do OMS](#consuming-oms-log-analytics-data), coberto neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60c5b-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="60c5b-166">Para obter mais informações sobre os atrasos em dados de log, consulte [aqui](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="60c5b-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="60c5b-167">Habilitar o registro em log com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="60c5b-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="60c5b-168">Abaixo está um exemplo de como tooenable e obter Logs de diagnóstico por meio de Olá Cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c5b-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="60c5b-169">Habilitando os Logs de Diagnóstico em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="60c5b-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="60c5b-170">Primeiro, faça logon e selecione uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="60c5b-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="60c5b-171">tooEnable Logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="60c5b-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="60c5b-172">tooEnable Logs de diagnóstico em um espaço de trabalho do OMS, use este comando:</span><span class="sxs-lookup"><span data-stu-id="60c5b-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="60c5b-173">Consumir logs de diagnóstico do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="60c5b-174">Esta seção descreve o esquema de saudação da análise de núcleo CDN hello, como eles são organizados dentro de uma conta de armazenamento do Azure e fornece Olá de toodownload do código de exemplo registra no arquivo CSV de tooa.</span><span class="sxs-lookup"><span data-stu-id="60c5b-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="60c5b-175">Usando o Gerenciador de Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="60c5b-176">Antes de poder acessar dados de análise de núcleo de saudação do hello conta de armazenamento do Azure, primeiro é necessário um conteúdo de saudação tooaccess ferramenta em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="60c5b-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="60c5b-177">Embora várias ferramentas estão disponíveis no mercado Olá, Olá que recomendamos é Olá Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="60c5b-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="60c5b-178">Você pode baixar a ferramenta de saudação do [aqui](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="60c5b-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="60c5b-179">Depois de baixar e instalar software hello, configure-toouse Olá a mesma conta de armazenamento do Azure que foi configurado como um destino toohello CDN Logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="60c5b-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="60c5b-180">Abra o **Gerenciador de Armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="60c5b-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="60c5b-181">Localize a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="60c5b-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="60c5b-182">Vá toohello **"Contêineres de Blob"** nó sob esse armazenamento de conta e expanda o nó Olá</span><span class="sxs-lookup"><span data-stu-id="60c5b-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="60c5b-183">Contêiner Olá selecione denominado **"insights-logs-coreanalytics"** e clique duas vezes</span><span class="sxs-lookup"><span data-stu-id="60c5b-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="60c5b-184">Mostrar os resultados de backup em Olá painel direito começando com hello primeiro nível, que se parece com **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="60c5b-185">Continue clicando em todo o caminho de saudação até que você veja o arquivo hello **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="60c5b-186">Consulte Olá Observação para obter explicação do caminho Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="60c5b-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="60c5b-187">Cada blob **PT1H.json** representa hello logs de análise para uma hora para um ponto de extremidade CDN específico ou seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="60c5b-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="60c5b-188">esquema de saudação do conteúdo Olá deste arquivo JSON é descrita na seção de saudação esquema de saudação Logs de análise de núcleo</span><span class="sxs-lookup"><span data-stu-id="60c5b-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="60c5b-189">**Formato de caminho de blob**</span><span class="sxs-lookup"><span data-stu-id="60c5b-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="60c5b-190">Os logs de análise principal são gerados a cada hora.</span><span class="sxs-lookup"><span data-stu-id="60c5b-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="60c5b-191">Todos os dados de uma hora são coletados e armazenados em um único Blob do Azure como um conteúdo JSON.</span><span class="sxs-lookup"><span data-stu-id="60c5b-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="60c5b-192">Olá caminho toothis BLOBs do Azure aparece como se houver uma estrutura hierárquica.</span><span class="sxs-lookup"><span data-stu-id="60c5b-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="60c5b-193">Isso é porque a ferramenta de Gerenciador de armazenamento Olá interpreta '/' como um separador de diretório e mostra a hierarquia de saudação para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="60c5b-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="60c5b-194">Na verdade, o caminho inteiro Olá apenas representa o nome de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="60c5b-195">Esse nome de blob Olá segue Olá seguindo a convenção de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="60c5b-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="60c5b-196">**Descrição dos campos:**</span><span class="sxs-lookup"><span data-stu-id="60c5b-196">**Description of fields:**</span></span>

|<span data-ttu-id="60c5b-197">value</span><span class="sxs-lookup"><span data-stu-id="60c5b-197">value</span></span>|<span data-ttu-id="60c5b-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="60c5b-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="60c5b-199">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="60c5b-199">Subscription ID</span></span>    |<span data-ttu-id="60c5b-200">ID da saudação assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c5b-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="60c5b-201">Isso está no formato de Guid de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="60c5b-202">Recurso</span><span class="sxs-lookup"><span data-stu-id="60c5b-202">Resource</span></span> |<span data-ttu-id="60c5b-203">Nome do grupo de recursos CDN Olá recurso grupo toowhich Olá pertence.</span><span class="sxs-lookup"><span data-stu-id="60c5b-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="60c5b-204">Nome do Perfil</span><span class="sxs-lookup"><span data-stu-id="60c5b-204">Profile Name</span></span> |<span data-ttu-id="60c5b-205">Nome da saudação perfil CDN</span><span class="sxs-lookup"><span data-stu-id="60c5b-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="60c5b-206">Nome do Ponto de Extremidade</span><span class="sxs-lookup"><span data-stu-id="60c5b-206">Endpoint Name</span></span> |<span data-ttu-id="60c5b-207">Nome do ponto de extremidade CDN da saudação</span><span class="sxs-lookup"><span data-stu-id="60c5b-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="60c5b-208">Ano</span><span class="sxs-lookup"><span data-stu-id="60c5b-208">Year</span></span>|  <span data-ttu-id="60c5b-209">representação de 4 dígitos do ano hello, por exemplo, de 2017</span><span class="sxs-lookup"><span data-stu-id="60c5b-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="60c5b-210">Mês</span><span class="sxs-lookup"><span data-stu-id="60c5b-210">Month</span></span>| <span data-ttu-id="60c5b-211">representação de 2 dígitos do número do mês hello.</span><span class="sxs-lookup"><span data-stu-id="60c5b-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="60c5b-212">01 = janeiro... 12 = dezembro</span><span class="sxs-lookup"><span data-stu-id="60c5b-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="60c5b-213">Dia</span><span class="sxs-lookup"><span data-stu-id="60c5b-213">Day</span></span>|   <span data-ttu-id="60c5b-214">representação de 2 dígitos de dia de saudação do mês de saudação</span><span class="sxs-lookup"><span data-stu-id="60c5b-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="60c5b-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="60c5b-215">PT1H.json</span></span>| <span data-ttu-id="60c5b-216">Armazenamento de dados de análise de saudação real do arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="60c5b-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="60c5b-217">Exportando Olá dados de análise de núcleo tooa arquivo CSV</span><span class="sxs-lookup"><span data-stu-id="60c5b-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="60c5b-218">toomake it tooaccess fácil Olá Core análise, podemos fornecer um código de exemplo para uma ferramenta que permite fazer o download de arquivos JSON de saudação em um formato de arquivo simples separados por vírgulas, que pode ser usado tooeasily criar gráficos ou outras agregações.</span><span class="sxs-lookup"><span data-stu-id="60c5b-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="60c5b-219">Aqui está como você pode usar a ferramenta de saudação:</span><span class="sxs-lookup"><span data-stu-id="60c5b-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="60c5b-220">Visite o link do github Olá: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="60c5b-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="60c5b-221">Baixar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="60c5b-221">Download hello code</span></span>
3.  <span data-ttu-id="60c5b-222">Siga as instruções toocompile e configurar</span><span class="sxs-lookup"><span data-stu-id="60c5b-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="60c5b-223">Execute a ferramenta de saudação</span><span class="sxs-lookup"><span data-stu-id="60c5b-223">Run hello tool</span></span>
5.  <span data-ttu-id="60c5b-224">Arquivo CSV resultante mostra dados de análise de saudação em uma hierarquia simples simple.</span><span class="sxs-lookup"><span data-stu-id="60c5b-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="60c5b-225">Consumir logs de diagnóstico de um repositório do OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="60c5b-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="60c5b-226">Análise de log é um serviço no OMS Operations Management Suite () que monitora o toomaintain de ambientes de nuvem e local sua disponibilidade e desempenho.</span><span class="sxs-lookup"><span data-stu-id="60c5b-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="60c5b-227">Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras análises de tooprovide ferramentas monitoramento em várias origens.</span><span class="sxs-lookup"><span data-stu-id="60c5b-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="60c5b-228">toouse análise de Log, você deve [habilitar registro em log](#enable-logging-with-azure-storage) repositório de análise de Log de OMS do Azure toohello, que é discutido neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60c5b-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="60c5b-229">Usando Olá repositório do OMS</span><span class="sxs-lookup"><span data-stu-id="60c5b-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="60c5b-230">Olá diagrama a seguir mostra a arquitetura de saudação de entradas de saudação e saídas do repositório de saudação:</span><span class="sxs-lookup"><span data-stu-id="60c5b-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Repositório do OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="60c5b-232">*Figura 3 – Repositório do Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="60c5b-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="60c5b-233">Você pode exibir dados de saudação em uma variedade de maneiras usando soluções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="60c5b-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="60c5b-234">Você pode obter as soluções de gerenciamento de saudação [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="60c5b-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="60c5b-235">Você pode instalar as soluções de gerenciamento do Azure marketplace clicando Olá **obtê-lo agora** link na parte inferior da saudação de cada solução.</span><span class="sxs-lookup"><span data-stu-id="60c5b-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="60c5b-236">Adicionar uma solução de gerenciamento de CDN do OMS</span><span class="sxs-lookup"><span data-stu-id="60c5b-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="60c5b-237">Siga essas etapas tooadd uma solução de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="60c5b-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="60c5b-238">Se você ainda não fez isso, entre em toohello portal do Azure usando sua assinatura do Azure e vá tooyour painel.</span><span class="sxs-lookup"><span data-stu-id="60c5b-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="60c5b-239">![Painel do Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="60c5b-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="60c5b-240">Em Olá **novo** folha sob **Marketplace**, selecione **monitoramento + gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="60c5b-242">Em Olá **monitoramento + gerenciamento** folha, clique em **ver todos os**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="60c5b-244">Pesquisar CDN na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-244">Search for CDN in hello search box.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="60c5b-246">Selecione **Análise de Núcleo de CDN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="60c5b-248">Depois de clicar em **criar**, você será perguntado toocreate um novo espaço de trabalho do OMS ou use uma existente.</span><span class="sxs-lookup"><span data-stu-id="60c5b-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="60c5b-250">Selecione o espaço de trabalho de saudação criado antes.</span><span class="sxs-lookup"><span data-stu-id="60c5b-250">Select hello workspace you created before.</span></span> <span data-ttu-id="60c5b-251">Em seguida, você precisa tooadd uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-251">You then need tooadd an automation account.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="60c5b-253">Olá tela a seguir mostra Olá formulário de conta de automação que deve preencher.</span><span class="sxs-lookup"><span data-stu-id="60c5b-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="60c5b-255">Depois que você criou a conta de automação hello, você está pronto tooadd sua solução.</span><span class="sxs-lookup"><span data-stu-id="60c5b-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="60c5b-256">Clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="60c5b-256">Click hello **Create** button.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="60c5b-258">Espaço de trabalho tooyour agora foi adicionada ao sua solução.</span><span class="sxs-lookup"><span data-stu-id="60c5b-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="60c5b-259">Volte tooyour painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60c5b-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="60c5b-261">Clique em espaço de trabalho de análise de Log Olá você criou o espaço de trabalho do toogo tooyour.</span><span class="sxs-lookup"><span data-stu-id="60c5b-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="60c5b-262">Clique em Olá **Portal do OMS** bloco toosee sua nova solução no portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="60c5b-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="60c5b-264">O portal do OMS deve agora ser semelhante Olá tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="60c5b-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="60c5b-266">Clique em uma saudação blocos toosee vários modos de exibição em seus dados.</span><span class="sxs-lookup"><span data-stu-id="60c5b-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="60c5b-268">Você pode rolar para a esquerda ou direita toosee mais blocos que representam a exibições individuais em dados saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="60c5b-269">Clicar em um dos blocos de saudação fornece mais detalhes sobre seus dados.</span><span class="sxs-lookup"><span data-stu-id="60c5b-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Ver tudo](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="60c5b-271">Ofertas e tipos de preços</span><span class="sxs-lookup"><span data-stu-id="60c5b-271">Offers and pricing tiers</span></span>

<span data-ttu-id="60c5b-272">Você pode ver ofertas e camadas de preços para soluções de gerenciamento do OMS e ofertas [aqui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="60c5b-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="60c5b-273">Personalizando exibições</span><span class="sxs-lookup"><span data-stu-id="60c5b-273">Customizing views</span></span>

<span data-ttu-id="60c5b-274">Você pode personalizar o modo de exibição de Olá em seus dados usando Olá **Designer de exibição**.</span><span class="sxs-lookup"><span data-stu-id="60c5b-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="60c5b-275">Vá tooyour espaço de trabalho do OMS e inicia a criação clicando Olá **View Designer** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="60c5b-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="60c5b-277">Você pode arrastar e remova os tipos de gráficos da esquerda hello e preencha Olá detalhes de dados que você deseja tooanalyze em saudação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="60c5b-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="60c5b-279">Atrasos em dados de log</span><span class="sxs-lookup"><span data-stu-id="60c5b-279">Log data delays</span></span>

<span data-ttu-id="60c5b-280">Atrasos em dados de log da Verizon</span><span class="sxs-lookup"><span data-stu-id="60c5b-280">Verizon log data delays</span></span> | <span data-ttu-id="60c5b-281">Atrasos em dados de log da Akamai</span><span class="sxs-lookup"><span data-stu-id="60c5b-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="60c5b-282">Dados de log Verizon é 1 hora atrasados e ocupam too2 toostart de horas que aparece após a conclusão da propagação de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="60c5b-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="60c5b-283">Dados de log do Akamai é 24 horas atrasadas e ocupam too2 toostart de horas que aparece se ele foi criado mais de 24 horas atrás.</span><span class="sxs-lookup"><span data-stu-id="60c5b-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="60c5b-284">Se tiver sido criado recentemente, pode demorar até too25 horas para Olá logs toostart que aparecem.</span><span class="sxs-lookup"><span data-stu-id="60c5b-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="60c5b-285">Tipos de log de diagnóstico para análise de núcleo de CDN</span><span class="sxs-lookup"><span data-stu-id="60c5b-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="60c5b-286">Atualmente, nós oferecemos somente logs de análise de núcleo, que contêm as métricas mostrando estatísticas de resposta HTTP e estatísticas de saída como visto no hello POPs CDN/bordas.</span><span class="sxs-lookup"><span data-stu-id="60c5b-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="60c5b-287">Detalhes das métricas da análise principal</span><span class="sxs-lookup"><span data-stu-id="60c5b-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="60c5b-288">Olá, a tabela a seguir mostra uma lista de métricas disponíveis no hello que logs de análise de núcleo.</span><span class="sxs-lookup"><span data-stu-id="60c5b-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="60c5b-289">Nem todas as métricas estão disponíveis de todos os provedores, embora essas diferenças sejam mínimas.</span><span class="sxs-lookup"><span data-stu-id="60c5b-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="60c5b-290">Olá, a tabela a seguir também mostra se uma determinada métrica está disponível de um provedor.</span><span class="sxs-lookup"><span data-stu-id="60c5b-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="60c5b-291">Observe que as métricas de Olá estão disponíveis para apenas esses pontos de extremidade CDN com tráfego neles.</span><span class="sxs-lookup"><span data-stu-id="60c5b-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="60c5b-292">Métrica</span><span class="sxs-lookup"><span data-stu-id="60c5b-292">Metric</span></span>                     | <span data-ttu-id="60c5b-293">Descrição</span><span class="sxs-lookup"><span data-stu-id="60c5b-293">Description</span></span>   | <span data-ttu-id="60c5b-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="60c5b-294">Verizon</span></span>  | <span data-ttu-id="60c5b-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="60c5b-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="60c5b-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="60c5b-296">RequestCountTotal</span></span>         |<span data-ttu-id="60c5b-297">Número total de ocorrências de solicitação durante esse período</span><span class="sxs-lookup"><span data-stu-id="60c5b-297">Total number of request hits during this period</span></span>| <span data-ttu-id="60c5b-298">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-298">Yes</span></span>  |<span data-ttu-id="60c5b-299">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-299">Yes</span></span>   |
| <span data-ttu-id="60c5b-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="60c5b-301">Contagem de todas as solicitações que resultaram em um código HTTP 2xx (por exemplo, 200, 202)</span><span class="sxs-lookup"><span data-stu-id="60c5b-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="60c5b-302">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-302">Yes</span></span>  |<span data-ttu-id="60c5b-303">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-303">Yes</span></span>   |
| <span data-ttu-id="60c5b-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="60c5b-305">Contagem de todas as solicitações que resultaram em um código HTTP 3xx (por exemplo, 300, 302)</span><span class="sxs-lookup"><span data-stu-id="60c5b-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="60c5b-306">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-306">Yes</span></span>  |<span data-ttu-id="60c5b-307">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-307">Yes</span></span>   |
| <span data-ttu-id="60c5b-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="60c5b-309">Contagem de todas as solicitações que resultaram em um código HTTP 4xx (por exemplo, 400, 404)</span><span class="sxs-lookup"><span data-stu-id="60c5b-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="60c5b-310">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-310">Yes</span></span>   |<span data-ttu-id="60c5b-311">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-311">Yes</span></span>   |
| <span data-ttu-id="60c5b-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="60c5b-313">Contagem de todas as solicitações que resultaram em um código HTTP 5xx (por exemplo, 500, 504)</span><span class="sxs-lookup"><span data-stu-id="60c5b-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="60c5b-314">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-314">Yes</span></span>  |<span data-ttu-id="60c5b-315">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-315">Yes</span></span>   |
| <span data-ttu-id="60c5b-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="60c5b-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="60c5b-317">Contagem de todos os outros códigos HTTP (fora de 2xx a 5xx)</span><span class="sxs-lookup"><span data-stu-id="60c5b-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="60c5b-318">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-318">Yes</span></span>  |<span data-ttu-id="60c5b-319">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-319">Yes</span></span>   |
| <span data-ttu-id="60c5b-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="60c5b-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="60c5b-321">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 200</span><span class="sxs-lookup"><span data-stu-id="60c5b-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="60c5b-322">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-322">No</span></span>   |<span data-ttu-id="60c5b-323">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-323">Yes</span></span>   |
| <span data-ttu-id="60c5b-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="60c5b-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="60c5b-325">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 206</span><span class="sxs-lookup"><span data-stu-id="60c5b-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="60c5b-326">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-326">No</span></span>   |<span data-ttu-id="60c5b-327">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-327">Yes</span></span>   |
| <span data-ttu-id="60c5b-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="60c5b-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="60c5b-329">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 302</span><span class="sxs-lookup"><span data-stu-id="60c5b-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="60c5b-330">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-330">No</span></span>   |<span data-ttu-id="60c5b-331">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-331">Yes</span></span>   |
| <span data-ttu-id="60c5b-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="60c5b-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="60c5b-333">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 304</span><span class="sxs-lookup"><span data-stu-id="60c5b-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="60c5b-334">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-334">No</span></span>   |<span data-ttu-id="60c5b-335">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-335">Yes</span></span>   |
| <span data-ttu-id="60c5b-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="60c5b-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="60c5b-337">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 404</span><span class="sxs-lookup"><span data-stu-id="60c5b-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="60c5b-338">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-338">No</span></span>   |<span data-ttu-id="60c5b-339">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-339">Yes</span></span>   |
| <span data-ttu-id="60c5b-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="60c5b-340">RequestCountCacheHit</span></span> |<span data-ttu-id="60c5b-341">Contagem de todas as solicitações que resultaram em uma Ocorrência no Cache.</span><span class="sxs-lookup"><span data-stu-id="60c5b-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="60c5b-342">Isso significa que o ativo de saudação foi servido diretamente Olá POP toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="60c5b-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="60c5b-343">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-343">Yes</span></span>  |<span data-ttu-id="60c5b-344">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-344">No</span></span>   |
| <span data-ttu-id="60c5b-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="60c5b-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="60c5b-346">Contagem de todas as solicitações que resultaram em uma Perda do Cache.</span><span class="sxs-lookup"><span data-stu-id="60c5b-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="60c5b-347">Isso significa Olá ativo não foi encontrado no cliente de toohello Olá POP mais próximo e, portanto, foi recuperado do hello origem.</span><span class="sxs-lookup"><span data-stu-id="60c5b-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="60c5b-348">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-348">Yes</span></span>   | <span data-ttu-id="60c5b-349">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-349">No</span></span>  |
| <span data-ttu-id="60c5b-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="60c5b-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="60c5b-351">Contagem de todas as solicitações tooan ativo que impediu que está sendo armazenado em cache devido a configuração do usuário tooa na borda de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="60c5b-352">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-352">Yes</span></span>   | <span data-ttu-id="60c5b-353">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-353">No</span></span>  |
| <span data-ttu-id="60c5b-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="60c5b-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="60c5b-355">Contagem de todas as solicitações tooassets impediu que está sendo armazenado em cache pelo controle de Cache do ativo Olá e expira cabeçalhos, que indicam que ele deve não ser armazenado em cache pelo cliente Olá HTTP ou um POP</span><span class="sxs-lookup"><span data-stu-id="60c5b-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="60c5b-356">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-356">Yes</span></span>   |<span data-ttu-id="60c5b-357">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-357">No</span></span>   |
| <span data-ttu-id="60c5b-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="60c5b-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="60c5b-359">Contagem de todas as solicitações com o status de cache não cobertas pelos itens acima.</span><span class="sxs-lookup"><span data-stu-id="60c5b-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="60c5b-360">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-360">Yes</span></span>   | <span data-ttu-id="60c5b-361">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-361">No</span></span>  |
| <span data-ttu-id="60c5b-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="60c5b-362">EgressTotal</span></span> | <span data-ttu-id="60c5b-363">Transferência de dados de saída em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="60c5b-364">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-364">Yes</span></span>   |<span data-ttu-id="60c5b-365">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-365">Yes</span></span>   |
| <span data-ttu-id="60c5b-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="60c5b-367">Transferência de dados de saída* para respostas com códigos de status HTTP 2xx em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="60c5b-368">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-368">Yes</span></span>   |<span data-ttu-id="60c5b-369">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-369">No</span></span>   |
| <span data-ttu-id="60c5b-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="60c5b-371">Transferência de dados de saída para respostas com códigos de status HTTP 3xx em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="60c5b-372">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-372">Yes</span></span>   |<span data-ttu-id="60c5b-373">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-373">No</span></span>   |
| <span data-ttu-id="60c5b-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="60c5b-375">Transferência de dados de saída para respostas com códigos de status HTTP 4xx em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="60c5b-376">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-376">Yes</span></span>   | <span data-ttu-id="60c5b-377">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-377">No</span></span>  |
| <span data-ttu-id="60c5b-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="60c5b-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="60c5b-379">Transferência de dados de saída para respostas com códigos de status HTTP 5xx em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="60c5b-380">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-380">Yes</span></span>   |  <span data-ttu-id="60c5b-381">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-381">No</span></span> |
| <span data-ttu-id="60c5b-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="60c5b-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="60c5b-383">Transferência de dados de saída para respostas com outros códigos de status HTTP em GB</span><span class="sxs-lookup"><span data-stu-id="60c5b-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="60c5b-384">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-384">Yes</span></span>   |<span data-ttu-id="60c5b-385">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-385">No</span></span>   |
| <span data-ttu-id="60c5b-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="60c5b-386">EgressCacheHit</span></span> |  <span data-ttu-id="60c5b-387">Saída de transferência de dados para respostas que foram entregues diretamente do cache CDN Olá em Olá POPs de CDN/bordas</span><span class="sxs-lookup"><span data-stu-id="60c5b-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="60c5b-388">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-388">Yes</span></span>   |  <span data-ttu-id="60c5b-389">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-389">No</span></span> |
| <span data-ttu-id="60c5b-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="60c5b-390">EgressCacheMiss</span></span> | <span data-ttu-id="60c5b-391">Transferência de dados de saída para respostas que não foram encontradas no hello mais próximo servidor POP e recuperadas do servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="60c5b-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="60c5b-392">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-392">Yes</span></span>   |  <span data-ttu-id="60c5b-393">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-393">No</span></span> |
| <span data-ttu-id="60c5b-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="60c5b-394">EgressCacheNoCache</span></span> | <span data-ttu-id="60c5b-395">Transferência de dados de saída para ativos que são impedidos de serem armazenados em cache devido a configuração do usuário tooa na borda da saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="60c5b-396">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-396">Yes</span></span>   |<span data-ttu-id="60c5b-397">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-397">No</span></span>   |
| <span data-ttu-id="60c5b-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="60c5b-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="60c5b-399">Transferência de dados de saída de ativos que são impedidos de serem armazenados em cache por Cache-Control do ativo hello e/ou expira, que indicam que ele deve não ser armazenado em cache em um POP ou pelo cliente Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="60c5b-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="60c5b-400">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-400">Yes</span></span>   | <span data-ttu-id="60c5b-401">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-401">No</span></span>  |
| <span data-ttu-id="60c5b-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="60c5b-402">EgressCacheOthers</span></span> |  <span data-ttu-id="60c5b-403">Transferências de dados de saída para outros cenários de cache.</span><span class="sxs-lookup"><span data-stu-id="60c5b-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="60c5b-404">Sim</span><span class="sxs-lookup"><span data-stu-id="60c5b-404">Yes</span></span>   | <span data-ttu-id="60c5b-405">Não</span><span class="sxs-lookup"><span data-stu-id="60c5b-405">No</span></span>  |

<span data-ttu-id="60c5b-406">* Transferência de dados saída refere-se tootraffic entregue do cliente de toohello servidores POPS de CDN.</span><span class="sxs-lookup"><span data-stu-id="60c5b-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="60c5b-407">Esquema de saudação Logs de análise de núcleo</span><span class="sxs-lookup"><span data-stu-id="60c5b-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="60c5b-408">Todos os logs são armazenados no formato JSON e cada entrada tem campos de cadeia de caracteres hello abaixo de esquema a seguir:</span><span class="sxs-lookup"><span data-stu-id="60c5b-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="60c5b-409">Onde 'tempo' de saudação representa a hora de início de saudação do limite de hora Olá para o qual as estatísticas de saudação é relatada.</span><span class="sxs-lookup"><span data-stu-id="60c5b-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="60c5b-410">Quando uma métrica não tem suporte por um provedor de CDN, em vez de um valor double ou integer, haverá um valor null.</span><span class="sxs-lookup"><span data-stu-id="60c5b-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="60c5b-411">Esse valor nulo indica ausência de saudação de uma métrica, e isso é diferente de um valor de 0.</span><span class="sxs-lookup"><span data-stu-id="60c5b-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="60c5b-412">Observe também que haja um conjunto de métricas por domínio configurado no ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="60c5b-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="60c5b-413">Propriedades de exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="60c5b-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="60c5b-414">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="60c5b-414">Additional resources</span></span>

* [<span data-ttu-id="60c5b-415">Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="60c5b-416">Análise principal por meio do portal suplementar da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="60c5b-417">Log Analytics do OMS do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="60c5b-418">API REST do Log Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="60c5b-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







