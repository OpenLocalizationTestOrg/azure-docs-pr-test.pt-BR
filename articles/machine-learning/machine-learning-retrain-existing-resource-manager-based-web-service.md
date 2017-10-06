---
title: "serviço web de aaaRetrain uma previsão existente | Microsoft Docs"
description: "Saiba como tooretrain um modelo e atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Readaptar um serviço Web de previsão existente
Este documento descreve Olá treinamento processo para Olá cenário a seguir:

* Você tem um experimento de treinamento e um experimento de previsão implantado como um serviço Web operacionalizado.
* Você tem novos dados que você deseja que seu tooperform de toouse de serviço web de previsão sua pontuação.

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

Começando com o serviço da web existente e experiências, você precisa toofollow estas etapas:

1. Atualize o modelo de saudação.
   1. Modifique seu tooallow de experiência de treinamento para as entradas e saídas.
   2. Implante a experiência de treinamento hello como um serviço web novos treinamentos.
   3. Use modelo de saudação do teste de treinamento Olá serviço de execução de lote (BES) tooretrain.
2. Use o teste da previsão de Olá Olá aprendizado de máquina do Azure PowerShell cmdlets tooupdate.
   1. Entrar tooyour conta do Azure Resource Manager.
   2. Obter definição de serviço web hello.
   3. Exporte a definição de serviço web hello como JSON.
   4. Atualização Olá toohello ilearner blob de referência no hello JSON.
   5. Importe Olá JSON em uma definição de serviço web.
   6. Atualize o serviço web de saudação com uma nova definição de serviço web.

## <a name="deploy-hello-training-experiment"></a>Implantar a experiência de treinamento Olá
experiência de treinamento toodeploy hello como um serviço web novos treinamentos, você deve adicionar o modelo toohello do web service entradas e saídas. Conectando-se um *saída do serviço Web* da experiência do módulo toohello  *[treinar modelo] [ train-model]*  módulo, habilitar Olá experiência de treinamento tooproduce um novo modelo treinado que você pode usar em sua experiência de previsão. Se você tiver um *avaliar modelo* módulo, você também pode anexar resultados da avaliação do web service saída tooget hello como saída.

tooupdate sua experiência de treinamento:

1. Conecte-se um *entrada de serviço da Web* dados tooyour do módulo de entrada (por exemplo, um *limpar dados ausentes* módulo). Geralmente, você deseja tooensure seus dados de entrada são processados em Olá mesma forma que os dados de treinamento original.
2. Conecte-se um *saída do serviço Web* saída do módulo toohello do seu *treinar modelo* módulo.
3. Se você tiver um *avaliar modelo* módulo e você deseja que os resultados de avaliação do toooutput hello, conecte-se um *saída do serviço Web* saída do módulo toohello do seu *avaliar modelo* módulo.

Execute seu experimento.

Em seguida, você deve implantar Olá experiência de treinamento como um serviço web que produz um modelo treinado e resultados de avaliação do modelo.  

Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web**e, em seguida, selecione **implantar o serviço de Web [novo]**. portal de serviços de Web de aprendizado de máquina do Azure Olá abre toohello **implantar o serviço da Web** página. Digite um nome para o serviço Web, escolha um plano de pagamento e clique em **Implantar**. Somente você pode usar o método de execução de lote hello para a criação de modelos treinados.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Treinar novamente o modelo de saudação com novos dados usando BES
Neste exemplo, estamos usando c# toocreate Olá treinamento de aplicativo. Você também pode usar essa tarefa Python ou R tooaccomplish de código de exemplo.

Olá toocall treinamento APIs:

1. Crie um aplicativo de console C# no Visual Studio: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.
2. Entrar toohello portal de serviços de Web do aprendizado de máquina.
3. Clique em Olá web service que você está trabalhando.
4. Clique em **Consumo**.
5. Na parte inferior de saudação do hello **consumir** página Olá **código de exemplo** seção, clique em **lote**.
6. Copie Olá c# código de exemplo para execução em lotes e cole-o no arquivo Program.cs de saudação. Certifique-se de que o namespace Olá permanece intacto.

