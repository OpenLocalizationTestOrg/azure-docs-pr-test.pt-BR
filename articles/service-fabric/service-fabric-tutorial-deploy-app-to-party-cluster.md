---
title: aaaDeploy um tooa de aplicativo do Azure Service Fabric parte Cluster | Microsoft Docs
description: Saiba como toodeploy tooa um aplicativo de Cluster de terceiros.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>Implantar um aplicativo tooa de Cluster no Azure
Este tutorial é a parte dois de uma série e mostra como toodeploy uma tooa de aplicativo do Azure Service Fabric Cluster de terceiros no Azure.

A parte dois da série de tutoriais hello, você aprenderá como:
> [!div class="checklist"]
> * Implantar um cluster remoto de tooa de aplicativo usando o Visual Studio
> * Remover um aplicativo de um cluster usando o Service Fabric Explorer

Nesta série de tutoriais, você aprenderá a:
> [!div class="checklist"]
> * [Criar um aplicativo .NET do Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * Implantar aplicativos de saudação tooa cluster remoto
> * [Configurar CI/CD usando o Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Instalar o Visual Studio de 2017](https://www.visualstudio.com/) e instalar Olá **desenvolvimento do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
- [Instalar Olá SDK do Service Fabric](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>Baixe o aplicativo de exemplo hello votação
Se você não criar aplicativo de exemplo hello voto [parte um esta série de tutoriais](service-fabric-tutorial-create-dotnet-app.md), você pode baixá-lo. Em uma janela de comando, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Configurar um Cluster Party
Clusters de terceiros são livres, tempo limitado clusters de malha do serviço hospedado no Azure e executar pela equipe do Service Fabric Olá em que qualquer pessoa pode implantar aplicativos e saiba mais sobre a plataforma de saudação. Gratuitamente!

tooget acesso tooa Cluster de terceiros, visite o site de toothis: http://aka.ms/tryservicefabric e siga Olá instruções tooget tooa cluster de acesso. É necessário um Facebook ou GitHub conta tooget acesso tooa de Cluster.

> [!NOTE]
> Clusters de terceiros não estão protegidos, para que seus aplicativos e quaisquer dados-los podem ser tooothers visível. Não implantar qualquer coisa que você não quiser que outras pessoas toosee. Ser tooread-se por meio de nossos termos de uso para todos os detalhes de saudação.

## <a name="configure-hello-listening-port"></a>Configurar a porta de escuta Olá
Quando Olá VotingWeb serviço de front-end é criada, o Visual Studio seleciona aleatoriamente uma porta para Olá serviço toolisten em.  Olá VotingWeb serviço atua como Olá front-end para este aplicativo e aceita tráfego externo, então vamos associar esse tooa serviço fixada e saber também a porta. No Gerenciador de Soluções, abra *VotingWeb/PackageRoot/ServiceManifest.xml*.  Localize Olá **ponto de extremidade** recurso Olá **recursos** seção e alterar Olá **porta** too80 de valor.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Também atualize o valor da propriedade URL do aplicativo hello no projeto de votação Olá para que um navegador da web abre a porta correta toohello quando você depurar usando 'F5'.  No Gerenciador de soluções, selecione Olá **votação** Olá projeto e atualize **URL do aplicativo** propriedade.

![URL do Aplicativo](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>Implantar Olá toohello de aplicativo do Azure
Agora que o aplicativo hello estiver pronto, você pode implantar toohello parte Cluster direta do Visual Studio.

1. Clique com botão direito **votação** em Olá Gerenciador de soluções e escolha **publicar**.

    ![Caixa de diálogo Publicar](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Digite hello ponto de extremidade de Conexão de saudação de Cluster em Olá **ponto de extremidade de Conexão** campo e clique em **publicar**.

    Depois de publicar Olá tiver terminado, você deve ser capaz de toosend um aplicativo de toohello de solicitação por meio de um navegador.

3. Abra preferencial navegador e digite o endereço de cluster de hello (Olá conexão ponto de extremidade sem informações de porta Olá - por exemplo, win1kw5649s.westus.cloudapp.azure.com).

    Agora você deve ver Olá mesmo resultado que você viu ao executar o aplicativo hello localmente.

    ![Resposta de API do Cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>Remover o aplicativo hello de um cluster usando o Gerenciador do Service Fabric
Gerenciador do Service Fabric é um tooexplore de interface gráfica do usuário e gerenciar aplicativos em um cluster do Service Fabric.

aplicativo de hello tooremove de saudação de Cluster:

1. Procure toohello Service Fabric Explorer, usando o link Olá fornecido pela página de inscrição de participante Cluster hello. Por exemplo, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. No Gerenciador do Service Fabric, vá toohello **fabric://Voting** nó em treeview Olá no lado esquerdo da saudação.

3. Clique em Olá **ação** botão no lado direito da saudação **Essentials** painel e escolha **excluir aplicativo**. Confirme excluir instância de aplicativo hello, que remove a instância de saudação do nosso aplicativo em execução no cluster de saudação.

![Excluir aplicativo no Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>Remover o tipo de aplicativo hello de um cluster usando o Gerenciador do Service Fabric
Aplicativos são implantados como tipos de aplicativos em um cluster do Service Fabric, que permite que você toohave várias instâncias e versões do aplicativo hello em execução no cluster de saudação. Depois de ter removido Olá executando a instância do nosso aplicativo, podemos também remover tipo hello, limpeza de saudação toocomplete de implantação de saudação.

Para obter mais informações sobre o modelo de aplicativo de saudação do Service Fabric, consulte [um aplicativo no serviço de malha de modelo](service-fabric-application-model.md).

1. Navegue toohello **VotingType** nó em treeview hello.

2. Clique em Olá **ação** botão no lado direito da saudação **Essentials** painel e escolha **desconfiguração tipo**. Confirme o tipo de aplicativo hello desprovisionamento.

![Desprovisionar o tipo do aplicativo Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Isso conclui o tutorial de saudação.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Implantar um cluster remoto de tooa de aplicativo usando o Visual Studio
> * Remover um aplicativo de um cluster usando o Service Fabric Explorer

Tutorial de Avançar de toohello avançado:
> [!div class="nextstepaction"]
> [Configurar a integração contínua usando o Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)