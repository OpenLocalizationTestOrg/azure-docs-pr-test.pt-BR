---
title: "desenvolvimento de software aaaAgile com o serviço de aplicativo do Azure"
description: "Saiba como toocreate alta escala aplicativos complexos com o serviço de aplicativo do Azure de forma que dá suporte ao desenvolvimento de software agile."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure
Neste tutorial, você aprenderá como aplicativos complexos de grande escala de toocreate com [do serviço de aplicativo do Azure](/azure/app-service/) de forma que dá suporte a [desenvolvimento de software agile](https://en.wikipedia.org/wiki/Agile_software_development). Ele pressupõe que você já sabe como muito[implantar aplicativos complexos previsível no Azure](app-service-deploy-complex-application-predictably.md).

Limitações em processos técnicas geralmente podem substituir o maneira Olá implementação bem-sucedida do metodologias agile. Serviço de aplicativo do Azure com recursos como [publicação contínua](app-service-continuous-deployment.md), [em ambientes de preparo](web-sites-staged-publishing.md) (slots), e [monitoramento](web-sites-monitor.md), quando associado criteriosamente orquestração hello e gerenciamento de implantação no [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), pode ser parte de uma solução excelente para desenvolvedores que adotam o desenvolvimento de software agile.

Olá, tabela a seguir é uma lista curta de requisitos associados ao desenvolvimento ágil, e como os serviços do Azure permitem que cada um deles.

| Requisito | Como o Azure o habilita |
| --- | --- |
| - Compilação com cada confirmação<br>- Compilação automática e rápida |Quando configurado com a implantação contínua, o Serviço de Aplicativo do Azure pode funcionar como compilações em execução em tempo real com base em uma ramificação de desenvolvimento. Sempre que o código é enviada por push o branch toohello, é automaticamente criado e em execução ao vivo no Azure. |
| - Realizar autoteste de compilações |Carregar testes, testes da web, etc., podem ser implantados com o modelo do Azure Resource Manager hello. |
| - Executar testes em um clone do ambiente de produção |Modelos do Gerenciador de recursos do Azure podem ser usado toocreate clones do ambiente de produção do Azure hello (incluindo as configurações do aplicativo, modelos de cadeia de caracteres de conexão, dimensionamento, etc.) para testar rapidamente e previsível. |
| - Exibir o resultado da compilação mais recente com facilidade |TooAzure implantação contínua de um repositório significa que você pode testar o novo código em um aplicativo ao vivo imediatamente após você confirmar suas alterações. |
| -Confirmar ramificação principal toohello todos os dias<br>- Automatizar a implantação |Integração contínua de um aplicativo de produção com ramificação principal do repositório implanta automaticamente a cada tooproduction de ramificação principal toohello confirmação/mesclagem. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>O que você fará
Você verá um fluxo de trabalho de desenvolvimento-teste de estágio de produção típico em ordem toopublish novas alterações toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) aplicativo de exemplo, que consiste em dois [aplicativos web](/services/app-service/web/), um sendo um front-end (FE) e Olá outro sendo um back-end da Web API (BE) e um [banco de dados SQL](/services/sql-database/). Você trabalhará com hello arquitetura de implantação a seguir:

![](./media/app-service-agile-software-development/what-1-architecture.png)

imagem de saudação tooput em palavras:

