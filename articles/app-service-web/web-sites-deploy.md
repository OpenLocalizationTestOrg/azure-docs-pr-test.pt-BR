---
title: "Implantar seu aplicativo no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como implantar seu aplicativo no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Implantar seu aplicativo no Serviço de Aplicativo do Azure
Este artigo ajuda você a determinar a melhor opção para implantar os arquivos de seu aplicativo Web, back-end de aplicativo móvel ou aplicativo de API no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714)e orienta você até os recursos apropriados com instruções específicas para sua opção preferida.

## <a name="overview"></a>Visão geral da implantação do Serviço de Aplicativo do Azure
O Serviço de Aplicativo do Azure mantém a estrutura de aplicativo para você (ASP.NET, PHP, Node.js etc). Algumas estruturas estão habilitadas por padrão enquanto outras, como Java e Python, talvez precisem de uma simples marca de seleção para habilitá-las. Além disso, você pode personalizar a estrutura do aplicativo, como a versão do PHP ou o número de bits de seu tempo de execução. Para saber mais, confira [Configurar seu aplicativo no Serviço de Aplicativo do Azure](web-sites-configure.md).

Como você não precisa se preocupar com a estrutura do servidor Web ou do aplicativo, a implantação do aplicativo no Serviço de Aplicativo é uma questão de implantação do código, dos binários, dos arquivos de conteúdo e suas respectivas estruturas de diretórios, no diretório [**/site/wwwroot**](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou no diretório **/site/wwwroot/App_Data/Jobs/** para Trabalhos Web). O Serviço de Aplicativo dá suporte a três diferentes processos de implantação. Todos os métodos de implantação neste artigo usam um dos seguintes processos: 

* [FTP ou FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): use sua ferramenta habilitada com FTP ou FTPS favorita para mover seus arquivos para o Azure, do [FileZilla](https://filezilla-project.org) para IDEs completos como o [NetBeans](https://netbeans.org). Esse é estritamente um processo de carregamento de arquivo. Nenhum outro serviço é fornecido pelo Serviço de Aplicativo, por exemplo, controle de versão, gerenciamento de estrutura de arquivos, etc. 
* [Kudu (Git/Mercurial ou OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu é o [mecanismo de implantação](https://github.com/projectkudu/kudu/wiki) no Serviço de Aplicativo. Envie diretamente seu código para o Kudu a partir de qualquer repositório. O Kudu também fornece outros serviços sempre que o código é enviado para ele, incluindo controle de versão, restauração de pacote, MSBuild e [ganchos da Web](https://github.com/projectkudu/kudu/wiki/Web-hooks) para implantação contínua e outras tarefas de automação. O mecanismo de implantação Kudu oferece suporte a três tipos diferentes de fontes de implantação:   
  
  * Sincronização de conteúdo do OneDrive e Dropbox   
  * Implantação contínua com base no repositório com a sincronização automática do GitHub, do Bitbucket e do Visual Studio Team Services  
  * Implantação baseada em repositório com sincronização manual do Git local  
* [Implantação da Web](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): implante código no Serviço de Aplicativo diretamente de suas ferramentas favoritas da Microsoft, como o Visual Studio, usando as mesmas ferramentas que automatizam a implantação em servidores IIS. Essa ferramenta oferece suporte à implantação apenas da diferença, criação de banco de dados, transformações de cadeias de conexão, etc. A Implantação da Web é diferente do Kudu no sentido de que os binários de aplicativo são criados antes de serem implantados no Azure. Como acontece com o FTP, nenhum serviço adicional é fornecido pelo Serviço de Aplicativo.

Populares ferramentas de desenvolvimento da Web oferecem suporte a um ou mais desses processos de implantação. Embora sua ferramenta escolhida determine os processos de implantação que podem ser aproveitados, a funcionalidade real do DevOps à sua disposição depende da combinação do processo de implantação e de ferramentas específicas escolhidas por você. Por exemplo, se você executar a Implantação da Web do [Visual Studio com o SDK do Azure](#vspros), apesar de não contar com a automação do Kudu, você obtém a restauração do pacote e a automação do MSBuild no Visual Studio. 

> [!NOTE]
> Na verdade, esses processos de implantação não [provisionam os recursos do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) dos quais seu aplicativo pode precisar. No entanto, a maioria dos artigos de instruções vinculados mostra como provisionar o aplicativo E implantar seu código no aplicativo, de ponta a ponta. Você também pode encontrar outras opções para o provisionamento de recursos do Azure na seção [Automatizar a implantação usando as ferramentas de linha de comando](#automate) .
> 
> 

## <a name="ftp"></a>Implantar manualmente ao carregar arquivos com FTP
Se estiver acostumado a copiar manualmente o conteúdo da Web para um servidor Web, você poderá usar um utilitário [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) para copiar arquivos, como o Windows Explorer ou o [FileZilla](https://filezilla-project.org/).

Os prós de copiar manualmente os arquivos são:

* Familiaridade e complexidade mínima de ferramentas de FTP. 
* Saber exatamente para onde vão os arquivos.
* Maior segurança com FTPS.

Os contras de copiar manualmente os arquivos são:

* Ter de saber como implantar os arquivos nos diretórios corretos no Serviço de Aplicativo. 
* Se falhas ocorrerem, não haverá um controle de versão para reversão.
* Nenhum histórico de implantação interno para solução de problemas de implantação.
* Tempos de implantação potencialmente longos porque várias ferramentas de FTP não oferecem a cópia apenas da diferença e simplesmente copiam todos os arquivos.  

### <a name="howtoftp"></a>Como carregar arquivos com o FTP
O [Portal do Azure](https://portal.azure.com) fornece todas as informações necessárias para se conectar aos diretórios do seu aplicativo usando FTP ou FTPS.

* [Implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Implantar ao sincronizar com uma pasta de nuvem
Uma boa alternativa à [cópia manual dos arquivos](#ftp) é sincronizar os arquivos e pastas no Serviço de Aplicativo de um serviço de armazenamento em nuvem, como o OneDrive e o Dropbox. A sincronização com uma pasta de nuvem utiliza o processo Kudu para implantação (confira [Visão geral dos processos de implantação](#overview)).

Os prós da sincronização com uma pasta de nuvem são:

* Simplicidade de implantação. Serviços como o OneDrive e o Dropbox fornecem clientes de sincronização de área de trabalho, assim o diretório de trabalho local também é o diretório de implantação.
* Implantação com um único clique.
* Toda a funcionalidade no mecanismo de implantação Kudu está disponível (por exemplo, restauração de pacote, automação).

Os contras da sincronização com uma pasta de nuvem são:

* Se falhas ocorrerem, não haverá um controle de versão para reversão.
* Nenhuma implantação automatizada, a sincronização manual é necessária.

### <a name="howtodropbox"></a>Como implantar ao sincronizar com uma pasta de nuvem
No [Portal do Azure](https://portal.azure.com), é possível designar uma pasta para sincronização de conteúdo no OneDrive ou no Dropbox ou em seu armazenamento em nuvem, trabalhar com o código e o conteúdo do aplicativo nessa pasta e sincronizá-la com o Serviço de Aplicativo com apenas um clique.

* [Sincronize o conteúdo de uma pasta de nuvem para o Serviço de Aplicativo do Azure](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Implantar continuamente de um sistema de controle do código-fonte baseado em nuvem
Se sua equipe de desenvolvimento usar um serviço SCM (gerenciamento de código-fonte) baseado em nuvem como o [Visual Studio Team Services](http://www.visualstudio.com/), o [GitHub](https://www.github.com), ou o [BitBucket](https://bitbucket.org/), você poderá configurar o Serviço de Aplicativo para integrar com seu repositório e implantar continuamente. 

As vantagens de implantar usando um serviço de controle de origem baseado na nuvem são:

* Controle de versão para habilitar a reversão.
* Capacidade de configurar a implantação contínua para repositórios Git (e o Mercurial, quando aplicável). 
* Implantação específica da ramificação, é possível implantar diferentes ramificações em diferentes [slots](web-sites-staged-publishing.md).
* Toda funcionalidade do mecanismo de implantação Kudu está disponível (por exemplo, controle de versão de implantação, reversão, restauração de pacote, automação).

A desvantagem de implantar usando um serviço de controle de origem baseado na nuvem é:

* Algum conhecimento do respectivo serviço SCM é necessário.

### <a name="vsts"></a>Como implantar continuamente de um sistema de controle do código-fonte baseado em nuvem
No [Portal do Azure](https://portal.azure.com), você pode configurar a implantação contínua do GitHub, do Bitbucket e do Visual Studio Team Services.

* [Implantação contínua no Serviço de Aplicativo do Azure](app-service-continuous-deployment.md). 

Para saber como configurar a implantação contínua manualmente a partir de um repositório de nuvem que não esteja listado pelo Portal do Azure (como o [GitLab](https://gitlab.com/)), confira [Configurar a implantação contínua usando etapas manuais](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Implantar por meio do Git local
Se sua equipe de desenvolvimento usar um serviço SCM (gerenciamento de código-fonte local) baseado em Git, você poderá configurar isso como uma fonte de implantação para o Serviço de Aplicativo. 

Estas são as vantagens de implantar do Git local:

* Controle de versão para habilitar a reversão.
* Implantação específica da ramificação, é possível implantar diferentes ramificações em diferentes [slots](web-sites-staged-publishing.md).
* Toda funcionalidade do mecanismo de implantação Kudu está disponível (por exemplo, controle de versão de implantação, reversão, restauração de pacote, automação).

Estas são as desvantagens de implantar do Git local:

* Algum conhecimento do respectivo sistema SCM é necessário.
* Não há soluções completas para a implantação contínua. 

### <a name="vsts"></a>Como implantar do Git local
No [Portal do Azure](https://portal.azure.com), você pode configurar a implantação do Git local.

* [Implantação do Git local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md). 
* [Publicando em Aplicativos Web por meio de qualquer repositório git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Implantar usando o IDE
Se já estiver usando o [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) com um [SDK do Azure](https://azure.microsoft.com/downloads/) ou outros pacotes de IDE, como [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org) e [IntelliJ IDEA](https://www.jetbrains.com/idea/), você poderá implantar no Azure diretamente de seu IDE. Essa opção é ideal para um desenvolvedor individual.

O Visual Studio oferece suporte a todos os três processos de implantação (FTP, Git e Implantação da Web), dependendo de sua preferência, enquanto outros IDEs podem implantar no Serviço de Aplicativo se tiverem integração com FTP ou Git (confira [Visão geral dos processos de implantação](#overview)).

Os prós da implantação usando um IDE são:

* Possibilidade de minimizar as ferramentas para o ciclo de vida completo do aplicativo. Desenvolver, depurar, acompanhar e implantar seu aplicativo no Azure sem sair do IDE. 

Os contras da implantação usando um IDE são:

* Complexidade das ferramentas.
* Ainda exige um sistema de controle de código-fonte para um projeto em equipe.

<a name="vspros"></a> Estas são vantagens adicionais da implantação usando o Visual Studio com o SDK do Azure:

* O SDK do Azure torna os recursos do Azure cidadãos de primeira classe no Visual Studio. Crie, exclua, edite, inicie e interrompa aplicativos, consulte o Banco de Dados SQL de back-end, depure em tempo real o aplicativo do Azure e muito mais. 
* Edição em tempo real dos arquivos de código no Azure.
* Depuração em tempo real de aplicativos no Azure.
* Gerenciador integrado do Azure.
* Implantação apenas da diferença. 

### <a name="vs"></a>Como implantar diretamente do Visual Studio
* [Introdução ao Microsoft Azure e ao ASP.NET](app-service-web-get-started-dotnet.md). Como criar e implantar um projeto da web ASP.NET MVC simples usando o Visual Studio e a Implantação da Web.
* [Como implantar Trabalhos Web do Azure usando o Visual Studio](websites-dotnet-deploy-webjobs.md). Como configurar projetos de Aplicativo de console para que sejam implantados como Trabalhos Web.  
* [Implantação da Web do ASP.NET usando o Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Uma série de tutoriais de 12 partes que abrange uma gama mais completa de tarefas de implantação do que os outros nessa lista. Alguns recursos de implantação do Azure foram adicionados desde que o tutorial foi escrito, mas anotações adicionadas posteriormente explicam o que está faltando.
* [Implantação direta de um site do ASP.NET no Azure no Visual Studio 2012 a partir de um repositório Git](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Explica como implantar um projeto da web ASP.NET no Visual Studio, usando o plug-in do Git para confirmar o código para o Git e conectar o Azure ao repositório Git. A partir do Visual Studio 2013, o suporte ao Git é integrado e não requer a instalação de um plug-in.

### <a name="aztk"></a>Como implantar usando os Kits de Ferramentas do Azure para Eclipse e IntelliJ IDEA
A Microsoft possibilita a implantação de Aplicativos Web no Azure diretamente do Eclipse e do IntelliJ por meio do [Kit de Ferramentas do Azure para Eclipse](../azure-toolkit-for-eclipse.md) e do [Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij.md). Os tutoriais a seguir ilustram as etapas envolvidas na implantação de um Aplicativo Web “Hello world” simples no Azure usando o IDE:

* [Criar um aplicativo Web Hello World para o Azure no Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure.
* [Criar um aplicativo Web Hello World para o Azure no IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Este tutorial mostra como usar o Kit de Ferramentas do Azure para IntelliJ para criar e implantar um aplicativo Web Hello World no Azure.

## <a name="automate"></a>Automatizar a implantação usando ferramentas de linha de comando
Se preferir o terminal de linha de comando como o ambiente de desenvolvimento, você poderá colocar em script as tarefas de implantação para seu aplicativo do Serviço de Aplicativo usando as ferramentas de linha de comando. 

As vantagens de implantar usando as ferramentas de linha de comando são:

* É possível ter cenários de implantação em script.
* Integração do provisionamento dos recursos do Azure e implantação de código.
* Integração da implantação do Azure aos scripts existentes de integração contínua.

A desvantagem de implantar usando as ferramentas de linha de comando é:

* Não servem para desenvolvedores que preferem a GUI.

### <a name="automatehow"></a>Como automatizar a implantação com ferramentas de linha de comando

Confira [Automate deployment of your Azure app with command-line tools](app-service-deploy-command-line.md) (Automatizar a implantação do seu aplicativo Azure com ferramentas de linha de comando) para obter uma lista de ferramentas de linha de comando e links para tutoriais. 

## <a name="nextsteps"></a>Próximas etapas
Em algumas situações, você provavelmente desejará ser capaz de alternar facilmente entre a versão de preparo e a versão de produção do seu aplicativo. Para obter mais informações, consulte [Implantação preparada em Aplicativos Web](web-sites-staged-publishing.md).

Uma parte importante de qualquer fluxo de trabalho de implantação é ter um plano de backup e restauração. Para saber mais sobre o recurso de backup e restauração do Serviço de Aplicativo, veja [Backups de Aplicativos Web](web-sites-backup.md).  

Para saber mais sobre como usar o Controle de Acesso Baseado em Função do Azure para gerenciar o acesso à implantação do Serviço de Aplicativo, consulte [RBAC e a publicação de Aplicativos Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

