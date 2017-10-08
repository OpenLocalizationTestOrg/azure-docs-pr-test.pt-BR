---
title: "aaaDeploy tooAzure seu aplicativo do serviço de aplicativo | Microsoft Docs"
description: "Saiba como toodeploy tooAzure seu aplicativo do serviço de aplicativo."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Implantar seu tooAzure de aplicativo do serviço de aplicativo
Este artigo ajuda você a determinar Olá melhor opção toodeploy Olá arquivos para o seu aplicativo web, o back-end do aplicativo móvel ou o aplicativo de API muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714)e o orientará você tooappropriate recursos com tooyour específico de instruções opção preferida.

## <a name="overview"></a>Visão geral da implantação do Serviço de Aplicativo do Azure
Serviço de aplicativo do Azure mantém a estrutura de aplicativo hello para você (ASP.NET, PHP, Node.js, etc.). Algumas estruturas são habilitadas por padrão, enquanto outros, como Java e Python, talvez seja necessário um tooenable de configuração de marca de seleção simples-lo. Além disso, você pode personalizar a estrutura do seu aplicativo, como versão do PHP hello ou número de bits de saudação do seu tempo de execução. Para saber mais, confira [Configurar seu aplicativo no Serviço de Aplicativo do Azure](web-sites-configure.md).