* arquitetura de implantação de saudação é separada em três ambientes distintos (ou [grupos de recursos](../azure-resource-manager/resource-group-overview.md) no Azure), cada qual com seu próprio [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [dimensionamento](web-sites-scale.md) configurações e o banco de dados SQL. 
* Cada ambiente pode ser gerenciado separadamente. Eles podem até mesmo existir em assinaturas diferentes.
* Preparo e produção são implementados como dois slots de saudação mesmo aplicativo de serviço de aplicativo. ramificação mestre Hello está configurada para integração contínua com hello slot de preparo.
* Quando uma ramificação de toomaster de confirmação é verificada em Olá preparo slot (com dados de produção), Olá Verificar preparação do aplicativo é trocado no slot de produção de hello [sem tempo de inatividade](web-sites-staged-publishing.md).

Olá ambiente de produção e preparo é definido pelo modelo de saudação [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Olá desenvolvimento e ambientes de teste são definidos pelo modelo de saudação [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Você também usará estratégia de ramificação típico hello, com o código de movimentação de ramificação de desenvolvimento Olá a ramificação de teste toohello, em seguida, toohello ramificação mestre (mover para cima na qualidade, caso toospeak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>O que você precisa
* Uma conta do Azure
* Uma conta do [GitHub](https://github.com/)
* Shell de Git (instalado com [GitHub para Windows](https://windows.github.com/))-permite que você toorun ambos Olá Git e do PowerShell comandos no hello mesma sessão 
* Bits do [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) mais recentes
* Noções básicas sobre Olá ferramentas a seguir:
  * Implantação do modelo do [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (consulte também [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Você precisa de uma conta do Azure toocomplete neste tutorial:
> 
> * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados você pode manter a conta de saudação e use livre serviços do Azure, como aplicativos Web.
> * É possível [ativar os benefícios para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) – todos os meses, sua assinatura do Visual Studio concede créditos que podem ser usados para experimentar serviços pagos do Azure.
> 
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="set-up-your-production-environment"></a>Configurar seu ambiente de produção
> [!NOTE]
> script Hello usado neste tutorial automaticamente configura a publicação contínua de seu repositório GitHub. Isso exige que suas credenciais do GitHub já são armazenados no Azure, caso contrário, Olá com script de implantação Falha ao tentar tooconfigure configurações de controle de origem para os aplicativos web hello. 
> 
> toostore seu GitHub credenciais no Azure, criar um aplicativo web no hello [portal do Azure](https://portal.azure.com/) e [configurar implantação GitHub](app-service-continuous-deployment.md). Você só precisa toodo desta vez. 
> 
> 

Em um cenário típico de DevOps, você tem um aplicativo que está em execução no Azure e desejar toomake tooit de alterações por meio da publicação contínua. Nesse cenário, você tem um modelo que você toodeploy desenvolvido, testado e usado Olá ambiente de produção. Você o configurará nesta seção.

1. Criar seu próprio bifurcação de saudação [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositório. Para obter informações sobre como criar a bifurcação, consulte [Bifurcar um repositório](https://help.github.com/articles/fork-a-repo/). Depois que a bifurcação é criada, você pode vê-la no navegador.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Abra uma sessão do Git Shell. Se ainda não tiver o Git Shell, instale o [GitHub para Windows](https://windows.github.com/) agora.
3. Crie um clone local de sua bifurcação executando Olá comando a seguir:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Uma vez que o clone local, navegue muito*&lt;repository_root >*\ARMTemplates e deploy.ps1 Olá execução de script da seguinte maneira:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Quando solicitado, digite Olá desejado de nome de usuário e senha para acesso ao banco de dados.
   
   Você deve ver Olá provisionamento progresso de vários recursos do Azure. Quando a implantação for concluída, o script hello inicia o aplicativo hello no navegador de saudação e oferecem um bipe amigável.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Dê uma olhada  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee como gera recursos com identificações exclusivas. Você pode usar o hello mesmo toocreate de abordagem clones de Olá implantação mesmo sem se preocupar com nomes de recursos conflitantes.
   > 
   > 
6. De volta à sessão do Git Shell, execute:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Quando o script hello termina, volte toobrowse toohello endereço do front-end (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) aplicativo hello de toosee em execução em produção.
8. Faça logon no toohello [portal do Azure](https://portal.azure.com/) e veja o que é criado.
   
   Você deve ser capaz de toosee dois os aplicativos web no hello mesmo grupo de recursos, um com hello `Api` sufixo no nome de saudação. Se você examinar o modo de exibição de grupo de recursos hello, também consulte Olá banco de dados SQL e servidor, Olá plano de serviço de aplicativo e slots de preparo Olá para aplicativos da web de saudação. Navegue pelos recursos diferentes hello e compará-los com  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json como eles são configurados no modelo de saudação.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Agora, você configurou o ambiente de produção de hello. Em seguida, você iniciará um novo aplicativo de toohello de atualização.

## <a name="create-dev-and-test-branches"></a>Criar o desenvolvimento e testar ramificações
Agora que você tem um aplicativo complexo em execução em produção no Azure, você criará um aplicativo de tooyour de atualização de acordo com a metodologia agile. Nesta seção, você criará Olá ramificações de desenvolvimento e teste que você precisará toomake Olá necessárias atualizações.

1. Crie ambiente de teste Olá primeiro. Na sua sessão do Shell de Git, seguinte Olá executar comandos toocreate ambiente de saudação para uma nova ramificação chamada **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Quando solicitado, digite Olá desejado de nome de usuário e senha para acesso ao banco de dados. 
   
   Quando a implantação for concluída, o script hello inicia o aplicativo hello no navegador de saudação e oferecem um bipe amigável. Agora você tem uma nova ramificação com ambiente de teste próprio. Leve um momento tooreview algumas coisas sobre esse ambiente de teste:
   
   * Você pode criá-lo em qualquer assinatura do Azure. Isso significa que o ambiente de produção de hello pode ser gerenciado separadamente do seu ambiente de teste.
   * Seu ambiente de teste está em execução em tempo real no Azure.
   * Ambiente de teste é o ambiente de produção toohello idênticos, exceto Olá slots de preparo e hello configurações de dimensionamento. Você sabe porque elas são as únicas diferenças Olá entre ProdandStage.json e dev.
   * Você pode gerenciar o ambiente de teste em seu próprio plano do Serviço de Aplicativo, com uma faixa de preço diferente (como **Gratuito**).
   * A exclusão desse ambiente de teste é tão simple quanto a exclusão de grupo de recursos de saudação. Você descobrirá como toodo isso [posteriormente](#delete).
3. Vá toocreate uma ramificação de desenvolvimento executando Olá comandos a seguir:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Quando solicitado, digite Olá desejado de nome de usuário e senha para acesso ao banco de dados. 
   
   Leve um momento tooreview algumas coisas sobre esse ambiente de desenvolvimento: 
   
   * Seu ambiente de desenvolvimento tem um ambiente de teste de toohello idênticos de configuração porque ele foi implantado usando Olá mesmo modelo.
   * Cada ambiente de desenvolvimento pode ser criado em saudação do desenvolvedor assinatura do Azure, deixando Olá toobe de ambiente de teste gerenciado separadamente.
   * O ambiente de desenvolvimento está em execução em tempo real no Azure.
   * Excluindo Olá dev ambiente é tão simple quanto a exclusão de grupo de recursos de saudação. Você descobrirá como toodo isso [posteriormente](#delete).

> [!NOTE]
> Quando você tiver vários desenvolvedores trabalhando em atualização de nova Olá, cada um deles pode criar facilmente uma ramificação e um ambiente de desenvolvimento dedicado com hello etapas a seguir:
> 
> 1. Criar seu próprios bifurcação do repositório de saudação no GitHub (consulte [dividir um repositório](https://help.github.com/articles/fork-a-repo/)).
> 2. Bifurcação de saudação do clone em seu computador local
> 3. Mesmo executar Olá comandos toocreate suas próprias ramificação de desenvolvimento e o ambiente.
> 
> 

Quando terminar, a bifurcação GitHub deverá ter três ramificações:

![](./media/app-service-agile-software-development/test-1-github-view.png)

E você deverá ter seis aplicativos Web (três conjuntos de dois) em três grupos de recursos separados:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json Especifica Olá Olá de toouse do ambiente de produção **padrão** preço, que é adequado para a escalabilidade do aplicativo de produção de hello.
> 
> 

## <a name="build-and-test-every-commit"></a>Compilar e testar cada confirmação
Olá arquivos de modelo ProdAndStage.json e dev já especificar parâmetros de controle de origem Olá, que por padrão define a publicação contínua de aplicativo da web de saudação. Portanto, cada ramificação de GitHub confirmação toohello dispara um tooAzure de implantação automática de ramificação. Vejamos como a configuração funciona.

1. Certifique-se de que você está na ramificação de desenvolvimento de saudação do repositório local hello. toodo, Olá executar comando no Shell de Git a seguir:
   
        git checkout Dev
2. Fazer a camada de interface do usuário do aplicativo de toohello uma alteração alterando Olá código toouse [Bootstrap](http://getbootstrap.com/components/) lista. Abra  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml e verifique Olá realçada alterações a seguir:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Se você não puder ler Olá imagem anterior: 
    > 
    > * Na linha 18, altere `check-list` muito`list-group`.
    > * Na linha 19, altere `class="check-list-item"` muito`class="list-group-item"`.
    > 
    > 
3. Salve a alteração de saudação. Volta no Shell de Git, execute Olá comandos a seguir:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Esses comandos git são semelhantes muito "Verificando no seu código" no outro sistema de controle do código-fonte como TFS. Quando você executa `git push`, confirmação novo Olá dispara um código automática por push tooAzure, que, em seguida, recria Olá aplicativo tooreflect Olá alteração no ambiente de desenvolvimento de saudação.
4. tooverify esse ambiente de desenvolvimento do código push tooyour ocorreu, acesse a página de aplicativo da web do ambiente de desenvolvimento tooyour e examinar Olá **implantação** parte. Você deve ser capaz de toosee sua última confirmação de mensagem existe.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. A partir daí, clique em **procurar** toosee Olá nova alteração no aplicativo em tempo real Olá no Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   É um aplicativo de toohello alteração secundária. No entanto, muitas vezes o novo aplicativo de web complexos de tooa alterações tem os efeitos colaterais não intencionais e indesejáveis. Sendo tooeasily capaz de teste cada confirmação em compilações ao vivo permite que você toocatch esses problemas antes dos clientes veem-los.

Agora, você deve estar familiarizado com a realização de saudação que, como um desenvolvedor em Olá **NewUpdate** projeto, você pode criar um ambiente de desenvolvimento para você mesmo, cada confirmação de compilação e teste de cada compilação.

## <a name="merge-code-into-test-environment"></a>Mesclar o código no ambiente de teste
Quando você estiver pronto toopush seu código de desenvolvimento de branch a ramificação tooNewUpdate, é saudação padrão git processo:

1. Mescle qualquer nova tooNewUpdate de confirmações no branch de desenvolvimento Olá no GitHub, como confirmações criados por outros desenvolvedores. Qualquer novo confirmação no GitHub dispara um push de código e a compilação no ambiente de desenvolvimento de saudação. Você pode, em seguida, verifique se que seu código no branch de desenvolvimento ainda funciona com os bits mais recentes de saudação do branch NewUpdate.
2. Mescle todas as confirmações novas da ramificação de desenvolvimento na ramificação NewUpdate no GitHub. Essa ação aciona um push de código e a compilação no ambiente de teste de saudação. 

Novamente, observe que como implantação contínua já está configurada com esses branches git, você não precisa tootake compilações de qualquer outra ação semelhante à execução de integração. Basta tooperform práticas recomendadas de controle de origem padrão usando o git, e o Azure executa todos os processos de compilação Olá para você.

Agora, vamos enviar seu código muito**NewUpdate** ramificação. No Shell de Git, execute Olá comandos a seguir:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

É isso! 

Página de aplicativo da web toohello vá para sua toosee do ambiente de teste seu novo confirmação (mesclada no branch de NewUpdate) agora enviada por push toohello ambiente de teste. Em seguida, clique em **procurar** toosee que Olá alterações de estilo está em execução ao vivo no Azure.

## <a name="deploy-update-tooproduction"></a>Implantar a atualização tooproduction
Enviar código toohello ambiente de produção e preparo deve ser diferente de que você já fez quando enviada por push o ambiente de teste de toohello de código. É muito simples. 

No Shell de Git, execute Olá comandos a seguir:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Lembre-se de que, com base na maneira Olá ambiente de preparo e produção de hello é configurado no ProdandStage.json, o novo código é enviada por push toohello **preparo** slot e está em execução há. Então se você navegar URL do slot preparo toohello, consulte novo código de saudação em execução lá. toodo, Olá execução seguinte cmdlet no Shell de Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

E agora, depois de verificar atualização Olá Olá slot de preparo, Olá somente coisa toodo é tooswap-lo em produção. No Shell de Git, basta execute Olá comandos a seguir:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Parabéns! Um novo aplicativo de web de produção de tooyour atualização ter publicado com êxito. E isso foi feita criando facilmente os ambientes de teste/desenvolvimento e compilando/testando todas as confirmações. Esses são elementos fundamentais para o desenvolvimento de software Agile.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Excluir os ambientes de desenvolvimento e teste
Como você propositadamente tiver desenvolvido seu desenvolvimento e grupos de recursos independentes de toobe de ambientes de teste, é fácil toodelete-los. Olá toodelete daqueles criados por você neste tutorial, ramificações do GitHub hello e artefatos do Azure, basta executar Olá comandos no Shell de Git a seguir:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Resumo
Desenvolvimento de software Agile é necessário para muitas empresas que desejam tooadopt Azure como sua plataforma de aplicativo. Neste tutorial, você aprendeu como toocreate e desmontagem réplicas exatas ou perto de réplicas de Olá ambiente de produção com facilidade, mesmo para aplicativos complexos. Você também aprendeu como tooleverage toocreate essa capacidade desenvolvimento de um processo que pode criar e testar cada confirmação única no Azure. Este tutorial Esperamos que mostraram a como melhor usar serviço de aplicativo do Azure e o Azure Resource Manager toocreate junto uma solução de DevOps que atende as metodologias de tooagile. Em seguida, você pode criar esse cenário executando técnicas avançadas de DevOps, por exemplo, [teste em produção](app-service-web-test-in-production-get-start.md). Para conhecer um cenário comum de teste em produção, consulte [Implantação de liberação de versões de pré-lançamento (teste beta) no Serviço de Aplicativo do Azure](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Mais recursos
* [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md)
* [Desenvolvimento Agile na prática: dicas e truques do ciclo de desenvolvimento modernizado](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Estratégias de implantação avançada para aplicativos Web do Azure usando modelos do Gerenciador de Recursos](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Criando modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Olá validador de JSON](http://jsonlint.com/)
* [ARMClient – configurar toosite de publicação do GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Ramificação Git – Conceitos básicos de ramificação e mesclagem](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog de David Ebbo](http://blog.davidebbo.com/)
* [PowerShell do Azure](/powershell/azure/overview)
* [Ferramentas de linha de comando de plataformas cruzadas do Azure](../cli-install-nodejs.md)
* [Criar ou editar usuários no AD do Azure](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Projeto Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