Adicione o pacote de NuGet Olá Microsoft.AspNet.WebApi.Client, conforme especificado nos comentários de saudação. tooadd Olá referência tooMicrosoft.WindowsAzure.Storage.dll, talvez seja necessário primeiro Olá tooinstall [biblioteca de cliente para serviços de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

Olá, seguinte captura de tela mostra Olá **consumir** página no portal de serviços de Web de aprendizado de máquina do Azure hello.

![Página Consumir][1]

### <a name="update-hello-apikey-declaration"></a>Atualizar a declaração de apikey Olá
Localizar Olá **apikey** declaração:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Em Olá **informações básicas de consumo** seção Olá **consumir** página, localize a chave primária hello e copiá-lo toohello **apikey** declaração.

### <a name="update-hello-azure-storage-information"></a>Atualizar informações de armazenamento do Azure Olá
Olá, código de exemplo do BES carrega um arquivo de um armazenamento de tooAzure de disco local (por exemplo, "C:\temp\CensusIpnput.csv"), processa e grava tooAzure armazenamento do retorno de resultados de saudação.  

informações de armazenamento do Azure do tooupdate hello, você deve recuperar informações de nome, a chave e o contêiner para sua conta de armazenamento de saudação portal clássico do Azure e, em seguida, atualização Olá correspondi após a execução de sua experiência, Olá resultante de conta de armazenamento Olá fluxo de trabalho deve ser a seguir toohello semelhante:

![Fluxo de trabalho resultante após a execução][4]valores NG código hello.

1. Entrar toohello portal clássico do Azure.
2. Na coluna de navegação à esquerda hello, clique em **armazenamento**.
3. Na lista de saudação de contas de armazenamento, selecione uma toostore saudação retreinados modelo.
4. Final Olá Olá página, clique em **gerenciar chaves de acesso**.
5. Copie e salve Olá **chave de acesso primária** e caixa de diálogo fechar hello.
6. Na parte superior de saudação da página de saudação, clique em **contêineres**.
7. Selecione um contêiner existente, ou crie um novo e salve o nome hello.

Localizar Olá *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* declarações e atualizar valores de saudação que você salvou no portal clássico Olá .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Você também deve garantir que arquivos de entrada hello está disponível no local de Olá especificado por você no código de saudação.

### <a name="specify-hello-output-location"></a>Especifique o local de saída Olá
Quando você especifica o local de saída de saudação em Olá carga de solicitação, Olá a extensão do arquivo hello especificado em *RelativeLocation* devem ser especificados como `ilearner`. Consulte Olá exemplo a seguir:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Olá, a seguir é um exemplo de saída de treinamento: ![treinamento de saída][6]

## <a name="evaluate-hello-retraining-results"></a>Avaliar Olá treinamento resultados
Quando você executa o aplicativo hello, saída de hello inclui Olá URL e token de assinaturas de acesso compartilhado que são os resultados da avaliação Olá tooaccess necessário.

Você pode ver os resultados de desempenho de saudação do modelo Olá treinados novamente combinando Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída para *output2* (conforme mostrado no hello anterior de treinamento a imagem de saída) e colando URL completa Olá na barra de endereços do navegador hello.  

Examine Olá resultados toodetermine se Olá recentemente treinado executa também suficiente Olá tooreplace existente a um.

Saudação de cópia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída.

## <a name="retrain-hello-web-service"></a>Treinar novamente o serviço web de saudação
Quando você treinar novamente um novo serviço da web, atualiza Olá web de previsão serviço definição tooreference Olá novo modelo treinado. definição de serviço web Hello é uma representação interna do modelo treinado de saudação do serviço web de saudação e não pode ser modificada diretamente. Certifique-se de que você está recuperando a definição de serviço web Olá para sua experiência de previsão e não sua experiência de treinamento.

## <a name="sign-in-tooazure-resource-manager"></a>Entrar no Gerenciador de recursos de tooAzure
Você deve primeiro entrar em tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Obter o objeto de definição de serviço Web de saudação
Em seguida, obter objeto de definição de serviço Web Olá Olá chamada [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

nome do grupo toodetermine Olá recursos de um serviço da web existente, execute o cmdlet de Get-AzureRmMlWebService de saudação sem serviços parâmetros toodisplay Olá web em sua assinatura. Localize o serviço web de saudação e, em seguida, examine a sua ID de serviço da web. nome de Olá Olá do grupo de recursos é quarto elemento Olá Olá ID, logo após Olá *resourceGroups* elemento. Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Como alternativa, toodetermine Olá recurso nome de grupo de um objeto existente serviço web, entre no portal de serviços de Web de aprendizado de máquina do Azure toohello. Selecione Olá web service. nome do grupo de recursos de saudação é elemento quinto Olá Olá URL do serviço da web de hello, logo após Olá *resourceGroups* elemento. Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Exportar o objeto de definição de serviço Web hello como JSON
definição de saudação toomodify de saudação do hello treinado toouse modelo treinado recentemente, primeiro você deve usar o hello [AzureRmMlWebService de exportação](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport-arquivo tooa formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Atualizar Olá referência toohello ilearner blob
Em ativos hello, localize Olá [treinado], atualização Olá *uri* valor Olá *locationInfo* nó com hello URI do blob de ilearner hello. Olá URI é gerado pela combinação Olá *BaseLocation* e hello *RelativeLocation* da saída de saudação de saudação chamada novos treinamentos BES.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Importar Olá JSON para um objeto de definição de serviço Web
Você deve usar o hello [AzureRmMlWebService importação](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Olá modificado arquivo JSON de volta para um objeto de definição de serviço Web que você pode usar o experimento predicative do tooupdate Olá.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Olá web serviço de atualização
Por fim, use Olá [AzureRmMlWebService atualização](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate cmdlet Olá experiência previsível.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
