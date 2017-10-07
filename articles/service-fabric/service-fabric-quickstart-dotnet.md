---
title: "aaaCreate um aplicativo de malha do serviço .NET no Azure | Microsoft Docs"
description: "Crie um aplicativo .NET do Azure usando o exemplo de início rápido do Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Criar um aplicativo .NET do Service Fabric no Azure
O Azure Service Fabric é uma plataforma de sistemas distribuídos para implantação e gerenciamento de contêineres e microsserviços escalonáveis e confiáveis. 

Este guia de início rápido mostra como toodeploy seu primeiro tooService de aplicativo .NET malha. Quando você terminar, você tiver um aplicativo votação com um front-end para que salva os resultados de votação em um serviço de back-end com monitoração de estado no cluster de saudação de web do ASP.NET Core.

![Captura de tela do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

Com esse aplicativo, você aprenderá a:
> [!div class="checklist"]
> * Criar um aplicativo usando o .NET e o Service Fabric
> * Usar o ASP.NET Core como um front-end da Web
> * Armazenar dados de aplicativo em um serviço com estado
> * Depurar o aplicativo localmente
> * Implantar Olá aplicativo tooa cluster no Azure
> * Aplicativo de expansão Olá em vários nós
> * Executar um upgrade sem interrupção do aplicativo

## <a name="prerequisites"></a>Pré-requisitos
toocomplete este guia de início rápido:
1. [Instalar o Visual Studio de 2017](https://www.visualstudio.com/) com hello **desenvolvimento do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
2. [Instalar o Git](https://git-scm.com/)
3. [Instalar Olá SDK do Microsoft Azure Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. Execute Olá comando tooenable Visual Studio toodeploy toohello Service Fabric cluster local a seguir:
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a>Baixe o exemplo hello
Em uma janela de comando, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
Clique o ícone do Visual Studio Olá no Menu Iniciar do hello e escolha **executar como administrador**. Em ordem tooattach Olá depurador tooyour os serviços, você precisa toorun Visual Studio como administrador.

Olá abrir **Voting.sln** solução do Visual Studio do repositório de saudação você clonado.

aplicativo de hello toodeploy, pressione **F5**.

> [!NOTE]
> Olá a primeira vez que você executar e implanta o aplicativo hello, o Visual Studio cria um cluster local para depuração. Essa operação pode levar algum tempo. status de criação de cluster Olá é exibido na janela de saída do Visual Studio hello.

Quando a saudação implantação estiver concluída, iniciar um navegador e abrir essa página: `http://localhost:8080` -Olá web front-end do aplicativo hello.

![Front-end do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

Agora, você pode adicionar um conjunto de opções de votação e começar a votar. aplicativo Hello executa e armazena todos os dados no cluster do Service Fabric, sem necessidade de saudação de um banco de dados separado.

## <a name="walk-through-hello-voting-sample-application"></a>Percorrer Olá votação de aplicativo de exemplo
Olá votação aplicativo consiste em dois serviços:
- (VotingWeb) de serviço front-end da Web – ASP.NET Core um serviço front-end, que serve a página da web de saudação e expõe web toocommunicate APIs com serviço de back-end de saudação.
- Serviço de back-end (VotingData)-um núcleo de ASP.NET web service, que expõe um voto de saudação do API toostore resulta em um dicionário confiável persistidos no disco.

![Diagrama de aplicativo](./media/service-fabric-quickstart-dotnet/application-diagram.png)

Quando você vota em Olá Olá do aplicativo a seguir podem ocorrer eventos:
1. Um JavaScript envia Olá voto solicitação toohello API da web no serviço de front-end de web hello como uma solicitação HTTP PUT.

2. serviço de front-end de web Hello usa um proxy toolocate e encaminhar a um serviço de back-end de toohello de solicitação HTTP PUT.

3. serviço de back-end Olá leva a solicitação de entrada hello e repositórios Olá atualizado resultam em um dicionário confiável, que obtém toomultiple replicado nós no cluster hello e mantidos em disco. Dados do aplicativo hello todos os são armazenados no cluster hello, portanto, nenhum banco de dados é necessária.

## <a name="debug-in-visual-studio"></a>Depuração no Visual Studio
Ao depurar o aplicativo no Visual Studio, você usa um cluster de desenvolvimento local do Service Fabric. Você tem Olá opção tooadjust seu cenário de tooyour experiência de depuração. Neste aplicativo, armazenamos dados em nosso serviço de back-end, usando um dicionário confiável. Visual Studio remove o aplicativo hello por padrão quando você interrompe o depurador hello. Remover o aplicativo hello faz com que dados Olá Olá back-end tooalso serviço ser removido. dados de saudação toopersist entre as sessões de depuração, você pode alterar Olá **o modo de depuração de aplicativo** como uma propriedade no hello **votação** projeto no Visual Studio.

toolook o que acontece no código hello, Olá concluir as etapas a seguir:
1. Olá abrir **VotesController.cs** arquivo e defina um ponto de interrupção da API da web hello **colocar** método (linha 47 -), você pode procurar arquivo Olá Olá Gerenciador de soluções do Visual Studio.

2. Olá abrir **VoteDataController.cs** arquivo e defina um ponto de interrupção na API de web **colocar** método (linha 50).

3. Voltar toohello navegador e clique em uma opção de votação ou adicionar uma nova opção de votação. Você atingiu o primeiro ponto de interrupção de saudação no controlador de api do Olá web front-end.
    - Isso é onde Olá JavaScript no navegador Olá envia um controlador de API da web solicitação toohello no serviço de front-end de saudação.
    
    ![Adicionar Serviço de Front-end de Voto](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - Primeiro, construímos Olá URL toohello ReverseProxy para nosso serviço de back-end **(1)**.
    - Em seguida, podemos enviar Olá HTTP PUT solicitação toohello ReverseProxy **(2)**.
    - Finalmente hello retornamos resposta de saudação do cliente do hello serviço back-end toohello **(3)**.

4. Pressione **F5** toocontinue
    - Agora você está no ponto de interrupção Olá no serviço de back-end de saudação.
    
    ![Adicionar Serviço de Back-End de Voto](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - Na primeira linha hello no método hello **(1)** estamos usando Olá `StateManager` tooget ou adicionar um dicionário confiável chamado `counts`.
    - Todas as interações com valores em um dicionário confiável exigem uma transação e, portanto, o uso da instrução **(2)** cria essa transação.
    - Transação Olá, é, em seguida, atualizar o valor de saudação de chave relevantes Olá Olá votar na opção e confirmações Olá operação **(3)**. Depois de confirmar Olá método retorna, Olá dados são atualizados no dicionário hello e replicados tooother nós no cluster de saudação. dados de saudação agora são armazenados com segurança no cluster hello e serviço de back-end de saudação pode falhar em nós de tooother, ainda com dados de saudação disponíveis.
5. Pressione **F5** toocontinue

Olá toostop depuração sessão, pressione **Shift + F5**.

## <a name="deploy-hello-application-tooazure"></a>Implantar Olá aplicativo tooAzure
cluster de tooa toodeploy Olá aplicativo no Azure, você pode escolher toocreate seu próprio cluster ou use um Cluster de terceiros.

Clusters de terceiros são livres, tempo limitado clusters de malha do serviço hospedado no Azure e executar pela equipe do Service Fabric Olá em que qualquer pessoa pode implantar aplicativos e saiba mais sobre a plataforma de saudação. acesso de tooget tooa de Cluster, [siga instruções Olá](http://aka.ms/tryservicefabric). 

Para obter informações sobre como criar seu próprio cluster, consulte [Criar seu primeiro cluster do Service Fabric no Azure](service-fabric-get-started-azure-cluster.md).

> [!Note]
> serviço de front-end de web de saudação é toolisten configurado na porta 8080 para tráfego de entrada. Verifique se a porta está aberta no cluster. Se você estiver usando Olá Cluster de terceiros, essa porta está aberta.
>

### <a name="deploy-hello-application-using-visual-studio"></a>Implantar o aplicativo hello usando o Visual Studio
Agora que o aplicativo hello estiver pronto, você pode implantar tooa cluster diretamente do Visual Studio.

1. Clique com botão direito **votação** em Olá Gerenciador de soluções e escolha **publicar**. caixa de diálogo de publicação de saudação é exibida.

    ![Caixa de diálogo Publicar](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. Digite hello ponto de extremidade de Conexão de cluster Olá Olá **ponto de extremidade de Conexão** campo e clique em **publicar**. Ao se inscrever para Olá Cluster de terceiros, Olá ponto de extremidade de Conexão é fornecida no navegador de saudação. – por exemplo, `winh1x87d1d.westus.cloudapp.azure.com:19000`.

3. Abra um navegador e digite no endereço de cluster Olá - por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com`. Agora você verá o aplicativo hello em execução no cluster Olá no Azure.

![Front-end do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>Dimensionar aplicativos e serviços em um cluster
Serviços de malha do serviço podem ser facilmente dimensionados em tooaccommodate um cluster de uma alteração na carga Olá nos serviços de saudação. Dimensionar um serviço alterando Olá número de instâncias em execução no cluster de saudação. Você tem vários modos de dimensionar seus serviços usando scripts ou comandos do PowerShell ou a CLI do Service Fabric (sfctl). Neste exemplo, estamos usando o Service Fabric Explorer.

Gerenciador do Service Fabric é executado em todos os clusters de malha do serviço e pode ser acessada em um navegador, navegando porta de gerenciamento de clusters HTTP toohello (19080), por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.

Olá tooscale serviço front-end da web, Olá seguintes etapas:

1. Abra o Service Fabric Explorer no cluster – por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
2. Clique em Olá reticências (três pontos) próximo toohello **malha: / votação/VotingWeb** nó no hello treeview e escolha **serviço escala**.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    Agora você pode escolher o número de saudação tooscale de instâncias do serviço de front-end de web hello.

3. Alterar o número de saudação muito**2** e clique em **serviço escala**.
4. Clique em Olá **fabric: / votação/VotingWeb** nó no Olá a exibição de árvore e expanda o nó da partição hello (representado por um GUID).

    ![Dimensionar Serviço do Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    Agora você pode ver que o serviço Olá tem duas instâncias e na exibição de árvore de saudação você ver quais nós Olá instâncias executadas em.

Por esta tarefa de gerenciamento simples, nós o dobro recursos de saudação disponíveis para nossa carga de usuário do serviço front-end tooprocess. É importante toounderstand que você não precisa de várias instâncias de um toohave serviço executados de modo confiável. Se um serviço falhar, o Service Fabric certifica-se de que uma nova instância de serviço é executado no cluster hello.

## <a name="perform-a-rolling-application-upgrade"></a>Executar um upgrade sem interrupção do aplicativo
Ao implantar o novo aplicativo de tooyour atualizações, Service Fabric lança Olá atualização de uma maneira segura. As atualizações sem interrupção fornecem tempo de inatividade zero durante a atualização, bem como a reversão automática no caso de erros.

tooupgrade Olá aplicativo, Olá a seguir:

1. Olá abrir **cshtml** arquivo no Visual Studio - você pode procurar arquivo Olá Olá Gerenciador de soluções do Visual Studio.
2. Alterar o título de saudação na página Olá adicionando algum texto - por exemplo.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. Salve o arquivo hello.
4. Clique com botão direito **votação** em Olá Gerenciador de soluções e escolha **publicar**. caixa de diálogo de publicação de saudação é exibida.
5. Clique em Olá **versão manifesto** botão toochange Olá versão Olá serviço e aplicativo.
6. Alterar a versão de saudação do hello **código** elemento sob **VotingWebPkg** muito "2.0.0", por exemplo e clique em **salvar**.

    ![Caixa de diálogo Alterar Versão](./media/service-fabric-quickstart-dotnet/change-version.png)
7. Em Olá **publicar aplicativo do Service Fabric** caixa de diálogo, caixa de seleção seleção Olá Olá atualização aplicativo e clique em **publicar**.

    ![Configuração de Upgrade da caixa de diálogo Publicar](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. Abra seu navegador e procurar o endereço de cluster toohello na porta 19080 - por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
9. Clique em Olá **aplicativos** nó no modo de exibição de árvore Olá e, em seguida, **atualizações em andamento** no painel direito da saudação. Você verá como a atualização de saudação acumula através de domínios de atualização de saudação em seu cluster, certificando-se de que cada domínio está íntegro antes de continuar toohello lado.
    ![Modo de Exibição de Upgrade no Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)

    Service Fabric faz atualizações seguro esperando dois minutos após a atualização de serviço de saudação em cada nó no cluster hello. Espere Olá toda atualização tootake aproximadamente oito minutos.

10. Durante a execução de atualização hello, você ainda pode usar o aplicativo hello. Porque você tem duas instâncias do serviço de saudação em execução no cluster hello, algumas das suas solicitações podem obter uma versão atualizada do aplicativo hello, enquanto outros usuários ainda poderão obter a versão antiga do hello.

## <a name="next-steps"></a>Próximas etapas
Neste guia de início rápido, você aprendeu a:

> [!div class="checklist"]
> * Criar um aplicativo usando o .NET e o Service Fabric
> * Usar o ASP.NET Core como um front-end da Web
> * Armazenar dados de aplicativo em um serviço com estado
> * Depurar o aplicativo localmente
> * Implantar Olá aplicativo tooa cluster no Azure
> * Aplicativo de expansão Olá em vários nós
> * Executar um upgrade sem interrupção do aplicativo

toolearn mais sobre o serviço de malha e .NET, examine este tutorial:
> [!div class="nextstepaction"]
> [Aplicativo .NET no Service Fabric](service-fabric-tutorial-create-dotnet-app.md)