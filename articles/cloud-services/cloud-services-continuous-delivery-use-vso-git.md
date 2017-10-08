---
title: entrega de aaaContinuous com Git e do Visual Studio Team Services no Azure | Microsoft Docs
description: "Saiba como tooconfigure o Visual Studio Team Services projetos da equipe toouse Git tooautomatically criar e implantar o recurso de aplicativo Web toohello nos serviços de nuvem ou do serviço de aplicativo do Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>Fornecimento contínuo tooAzure usando o Visual Studio Team Services e o Git
Você pode usar toohost de projetos de equipe do Visual Studio Team Services um repositório Git para seu código-fonte e automaticamente criar e implantar aplicativos da web de tooAzure ou serviços em nuvem sempre que você enviar por push a um repositório de toohello de confirmação.

Você precisará Visual Studio 2013 e hello SDK do Azure instalado. Se você ainda não tiver o Visual Studio 2013, baixá-lo escolhendo Olá **comece gratuitamente** link [www.visualstudio.com](http://www.visualstudio.com). Instalar Olá SDK do Azure na [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> É necessário um toocomplete de conta do Visual Studio Team Services este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset a um tooautomatically de serviço de nuvem compilar e implantar tooAzure usando o Visual Studio Team Services, siga estas etapas.

## <a name="1-create-a-git-repository"></a>1: Criar um repositório Git
1. Se você ainda não tiver uma conta do Visual Studio Team Services, pode obter uma [aqui](http://go.microsoft.com/fwlink/?LinkId=397665). Quando criar seu projeto da equipe, escolha o Git como seu sistema de controle do código-fonte. Execute o projeto de equipe de tooyour Olá instruções tooconnect Visual Studio.
2. Em **Team Explorer**, escolha Olá **a clonagem deste repositório** link.
   
    ![][3]
3. Especificar local de saudação da cópia local do hello e escolha Olá **Clone** botão.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: criar um projeto e confirmá-la toohello repositório
1. Em **Team Explorer**, em Olá **soluções** , escolha Olá **novo** link toocreate um novo projeto no repositório local hello.
   
    ![][4]
2. Você pode implantar um aplicativo web ou um serviço de nuvem (aplicativo do Azure) pelo Olá seguir as etapas neste passo a passo. Crie um novo projeto de Serviço de Nuvem do Azure ou um novo projeto ASP.NET MVC. Certifique-se de destinos do projeto Olá Olá .NET Framework 4 ou posterior. Se você está criando um projeto de serviço de nuvem, adicione uma função de trabalho e uma função web MVC do ASP.NET.
   Se você quiser toocreate um aplicativo web, escolha Olá **aplicativo Web ASP.NET** modelo de projeto e escolha **MVC**. Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md) para obter mais informações.
3. Abra Olá menu de atalho Olá solução e escolha **confirmar**.
   
    ![][7]
4. Se esse for Olá pela primeira vez que você usou o Git no Visual Studio Team Services, você precisará tooprovide tooidentify algumas informações por conta própria no Git. Em Olá **alterações pendentes** área de **Team Explorer**, insira seu nome de usuário e endereço de email. Digite um comentário para confirmação hello e escolha Olá **confirmação** botão.
   
    ![][8]
5. Observação: Olá opções tooinclude ou excluir alterações específicas ao fazer check-in. Se Olá alterações que você deseja são excluídos, escolha **incluir tudo**.
6. Você tem agora Olá confirmada alterações em sua cópia local do repositório de saudação. Em seguida, sincronizar as alterações com o servidor de saudação escolhendo Olá **sincronização** link.

## <a name="3-connect-hello-project-tooazure"></a>3: conectar Olá projeto tooAzure
1. Agora que você tem um repositório Git no Visual Studio Team Services com um código de origem nele, você está pronto tooconnect seu tooAzure de repositório do git.  Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione o aplicativo web ou serviço de nuvem ou crie um novo escolhendo o ícone na esquerda inferior hello e escolhendo + Olá **serviço de nuvem** ou **aplicativo Web**e **criação rápida**.
   
    ![][9]
2. Para serviços de nuvem, escolha Olá **configurar a publicação com o Visual Studio Team Services** link. Para aplicativos da web, escolha Olá **configurar a implantação do controle de origem** link.
   
    ![][10]
3. No Assistente de saudação, digite o nome de saudação da sua conta do Visual Studio Team Services na caixa de texto de saudação e escolha Olá **autorizar agora** link. Você pode ser solicitado toosign no.
   
    ![][11]
4. Em Olá **solicitação de Conexão** caixa de diálogo pop-up, escolha **aceitar** tooauthorize tooconfigure do Azure que sua equipe de projeto no Visual Studio Team Services.
   
    ![][12]
5. Depois que a autorização obtiver êxito, você verá uma lista suspensa que contém os projetos de equipe do Visual Studio Team Services.  Selecione Olá nome de projeto de equipe que você criou nas etapas anteriores hello e escolha o botão de marca de seleção do Assistente de saudação.
   
    ![][13]
   
    Olá próxima vez que você enviar por push a um repositório de tooyour confirmação, o Visual Studio Team Services criará e implantará tooAzure seu projeto.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Disparar uma recompilação e reimplantar seu projeto
1. No Visual Studio, abra um arquivo e altere-o. Por exemplo, altere o arquivo hello `_Layout.cshtml` em modos de exibição de saudação\\pasta compartilhada em uma função da web MVC.
   
    ![][17]
2. Editar texto de rodapé Olá para o site de saudação e salve o arquivo hello.
   
    ![][18]
3. Em **Solution Explorer**, abra o menu de atalho de Olá Olá Olá, nó de projeto ou nó da solução arquivo você alterado e, em seguida, escolha **confirmar**.
4. Digite um comentário e escolha **Confirmar**.
   
    ![][20]
5. Escolha Olá **sincronização** link.
   
    ![][38]
6. Escolha Olá **Push** link toopush seu repositório de toohello de confirmação no Visual Studio Team Services. (Você também pode usar o hello **sincronização** botão toocopy seu repositório de toohello confirmações. Olá diferença é que **sincronização** também recebe Olá últimas alterações no repositório de hello.)
   
    ![][39]
7. Escolha Olá **inicial** botão tooreturn toohello **Team Explorer** página inicial.
   
    ![][21]
8. Escolha **cria** tooview Olá compilações em andamento.
   
    ![][22]
   
    **Team Explorer** mostra que uma compilação foi disparada para seu check-in.
   
    ![][23]
9. tooview um log detalhado Olá compilação em andamento, clique duas vezes no nome Olá Olá compilação em andamento.
10. Enquanto a compilação de saudação está em andamento, dê uma olhada na definição de compilação de saudação que foi criada quando você usou Olá Assistente toolink tooAzure.  Abra o menu de atalho Olá Olá para definição de compilação e escolha **editar definição de compilação**.
    
    ![][25]
11. Em Olá **gatilho** guia, você verá que definição de compilação de saudação é definida toobuild em cada check-in, por padrão. (Para um serviço de nuvem do Visual Studio Team Services cria e implanta Olá ramificação mestre toohello automaticamente o ambiente de preparo. Você ainda terá toodo site ao vivo do toodeploy toohello uma etapa manual. Para um aplicativo web que não tem um ambiente de preparo, implanta ramificação mestre Olá diretamente toohello live site.
    
    ![][26]
12. Em Olá **processo** guia, você pode ver o ambiente de implantação Olá é definido toohello nome do seu aplicativo web ou serviço de nuvem.
    
     ![][27]
13. Especifica valores para propriedades de saudação se você quiser que os valores diferentes de padrões de saudação. Olá propriedades de publicação do Azure estão em Olá **implantação** seção e você talvez também seja necessário tooset MSBuild parâmetros. Por exemplo, em um projeto de serviço de nuvem, toospecify uma configuração de serviço diferente de "Nuvem", definir muito Olá MSbuild parâmetros`/p:TargetProfile=[YourProfile]` onde *[YourProfile]* corresponde a um arquivo de configuração de serviço com um nome como ServiceConfiguration. *YourProfile*. cscfg.
    
     Olá tabela a seguir mostra propriedades disponíveis Olá em Olá **implantação** seção:
    
    | Propriedade | Valor Padrão |
    | --- | --- |
    | Permitir certificados não confiáveis |Se falso, os certificados SSL deve ser assinados por uma autoridade raiz. |
    | Permitir Atualização |Olá implantação tooupdate permite que uma implantação existente em vez de criar um novo. Preserva o endereço IP hello. |
    | Não exclua |Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida). |
    | Caminho tooDeployment configurações |Olá caminho tooyour. pubxml arquivo para um aplicativo web, a pasta raiz de toohello relativo do repositório de saudação. Ignorado para serviços de nuvem. |
    | Ambiente de implantação do Sharepoint |Olá mesmo como o nome do serviço hello. |
    | Ambiente de implantação do Azure |Olá aplicativo ou nuvem nome do serviço web. |
14. A essa altura, sua compilação deve estar concluída com êxito.
    
     ![][28]
15. Se você clicar duas vezes nome de compilação hello, o Visual Studio mostra uma **Resumo da compilação**, incluindo os resultados dos testes de associadas a projetos de teste de unidade.
    
     ![][29]
16. Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você pode exibir a implantação de saudação associada em Olá **implantações** guia quando Olá ambiente de preparo é selecionado.
    
     ![][30]
17. Procure tooyour URL do seu site. Para um aplicativo web, basta escolher Olá **procurar** botão no portal de saudação. De um serviço de nuvem, escolha URL Olá Olá **rápidos** seção Olá **painel** página que mostra o ambiente de preparo hello.
    
    As implantações de integração contínua para serviços de nuvem são publicados toohello ambiente de preparo por padrão. Você pode alterar essa configuração Olá **ambiente de serviço de nuvem alternativo** propriedade muito**produção**. Aqui é onde Olá URL do site na página do painel do serviço de nuvem hello.
    
    ![][31]
    
    Uma nova guia do navegador será aberto tooreveal seu site em execução.
    
    ![][32]
18. Se você fizer outras alterações tooyour projeto, você gatilho mais cria e acumularão várias implantações. Olá mais recente um é marcado como ativo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Reimplantar um build anterior
Esta etapa é opcional. Olá portal clássico do Azure, escolha uma implantação anterior e escolha **reimplantar** toorewind tooan seu site anteriormente check-in. Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: alterar a implantação de produção de hello
Quando você estiver pronto, você pode promover Olá preparo toohello ambiente de produção, escolhendo **trocar** em Olá portal clássico do Azure. ambiente de preparo Olá implantado recentemente é promovida tooProduction e ambiente de produção anterior hello, se houver, torna-se um ambiente de preparo. Olá implantação ativa pode ser diferente para ambientes de preparo e produção de hello, mas o histórico de implantação de saudação de builds recentes é Olá mesmo independentemente do ambiente.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: Implantar por meio de uma ramificação em funcionamento.
Quando você usa o Git, você normalmente fazer alterações em uma ramificação de trabalho e integrar a ramificação mestre hello quando o desenvolvimento de atinge um estado concluído. Durante a fase de desenvolvimento de saudação de um projeto, você deseja toobuild e implantar Olá tooAzure de ramificação de trabalho.

1. Em **Team Explorer**, escolha Olá **início** botão e, em seguida, escolha Olá **ramificações** botão.
   
    ![][40]
2. Escolha Olá **nova ramificação** link.
   
    ![][41]
3. Insira nome de saudação do branch hello, como "trabalho" e escolha **criar ramificação**. Isso cria uma nova ramificação local.
   
    ![][42]
4. Publica o branch de saudação. Escolher nome de branch Olá em **não publicado ramificações**e escolha **publicar**.
   
    ![][44]
5. Por padrão, somente altera o disparador de ramificação mestre toohello uma compilação contínua. tooset backup contínua compilação para uma ramificação de trabalho, escolha Olá **cria** página **Team Explorer**e escolha **editar definição de compilação**.
6. Olá abrir **configurações de fonte** guia. Em **monitorados ramificações de integração contínua e compilação**, escolha **clique aqui tooadd uma nova linha**.
   
    ![][47]
7. Especifique a ramificação de saudação que você criou, como cabeçalhos/refs/trabalho.
   
    ![][48]
8. Faça uma alteração no código hello, menu de atalho Olá abrir arquivo hello alterado e, em seguida, escolha **confirmar**.
   
    ![][43]
9. Escolha Olá **as confirmações** link e escolha Olá **sincronização** botão ou hello **Push** saudação do link toocopy altera toohello cópia de ramificação de trabalho Olá no Visual Studio Serviços de equipe.
   
   ![][45]
10. Navegue toohello **cria** exibir e encontrar a compilação de saudação que foi disparada apenas para a ramificação de trabalho hello.

## <a name="next-steps"></a>Próximas etapas
toolearn mais dicas sobre como usar o Git com o Visual Studio Team Services, consulte [desenvolver e compartilhar seu código no Git usando o Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) e para obter informações sobre como usar um repositório Git que não é gerenciado pelo Visual Studio Team Services toopublish tooAzure, consulte [tooAzure implantação contínua do serviço de aplicativo](../app-service-web/app-service-continuous-deployment.md). Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
