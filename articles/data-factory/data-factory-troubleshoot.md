---
title: problemas do Azure Data Factory aaaTroubleshoot
description: Saiba como tootroubleshoot problemas com o uso do Azure Data Factory.
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="f83f1-103">Solucionar problemas do Data Factory</span><span class="sxs-lookup"><span data-stu-id="f83f1-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="f83f1-104">Esse artigo fornece dicas de solução de problemas ao usar o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f83f1-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="f83f1-105">Este artigo não lista todos os possíveis problemas de saudação ao usar o serviço hello, mas ele aborda alguns problemas e dicas de solução de problemas gerais.</span><span class="sxs-lookup"><span data-stu-id="f83f1-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="f83f1-106">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="f83f1-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="f83f1-107">Erro: assinatura de saudação não está registrado toouse namespace 'DataFactory'</span><span class="sxs-lookup"><span data-stu-id="f83f1-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="f83f1-108">Se você receber esse erro, o provedor de recursos do Azure Data Factory Olá não foi registrado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f83f1-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="f83f1-109">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f83f1-109">Do hello following:</span></span>

1. <span data-ttu-id="f83f1-110">Inicie o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f83f1-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="f83f1-111">Faça logon no tooyour conta do Azure usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f83f1-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="f83f1-112">Execute Olá provedor do Azure Data Factory do comando tooregister Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="f83f1-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="f83f1-113">Problema: Erro não autorizado ao executar um cmdlet da Data Factory</span><span class="sxs-lookup"><span data-stu-id="f83f1-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="f83f1-114">Você provavelmente não estiver usando o direito de saudação conta do Azure ou assinatura com hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f83f1-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="f83f1-115">Use Olá cmdlets tooselect Olá direita toouse de conta e assinatura do Azure com hello Azure PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="f83f1-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="f83f1-116">Logon AzureRmAccount - Use Olá direita ID e senha</span><span class="sxs-lookup"><span data-stu-id="f83f1-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="f83f1-117">Get-AzureRmSubscription - todos Olá assinaturas para a conta de saudação do modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f83f1-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="f83f1-118">Selecione AzureRmSubscription &lt;nome da assinatura&gt; -assinatura de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="f83f1-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="f83f1-119">Use Olá mesmo que você usar toocreate uma fábrica de dados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f83f1-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="f83f1-120">Problema: Não toolaunch Express instalação do Gateway do gerenciamento de dados do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f83f1-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="f83f1-121">instalação do Express Olá para Olá Data Management Gateway requer o Internet Explorer ou um navegador da web compatível com o Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f83f1-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="f83f1-122">Se Olá instalação expressa falhar toostart, faça um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="f83f1-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="f83f1-123">Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f83f1-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="f83f1-124">Se você estiver usando o Chrome, vá toohello [repositório na web do Chrome](https://chrome.google.com/webstore/), pesquisar "ClickOnce" palavra-chave with, escolha uma das extensões de ClickOnce hello e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="f83f1-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="f83f1-125">Olá mesmo para o Firefox (instalação do suplemento).</span><span class="sxs-lookup"><span data-stu-id="f83f1-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="f83f1-126">Botão Abrir Menu na barra de ferramentas da saudação (três linhas horizontais no canto superior direito de saudação), complementos, com "ClickOnce" palavra-chave de pesquisa, escolha uma das extensões de ClickOnce hello e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="f83f1-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="f83f1-127">Saudação de uso **instalação Manual** link mostrado em Olá mesmo folha no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="f83f1-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="f83f1-128">Use este arquivo de instalação toodownload abordagem e executá-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="f83f1-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="f83f1-129">Após Olá instalação for bem-sucedida, você verá a caixa de diálogo de configuração de Gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f83f1-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="f83f1-130">Saudação de cópia **chave** da tela de portal hello e usar no hello configuration manager toomanually registrar gateway Olá Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="f83f1-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="f83f1-131">Problema: Não tooconnect tooon-local do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f83f1-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="f83f1-132">Iniciar **Gerenciador de configuração de Gateway de gerenciamento de dados** Olá máquina de gateway e usar Olá **solução de problemas** guia tootest Olá conexão tooSQL Server do computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="f83f1-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="f83f1-133">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="f83f1-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="f83f1-134">Problema: as fatias de entrada ficam sempre no estado Aguardando</span><span class="sxs-lookup"><span data-stu-id="f83f1-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="f83f1-135">fatias de saudação poderiam estar em **esperando** estado devido a motivos de toovarious.</span><span class="sxs-lookup"><span data-stu-id="f83f1-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="f83f1-136">Um dos motivos comuns de saudação é que hello **externo** propriedade não está definida muito**true**.</span><span class="sxs-lookup"><span data-stu-id="f83f1-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="f83f1-137">Qualquer conjunto de dados que é o escopo de produzidos Olá fora do Azure Data Factory deve ser marcado com **externo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="f83f1-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="f83f1-138">Essa propriedade indica que dados saudação são externo e não foi feito por qualquer pipelines na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="f83f1-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="f83f1-139">fatias de dados Olá são marcadas como **pronto** quando dados saudação estão disponíveis na respectiva loja de saudação.</span><span class="sxs-lookup"><span data-stu-id="f83f1-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="f83f1-140">Consulte Olá seguinte exemplo para uso de saudação do hello **externo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="f83f1-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="f83f1-141">Você pode opcionalmente especificar **externalData*** quando você define tootrue externo.</span><span class="sxs-lookup"><span data-stu-id="f83f1-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="f83f1-142">Consulte o artigo [Conjuntos de dados](data-factory-create-datasets.md) para obter mais detalhes sobre essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="f83f1-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="f83f1-143">tooresolve Olá erro, adicione Olá **externo** propriedade e hello opcional **externalData** seção toohello definição de JSON da tabela de entrada hello e recriar tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f83f1-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="f83f1-144">Problema: Falha na operação de cópia híbrida</span><span class="sxs-lookup"><span data-stu-id="f83f1-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="f83f1-145">Consulte [solucionar problemas do gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para etapas tootroubleshoot problemas com copiar para/de dados de um local de armazenam usando Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f83f1-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="f83f1-146">Problema: falha no provisionamento sob demanda do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f83f1-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="f83f1-147">Ao usar um serviço vinculado do tipo HDInsightOnDemand, é necessário toospecify um linkedServiceName que aponta tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f83f1-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="f83f1-148">Serviço de fábrica de dados usa esse armazenamento toostore logs e arquivos de suporte para o cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="f83f1-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="f83f1-149">Às vezes, o provisionamento de um cluster do HDInsight sob demanda falha com hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="f83f1-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="f83f1-150">Esse erro geralmente indica que local Olá Olá da conta de armazenamento especificada na Olá linkedServiceName não está em Olá mesmo data center local onde o provisionamento de HDInsight hello está acontecendo.</span><span class="sxs-lookup"><span data-stu-id="f83f1-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="f83f1-151">Exemplo: se sua fábrica de dados está no Oeste dos EUA e Olá armazenamento do Azure está no Leste dos EUA, Olá falha de provisionamento sob demanda no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="f83f1-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="f83f1-152">Além disso, há uma segunda propriedade JSON additionalLinkedServiceNames, em que as contas de armazenamento adicionais podem ser especificadas no HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="f83f1-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="f83f1-153">Essas contas de armazenamento vinculada adicional devem estar no hello mesmo local que o cluster do HDInsight hello ou falha com hello mesmo erro.</span><span class="sxs-lookup"><span data-stu-id="f83f1-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="f83f1-154">Problema: falha de atividade .NET personalizada</span><span class="sxs-lookup"><span data-stu-id="f83f1-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="f83f1-155">Consulte [Depurar um pipeline com atividade personalizada](data-factory-use-custom-activities.md#troubleshoot-failures) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="f83f1-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="f83f1-156">Use tootroubleshoot portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f83f1-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="f83f1-157">Usando as folhas do portal</span><span class="sxs-lookup"><span data-stu-id="f83f1-157">Using portal blades</span></span>
<span data-ttu-id="f83f1-158">Consulte [Monitorar pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="f83f1-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="f83f1-159">Usando o Aplicativo Monitorar e Gerenciar</span><span class="sxs-lookup"><span data-stu-id="f83f1-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="f83f1-160">Consulte [Monitorar e gerenciar os pipelines do Data Factory usando o Aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f83f1-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="f83f1-161">Use o PowerShell do Azure tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="f83f1-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="f83f1-162">Usar o Azure PowerShell tootroubleshoot um erro</span><span class="sxs-lookup"><span data-stu-id="f83f1-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="f83f1-163">Consulte [Monitorar pipelines do Data Factory usando o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f83f1-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
