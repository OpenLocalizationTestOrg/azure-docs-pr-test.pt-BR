---
title: "integração de aaaContinuous no VS Team Services usando projetos de grupo de recursos do Azure | Microsoft Docs"
description: "Descreve como tooset a integração contínua no Visual Studio Team Services usando a implantação do grupo de recursos do Azure projetos no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Integração contínua no Visual Studio Team Services usando os projetos de implantação do Grupo de recursos do Azure
toodeploy um modelo do Azure, você executar tarefas em vários estágios: Crie, teste, tooAzure de cópia (também chamado de "Preparação") e implantar o modelo. Há duas maneiras diferentes toodeploy modelos tooVisual Studio Team Services (VS Team Services). Ambos os métodos fornecem Olá mesmos resultados, portanto escolha Olá que melhor se adapta o fluxo de trabalho.

1. Adicione uma definição de compilação de tooyour única etapa que executa o script do PowerShell Olá que está incluído no projeto de implantação do grupo de recursos do Azure hello (implantar AzureResourceGroup.ps1). script Hello copia artefatos e depois implanta o modelo de saudação.
2. Adicione várias etapas de compilação do VS Team Services, cada uma executando uma tarefa do estágio.

Este artigo demonstra ambas as opções. opção primeira Olá tem a vantagem de saudação de usando Olá mesmo script usado por desenvolvedores do Visual Studio e fornecer consistência em todo o ciclo de vida de saudação. opção de segundo Olá oferece um script interno toohello alternativa conveniente. Ambos os procedimentos supõem que você já tem um projeto de implantação do Visual Studio no VS Team Services.

## <a name="copy-artifacts-tooazure"></a>Copiar artefatos tooAzure
Independentemente de cenário hello, se você tiver quaisquer artefatos necessários para a implantação de modelo, você deve atribuir toothem de acesso do Azure Resource Manager. Esses artefatos podem incluir arquivos como:

* Modelos aninhados
* Scripts de configuração e scripts DSC
* Binários do aplicativo

