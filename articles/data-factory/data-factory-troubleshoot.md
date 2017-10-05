---
title: Solucionar problemas do Data Factory do Azure
description: Saiba como solucionar problemas com o uso do Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="3156b-103">Solucionar problemas do Data Factory</span><span class="sxs-lookup"><span data-stu-id="3156b-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="3156b-104">Esse artigo fornece dicas de solução de problemas ao usar o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3156b-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="3156b-105">Este artigo não lista todos os possíveis problemas ao usar o serviço, mas abrange alguns problemas e dicas de solução geral de problemas.</span><span class="sxs-lookup"><span data-stu-id="3156b-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="3156b-106">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="3156b-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="3156b-107">Erro: a assinatura não está registada para usar o namespace 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="3156b-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="3156b-108">Caso você receba esse erro, o provedor de recursos do Azure Data Factory não foi registrado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3156b-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="3156b-109">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3156b-109">Do the following:</span></span>

1. <span data-ttu-id="3156b-110">Inicie o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3156b-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="3156b-111">Faça logon na conta do Azure usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="3156b-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="3156b-112">Execute o seguinte comando para registrar o provedor do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3156b-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="3156b-113">Problema: Erro não autorizado ao executar um cmdlet da Data Factory</span><span class="sxs-lookup"><span data-stu-id="3156b-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="3156b-114">Você provavelmente não está usando a assinatura ou conta do Azure correta com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3156b-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="3156b-115">Use os cmdlets a seguir para selecionar a assinatura e conta do Azure corretas para usar com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3156b-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="3156b-116">Login-AzureRmAccount - Use a ID de usuário e a senha corretas</span><span class="sxs-lookup"><span data-stu-id="3156b-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="3156b-117">Get-AzureRmSubscription: exiba todas as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="3156b-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="3156b-118">Select-AzureRmSubscription &lt;nome da assinatura&gt; - Selecione a assinatura correta.</span><span class="sxs-lookup"><span data-stu-id="3156b-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="3156b-119">Use a mesma assinatura usada para criar um data factory no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3156b-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="3156b-120">Problema: falha ao inicializar a Configura Expressa do Gateway de Gerenciamento de Dados no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3156b-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="3156b-121">A instalação Expressa do Gateway de Gerenciamento de Dados requer o Internet Explorer ou um navegador da Web compatível com Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="3156b-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="3156b-122">Se a Instalação Expressa não for iniciada, siga um destes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="3156b-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="3156b-123">Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="3156b-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="3156b-124">Se você estiver usando o Chrome, vá para a [loja na Web do Chrome](https://chrome.google.com/webstore/), pesquise a palavra-chave "ClickOnce", escolha uma das extensões do ClickOnce e instale-a.</span><span class="sxs-lookup"><span data-stu-id="3156b-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="3156b-125">Faça o mesmo para o Firefox (instalar o suplemento).</span><span class="sxs-lookup"><span data-stu-id="3156b-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="3156b-126">Clique no botão Abrir menu na barra de ferramentas (três linhas horizontais no canto superior direito), clique em Complementos, pesquise a palavra-chave "ClickOnce", escolha uma das extensões do ClickOnce e instale-a.</span><span class="sxs-lookup"><span data-stu-id="3156b-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="3156b-127">Use o link **Configuração Manual** mostrado na mesma folha no portal.</span><span class="sxs-lookup"><span data-stu-id="3156b-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="3156b-128">Use essa abordagem para baixar o arquivo de instalação e executá-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="3156b-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="3156b-129">Depois que a instalação for bem-sucedida, você verá a caixa de diálogo Configuração do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="3156b-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="3156b-130">Copie a **chave** na tela do portal e use-a no gerenciador de configuração para registrar manualmente o gateway com o serviço.</span><span class="sxs-lookup"><span data-stu-id="3156b-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="3156b-131">Problema: falha ao se conectar ao SQL Server local</span><span class="sxs-lookup"><span data-stu-id="3156b-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="3156b-132">Inicie o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados** no computador do gateway e use a guia **Solução de Problemas** para testar a conexão ao SQL Server do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="3156b-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="3156b-133">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="3156b-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="3156b-134">Problema: as fatias de entrada ficam sempre no estado Aguardando</span><span class="sxs-lookup"><span data-stu-id="3156b-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="3156b-135">As fatias podem estar no estado **Aguardando** devido a vários motivos.</span><span class="sxs-lookup"><span data-stu-id="3156b-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="3156b-136">Um dos motivos comuns é que a propriedade **external** não está definida como **true**.</span><span class="sxs-lookup"><span data-stu-id="3156b-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="3156b-137">Qualquer conjunto de dados que seja produzido fora do escopo do Azure Data Factory deve ser marcado com a propriedade **external** .</span><span class="sxs-lookup"><span data-stu-id="3156b-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="3156b-138">Essa propriedade indica que os dados são externos e não são compatíveis com pipelines no data factory.</span><span class="sxs-lookup"><span data-stu-id="3156b-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="3156b-139">As fatias de dados são marcadas como **Pronto** depois que os dados estão disponíveis no respectivo armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3156b-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="3156b-140">Consulte o exemplo a seguir para o uso da propriedade **external** .</span><span class="sxs-lookup"><span data-stu-id="3156b-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="3156b-141">Como opção, você pode especificar **externalData*** quando definir external como true.</span><span class="sxs-lookup"><span data-stu-id="3156b-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="3156b-142">Consulte o artigo [Conjuntos de dados](data-factory-create-datasets.md) para obter mais detalhes sobre essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="3156b-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="3156b-143">Para resolver o erro, adicione a propriedade **external** e a seção opcional **externalData** à definição de JSON da tabela de entrada e recrie a tabela.</span><span class="sxs-lookup"><span data-stu-id="3156b-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="3156b-144">Problema: Falha na operação de cópia híbrida</span><span class="sxs-lookup"><span data-stu-id="3156b-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="3156b-145">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver as etapas para solucionar os problemas de cópia para/a partir de um armazenamento de dados local usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="3156b-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="3156b-146">Problema: falha no provisionamento sob demanda do HDInsight</span><span class="sxs-lookup"><span data-stu-id="3156b-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="3156b-147">Ao usar um serviço vinculado do tipo HDInsightOnDemand, você deve especificar um linkedServiceName que aponta para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3156b-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="3156b-148">O serviço do Data Factory usa esse armazenamento para armazenar logs e arquivos de suporte para seu cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="3156b-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="3156b-149">Às vezes, o provisionamento de um cluster de HDInsight sob demanda falha com o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="3156b-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="3156b-150">Esse erro normalmente indica que o local da conta de armazenamento especificado no linkedServiceName não está no mesmo local de datacenter, no qual o provisionamento do HDInsight está ocorrendo.</span><span class="sxs-lookup"><span data-stu-id="3156b-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="3156b-151">Exemplo: se seu data factory estiver no Oeste dos EUA e o armazenamento do Azure estiver no Leste dos EUA, o provisionamento sob demanda falhará no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="3156b-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="3156b-152">Além disso, há uma segunda propriedade JSON additionalLinkedServiceNames, em que as contas de armazenamento adicionais podem ser especificadas no HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="3156b-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="3156b-153">Essas contas de armazenamento adicionais vinculadas devem estar no mesmo local que o cluster HDInsight, ou falharão com o mesmo erro.</span><span class="sxs-lookup"><span data-stu-id="3156b-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="3156b-154">Problema: falha de atividade .NET personalizada</span><span class="sxs-lookup"><span data-stu-id="3156b-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="3156b-155">Consulte [Depurar um pipeline com atividade personalizada](data-factory-use-custom-activities.md#troubleshoot-failures) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="3156b-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="3156b-156">Usar o portal do Azure para solucionar o problema</span><span class="sxs-lookup"><span data-stu-id="3156b-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="3156b-157">Usando as folhas do portal</span><span class="sxs-lookup"><span data-stu-id="3156b-157">Using portal blades</span></span>
<span data-ttu-id="3156b-158">Consulte [Monitorar pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="3156b-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="3156b-159">Usando o Aplicativo Monitorar e Gerenciar</span><span class="sxs-lookup"><span data-stu-id="3156b-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="3156b-160">Consulte [Monitorar e gerenciar os pipelines do Data Factory usando o Aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3156b-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="3156b-161">Usar o Azure PowerShell para solucionar o problema</span><span class="sxs-lookup"><span data-stu-id="3156b-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="3156b-162">Usar o Azure PowerShell para solucionar o erro</span><span class="sxs-lookup"><span data-stu-id="3156b-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="3156b-163">Consulte [Monitorar pipelines do Data Factory usando o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3156b-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