Como você não tem tooworry sobre estrutura de servidor ou aplicativo da web hello, implantar o serviço de tooApp do aplicativo é uma questão de implantar seu código, binários, arquivos de conteúdo e sua estrutura de diretório do respectivos, toohello [   **/site /wwwroot** diretório](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou hello **/site/wwwroot/App_Data/trabalhos/** diretório para WebJobs). O Serviço de Aplicativo dá suporte a três diferentes processos de implantação. Todos os métodos de implantação de saudação neste artigo usem uma saudação processos a seguir: 

* [FTP ou FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): Use seus favoritos FTP ou FTPS habilitada toomove ferramenta tooAzure seus arquivos, de [FileZilla](https://filezilla-project.org) IDEs em destaque toofull como [NetBeans](https://netbeans.org). Esse é estritamente um processo de carregamento de arquivo. Nenhum outro serviço é fornecido pelo Serviço de Aplicativo, por exemplo, controle de versão, gerenciamento de estrutura de arquivos, etc. 
* [O kudu (Git/Mercurial ou OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu é hello [mecanismo de implantação](https://github.com/projectkudu/kudu/wiki) no serviço de aplicativo. Enviar por push tooKudu seu código diretamente de um repositório. O kudu também fornece serviços adicionados sempre que o código é enviada por push tooit, incluindo controle de versão, restauração do pacote, o MSBuild, e [web ganchos](https://github.com/projectkudu/kudu/wiki/Web-hooks) para implantação contínua e outras tarefas de automação. mecanismo de implantação Olá Kudu oferece suporte a 3 tipos diferentes de fontes de implantação:   
  
  * Sincronização de conteúdo do OneDrive e Dropbox   
  * Implantação contínua com base no repositório com a sincronização automática do GitHub, do Bitbucket e do Visual Studio Team Services  
  * Implantação baseada em repositório com sincronização manual do Git local  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): implantar código tooApp serviço diretamente a partir do Microsoft favorito ferramentas, como o Visual Studio usando Olá ferramentas mesmo que automatiza servidores tooIIS de implantação. Essa ferramenta oferece suporte à implantação apenas da diferença, criação de banco de dados, transformações de cadeias de conexão, etc. A implantação da Web difere de Kudu aplicativo binários são criados antes que eles sejam implantados tooAzure. TooFTP semelhante, não há serviços adicionais são fornecidos pelo serviço de aplicativo.

Populares ferramentas de desenvolvimento da Web oferecem suporte a um ou mais desses processos de implantação. Enquanto a ferramenta que você escolher hello determina os processos de implantação Olá você pode aproveitar, hello real DevOps funcionalidades à sua disposição dependem da combinação de saudação do processo de implantação de saudação e hello ferramentas específicas você escolher. Por exemplo, se você executar a Implantação da Web do [Visual Studio com o SDK do Azure](#vspros), apesar de não contar com a automação do Kudu, você obtém a restauração do pacote e a automação do MSBuild no Visual Studio. 

> [!NOTE]
> Esses processos de implantação, na verdade, não [provisionar Olá recursos do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) que seu aplicativo pode precisar. No entanto, a maioria das Olá vinculado como-tooarticles mostra como tooprovision Olá aplicativo e implantar seu código tooit ponta a ponta. Você também pode encontrar opções adicionais para o provisionamento de recursos do Azure Olá [automatizar a implantação usando as ferramentas de linha de comando](#automate) seção.
> 
> 

## <a name="ftp"></a>Implantar manualmente ao carregar arquivos com FTP
Se você estiver usado toomanually copiando o servidor web tooa conteúdo da web, você pode usar um [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) arquivos toocopy do utilitário, como o Windows Explorer ou [FileZilla](https://filezilla-project.org/).

os profissionais de saudação de copiar arquivos manualmente são:

* Familiaridade e complexidade mínima de ferramentas de FTP. 
* Saber exatamente para onde vão os arquivos.
* Maior segurança com FTPS.

são desvantagens de saudação de copiar arquivos manualmente:

* Tendo tooknow como toodeploy arquivos diretórios correto toohello no serviço de aplicativo. 
* Se falhas ocorrerem, não haverá um controle de versão para reversão.
* Nenhum histórico de implantação interno para solução de problemas de implantação.
* Implantação potencial de longo tempo porque muitas ferramentas FTP não fornecem uma cópia somente para comparação e simplesmente copie todos os arquivos de saudação.  

### <a name="howtoftp"></a>Como os arquivos de tooupload com FTP
Olá [Portal do Azure](https://portal.azure.com) fornece todas as informações de saudação precisar diretórios do aplicativo do tooconnect tooyour usando FTP ou FTPS.

* [Implantar seu tooAzure de aplicativo do serviço de aplicativo usando o FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Implantar ao sincronizar com uma pasta de nuvem
Uma boa alternativa muito[copiar arquivos manualmente](#ftp) está sincronizando arquivos e pastas tooApp serviço de um serviço de armazenamento de nuvem como o OneDrive e o Dropbox. Sincronizando com uma pasta de nuvem utiliza o processo de Kudu Olá para implantação (consulte [visão geral dos processos de implantação](#overview)).

os profissionais de saudação de sincronização com uma pasta de nuvem são:

* Simplicidade de implantação. Serviços como o OneDrive e o Dropbox fornecem clientes de sincronização de área de trabalho, assim o diretório de trabalho local também é o diretório de implantação.
* Implantação com um único clique.
* Todas as funcionalidades do mecanismo de implantação de Kudu hello estão disponível (por exemplo, a restauração do pacote, automação).

desvantagens de saudação da sincronização com uma pasta de nuvem são:

* Se falhas ocorrerem, não haverá um controle de versão para reversão.
* Nenhuma implantação automatizada, a sincronização manual é necessária.

### <a name="howtodropbox"></a>Como toodeploy por sincronização com uma pasta de nuvem
Em Olá [Portal do Azure](https://portal.azure.com), você pode designar uma pasta para sincronização de conteúdo no seu armazenamento em nuvem OneDrive ou Dropbox, com o código do aplicativo e o conteúdo na pasta de trabalho e sincronização tooApp serviço com hello clique de um botão.

* [Sincronizar o conteúdo de uma pasta de nuvem tooAzure do serviço de aplicativo](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Implantar continuamente de um sistema de controle do código-fonte baseado em nuvem
Se sua equipe de desenvolvimento usa um serviço de gerenciamento (SCM) do código de origem baseado em nuvem como [do Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), ou [BitBucket](https://bitbucket.org/), você pode configurar o aplicativo Toointegrate com o repositório de serviço e implantar continuamente. 

os profissionais de saudação de implantação de um serviço de controle de origem baseado em nuvem são:

* Reversão de tooenable de controle de versão.
* Implantação contínua com tooconfigure capacidade de Git (e do Mercurial quando aplicável) repositórios. 
* Implantação de ramificação específica, pode implantar diferentes ramos toodifferent [slots](web-sites-staged-publishing.md).
* Todas as funcionalidades do mecanismo de implantação de Kudu hello estão disponível (por exemplo, o controle de versão de implantação, rollback, restauração do pacote, automação).

con Olá de implantação de um serviço de controle de origem baseado em nuvem é:

* Algum conhecimento de serviço SCM respectivo Olá necessário.

### <a name="vsts"></a>Como toodeploy continuamente a partir de uma fonte baseada em nuvem controlar o serviço
Em Olá [Portal do Azure](https://portal.azure.com), você pode configurar implantação contínua do GitHub, Bitbucket e Visual Studio Team Services.

* [TooAzure implantação contínua do serviço de aplicativo](app-service-continuous-deployment.md). 

toofind-out como a implantação contínua tooconfigure manualmente a partir de um repositório de nuvem não listada Olá Portal do Azure (como [GitLab](https://gitlab.com/)), consulte [Configurando implantação contínua usando as etapas manuais](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Implantar por meio do Git local
Se sua equipe de desenvolvimento usa um serviço de gerenciamento (SCM) de código do local no local de origem com base no Git, você pode configurar isso como uma origem de implantação tooApp serviço. 

Estas são as vantagens de implantar do Git local:

* Reversão de tooenable de controle de versão.
* Implantação de ramificação específica, pode implantar diferentes ramos toodifferent [slots](web-sites-staged-publishing.md).
* Todas as funcionalidades do mecanismo de implantação de Kudu hello estão disponível (por exemplo, o controle de versão de implantação, rollback, restauração do pacote, automação).

Estas são as desvantagens de implantar do Git local:

* Algum conhecimento dos sistema SCM respectivo Olá necessário.
* Não há soluções completas para a implantação contínua. 

### <a name="vsts"></a>Como toodeploy do Git local
Em Olá [Portal do Azure](https://portal.azure.com), você pode configurar a implantação local do Git.

* [TooAzure local de implantação do Git do serviço de aplicativo](app-service-deploy-local-git.md). 
* [Publicação de aplicativos tooWeb de qualquer repositório git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Implantar usando o IDE
Se você já estiver usando [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) com um [SDK do Azure](https://azure.microsoft.com/downloads/), ou outros conjuntos IDE, como [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), e [ IntelliJ IDEIA](https://www.jetbrains.com/idea/), você pode implantar tooAzure diretamente do seu IDE. Essa opção é ideal para um desenvolvedor individual.

O Visual Studio oferece suporte a todos os processos de implantação de três (FTP, Git e implantação da Web), dependendo de sua preferência, enquanto outros IDEs pode implantar tooApp serviço se eles tiverem a integração de FTP ou Git (consulte [visão geral dos processos de implantação](#overview)).

os profissionais de saudação de implantação usando uma IDE são:

* Minimize potencialmente Olá ferramentas para o seu ciclo de vida do aplicativo de ponta a ponta. Desenvolver, depurar, acompanhar e implantar seu aplicativo tooAzure sem mover fora de seu IDE. 

contras Olá de implantação usando uma IDE são:

* Complexidade das ferramentas.
* Ainda exige um sistema de controle de código-fonte para um projeto em equipe.

<a name="vspros"></a> Estas são vantagens adicionais da implantação usando o Visual Studio com o SDK do Azure:

* O SDK do Azure torna os recursos do Azure cidadãos de primeira classe no Visual Studio. Criar, excluir, editar, iniciar e interromper aplicativos, banco de dados SQL back-end de saudação de consulta, a saudação de depuração ao vivo do aplicativo do Azure e muito mais. 
* Edição em tempo real dos arquivos de código no Azure.
* Depuração em tempo real de aplicativos no Azure.
* Gerenciador integrado do Azure.
* Implantação apenas da diferença. 

### <a name="vs"></a>Como toodeploy diretamente do Visual Studio
* [Introdução ao Microsoft Azure e ao ASP.NET](app-service-web-get-started-dotnet.md). Como toocreate e implantar um projeto simples de web do ASP.NET MVC usando o Visual Studio e a implantação da Web.
* [Como tooDeploy WebJobs do Azure usando o Visual Studio](websites-dotnet-deploy-webjobs.md). Como tooconfigure aplicativo de Console projetos para que eles implantar como WebJobs.  
* [Implantação da Web do ASP.NET usando o Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Uma série de 12 parte tutorial que abrange uma gama mais completa de tarefas de implantação de Olá outros nessa lista. Alguns recursos de implantação do Azure foram adicionados como Olá tutorial foi escrito, mas anotações adicionadas posteriormente explicam o que está faltando.
* [Implantando um tooAzure site ASP.NET no Visual Studio 2012 de um repositório Git diretamente](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Explica como toodeploy da web do ASP.NET um projeto no Visual Studio, usando Olá Git toocommit plug-in Olá código tooGit e conectar o repositório do Git toohello do Azure. A partir do Visual Studio 2013, o suporte ao Git é integrado e não requer a instalação de um plug-in.

### <a name="aztk"></a>Como usar toodeploy hello kits de ferramentas do Azure para Eclipse e IDEIA IntelliJ
A Microsoft torna isso possível toodeploy tooAzure de aplicativos Web diretamente do Eclipse e IntelliJ via Olá [Kit de ferramentas do Azure para Eclipse](../azure-toolkit-for-eclipse.md) e [Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij.md). Olá tutoriais a seguir ilustram etapas Olá envolvidas na implantação simples um "Hello" world aplicativo Web tooAzure usando qualquer IDE:

* [Criar um aplicativo Web Hello World para o Azure no Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Este tutorial mostra como toouse hello Kit de ferramentas do Azure para Eclipse toocreate e implantar um aplicativo da Web Hello World para Azure.
* [Criar um aplicativo Web Hello World para o Azure no IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Este tutorial mostra como toouse hello Kit de ferramentas do Azure para IntelliJ toocreate e implantar um aplicativo da Web Hello World para Azure.

## <a name="automate"></a>Automatizar a implantação usando ferramentas de linha de comando
Se você preferir terminal de linha de comando hello como ambiente de desenvolvimento de saudação de preferência, é possível fazer scripts tarefas de implantação para seu aplicativo de serviço de aplicativo usando ferramentas de linha de comando. 

As vantagens de implantar usando as ferramentas de linha de comando são:

* É possível ter cenários de implantação em script.
* Integração do provisionamento dos recursos do Azure e implantação de código.
* Integração da implantação do Azure aos scripts existentes de integração contínua.

A desvantagem de implantar usando as ferramentas de linha de comando é:

* Não servem para desenvolvedores que preferem a GUI.

### <a name="automatehow"></a>Como a implantação tooautomate com as ferramentas de linha de comando

Consulte [automatizar a implantação do aplicativo do Azure com as ferramentas de linha de comando](app-service-deploy-command-line.md) para obter uma lista de tootutorials links e ferramentas de linha de comando. 

## <a name="nextsteps"></a>Próximas etapas
Em alguns cenários, você pode querer toobe tooeasily capaz de comutador e para trás entre uma preparação e uma versão de produção do seu aplicativo. Para obter mais informações, consulte [Implantação preparada em Aplicativos Web](web-sites-staged-publishing.md).

Uma parte importante de qualquer fluxo de trabalho de implantação é ter um plano de backup e restauração. Para obter informações sobre hello backup do serviço de aplicativo e o recurso de restauração, consulte [Backups de aplicativos Web](web-sites-backup.md).  

Para obter informações sobre como toomanage de controle de acesso baseado em função do Azure toouse acessam tooApp de implantação de serviço, consulte [RBAC e publicação de aplicativo da Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