### <a name="nested-templates-and-configuration-scripts"></a>Modelos aninhados e scripts de configuração
Quando você usa modelos de saudação fornecidos pelo Visual Studio (ou criado com trechos de código do Visual Studio), Olá script do PowerShell não apenas prepara artefatos hello, ele também parametriza hello URI para recursos de saudação de diferentes implantações. script Hello, em seguida, copia Olá artefatos tooa seguras de contêiner no Azure, cria um token SaS para o contêiner e, em seguida, transmite essas informações na implantação de modelo toohello. Consulte [criar uma implantação de modelo](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn mais sobre modelos de aninhados.  Ao usar tarefas em VS Team Services, você deve selecionar tarefas apropriadas Olá para sua implantação de modelo e se necessário, passar valores de parâmetro de saudação etapa toohello modelo implantação de preparo.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Configurar a implantação contínua no VS Team Services
script do PowerShell toocall Olá no VS Team Services, você precisa tooupdate sua definição de compilação. Em suma, etapas de saudação são: 

1. Edite definição de compilação de saudação.
2. Configurar a autorização do Azure no VS Team Services.
3. Adicione uma etapa de compilação do PowerShell do Azure que referencia o script do PowerShell Olá no projeto de implantação do grupo de recursos do Azure hello.
4. Definir valor Olá Olá *- ArtifactsStagingDirectory* toowork de parâmetro com um projeto criado no VS Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Passo a passo detalhado da Opção 1
Olá procedimentos a seguir orientam você durante implantação contínua do hello etapas tooconfigure necessárias no VS Team Services usando uma única tarefa que executa o script do PowerShell Olá em seu projeto. 

1. Edite sua definição de compilação do VS Team Services e adicione uma etapa de compilação do Azure PowerShell. Escolha a definição de compilação de saudação em Olá **definições de compilação** categoria e, em seguida, escolha Olá **editar** link.
   
   ![Editar a definição de build][0]
2. Adicionar um novo **Azure PowerShell** definição de compilação de toohello de etapa de compilação e, em seguida, escolha Olá **adicionar a etapa de compilação...** .
   
   ![Adicionar etapa de build][1]
3. Escolha Olá **tarefa de implantar** categoria, selecione Olá **Azure PowerShell** de tarefas e, em seguida, escolha seu **adicionar** botão.
   
   ![Adicionar tarefas][2]
4. Escolha Olá **Azure PowerShell** passo de compilação e, em seguida, preencha seus valores.
   
   1. Se você já tiver um ponto de extremidade de serviço do Azure adicionada tooVS Team Services, escolha a assinatura de saudação em Olá **assinatura do Azure** caixa de listagem suspensa e, em seguida, ignorar toohello próxima seção. 
      
      Se você não tiver um ponto de extremidade de serviço do Azure no VS Team Services, será necessário tooadd um. Esta subseção leva você através do processo de saudação. Se sua conta do Azure usa uma conta da Microsoft (por exemplo, Hotmail), você deve tomar Olá tooget as etapas a seguir uma entidade de serviço de autenticação.
   2. Escolha Olá **gerenciar** link próximo toohello **assinatura do Azure** caixa de listagem suspensa.
      
      ![Gerenciar assinaturas do Azure][3]
   3. Escolha **Azure** em Olá **novo ponto de extremidade de serviço** caixa de listagem suspensa.
      
      ![Novo ponto de extremidade de serviço][4]
   4. Em Olá **Adicionar assinatura do Azure** caixa de diálogo, selecione Olá **entidade de serviço** opção.
      
      ![Opção da entidade de serviço][5]
   5. Adicionar seu toohello de informações de assinatura do Azure **Adicionar assinatura do Azure** caixa de diálogo. Você precisa Olá tooprovide itens a seguir:
      
      * ID da assinatura
      * Nome da assinatura
      * Id da Entidade de serviço
      * Chave da Entidade de serviço
      * ID do locatário
   6. Adicionar um nome de sua escolha toohello **assinatura** caixa nome. Esse valor é exibida posteriormente no hello **assinatura do Azure** lista suspensa no VS Team Services. 
   7. Se você não souber a ID de assinatura do Azure, você pode usar uma saudação tooretrieve comandos a segui-lo.
      
      Para scripts do PowerShell, use:
      
      `Get-AzureRmSubscription`
      
      Para a CLI do Azure, use:
      
      `azure account show`
   8. tooget uma ID de entidade de serviço, chave de entidade de serviço e a ID de locatário, siga o procedimento Olá [entidade de serviço usando o portal e de aplicativo do Active Directory crie](resource-group-create-service-principal-portal.md) ou [autenticar uma entidade de serviço com Gerenciador de recursos do Azure](resource-group-authenticate-service-principal.md).
   9. Adicionar Olá toohello de valores de ID de entidade de serviço, chave de entidade de serviço e ID de locatário **Adicionar assinatura do Azure** caixa de diálogo caixa e, em seguida, escolha Olá **Okey** botão.
      
      Agora você tem uma saudação de toorun toouse de entidade de serviço válido de script do PowerShell do Azure.
5. Editar definição de compilação hello e escolha Olá **Azure PowerShell** passo de compilação. Selecione a assinatura de saudação em Olá **assinatura do Azure** caixa de listagem suspensa. (Se a assinatura de saudação não aparecer, escolha Olá **atualizar** Olá próximo botão **gerenciar** link.) 
   
   ![Configurar tarefa de build do Azure PowerShell][8]
6. Fornece um caminho toohello script do PowerShell AzureResourceGroup.ps1 implantar. toodo isso, escolha Olá reticências (...) botão próximo toohello **caminho de Script** caixa, navegue até o script de PowerShell implantar AzureResourceGroup.ps1 toohello em hello **Scripts** pasta do seu projeto, selecione-o, e, em seguida, escolha Olá **Okey** botão.    
   
   ![Selecione o caminho tooscript][9]
7. Depois de selecionar o script hello, atualize o script de toohello de caminho de Olá para que ele é executado de saudação Build.StagingDirectory (Olá mesmo diretório que *ArtifactsLocation* é definido como). Você pode fazer isso adicionando "$(Build.StagingDirectory)/" toohello início do caminho do script hello.
   
    ![Editar tooscript de caminho][10]
8. Em Olá **argumentos de Script** , digite Olá parâmetros (em uma única linha) a seguir. Quando você executa o script hello no Visual Studio, você pode ver como usa VS Olá parâmetros em Olá **saída** janela. Você pode usar isso como um ponto de partida para definir valores de parâmetro de saudação em sua etapa de compilação.
   
   | Parâmetro | Descrição |
   | --- | --- |
   | -ResourceGroupLocation |Olá valor de localização geográfica onde está localizado, como o grupo de recursos Olá **eastus** ou **'Leste dos Estados Unidos'**. (Adicionar aspas se houver um espaço no nome da saudação). Veja [Regiões do Azure](https://azure.microsoft.com/en-us/regions/) para saber mais. |
   | -ResourceGroupName |nome de Olá Olá do grupo de recursos usado para essa implantação. |
   | -UploadArtifacts |Esse parâmetro, quando presente, especifica que os artefatos que precisam toobe carregado tooAzure do sistema local hello. Você só precisa tooset essa opção se sua implantação do modelo exigir artefatos adicionais que você deseja toostage usando script do PowerShell hello (como scripts de configuração ou modelos aninhados). |
   | -StorageAccountName |nome de Olá Olá da conta de armazenamento usado toostage artefatos para essa implantação. Esse parâmetro será usado somente se você estiver preparando artefatos para implantação. Se esse parâmetro for fornecido, uma nova conta de armazenamento é criada se script hello não tiver criado uma durante uma implantação anterior. Se o parâmetro hello for especificado, conta de armazenamento Olá já deve existir. |
   | -StorageAccountResourceGroupName |nome de Olá Olá do grupo de recursos associado à conta de armazenamento hello. Esse parâmetro é necessário somente se você fornecer um valor para o parâmetro de StorageAccountName hello. |
   | -TemplateFile |arquivo de modelo Olá caminho toohello no projeto de implantação do grupo de recursos do Azure hello. tooenhance flexibilidade, use um caminho para este parâmetro que é local relativo toohello de saudação script do PowerShell em vez de um caminho absoluto. |
   | -TemplateParametersFile |arquivo de parâmetros Olá caminho toohello no projeto de implantação do grupo de recursos do Azure hello. tooenhance flexibilidade, use um caminho para este parâmetro que é local relativo toohello de saudação script do PowerShell em vez de um caminho absoluto. |
   | -ArtifactStagingDirectory |Esse parâmetro permite que o script do PowerShell Olá Saiba pasta Olá de onde os arquivos binários do projeto Olá devem ser copiados. Esse valor substitui o valor de padrão de saudação usado pelo Olá script do PowerShell. Para usar o VS Team Services, defina o valor de saudação para: - ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   Veja a seguir um exemplo de argumentos de script (linha quebrada para facilitar a leitura):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Quando tiver terminado, Olá **argumentos de Script** caixa deve ser semelhante a saudação lista a seguir:
   
   ![Argumentos de script][11]
9. Depois que você adicionou todos Olá toohello itens necessários passo de compilação do PowerShell do Azure, escolha Olá **fila** compilar o projeto de saudação do botão toobuild. Olá **criar** tela mostra a saída de saudação do hello script do PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Passo a passo detalhado da Opção 2
Olá procedimentos a seguir orientam você durante implantação contínua do hello etapas tooconfigure necessárias no VS Team Services usando tarefas internas hello.

1. Edite as VS Team Services compilação definição tooadd duas novas etapas de compilação. Escolha a definição de compilação de saudação em Olá **definições de compilação** categoria e, em seguida, escolha Olá **editar** link.
   
   ![Editar a definição de build][12]
2. Saudação de adicionar novas etapas de compilação toohello definição de compilação usando Olá **adicionar a etapa de compilação...** .
   
   ![Adicionar etapa de build][13]
3. Escolha Olá **implantar** categoria da tarefa, selecione Olá **cópia de arquivo do Azure** de tarefas e, em seguida, escolha seu **adicionar** botão.
   
   ![tarefa Adicionar Cópias de Arquivos do Azure][14]
4. Escolha Olá **implantação de grupo de recursos do Azure** de tarefas, em seguida, escolha seu **adicionar** botão e, em seguida, **fechar** Olá **tarefa catálogo**.
   
   ![tarefa Adicionar Implantação do Grupo de Recursos do Azure][15]
5. Escolha Olá **cópia de arquivo do Azure** tarefas e preencher seus valores.
   
   Se você já tiver um ponto de extremidade de serviço do Azure adicionada tooVS Team Services, escolha a assinatura de saudação em Olá **assinatura do Azure** caixa de listagem suspensa. Se você não tiver uma assinatura, veja a [Opção 1](#detailed-walkthrough-for-option-1) para obter instruções de como configurar uma no VS Team Services.
   
   * Origem: insira **$(Build.StagingDirectory)**
   * Tipo de Conexão do Azure: escolha **Azure Resource Manager**
   * Assinatura do Azure do RM - assinatura selecione Olá Olá conta de armazenamento você deseja toouse em Olá **assinatura do Azure** caixa de listagem suspensa. Se a assinatura de saudação não aparecer, escolha Olá **atualizar** Olá próximo botão **gerenciar** link.
   * Tipo de Destino: escolha **Blob do Azure**
   * Conta de armazenamento RM - selecione conta de armazenamento Olá você gostaria que toouse para artefatos de teste
   * Nome do contêiner - insira o nome de saudação do contêiner Olá você gostaria que toouse para preparação; ele pode ser qualquer nome de contêiner válido, mas use uma definição de compilação toothis dedicado
   
   Para valores de saída de hello:
   
   * URI do Contêiner de Armazenamento: insira **artifactsLocation**
   * Token SAS do Contêiner de Armazenamento: insira **artifactsLocationSasToken**
   
   ![tarefa Configurar Cópias de Arquivos do Azure][16]
6. Escolha Olá **implantação de grupo de recursos do Azure** passo de compilação e, em seguida, preencha seus valores.
   
   * Tipo de Conexão do Azure: escolha **Azure Resource Manager**
   * Assinatura do Azure do RM - assinatura selecione Olá para implantação no hello **assinatura do Azure** caixa de listagem suspensa. Isso geralmente será Olá mesma assinatura usada na etapa anterior Olá
   * Ação – escolha **Criar ou Atualizar Grupo de Recursos**
   * Grupo de recursos - selecionar um grupo de recursos ou digitar nome de saudação do novo grupo de recursos para implantação de saudação
   * Local - local selecione Olá Olá para grupo de recursos
   * Modelo - Inserir nome e caminho de saudação do hello modelo toobe implantado acrescentando **$(Build.StagingDirectory)**, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parâmetros de modelo - insira o caminho de saudação e nome de saudação parâmetros toobe usado, acrescentando **$(Build.StagingDirectory)**, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Substituir parâmetros de modelo - digite ou copie e cole Olá código a seguir:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Tarefa Configurar Implantação do Grupo de Recursos do Azure][17]
7. Depois de ter adicionado todos os itens de saudação necessárias, salvar a definição de compilação hello e escolha **enfileirar nova compilação** na parte superior da saudação.

## <a name="next-steps"></a>Próximas etapas
Leitura [visão geral do Gerenciador de recursos do Azure](azure-resource-manager/resource-group-overview.md) toolearn mais sobre o Gerenciador de recursos do Azure e grupos de recursos do Azure.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
