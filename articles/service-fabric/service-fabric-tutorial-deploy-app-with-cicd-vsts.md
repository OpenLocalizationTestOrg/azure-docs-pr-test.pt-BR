---
title: "aaaDeploy um aplicativo do Azure Service Fabric com integração contínua (Team Services) | Microsoft Docs"
description: "Saiba como tooset integração contínua e implantação para um aplicativo de malha do serviço usando o Visual Studio Team Services.  Implante um cluster do Service Fabric do tooa de aplicativo no Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Implantar um aplicativo com o cluster do CI/CD tooa do Service Fabric
Este tutorial é parte três de uma série e descreve como tooset integração contínua e implantação de um aplicativo do Azure Service Fabric usando o Visual Studio Team Services.  Um aplicativo do Service Fabric existente é necessária, o aplicativo hello criado no [criar um aplicativo .NET](service-fabric-tutorial-create-dotnet-app.md) é usado como um exemplo.

Na parte três Olá série, você aprenderá como:

> [!div class="checklist"]
> * Adicionar projeto de tooyour de controle de origem
> * Criar uma definição de build no Team Services
> * Criar uma definição de versão no Team Services
> * Implantar e atualizar automaticamente um aplicativo

Nesta série de tutoriais, você aprenderá a:
> [!div class="checklist"]
> * [Criar um aplicativo .NET do Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * [Implantar aplicativos de saudação tooa cluster remoto](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurar CI/CD usando o Visual Studio Team Services

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Instalar o Visual Studio de 2017](https://www.visualstudio.com/) e instalar Olá **desenvolvimento do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
- [Instalar Olá SDK do Service Fabric](service-fabric-get-started.md)
- Crie um aplicativo do Service Fabric; você pode [seguir este tutorial](service-fabric-tutorial-create-dotnet-app.md) como exemplo. 
- Crie um cluster do Service Fabric do Windows no Azure; você pode [seguir este tutorial](service-fabric-tutorial-create-cluster-azure-ps.md) como exemplo
- Crie uma [conta do Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Baixe o aplicativo de exemplo hello votação
Se você não criar aplicativo de exemplo hello voto [parte um esta série de tutoriais](service-fabric-tutorial-create-dotnet-app.md), você pode baixá-lo. Em uma janela de comando, execute Olá comando tooclone Olá aplicativo repositório tooyour local máquina de exemplo a seguir.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Preparar um perfil de publicação
Agora que você já [criou um aplicativo](service-fabric-tutorial-create-dotnet-app.md) e ter [implantado Olá aplicativo tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), você está pronto tooset a integração contínua.  Primeiro, prepare um perfil de publicação dentro de seu aplicativo para uso pelo processo de implantação de saudação que é executado no Team Services.  saudação de perfil de publicação deve ser o cluster de saudação tootarget configurado que você criou anteriormente.  Inicie o Visual Studio e abra um projeto de aplicativo do Service Fabric existente.  Em **Solution Explorer**, aplicativo hello e selecione **publicar...** .

Escolha um perfil de destino em seu toouse de projeto de aplicativo para o fluxo de trabalho de integração contínua e, em seguida, por exemplo na nuvem.  Especifique o ponto de extremidade de conexão de cluster hello.  Verificar Olá **atualização Olá aplicativo** caixa de seleção para que seu aplicativo atualizado para cada implantação no Team Services.  Clique em Olá **salvar** hiperlink toosave Olá configurações toohello perfil de publicação e, em seguida, clique em **Cancelar** tooclose caixa de diálogo de saudação.  

![Perfil de envio por push][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Compartilhar seu repositório Git do Team Services novo Visual Studio solução tooa
Compartilhe seus arquivos de origem do aplicativo tooa o projeto de equipe no Team Services, portanto, você pode gerar cria.  

Criar um novo repositório Git local para seu projeto selecionando **adicionar tooSource controle** -> **Git** na barra de status de saudação no canto inferior direito de saudação do Visual Studio. 

Em Olá **Push** exibir em **Team Explorer**, selecione Olá **publicar o repositório do Git** botão em **Push tooVisual Studio Team Services**.

![Enviar por push o repositório Git][push-git-repo]

Verifique seu email e selecione sua conta no hello **equipe de serviços de domínio** lista suspensa. Digite o nome do seu repositório e selecione **Publicar Repositório**.

![Enviar por push o repositório Git][publish-code]

Publicar o repositório de saudação cria um novo projeto de equipe em sua conta com hello mesmo nome como o repositório local hello. repositório de saudação toocreate em um projeto de equipe existente, clique em **avançado** Avançar muito**repositório** nome e selecione um projeto de equipe. Você pode exibir seu código em Olá web selecionando **vê-lo na web hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurar a entrega contínua com VSTS
Uma definição de build do Team Services descreve um fluxo de trabalho composto por um conjunto de etapas de compilação que são executadas sequencialmente. Crie uma definição de compilação que produz um pacote de aplicativo de malha do serviço e outros artefatos, cluster do toodeploy tooa do Service Fabric. Saiba mais sobre as [definições de build do Team Services](https://www.visualstudio.com/docs/build/define/create). 

Uma definição de versão do Team Services descreve um fluxo de trabalho que implanta um cluster de tooa do pacote de aplicativo. Quando usados juntos, a definição de compilação hello e definição versão executar o fluxo de trabalho inteiro Olá começando com tooending de arquivos de origem com um aplicativo em execução no cluster. Saiba mais sobre as [definições de versão](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)do Team Services.

### <a name="create-a-build-definition"></a>Criar a definição de build
Abra um navegador da web e navegue tooyour novo projeto de equipe em: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Selecione Olá **Build e versão** guia, em seguida, **cria**, em seguida, **+ nova definição de**.  Em **selecionar um modelo de**, selecione Olá **aplicativo do Azure Service Fabric** modelo e clique em **aplicar**. 

![Escolher o modelo de build][select-build-template] 

Olá votação de aplicativo contém um projeto .NET Core, para adicionar uma tarefa que restaura dependências hello. Em Olá **tarefas** exibição, selecione **+ adicionar tarefa** na parte inferior de saudação à esquerda. Pesquisar na tarefa de linha de comando "Linha de comando" toofind hello, clique em **adicionar**. 

![Adicionar tarefa][add-task] 

Na nova tarefa de hello, digite "Executar dotnet.exe" do **nome de exibição**, "dotnet.exe" em **ferramenta**e "restauração" no **argumentos**. 

![Nova tarefa][new-task] 

Em Olá **gatilhos** exibir, clique em Olá **habilitar esse gatilho** alternar em **integração contínua**. 

Selecione **Salvar & fila** e insira as "Hospedado VS2017" hello **fila Agent**. Selecione **fila** toomanually iniciar uma compilação.  A compilação também é disparada durante o push ou check-in.

toocheck o progresso da compilação, comutador toohello **cria** guia.  Depois de confirmar que a compilação de saudação for executado com êxito, defina uma definição de lançamento que implanta o cluster de tooa do aplicativo. 

### <a name="create-a-release-definition"></a>Criar uma definição de versão  

Selecione Olá **Build e versão** guia, em seguida, **versões**, em seguida, **+ nova definição**.  Em **criar definição de versão**, selecione Olá **implantação de malha do serviço Azure** modelo na lista de saudação e clique em **próximo**.  Selecione Olá **criar** de origem, verifique Olá **implantação contínua** caixa e clique em **criar**. 

Em Olá **ambientes** exibir, clique em **adicionar** toohello à direita do **Conexão Cluster**.  Especifique um nome de conexão de "mysftestcluster", um ponto de extremidade do cluster de "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" e Olá Active Directory do Azure ou as credenciais de certificado para o cluster de saudação. As credenciais do Active Directory do Azure, definir credenciais de saudação deseja toouse tooconnect toohello cluster Olá **Username** e **senha** campos. Para a autenticação baseada em certificado, defina Olá Base64 codificação do arquivo de certificado de cliente Olá no hello **certificado de cliente** campo.  Consulte a Ajuda pop-up a saudação nesse campo para obter informações sobre como tooget esse valor.  Se o certificado for protegido por senha, definir senha de saudação em Olá **senha** campo.  Clique em **salvar** toosave definição de versão de saudação.

![Adicionar conexão do cluster][add-cluster-connection] 

Clique em **Executar em agente** e selecione **VS2017 Hospedado** para **Fila de implantação**. Clique em **salvar** toosave definição de versão de saudação.

![Executar no agente][run-on-agent]

Selecione **+ versão** -> **criar versão** -> **criar** toomanually criar uma versão.  Verifique se que Olá implantação bem-sucedida e o aplicativo hello está em execução no cluster de saudação.  Abra um navegador da web e navegue muito[http://mysftestcluster.westus.cloudapp.azure.com:19080Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Observe a versão do aplicativo hello, neste exemplo é "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Confirmar e enviar alterações por push, disparar uma versão
tooverify que Olá pipeline de integração contínua está funcionando, verificando em algumas alterações de código tooTeam serviços.    

Ao escrever seu código, suas alterações são rastreadas automaticamente pelo Visual Studio. Confirmar alterações tooyour repositório local do Git selecionando Olá pendentes alterações ícone (![Pendente][pending]) na barra de status de saudação na parte inferior de saudação à direita.

Em Olá **alterações** no Team Explorer, adicione uma mensagem que descreve a atualização e confirmar as alterações.

![Confirmar tudo][changes]

Ícone de barra de status de alterações não publicadas Olá Select (![alterações não publicadas][unpublished-changes]) ou Olá exibição de sincronização no Team Explorer. Selecione **Push** tooupdate seu código no Team Services/TFS.

![Enviar alterações por push][push]

Enviar por push Olá alterações tooTeam Services automaticamente gatilhos uma compilação.  Quando a definição de compilação Olá for concluído com êxito, uma versão é criada automaticamente e inicia a atualização de aplicativo hello no cluster hello.

toocheck o progresso da compilação, comutador toohello **cria** guia **Team Explorer** no Visual Studio.  Depois de confirmar que a compilação de saudação for executado com êxito, defina uma definição de lançamento que implanta o cluster de tooa do aplicativo.

Verifique se que Olá implantação bem-sucedida e o aplicativo hello está em execução no cluster de saudação.  Abra um navegador da web e navegue muito[http://mysftestcluster.westus.cloudapp.azure.com:19080Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Observe a versão do aplicativo hello, neste exemplo é "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Atualizar o aplicativo hello
Fazer alterações de código no aplicativo hello.  Salve e confirmar as alterações hello, seguindo as etapas anteriores hello.

Depois de atualização de saudação do aplicativo hello começa, você pode assistir o progresso da atualização Olá no Gerenciador do Service Fabric:

![Service Fabric Explorer][sfx2]

atualização do aplicativo Hello pode levar vários minutos. Quando a saudação atualização for concluída, aplicativo hello executará próxima versão de saudação.  Neste exemplo, "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Adicionar projeto de tooyour de controle de origem
> * Criar a definição de build
> * Criar uma definição de versão
> * Implantar e atualizar automaticamente um aplicativo

Agora que você tiver um aplicativo implantado e configurado a integração contínua, tente o seguinte hello:
- [Atualizar um aplicativo](service-fabric-application-upgrade.md)
- [Testar um aplicativo](service-fabric-testability-overview.md) 
- [Monitorar e diagnosticar](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png