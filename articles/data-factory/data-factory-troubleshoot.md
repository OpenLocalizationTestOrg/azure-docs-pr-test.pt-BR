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
# <a name="troubleshoot-data-factory-issues"></a>Solucionar problemas do Data Factory
Esse artigo fornece dicas de solução de problemas ao usar o Azure Data Factory. Este artigo não lista todos os possíveis problemas de saudação ao usar o serviço hello, mas ele aborda alguns problemas e dicas de solução de problemas gerais.   

## <a name="troubleshooting-tips"></a>Dicas de solução de problemas
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Erro: assinatura de saudação não está registrado toouse namespace 'DataFactory'
Se você receber esse erro, o provedor de recursos do Azure Data Factory Olá não foi registrado no seu computador. Olá a seguir:

1. Inicie o Azure PowerShell.
2. Faça logon no tooyour conta do Azure usando o comando a seguir de saudação.

    ```powershell
    Login-AzureRmAccount
    ```
3. Execute Olá provedor do Azure Data Factory do comando tooregister Olá a seguir.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problema: Erro não autorizado ao executar um cmdlet da Data Factory
Você provavelmente não estiver usando o direito de saudação conta do Azure ou assinatura com hello Azure PowerShell. Use Olá cmdlets tooselect Olá direita toouse de conta e assinatura do Azure com hello Azure PowerShell a seguir.

1. Logon AzureRmAccount - Use Olá direita ID e senha
2. Get-AzureRmSubscription - todos Olá assinaturas para a conta de saudação do modo de exibição.
3. Selecione AzureRmSubscription &lt;nome da assinatura&gt; -assinatura de saudação à direita. Use Olá mesmo que você usar toocreate uma fábrica de dados em Olá portal do Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problema: Não toolaunch Express instalação do Gateway do gerenciamento de dados do portal do Azure
instalação do Express Olá para Olá Data Management Gateway requer o Internet Explorer ou um navegador da web compatível com o Microsoft ClickOnce. Se Olá instalação expressa falhar toostart, faça um dos seguintes hello:

* Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.

    Se você estiver usando o Chrome, vá toohello [repositório na web do Chrome](https://chrome.google.com/webstore/), pesquisar "ClickOnce" palavra-chave with, escolha uma das extensões de ClickOnce hello e instalá-lo.

    Olá mesmo para o Firefox (instalação do suplemento). Botão Abrir Menu na barra de ferramentas da saudação (três linhas horizontais no canto superior direito de saudação), complementos, com "ClickOnce" palavra-chave de pesquisa, escolha uma das extensões de ClickOnce hello e instalá-lo.
* Saudação de uso **instalação Manual** link mostrado em Olá mesmo folha no portal de saudação. Use este arquivo de instalação toodownload abordagem e executá-lo manualmente. Após Olá instalação for bem-sucedida, você verá a caixa de diálogo de configuração de Gateway de gerenciamento de dados de saudação. Saudação de cópia **chave** da tela de portal hello e usar no hello configuration manager toomanually registrar gateway Olá Olá serviço.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problema: Não tooconnect tooon-local do SQL Server
Iniciar **Gerenciador de configuração de Gateway de gerenciamento de dados** Olá máquina de gateway e usar Olá **solução de problemas** guia tootest Olá conexão tooSQL Server do computador do gateway hello. Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problema: as fatias de entrada ficam sempre no estado Aguardando
fatias de saudação poderiam estar em **esperando** estado devido a motivos de toovarious. Um dos motivos comuns de saudação é que hello **externo** propriedade não está definida muito**true**. Qualquer conjunto de dados que é o escopo de produzidos Olá fora do Azure Data Factory deve ser marcado com **externo** propriedade. Essa propriedade indica que dados saudação são externo e não foi feito por qualquer pipelines na fábrica de dados hello. fatias de dados Olá são marcadas como **pronto** quando dados saudação estão disponíveis na respectiva loja de saudação.

Consulte Olá seguinte exemplo para uso de saudação do hello **externo** propriedade. Você pode opcionalmente especificar **externalData*** quando você define tootrue externo.

Consulte o artigo [Conjuntos de dados](data-factory-create-datasets.md) para obter mais detalhes sobre essa propriedade.

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

tooresolve Olá erro, adicione Olá **externo** propriedade e hello opcional **externalData** seção toohello definição de JSON da tabela de entrada hello e recriar tabela de saudação.

### <a name="problem-hybrid-copy-operation-fails"></a>Problema: Falha na operação de cópia híbrida
Consulte [solucionar problemas do gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para etapas tootroubleshoot problemas com copiar para/de dados de um local de armazenam usando Olá Gateway de gerenciamento de dados.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problema: falha no provisionamento sob demanda do HDInsight
Ao usar um serviço vinculado do tipo HDInsightOnDemand, é necessário toospecify um linkedServiceName que aponta tooan armazenamento de BLOBs do Azure. Serviço de fábrica de dados usa esse armazenamento toostore logs e arquivos de suporte para o cluster do HDInsight sob demanda.  Às vezes, o provisionamento de um cluster do HDInsight sob demanda falha com hello erro a seguir:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Esse erro geralmente indica que local Olá Olá da conta de armazenamento especificada na Olá linkedServiceName não está em Olá mesmo data center local onde o provisionamento de HDInsight hello está acontecendo. Exemplo: se sua fábrica de dados está no Oeste dos EUA e Olá armazenamento do Azure está no Leste dos EUA, Olá falha de provisionamento sob demanda no Oeste dos EUA.

Além disso, há uma segunda propriedade JSON additionalLinkedServiceNames, em que as contas de armazenamento adicionais podem ser especificadas no HDInsight sob demanda. Essas contas de armazenamento vinculada adicional devem estar no hello mesmo local que o cluster do HDInsight hello ou falha com hello mesmo erro.

### <a name="problem-custom-net-activity-fails"></a>Problema: falha de atividade .NET personalizada
Consulte [Depurar um pipeline com atividade personalizada](data-factory-use-custom-activities.md#troubleshoot-failures) para obter etapas detalhadas.

## <a name="use-azure-portal-tootroubleshoot"></a>Use tootroubleshoot portal do Azure
### <a name="using-portal-blades"></a>Usando as folhas do portal
Consulte [Monitorar pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para obter as etapas.

### <a name="using-monitor-and-manage-app"></a>Usando o Aplicativo Monitorar e Gerenciar
Consulte [Monitorar e gerenciar os pipelines do Data Factory usando o Aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.

## <a name="use-azure-powershell-tootroubleshoot"></a>Use o PowerShell do Azure tootroubleshoot
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Usar o Azure PowerShell tootroubleshoot um erro
Consulte [Monitorar pipelines do Data Factory usando o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) para obter detalhes.

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
