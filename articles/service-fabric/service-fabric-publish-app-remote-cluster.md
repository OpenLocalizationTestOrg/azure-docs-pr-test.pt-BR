---
title: aaaPublish um cluster remoto de tooa do aplicativo com o Visual Studio | Microsoft Docs
description: "Saiba como toopublish uma malha de serviço remoto do aplicativo tooa de cluster usando o Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Implantar e remover aplicativos usando o Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [APIs de FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Olá extensão do Azure Service Fabric para Visual Studio fornece uma maneira fácil, repetíveis e programável toopublish um cluster de malha do serviço do aplicativo tooa.

## <a name="hello-artifacts-required-for-publishing"></a>artefatos de saudação necessários para publicação
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
Este é um script do PowerShell que usa um caminho de perfil de publicação como um parâmetro para a publicação de aplicativos do Service Fabric. Como esse script faz parte do seu aplicativo, você está toomodify bem-vindo-lo conforme necessário para seu aplicativo.

### <a name="publish-profiles"></a>Perfis de publicação
Uma pasta no projeto de aplicativo do Service Fabric Olá chamada **PublishProfiles** contém os arquivos XML que armazenam informações essenciais para publicar um aplicativo, como:

* Parâmetros de conexão de cluster do Service Fabric
* Arquivo de parâmetro de aplicativo do caminho tooan
* Configurações de atualização

Por padrão, o aplicativo incluirá três perfis de publicação: Local.1Node.xml, Local.5Node.xml e Cloud.xml. Você pode adicionar mais perfis copiando e colando um dos arquivos de padrão de saudação.

