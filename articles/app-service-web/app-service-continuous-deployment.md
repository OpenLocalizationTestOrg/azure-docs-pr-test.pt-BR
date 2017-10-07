---
title: "aaaContinuous tooAzure de implantação do serviço de aplicativo | Microsoft Docs"
description: "Saiba como tooenable tooAzure de implantação contínua do serviço de aplicativo."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>TooAzure de implantação contínua do serviço de aplicativo
Este tutorial mostra como tooconfigure um fluxo de trabalho de implantação contínua para seu [do serviço de aplicativo do Azure] aplicativo. Integração com o serviço de aplicativo com BitBucket, GitHub, e [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) habilita um contínua fluxo de trabalho de implantação onde Azure recebe atualizações mais recentes de saudação do seu projeto publicado tooone desses serviços. A implantação contínua é uma ótima opção para projetos nos quais várias contribuições frequentes são integradas.

toofind-out como a implantação contínua tooconfigure manualmente a partir de um repositório de nuvem não listada Olá Portal do Azure (como [GitLab](https://gitlab.com/)), consulte [Configurando implantação contínua usando as etapas manuais](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Habilitar a implantação contínua
implantação contínua de tooenable,

1. Publica o repositório de conteúdo toohello do aplicativo que será usado para implantação contínua.  
    Para obter mais informações sobre a publicação de seus serviços de toothese de projeto, consulte [criar um repositório (GitHub)], [criar um repositório (BitBucket)], e [Introdução ao VSTS].
2. Na folha de menu do aplicativo no hello [portal do Azure], clique em **implantação de aplicativos > Opções de implantação**. Clique em **Escolher fonte**, em seguida, selecione origem de implantação de saudação.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure uma conta do VSTS para implantação de serviço de aplicativo, consulte este [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Concluir o fluxo de trabalho de autorização de saudação.
4. Em Olá **origem de implantação** folha, escolha o projeto hello e branch toodeploy do. Quando terminar, clique em **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Ao habilitar a implantação contínua com GitHub ou BitBucket, os projetos públicos e privados serão exibidos.
   > 
   > 
   
    Serviço de aplicativo cria uma associação com o repositório selecionado hello, extrai nos arquivos de saudação do branch de saudação especificado e mantém um clone do repositório para seu aplicativo de serviço de aplicativo. Quando você configurar uma implantação contínua de saudação do portal Azure VSTS, integração Olá usa saudação do serviço de aplicativo [mecanismo de implantação do Kudu](https://github.com/projectkudu/kudu/wiki), que já automatiza tarefas de compilação e implantação com cada `git push`. Você não precisa tooseparately configurar implantação contínua no VSTS. Depois que esse processo for concluído, hello **opções de implantação** folha aplicativo mostrará uma implantação ativa que indica a implantação foi bem-sucedida.
5. tooverify Olá aplicativo é implantado com êxito, clique em Olá **URL** na parte superior de saudação da folha de saudação do aplicativo no portal do Azure de saudação.
6. tooverify implantação contínua está ocorrendo no repositório de saudação de sua escolha, enviar por push a um repositório de toohello de alteração. Seu aplicativo deve atualizar as alterações de saudação tooreflect logo após a conclusão do repositório de toohello push hello. Você pode verificar que ter recebido atualização Olá Olá **opções de implantação** folha do seu aplicativo.

## <a name="VSsolution"></a>Implantação contínua de uma solução do Visual Studio
Enviar um tooAzure de solução do Visual Studio do serviço de aplicativo é tão fácil quanto enviar um arquivo simples index. HTML. Olá processo de implantação do serviço de aplicativo simplifica a todos os detalhes de hello, incluindo restauração dependências do NuGet e compilar os binários do aplicativo hello. Você pode siga as práticas recomendadas de controle do código-fonte de saudação de manter o código apenas em seu repositório Git e permitem que a implantação do serviço de aplicativo cuidar do rest hello.

Olá etapas para enviar por push o tooApp de solução do Visual Studio são Olá mesmo como Olá [seção anterior](#overview), desde que você configure sua solução e o repositório da seguinte maneira:

* Use Olá Visual Studio fonte controle opção toogenerate um `.gitignore` arquivo como imagem de saudação abaixo ou adicione manualmente um `.gitignore` arquivo na raiz do repositório com conteúdo toothis semelhante [. gitignore exemplo](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Adicione repositório de tooyour árvore do diretório da solução inteira Olá, com o arquivo hello na raiz do repositório de saudação.

Depois de configurar o repositório conforme descrito e configurado o seu aplicativo no Azure para a publicação contínua de um dos repositórios Git on-line de saudação, você pode desenvolver seu aplicativo ASP.NET localmente no Visual Studio e continuamente implantar seu código simplesmente por Enviar por push o repositório do Git alterações tooyour on-line.

## <a name="disableCD"></a>Desabilitar a implantação contínua
implantação contínua de toodisable,

1. Na folha de menu do aplicativo no hello [portal do Azure], clique em **implantação de aplicativos > Opções de implantação**. Em seguida, clique em **Disconnect** em Olá **opções de implantação** folha.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Depois de responder **Sim** toohello mensagem de confirmação, você pode retornar a folha de tooyour do aplicativo e clique em **implantação de aplicativos > Opções de implantação** se você gostaria que tooset a publicação de outra origem.

## <a name="additional-resources"></a>Recursos adicionais
* [Como tooinvestigate comum problemas com implantação contínua](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Como toouse PowerShell do Azure]
* [Como toouse Olá ferramentas de linha de comando do Azure para Mac e Linux]
* [Documentação do Git]
* [Kudu do Projeto](https://github.com/projectkudu/kudu/wiki)
* [Usar o Azure tooautomatically gerar um aplicativo do CI/CD pipeline toodeploy um ASP.NET 4](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

[do serviço de aplicativo do Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portal do Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Como toouse PowerShell do Azure]: /powershell/azureps-cmdlets-docs
[Como toouse Olá ferramentas de linha de comando do Azure para Mac e Linux]:../cli-install-nodejs.md
[Documentação do Git]: http://git-scm.com/documentation

[criar um repositório (GitHub)]: https://help.github.com/articles/create-a-repo
[criar um repositório (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Introdução ao VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
