---
title: aaaQuickly implantar um cluster existente do aplicativo tooan Azure Service Fabric
description: Use um cluster de Azure Service Fabric toohost um aplicativo Node. js existente com o Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Hospedar um aplicativo Node.js no Azure Service Fabric

Este guia de início rápido o ajuda a implantar um cluster existente de malha do serviço tooa (Node. js neste exemplo) do aplicativo em execução no Azure.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você [configurou o ambiente de desenvolvimento](service-fabric-get-started.md). Que inclui a instalação Olá SDK do Service Fabric e 2017 do Visual Studio ou 2015.

Você também precisa toohave um aplicativo Node. js existente para a implantação. Este guia de início rápido usa um site Node.js simples que pode ser baixado [aqui][download-sample]. Extrair esse arquivo tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` pasta depois de criar o projeto de saudação na próxima etapa do hello.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita][create-account].

## <a name="create-hello-service"></a>Criar serviço Olá

Inicie o Visual Studio como um **administrador**.

Criar um projeto com `CTRL`+`SHIFT`+`N`

Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.

Nome do aplicativo hello **MyGuestApp** e pressione **Okey**.

>[!IMPORTANT]
>Node. js facilmente pode quebrar o limite de caracteres 260 Olá para caminhos com windows. Usar um caminho curto para o próprio projeto hello como **c:\code\svc1**.
   
![Caixa de diálogo Novo projeto no Visual Studio][new-project]

Você pode criar qualquer tipo de serviço de malha do serviço na próxima caixa de diálogo de saudação. Para este guia de início rápido, escolha **Executável Convidado**.

Nome do serviço de saudação **MyGuestService** e definir opções de saudação em toohello direita Olá valores a seguir:

| Configuração                   | Valor |
| ------------------------- | ------ |
| Pasta do Pacote de Código       | _&lt;pasta de saudação com seu aplicativo Node. js&gt;_ |
| Comportamento do Pacote de Código     | Copie a pasta conteúdo tooproject |
| Programa                   | node.exe |
| Argumentos                 | server.js |
| Pasta de trabalho            | CodePackage |

Pressione **OK**.

![Caixa de diálogo Novo serviço no Visual Studio][new-service]

Visual Studio cria o projeto de aplicativo hello e projeto de serviço de ator hello e exibe-os no Gerenciador de soluções.

projeto de aplicativo Hello (**MyGuestApp**) não contém qualquer código diretamente. Em vez disso, ele faz referência a um conjunto de projetos de serviço. Além disso, ele contém três outros tipos de conteúdo:

* **Perfis de publicação**  
Preferências de ferramentas para ambientes diferentes.

* **Scripts**  
Script do PowerShell para a implantação/atualização de seu aplicativo.

* **Definição de aplicativo**  
Inclui o manifesto do aplicativo hello em *ApplicationPackageRoot*. Arquivos de parâmetro de aplicativo associados estão sob *ApplicationParameters*, que definem o aplicativo hello e permitem que você tooconfigure especificamente para um determinado ambiente.
    
Para obter uma visão geral do conteúdo de saudação do projeto de serviço hello, consulte [Introdução aos serviços confiável](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Configurar a rede

exemplo Hello aplicativo Node. js que esteja implantando usa a porta **80** e precisamos tootell Service Fabric é necessário que a porta expostos.

Olá abrir **ServiceManifest.xml** arquivo no projeto de saudação. Na parte inferior de saudação do manifesto hello, há um `<Resources> \ <Endpoints>` com uma entrada já definida. Modificar essa entrada tooadd `Port`, `Protocol`, e `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Implantar tooAzure

Se você pressionar **F5** e executar o projeto Olá, é cluster local toohello implantado. No entanto, vamos implantar tooAzure em vez disso.

Clique com botão direito no projeto hello e escolha **publicar...**  que abre um tooAzure de toopublish da caixa de diálogo.

![Caixa de diálogo tooazure para um serviço de malha publicar][publish]

Selecione Olá **PublishProfiles\Cloud.xml** perfil de destino.

Se você ainda não anteriormente, escolha um toodeploy de conta do Azure para. Se você ainda não tiver uma conta, [inscreva-se][create-account].

Em **ponto de extremidade de Conexão**, selecione Olá toodeploy de cluster do Service Fabric para. Se você não tiver um, selecione  **&lt;criar novo Cluster... &gt;**  que abre a toohello de janela de navegador da web portal do Azure. Para obter mais informações, consulte [criar um cluster no portal de saudação](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Quando você cria o cluster do Service Fabric hello, fazer se Olá de tooset **pontos de extremidade personalizado** configuração muito**80**.

![Configuração de tipo de nó do Service Fabric com o ponto de extremidade personalizado][custom-endpoint]

Criar um novo cluster do Service Fabric leva alguns toocomplete de tempo. Depois que ele tiver sido criado, vá toohello back caixa de diálogo Publicar e selecione  **&lt;atualizar&gt;**. cluster novo Hello está listado na caixa de lista suspensa Olá; Selecione-o.

Pressione **publicar** e aguarde Olá toofinish de implantação.

Isso pode levar alguns minutos. Depois que ele for concluído, ele pode levar alguns minutos para Olá aplicativo toobe totalmente disponível.

## <a name="test-hello-website"></a>Site de saudação do teste

Depois que o serviço foi publicado, teste-o em um navegador da Web. 

Primeiro, abra Olá portal do Azure e localizar seu serviço de malha do serviço.

Verifique a folha de visão geral de Olá Olá do endereço do serviço. Use o nome de domínio Olá da saudação _ponto de extremidade de conexão de cliente_ propriedade. Por exemplo: `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Folha de visão geral de malha do serviço no hello portal do Azure][overview]

Navegue toothis endereço onde você verá Olá `HELLO WORLD` resposta.

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

Não se esqueça de toodelete todos os recursos de saudação que você criou para este guia de início rápido, como você são cobrados por esses recursos.

## <a name="next-steps"></a>Próximas etapas
Leia mais sobre [executáveis convidados](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F