### <a name="application-parameter-files"></a>Arquivos de parâmetros de aplicativo
Uma pasta no projeto de aplicativo do Service Fabric Olá chamada **ApplicationParameters** contém arquivos XML para valores de parâmetro de manifesto do aplicativo especificado pelo usuário. Os arquivos de manifesto do aplicativo podem ser parametrizados, de modo que você possa usar valores diferentes para configurações de implantação. toolearn mais sobre a parametrização de seu aplicativo, consulte [gerenciar vários ambientes na malha do serviço](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Para serviços de ator, você deve compilar o projeto de saudação primeiro antes de tentar o arquivo de saudação tooedit em um editor ou por meio de saudação caixa de diálogo Publicar. Isso ocorre porque a parte dos arquivos de manifesto hello será gerado durante a compilação de saudação.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish um aplicativo usando a caixa de diálogo Publicar aplicativo do Service Fabric Olá
Olá etapas a seguir demonstram como toopublish usando um aplicativo hello **publicar aplicativo do Service Fabric** caixa de diálogo fornecida pelo Olá ferramentas do Visual Studio Service Fabric.

1. No menu de atalho de saudação do projeto de aplicativo do Service Fabric hello, escolha **publicar...** Olá tooview **publicar aplicativo do Service Fabric** caixa de diálogo.
   
    ![Olá * * caixa de diálogo Publicar serviço malha aplicativo * *][0]
   
    arquivo Hello selecionado no hello **perfil de destino** caixa de listagem suspensa é o local onde todas as configurações de hello, exceto **manifesto versões**, são salvas. Você pode reutilizar um perfil existente ou crie um novo escolhendo **<... para gerenciar perfis >** em Olá **perfil de destino** caixa de listagem suspensa. Quando você escolhe um perfil de publicação, seu conteúdo aparece nos campos correspondentes de Olá Olá da caixa de diálogo. toosave as alterações a qualquer momento, escolha Olá **Salvar perfil** link.    
2. Em Olá **ponto de extremidade de Conexão** seção, especifique o ponto de extremidade de um cluster local ou remota do Service Fabric publicação. tooadd ou alterar Olá ponto de extremidade de conexão, clique em Olá **ponto de extremidade de Conexão** lista suspensa. lista de saudação mostra Olá disponíveis do Service Fabric cluster conexão pontos de extremidade toowhich que você pode publicar com base em sua assinatura do Azure (s). Observe que se você não ainda tiver entrado no tooVisual Studio, você será solicitado toodo assim.
   
    Use toochoose de caixa de diálogo Olá cluster seleção de conjunto de saudação de assinaturas disponíveis e os clusters.
   
    ![Olá * * caixa de diálogo Selecionar serviço malha Cluster * *][1]
   
   > [!NOTE]
   > Se você quiser toopublish tooan arbitrário ponto de extremidade (por exemplo, um cluster de terceiros), consulte Olá **publicação ponto de extremidade de cluster arbitrário tooan** seção abaixo.
   > 
   > 
   
    Depois que você escolher um ponto de extremidade, o Visual Studio valida cluster do Service Fabric do hello conexão toohello selecionado. Se o cluster de saudação não é seguro, Visual Studio pode se conectar tooit imediatamente. No entanto, se o cluster de saudação é segura, você precisará tooinstall um certificado no computador local antes de continuar. Consulte [como tooconfigure proteger conexões](service-fabric-visualstudio-configure-secure-connections.md) para obter mais informações. Quando terminar, escolha Olá **Okey** botão. cluster selecionado Olá aparece no hello **publicar aplicativo do Service Fabric** caixa de diálogo.
3. Em Olá **arquivo de parâmetro de aplicativo** lista suspensa caixa, navegue até o arquivo de parâmetro de aplicativo tooan. Um arquivo de parâmetro de aplicativo contém os valores especificados pelo usuário para os parâmetros no arquivo de manifesto de aplicativo hello. tooadd ou alterar um parâmetro, escolha Olá **editar** botão. Insira ou altere o valor do parâmetro hello em Olá **parâmetros** grade. Quando terminar, escolha Olá **salvar** botão.
   
    ![Olá * * caixa de diálogo Editar parâmetros * *][2]
4. Saudação de uso **atualização Olá aplicativo** toospecify da caixa de seleção se esta ação de publicação é uma atualização. Ações de publicação de atualização são diferentes das ações de publicação normais. Confira [Atualização de Aplicativo do Service Fabric](service-fabric-application-upgrade.md) para obter uma lista das diferenças. configurações de atualização tooconfigure, escolha Olá **configurar configurações de atualização de** link. editor de parâmetro de atualização de saudação aparece. Consulte [configurar a atualização de um aplicativo do Service Fabric Olá](service-fabric-visualstudio-configure-upgrade.md) toolearn mais sobre os parâmetros de atualização.
5. Escolha Olá **versões de manifesto...** saudação do botão tooview **editar versões** caixa de diálogo. Você precisará tooupdate aplicativo e as versões de serviço para um local de atualização tootake. Consulte [tutorial do aplicativo de atualização do Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn como aplicativo e versões de manifesto do serviço afetam um processo de atualização.
   
    ![Olá * * caixa de diálogo Editar versões * *][3]
   
    Se o aplicativo hello e versões de serviço usam controle de versão semântico como 1.0.0 ou valores numéricos no formato de saudação do 1.0.0.0, selecione Olá **atualizar automaticamente o aplicativo e as versões de serviço** opção. Quando você escolher essa opção, o serviço de saudação e números de versão do aplicativo são atualizados automaticamente sempre que um código, configuração ou versão do pacote de dados é atualizado. Se você preferir versões de saudação tooedit manualmente, desmarque Olá caixa de seleção toodisable esse recurso.
   
   > [!NOTE]
   > Para todos os tooappear de entradas de pacote para um projeto de ator, primeiro crie o hello projeto toogenerate entradas Olá nos arquivos de manifesto do serviço de saudação.
   > 
   > 
6. Quando você terminar especificar todas as configurações necessárias do hello, escolha Olá **publicar** botão toopublish seu toohello de aplicativo selecionado cluster do Service Fabric. Olá configurações que você especificou são aplicadas toohello o processo de publicação.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Publicar o ponto de extremidade do cluster arbitrário tooan (incluindo clusters de terceiros)
Olá experiência de publicação do Visual Studio é otimizado para a publicação de clusters tooremote associados a uma de suas assinaturas do Azure. No entanto, é toopublish possíveis pontos de extremidade de tooarbitrary (como clusters de parte do Service Fabric) por diretamente editando Olá publicar perfil XML. Conforme descrito acima, três perfis de publicação são fornecidos por padrão –**Local.1Node.xml**, **Local.5Node.xml**, e **Cloud.xml**– mas toocreate boas-vinda perfis adicionais para ambientes diferentes. Por exemplo, você pode querer toocreate um perfil de publicação tooparty clusters, talvez denominados **Party.xml**.

Se você estiver se conectando tooan não segura de cluster, tudo que é necessário é a extremidade de conexão do cluster Olá, como `partycluster1.eastus.cloudapp.azure.com:19000`. Nesse caso, ponto de extremidade de conexão de saudação em Olá publicar perfil seria semelhante a esta:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Se você estiver se conectando cluster protegido tooa, você também precisará tooprovide detalhes de saudação do certificado de cliente de saudação do hello repositório local toobe usado para autenticação. Para obter mais detalhes, consulte [cluster do Service Fabric do Configurando conexões seguras tooa](service-fabric-visualstudio-configure-secure-connections.md).

  Depois de configurar seu perfil de publicação, você pode referenciá-lo no hello caixa de diálogo Publicar, conforme mostrado abaixo.

  ![Novo perfil de publicação na caixa de diálogo de publicação][4]

  Observe que nesse caso, Olá novo perfil de publicação pontos tooone saudação padrão parâmetro dos arquivos de aplicativo. Isso é apropriado se você quiser toopublish Olá mesmo número de tooa de configuração de aplicativo de ambientes. Por outro lado, em casos onde você deseja toohave a configurações diferentes para cada ambiente que você deseja toopublish para, faria sentido toocreate um arquivo de parâmetro correspondente do aplicativo.

## <a name="next-steps"></a>Próximas etapas
toolearn como o processo de publicação Olá tooautomate em um ambiente de integração contínua, consulte [configurar a integração contínua do Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
