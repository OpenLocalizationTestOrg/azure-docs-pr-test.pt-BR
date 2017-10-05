---
title: "Análise de logs da CDN do Azure | Microsoft Docs"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="ad882-103">Logs de Diagnóstico para a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="ad882-104">Depois de habilitar a CDN para seu aplicativo, provavelmente você desejará monitorar o uso da CDN, verificar a integridade da entrega e solucionar possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="ad882-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="ad882-105">A CDN do Azure fornece esses recursos com a [Análise de Núcleo de CDN](cdn-analyze-usage-patterns.md) e os [Logs de Diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="ad882-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="ad882-106">Análise de Núcleo de CDN</span><span class="sxs-lookup"><span data-stu-id="ad882-106">CDN Core Analytics</span></span>
<span data-ttu-id="ad882-107">Como um usuário atual da CDN do Azure com o perfil Verizon Standard ou Premium, você já pode exibir a análise principal no portal suplementar acessível por meio da opção “Gerenciar” do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad882-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="ad882-108">Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="ad882-109">Azure Com esse novo recurso, você pode exibir a análise de núcleo e salvá-la em um ou mais destinos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="ad882-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="ad882-110">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-110">Azure Storage account</span></span>
 - <span data-ttu-id="ad882-111">Hubs de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="ad882-112">Repositório do OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ad882-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="ad882-113">Esse recurso está disponível para todos os pontos de extremidade da CDN que pertencem a perfis da CDN Verizon (Standard e Premium) e Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="ad882-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="ad882-114">Os logs de diagnóstico permitem que você exporte métricas de uso básicas do seu ponto de extremidade da CDN para uma variedade de origens para que possa consumi-las de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="ad882-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="ad882-115">Por exemplo, você pode realizar os seguintes tipos de exportação de dados:</span><span class="sxs-lookup"><span data-stu-id="ad882-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="ad882-116">Exportar dados para o Armazenamento de Blobs, exportar para CSV e gerar gráficos no Excel.</span><span class="sxs-lookup"><span data-stu-id="ad882-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="ad882-117">Exportar dados para hubs de eventos e correlacionar com os dados de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad882-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="ad882-118">Exportar dados para o Log Analytics e exibir dados no seu próprio espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="ad882-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="ad882-119">A figura a seguir mostra uma exibição de Análise de Núcleo de CDN típica nos dados.</span><span class="sxs-lookup"><span data-stu-id="ad882-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="ad882-121">*Figura 1 – exibição de Análise de Núcleo de CDN*</span><span class="sxs-lookup"><span data-stu-id="ad882-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="ad882-122">O passo a passo a seguir revisa o esquema dos dados de análise de núcleo, as etapas envolvidas na habilitação do recurso e entrega deles a vários destinos e consumo desses destinos.</span><span class="sxs-lookup"><span data-stu-id="ad882-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="ad882-123">Habilitar registro em log com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="ad882-124">Os logs de diagnóstico estão **desligados** por padrão.</span><span class="sxs-lookup"><span data-stu-id="ad882-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="ad882-125">Siga as etapas abaixo para habilitar o registro em log da Análise de Núcleo de CDN:</span><span class="sxs-lookup"><span data-stu-id="ad882-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="ad882-126">Entre no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad882-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ad882-127">Se você ainda não tiver a CDN habilitada para o fluxo de trabalho, [Habilite a CDN do Azure](cdn-create-new-endpoint.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ad882-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="ad882-128">No portal, navegue até **Perfil CDN**.</span><span class="sxs-lookup"><span data-stu-id="ad882-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="ad882-129">Selecione um perfil CDN e selecione o ponto de extremidade da CDN do qual você deseja habilitar os **Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ad882-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="ad882-131">Acesse a folha **Logs de Diagnóstico** na seção **Monitoramento** e altere o status para **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="ad882-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="ad882-133">Habilitar registro em log com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="ad882-134">Para usar o Armazenamento do Azure é usado para armazenar os logs, selecione **Arquivar em uma conta de armazenamento**, selecione os dias de retenção e clique em **CoreAnalytics** em **Log**.</span><span class="sxs-lookup"><span data-stu-id="ad882-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="ad882-136">*Figura 2 – Registro em log com o Armazenamento do Azure*</span><span class="sxs-lookup"><span data-stu-id="ad882-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="ad882-137">Registro em log com o OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ad882-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="ad882-138">Para usar o OMS Log Analytics para armazenar os logs, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ad882-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="ad882-139">Da folha **Logs de Diagnóstico** sob **Monitoramento**, selecione **Enviar para o Log Analytics** de</span><span class="sxs-lookup"><span data-stu-id="ad882-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="ad882-141">Configure o registro em log do Log Analytics clicando em configurar.</span><span class="sxs-lookup"><span data-stu-id="ad882-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="ad882-142">Isso leva você até uma caixa de diálogo em que você pode selecionar um espaço de trabalho anterior ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="ad882-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="ad882-144">Clique em **Criar Novo Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ad882-144">Click **Create New Workspace**.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="ad882-146">Em seguida, você deve selecionar um novo nome de espaço de trabalho, uma assinatura existente, um grupo de recursos (novo ou existente), um local e um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="ad882-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="ad882-147">Você tem a opção de fixar essa configuração em seu painel.</span><span class="sxs-lookup"><span data-stu-id="ad882-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="ad882-148">Clique em OK para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="ad882-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="ad882-149">Em seguida, você verá seu espaço de trabalho com os nomes do grupo de recursos e do Espaço de Trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="ad882-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="ad882-150">Os nomes devem ser exclusivos e podem usar apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="ad882-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="ad882-151">Espaços e sublinhados não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="ad882-151">Spaces and underscores are not allowed.</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="ad882-153">Em seguida, você recebe uma mensagem curta informando que seu espaço de trabalho foi criado e você retorna à tela de configuração de registro em log.</span><span class="sxs-lookup"><span data-stu-id="ad882-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="ad882-154">Você pode confirmar o nome do espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ad882-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="ad882-156">Depois que você fizer a configuração do Log Analytics, verifique se você também marcou a caixa CoreAnalytics para o registro em log da CDN.</span><span class="sxs-lookup"><span data-stu-id="ad882-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="ad882-157">Se tudo estiver de acordo com sua preferência, clique no botão **Salvar** na parte superior da caixa de diálogo de configuração.</span><span class="sxs-lookup"><span data-stu-id="ad882-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="ad882-159">O botão **Salvar** não está mais ativo e o botão LIGADO/DESLIGADO está agora LIGADO, mas azul em vez de roxo.</span><span class="sxs-lookup"><span data-stu-id="ad882-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="ad882-160">Se você quiser ver seu novo espaço de trabalho do OMS, vá para o painel do Portal do Azure e clique no nome do seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ad882-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="ad882-161">Em seguida, você verá seu espaço de trabalho (verifique se o espaço de trabalho do OMS está realçado à esquerda).</span><span class="sxs-lookup"><span data-stu-id="ad882-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="ad882-162">Clique no bloco do Portal do OMS para ver seu espaço de trabalho no repositório do OMS.</span><span class="sxs-lookup"><span data-stu-id="ad882-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="ad882-164">O repositório do OMS está pronto para registrar dados em log.</span><span class="sxs-lookup"><span data-stu-id="ad882-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="ad882-165">Para consumir esses dados, você deve usar uma [solução do OMS](#consuming-oms-log-analytics-data), abordada posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ad882-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="ad882-166">Para obter mais informações sobre os atrasos em dados de log, consulte [aqui](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="ad882-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="ad882-167">Habilitar o registro em log com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad882-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="ad882-168">Abaixo está um exemplo de como habilitar e obter Logs de Diagnóstico por meio de cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad882-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="ad882-169">Habilitando os Logs de Diagnóstico em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ad882-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="ad882-170">Primeiro, faça logon e selecione uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="ad882-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="ad882-171">Para habilitar os Logs de Diagnóstico em uma Conta de Armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="ad882-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="ad882-172">Para habilitar os logs de diagnóstico em um espaço de trabalho do OMS, use este comando:</span><span class="sxs-lookup"><span data-stu-id="ad882-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="ad882-173">Consumir logs de diagnóstico do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="ad882-174">Esta seção descreve o esquema da análise de núcleo da CDN, como eles são organizados dentro de uma Conta de Armazenamento do Azure e fornece código de exemplo para baixar os logs em um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="ad882-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="ad882-175">Usando o Gerenciador de Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="ad882-176">Antes de poder acessar os dados da análise principal da Conta de Armazenamento do Azure, primeiro você precisa de uma ferramenta para acessar o conteúdo em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ad882-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="ad882-177">Embora haja várias ferramentas disponíveis no mercado, a que recomendamos é o Gerenciador de Armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ad882-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="ad882-178">Você pode baixar a ferramenta [aqui](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ad882-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="ad882-179">Depois de baixar e instalar o software, configure-o para usar a mesma Conta de Armazenamento do Azure que foi configurada como um destino para os Logs de Diagnóstico da CDN.</span><span class="sxs-lookup"><span data-stu-id="ad882-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="ad882-180">Abra o **Gerenciador de Armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="ad882-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="ad882-181">Localize a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ad882-181">Locate the storage account</span></span>
3.  <span data-ttu-id="ad882-182">Vá para o nó **"Contêineres de Blob"** nessa conta de armazenamento e expanda o nó</span><span class="sxs-lookup"><span data-stu-id="ad882-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="ad882-183">Selecione o contêiner chamado **“insights-logs-coreanalytics”** e clique duas vezes nele</span><span class="sxs-lookup"><span data-stu-id="ad882-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="ad882-184">Os resultados são mostrados no painel da direita começando com o primeiro nível, que se parece com **“resourceId=”**.</span><span class="sxs-lookup"><span data-stu-id="ad882-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="ad882-185">Continue clicando em todo o caminho até encontrar o arquivo **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="ad882-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="ad882-186">Consulte a observação a seguir para obter a explicação do caminho.</span><span class="sxs-lookup"><span data-stu-id="ad882-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="ad882-187">Cada blob **PT1H.json** representa os logs de análise de uma hora para um ponto de extremidade da CDN específico ou seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ad882-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="ad882-188">O esquema do conteúdo desse arquivo JSON é descrito na seção Esquema dos logs de análise principal</span><span class="sxs-lookup"><span data-stu-id="ad882-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="ad882-189">**Formato de caminho de blob**</span><span class="sxs-lookup"><span data-stu-id="ad882-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="ad882-190">Os logs de análise principal são gerados a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ad882-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="ad882-191">Todos os dados de uma hora são coletados e armazenados em um único Blob do Azure como um conteúdo JSON.</span><span class="sxs-lookup"><span data-stu-id="ad882-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="ad882-192">O caminho para esse Blob do Azure aparece como se houvesse uma estrutura hierárquica.</span><span class="sxs-lookup"><span data-stu-id="ad882-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="ad882-193">Isso é porque a ferramenta de Gerenciador de Armazenamento interpreta '/' como um separador de diretório e mostra a hierarquia para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="ad882-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="ad882-194">Na verdade, o caminho inteiro representa apenas o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="ad882-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="ad882-195">Esse nome do blob segue a convenção de nomenclatura abaixo</span><span class="sxs-lookup"><span data-stu-id="ad882-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="ad882-196">**Descrição dos campos:**</span><span class="sxs-lookup"><span data-stu-id="ad882-196">**Description of fields:**</span></span>

|<span data-ttu-id="ad882-197">value</span><span class="sxs-lookup"><span data-stu-id="ad882-197">value</span></span>|<span data-ttu-id="ad882-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad882-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="ad882-199">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="ad882-199">Subscription ID</span></span>    |<span data-ttu-id="ad882-200">ID da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad882-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="ad882-201">Esse é o formato de Guid.</span><span class="sxs-lookup"><span data-stu-id="ad882-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="ad882-202">Recurso</span><span class="sxs-lookup"><span data-stu-id="ad882-202">Resource</span></span> |<span data-ttu-id="ad882-203">Nome do Grupo   Nome do grupo de recursos ao qual os recursos da CDN pertencem.</span><span class="sxs-lookup"><span data-stu-id="ad882-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="ad882-204">Nome do Perfil</span><span class="sxs-lookup"><span data-stu-id="ad882-204">Profile Name</span></span> |<span data-ttu-id="ad882-205">Nome do perfil CDN</span><span class="sxs-lookup"><span data-stu-id="ad882-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="ad882-206">Nome do Ponto de Extremidade</span><span class="sxs-lookup"><span data-stu-id="ad882-206">Endpoint Name</span></span> |<span data-ttu-id="ad882-207">Nome do ponto de extremidade da CDN</span><span class="sxs-lookup"><span data-stu-id="ad882-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="ad882-208">Ano</span><span class="sxs-lookup"><span data-stu-id="ad882-208">Year</span></span>|  <span data-ttu-id="ad882-209">Representação de 4 dígitos do ano, por exemplo, 2017</span><span class="sxs-lookup"><span data-stu-id="ad882-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="ad882-210">Mês</span><span class="sxs-lookup"><span data-stu-id="ad882-210">Month</span></span>| <span data-ttu-id="ad882-211">Representação de 2 dígitos do número do mês.</span><span class="sxs-lookup"><span data-stu-id="ad882-211">2-digit representation of the month number.</span></span> <span data-ttu-id="ad882-212">01 = janeiro... 12 = dezembro</span><span class="sxs-lookup"><span data-stu-id="ad882-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="ad882-213">Dia</span><span class="sxs-lookup"><span data-stu-id="ad882-213">Day</span></span>|   <span data-ttu-id="ad882-214">Representação de 2 dígitos do dia do mês</span><span class="sxs-lookup"><span data-stu-id="ad882-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="ad882-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="ad882-215">PT1H.json</span></span>| <span data-ttu-id="ad882-216">Arquivo JSON real em que os dados da análise são armazenados</span><span class="sxs-lookup"><span data-stu-id="ad882-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="ad882-217">Exportando os dados da análise principal para um arquivo CSV</span><span class="sxs-lookup"><span data-stu-id="ad882-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="ad882-218">Para facilitar o acesso à Análise de Núcleo, fornecemos um código de exemplo para uma ferramenta, que permite baixar os arquivos JSON em um formato de arquivo simples separado por vírgula que pode ser usado para criar facilmente gráficos ou outras agregações.</span><span class="sxs-lookup"><span data-stu-id="ad882-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="ad882-219">Aqui está como você pode usar a ferramenta:</span><span class="sxs-lookup"><span data-stu-id="ad882-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="ad882-220">Visite o link do GitHub: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="ad882-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="ad882-221">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="ad882-221">Download the code</span></span>
3.  <span data-ttu-id="ad882-222">Siga as instruções para compilar e configurar</span><span class="sxs-lookup"><span data-stu-id="ad882-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="ad882-223">Execute a ferramenta</span><span class="sxs-lookup"><span data-stu-id="ad882-223">Run the tool</span></span>
5.  <span data-ttu-id="ad882-224">O arquivo CSV resultante mostra os dados de análise em uma hierarquia simples.</span><span class="sxs-lookup"><span data-stu-id="ad882-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="ad882-225">Consumir logs de diagnóstico de um repositório do OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ad882-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="ad882-226">O Log Analytics é um serviço no Operations Management Suite (OMS) que monitora seus ambientes na nuvem e locais a fim de manter a disponibilidade e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="ad882-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="ad882-227">Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras ferramentas de monitoramento para fornecer análise de várias fontes.</span><span class="sxs-lookup"><span data-stu-id="ad882-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="ad882-228">Para usar o Log Analytics, você deve [habilitar o registro em log](#enable-logging-with-azure-storage) para o repositório do OMS Log Analytics do Azure, que é discutido anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ad882-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="ad882-229">Usando o repositório do OMS</span><span class="sxs-lookup"><span data-stu-id="ad882-229">Using the OMS Repository</span></span>

 <span data-ttu-id="ad882-230">O diagrama a seguir mostra a arquitetura das entradas e saídas do repositório:</span><span class="sxs-lookup"><span data-stu-id="ad882-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![Repositório do OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="ad882-232">*Figura 3 – Repositório do Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="ad882-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="ad882-233">Você pode exibir os dados de várias maneiras usando soluções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ad882-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="ad882-234">Você pode obter as soluções de gerenciamento do [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="ad882-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="ad882-235">Você pode instalar as soluções de gerenciamento do Azure marketplace clicando no link **Obtenha agora** na parte inferior de cada solução.</span><span class="sxs-lookup"><span data-stu-id="ad882-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="ad882-236">Adicionar uma solução de gerenciamento de CDN do OMS</span><span class="sxs-lookup"><span data-stu-id="ad882-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="ad882-237">Siga estas etapas para adicionar uma solução de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="ad882-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="ad882-238">Se ainda não tiver feito isso, entre no Portal do Azure usando a sua assinatura do Azure e vá para o seu painel.</span><span class="sxs-lookup"><span data-stu-id="ad882-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="ad882-239">![Painel do Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="ad882-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="ad882-240">Na folha **Novo** em **Marketplace**, selecione **Monitoramento + gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="ad882-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="ad882-242">Na folha **Monitoramento + gerenciamento**, clique em **Ver todos**.</span><span class="sxs-lookup"><span data-stu-id="ad882-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="ad882-244">Pesquise pela CDN na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ad882-244">Search for CDN in the search box.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="ad882-246">Selecione **Análise de Núcleo de CDN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ad882-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="ad882-248">Depois de clicar em **Criar**, você deverá criar um novo espaço de trabalho do OMS ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="ad882-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="ad882-250">Selecione o espaço de trabalho que você criou antes.</span><span class="sxs-lookup"><span data-stu-id="ad882-250">Select the workspace you created before.</span></span> <span data-ttu-id="ad882-251">Em seguida, você precisa adicionar uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="ad882-251">You then need to add an automation account.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="ad882-253">A tela a seguir mostra o formulário de conta de automação que você deve preencher.</span><span class="sxs-lookup"><span data-stu-id="ad882-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="ad882-255">Depois que você criar a conta de automação, você estará pronto para adicionar sua solução.</span><span class="sxs-lookup"><span data-stu-id="ad882-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="ad882-256">Selecione o botão **Criar** .</span><span class="sxs-lookup"><span data-stu-id="ad882-256">Click the **Create** button.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="ad882-258">A solução foi agora adicionada ao espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ad882-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="ad882-259">Volte para seu painel do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad882-259">Go back to your Azure portal Dashboard.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="ad882-261">Clique no espaço de trabalho do Log Analytics que você criou para ir para o seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ad882-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="ad882-262">Clique no bloco **Portal do OMS** para ver a nova solução no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="ad882-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="ad882-264">O portal do OMS deve agora ser semelhante à tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad882-264">Your OMS portal should now look like the following screen:</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="ad882-266">Clique em um dos blocos para ver várias exibições nos dados.</span><span class="sxs-lookup"><span data-stu-id="ad882-266">Click one of the tiles to see several views into your data.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="ad882-268">Você pode rolar à esquerda ou direita para ver mais blocos representando exibições individuais nos dados.</span><span class="sxs-lookup"><span data-stu-id="ad882-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="ad882-269">Clicar em um dos blocos lhe fornece mais detalhes sobre seus dados.</span><span class="sxs-lookup"><span data-stu-id="ad882-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![Ver tudo](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="ad882-271">Ofertas e tipos de preços</span><span class="sxs-lookup"><span data-stu-id="ad882-271">Offers and pricing tiers</span></span>

<span data-ttu-id="ad882-272">Você pode ver ofertas e camadas de preços para soluções de gerenciamento do OMS e ofertas [aqui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="ad882-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="ad882-273">Personalizando exibições</span><span class="sxs-lookup"><span data-stu-id="ad882-273">Customizing views</span></span>

<span data-ttu-id="ad882-274">Você pode personalizar a exibição em seus dados usando o **Designer de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="ad882-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="ad882-275">Acesse seu espaço de trabalho do OMS e comece a criação clicando no bloco **Designer de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="ad882-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="ad882-277">Você pode arrastar e soltar os tipos de gráficos da esquerda e preencher os detalhes de dados que você deseja analisar à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ad882-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="ad882-279">Atrasos em dados de log</span><span class="sxs-lookup"><span data-stu-id="ad882-279">Log data delays</span></span>

<span data-ttu-id="ad882-280">Atrasos em dados de log da Verizon</span><span class="sxs-lookup"><span data-stu-id="ad882-280">Verizon log data delays</span></span> | <span data-ttu-id="ad882-281">Atrasos em dados de log da Akamai</span><span class="sxs-lookup"><span data-stu-id="ad882-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="ad882-282">Os dados de log de Verizon estão 1 hora atrasados e demoram até 2 horas para começar a aparecer após a conclusão da propagação do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ad882-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="ad882-283">Os dados de log de Akamai estão 24 horas atrasados e demoram até 2 horas para começar a aparecer se tiverem sido criados há mais de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ad882-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="ad882-284">Se eles tiverem sido criados recentemente, poderá demorar até 25 horas para os logs começarem a aparecer.</span><span class="sxs-lookup"><span data-stu-id="ad882-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="ad882-285">Tipos de log de diagnóstico para análise de núcleo de CDN</span><span class="sxs-lookup"><span data-stu-id="ad882-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="ad882-286">Atualmente, oferecemos somente logs de Análise de Núcleo, que contêm as métricas mostrando estatísticas de resposta HTTP e estatísticas de saída como visto nos POPs/bordas da CDN.</span><span class="sxs-lookup"><span data-stu-id="ad882-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="ad882-287">Detalhes das métricas da análise principal</span><span class="sxs-lookup"><span data-stu-id="ad882-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="ad882-288">A tabela a seguir mostra uma lista de métricas disponíveis nos logs de análise de núcleo.</span><span class="sxs-lookup"><span data-stu-id="ad882-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="ad882-289">Nem todas as métricas estão disponíveis de todos os provedores, embora essas diferenças sejam mínimas.</span><span class="sxs-lookup"><span data-stu-id="ad882-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="ad882-290">A tabela a seguir também mostra se uma determinada métrica está disponível de um provedor.</span><span class="sxs-lookup"><span data-stu-id="ad882-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="ad882-291">Observe que as métricas estão disponíveis apenas para os pontos de extremidade da CDN que têm tráfego neles.</span><span class="sxs-lookup"><span data-stu-id="ad882-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="ad882-292">Métrica</span><span class="sxs-lookup"><span data-stu-id="ad882-292">Metric</span></span>                     | <span data-ttu-id="ad882-293">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad882-293">Description</span></span>   | <span data-ttu-id="ad882-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="ad882-294">Verizon</span></span>  | <span data-ttu-id="ad882-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="ad882-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="ad882-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="ad882-296">RequestCountTotal</span></span>         |<span data-ttu-id="ad882-297">Número total de ocorrências de solicitação durante esse período</span><span class="sxs-lookup"><span data-stu-id="ad882-297">Total number of request hits during this period</span></span>| <span data-ttu-id="ad882-298">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-298">Yes</span></span>  |<span data-ttu-id="ad882-299">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-299">Yes</span></span>   |
| <span data-ttu-id="ad882-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ad882-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="ad882-301">Contagem de todas as solicitações que resultaram em um código HTTP 2xx (por exemplo, 200, 202)</span><span class="sxs-lookup"><span data-stu-id="ad882-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="ad882-302">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-302">Yes</span></span>  |<span data-ttu-id="ad882-303">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-303">Yes</span></span>   |
| <span data-ttu-id="ad882-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ad882-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="ad882-305">Contagem de todas as solicitações que resultaram em um código HTTP 3xx (por exemplo, 300, 302)</span><span class="sxs-lookup"><span data-stu-id="ad882-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="ad882-306">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-306">Yes</span></span>  |<span data-ttu-id="ad882-307">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-307">Yes</span></span>   |
| <span data-ttu-id="ad882-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ad882-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="ad882-309">Contagem de todas as solicitações que resultaram em um código HTTP 4xx (por exemplo, 400, 404)</span><span class="sxs-lookup"><span data-stu-id="ad882-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="ad882-310">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-310">Yes</span></span>   |<span data-ttu-id="ad882-311">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-311">Yes</span></span>   |
| <span data-ttu-id="ad882-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ad882-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="ad882-313">Contagem de todas as solicitações que resultaram em um código HTTP 5xx (por exemplo, 500, 504)</span><span class="sxs-lookup"><span data-stu-id="ad882-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="ad882-314">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-314">Yes</span></span>  |<span data-ttu-id="ad882-315">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-315">Yes</span></span>   |
| <span data-ttu-id="ad882-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ad882-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="ad882-317">Contagem de todos os outros códigos HTTP (fora de 2xx a 5xx)</span><span class="sxs-lookup"><span data-stu-id="ad882-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="ad882-318">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-318">Yes</span></span>  |<span data-ttu-id="ad882-319">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-319">Yes</span></span>   |
| <span data-ttu-id="ad882-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="ad882-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="ad882-321">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 200</span><span class="sxs-lookup"><span data-stu-id="ad882-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="ad882-322">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-322">No</span></span>   |<span data-ttu-id="ad882-323">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-323">Yes</span></span>   |
| <span data-ttu-id="ad882-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="ad882-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="ad882-325">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 206</span><span class="sxs-lookup"><span data-stu-id="ad882-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="ad882-326">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-326">No</span></span>   |<span data-ttu-id="ad882-327">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-327">Yes</span></span>   |
| <span data-ttu-id="ad882-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="ad882-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="ad882-329">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 302</span><span class="sxs-lookup"><span data-stu-id="ad882-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="ad882-330">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-330">No</span></span>   |<span data-ttu-id="ad882-331">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-331">Yes</span></span>   |
| <span data-ttu-id="ad882-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="ad882-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="ad882-333">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 304</span><span class="sxs-lookup"><span data-stu-id="ad882-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="ad882-334">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-334">No</span></span>   |<span data-ttu-id="ad882-335">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-335">Yes</span></span>   |
| <span data-ttu-id="ad882-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="ad882-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="ad882-337">Contagem de todas as solicitações que resultaram em um código de resposta HTTP 404</span><span class="sxs-lookup"><span data-stu-id="ad882-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="ad882-338">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-338">No</span></span>   |<span data-ttu-id="ad882-339">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-339">Yes</span></span>   |
| <span data-ttu-id="ad882-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="ad882-340">RequestCountCacheHit</span></span> |<span data-ttu-id="ad882-341">Contagem de todas as solicitações que resultaram em uma Ocorrência no Cache.</span><span class="sxs-lookup"><span data-stu-id="ad882-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="ad882-342">Isso significa que o ativo foi servido diretamente do POP para o cliente.</span><span class="sxs-lookup"><span data-stu-id="ad882-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="ad882-343">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-343">Yes</span></span>  |<span data-ttu-id="ad882-344">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-344">No</span></span>   |
| <span data-ttu-id="ad882-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ad882-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="ad882-346">Contagem de todas as solicitações que resultaram em uma Perda do Cache.</span><span class="sxs-lookup"><span data-stu-id="ad882-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="ad882-347">Isso significa que o ativo não foi encontrado no POP mais próximo ao cliente e, portanto, foi recuperado da Origem.</span><span class="sxs-lookup"><span data-stu-id="ad882-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="ad882-348">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-348">Yes</span></span>   | <span data-ttu-id="ad882-349">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-349">No</span></span>  |
| <span data-ttu-id="ad882-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ad882-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="ad882-351">Contagem de todas as solicitações para um ativo que são impedidas de serem armazenadas em cache devido a uma configuração do usuário na borda.</span><span class="sxs-lookup"><span data-stu-id="ad882-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="ad882-352">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-352">Yes</span></span>   | <span data-ttu-id="ad882-353">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-353">No</span></span>  |
| <span data-ttu-id="ad882-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ad882-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="ad882-355">Contagem de todas as solicitações para ativos que são impedidas de serem armazenadas em cache pelos cabeçalhos Cache-Control e Expires do ativo, que indicam que não devem ser armazenadas em cache em um POP ou pelo cliente HTTP</span><span class="sxs-lookup"><span data-stu-id="ad882-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="ad882-356">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-356">Yes</span></span>   |<span data-ttu-id="ad882-357">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-357">No</span></span>   |
| <span data-ttu-id="ad882-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ad882-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="ad882-359">Contagem de todas as solicitações com o status de cache não cobertas pelos itens acima.</span><span class="sxs-lookup"><span data-stu-id="ad882-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="ad882-360">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-360">Yes</span></span>   | <span data-ttu-id="ad882-361">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-361">No</span></span>  |
| <span data-ttu-id="ad882-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="ad882-362">EgressTotal</span></span> | <span data-ttu-id="ad882-363">Transferência de dados de saída em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="ad882-364">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-364">Yes</span></span>   |<span data-ttu-id="ad882-365">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-365">Yes</span></span>   |
| <span data-ttu-id="ad882-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ad882-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="ad882-367">Transferência de dados de saída* para respostas com códigos de status HTTP 2xx em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="ad882-368">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-368">Yes</span></span>   |<span data-ttu-id="ad882-369">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-369">No</span></span>   |
| <span data-ttu-id="ad882-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ad882-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="ad882-371">Transferência de dados de saída para respostas com códigos de status HTTP 3xx em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="ad882-372">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-372">Yes</span></span>   |<span data-ttu-id="ad882-373">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-373">No</span></span>   |
| <span data-ttu-id="ad882-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ad882-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="ad882-375">Transferência de dados de saída para respostas com códigos de status HTTP 4xx em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ad882-376">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-376">Yes</span></span>   | <span data-ttu-id="ad882-377">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-377">No</span></span>  |
| <span data-ttu-id="ad882-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ad882-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="ad882-379">Transferência de dados de saída para respostas com códigos de status HTTP 5xx em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ad882-380">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-380">Yes</span></span>   |  <span data-ttu-id="ad882-381">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-381">No</span></span> |
| <span data-ttu-id="ad882-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ad882-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="ad882-383">Transferência de dados de saída para respostas com outros códigos de status HTTP em GB</span><span class="sxs-lookup"><span data-stu-id="ad882-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="ad882-384">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-384">Yes</span></span>   |<span data-ttu-id="ad882-385">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-385">No</span></span>   |
| <span data-ttu-id="ad882-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="ad882-386">EgressCacheHit</span></span> |  <span data-ttu-id="ad882-387">Transferência de dados de saída para respostas que foram entregues diretamente do cache da CDN nos POPs/Bordas da CDN</span><span class="sxs-lookup"><span data-stu-id="ad882-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="ad882-388">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-388">Yes</span></span>   |  <span data-ttu-id="ad882-389">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-389">No</span></span> |
| <span data-ttu-id="ad882-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ad882-390">EgressCacheMiss</span></span> | <span data-ttu-id="ad882-391">Transferência de dados de saída de respostas que não foram encontradas no servidor POP mais próximo e foram recuperadas do servidor de origem</span><span class="sxs-lookup"><span data-stu-id="ad882-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="ad882-392">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-392">Yes</span></span>   |  <span data-ttu-id="ad882-393">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-393">No</span></span> |
| <span data-ttu-id="ad882-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ad882-394">EgressCacheNoCache</span></span> | <span data-ttu-id="ad882-395">Transferência de dados de saída para ativos que são impedidos de serem armazenados em cache devido a uma configuração do usuário na borda.</span><span class="sxs-lookup"><span data-stu-id="ad882-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="ad882-396">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-396">Yes</span></span>   |<span data-ttu-id="ad882-397">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-397">No</span></span>   |
| <span data-ttu-id="ad882-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ad882-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="ad882-399">Transferência de dados de saída para ativos que são impedidos de serem armazenados em cache pelos cabeçalhos Cache-Control e/ou Expires do ativo, que indicam que não devem ser armazenadas em cache em um POP ou pelo cliente HTTP</span><span class="sxs-lookup"><span data-stu-id="ad882-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="ad882-400">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-400">Yes</span></span>   | <span data-ttu-id="ad882-401">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-401">No</span></span>  |
| <span data-ttu-id="ad882-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ad882-402">EgressCacheOthers</span></span> |  <span data-ttu-id="ad882-403">Transferências de dados de saída para outros cenários de cache.</span><span class="sxs-lookup"><span data-stu-id="ad882-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="ad882-404">Sim</span><span class="sxs-lookup"><span data-stu-id="ad882-404">Yes</span></span>   | <span data-ttu-id="ad882-405">Não</span><span class="sxs-lookup"><span data-stu-id="ad882-405">No</span></span>  |

<span data-ttu-id="ad882-406">*Transferência de dados de saída refere-se ao tráfego entregue de servidores POP da CDN para o cliente.</span><span class="sxs-lookup"><span data-stu-id="ad882-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="ad882-407">Esquema dos logs de análise principal</span><span class="sxs-lookup"><span data-stu-id="ad882-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="ad882-408">Todos os logs são armazenados no formato JSON e cada entrada tem campos de cadeia de caracteres que seguem o esquema abaixo:</span><span class="sxs-lookup"><span data-stu-id="ad882-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="ad882-409">Em que ‘time’ representa a hora de início do limite da hora pela qual as estatísticas são relatadas.</span><span class="sxs-lookup"><span data-stu-id="ad882-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="ad882-410">Quando uma métrica não tem suporte por um provedor de CDN, em vez de um valor double ou integer, haverá um valor null.</span><span class="sxs-lookup"><span data-stu-id="ad882-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="ad882-411">Esse valor null indica a ausência de uma métrica e isso é diferente de um valor 0.</span><span class="sxs-lookup"><span data-stu-id="ad882-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="ad882-412">Observe também que haverá um conjunto dessas métricas por domínio configurado no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ad882-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="ad882-413">Propriedades de exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="ad882-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="ad882-414">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ad882-414">Additional resources</span></span>

* [<span data-ttu-id="ad882-415">Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="ad882-416">Análise principal por meio do portal suplementar da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="ad882-417">Log Analytics do OMS do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="ad882-418">API REST do Log Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="ad882-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







