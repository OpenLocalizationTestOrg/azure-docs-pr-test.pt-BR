---
title: "aaaCreate um aplicativo da web ASP.NET Core no código do Visual Studio"
description: "Este tutorial ilustra como toocreate um núcleo de ASP.NET web app usando o código do Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Criar um aplicativo Web ASP.NET Core no Visual Studio Code
## <a name="overview"></a>Visão geral
Este tutorial mostra como toocreate um núcleo de ASP.NET web app usando [código do Visual Studio (VS código)](http://code.visualstudio.com//Docs/whyvscode) e implantá-lo muito[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Embora este artigo se refere a aplicativos tooweb, ela também se aplica tooAPI aplicativos e aplicativos móveis. 
> 
> 

O ASP.NET Core é uma reestruturação significativa do ASP.NET. ASP.NET Core é uma nova estrutura de código-fonte aberto entre plataformas para criar modernos aplicativos em nuvem da Web usando o .NET. Para obter mais informações, consulte [tooASP.NET Introdução Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Para obter informações sobre aplicativos Web do Serviço de Aplicativo do Azure, consulte [Visão geral de aplicativos Web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Pré-requisitos
* Instale o [Código do VS](http://code.visualstudio.com/Docs/setup).
* Instalar o Git – você pode instalá-lo de um destes locais: [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads). Se você for novo tooGit, escolha [git scm.com](http://git-scm.com/downloads) e selecione a opção de saudação muito**Git de uso de saudação de Prompt de comando do Windows**. Depois de instalar o Git, você também precisará email e o nome de usuário de Git tooset Olá conforme necessário mais tarde no tutorial de saudação (quando executar uma confirmação do VS código).  

## <a name="install-aspnet-core"></a>Instalar o ASP.NET Core
O ASP.NET Core é uma pilha enxuta do .NET para criar aplicativos da Web e de nuvem modernos e executados em OS X, Linux e Windows. Ele foi criado de saudação Terra backup tooprovide uma estrutura de desenvolvimento otimizado para aplicativos que são qualquer nuvem toohello implantado ou executado localmente. Ele consiste em componentes modulares com sobrecarga mínima, para que você mantenha a flexibilidade durante a construção de suas soluções.

Este tutorial é projetado tooget você começou a criar aplicativos com versões mais recentes de desenvolvimento saudação do ASP.NET Core. Olá instruções a seguir é tooWindows específico. Para instruções de instalação no OS X, no Linux e no Windows, veja [Introdução ao ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Para obter instruções de instalação mais detalhadas para OS X, Linux e Windows, consulte [Instalação do ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Criar aplicativo web de saudação
Esta seção mostra como tooscaffold um novo aplicativo ASP.NET web aplicativo usando a ferramenta de .NET CLI hello. 

1. Digite o seguinte Olá Olá prompt de comando toocreate Olá projeto pasta scaffold Olá aplicativo e.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI – gerador do ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore Olá pacotes do NuGet necessários, execute Olá comando a seguir:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Executar o aplicativo da web de saudação localmente
Agora que você criou Olá web app e todos os pacotes do NuGet Olá para o aplicativo hello recuperados, você pode executar o aplicativo da web de saudação localmente.

1. Executar o aplicativo hello (Olá `dotnet run` comando criará o aplicativo hello quando ele está desatualizado):
    ```terminal
    dotnet run
    ```
2. Abra um navegador e navegue toohello URL a seguir.
   
    **http://localhost:5000**
   
    a página de aplicativo da web de saudação padrão Olá será exibida da seguinte maneira.
   
    ![Aplicativo Web local em um navegador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Feche o navegador. Em Olá **janela comando**, pressione **Ctrl + C** tooshut aplicativo hello e fechar Olá **janela de comando**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Criar um aplicativo web no hello Portal do Azure
Olá etapas a seguir orientará você durante a criação de um aplicativo web no hello Portal do Azure.

1. Faça logon no toohello [Portal do Azure](https://portal.azure.com).
2. Clique em **novo** em Olá superior esquerda da saudação Portal.
3. Clique em **Aplicativos Web > Aplicativo Web**.
   
    ![Novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Insira um valor para **Nome**, como **SampleWebAppDemo**. Observe que esse nome precisa toobe exclusivo e portal Olá irá impor que durante a tentativa de nome de saudação tooenter. Portanto, se você selecionar uma Insira um valor diferente, você precisará toosubstitute esse valor para cada ocorrência de **SampleWebAppDemo** que você vê neste tutorial. 
5. Selecione um **Plano de Serviço de Aplicativo** existente ou crie um novo. Se você criar um novo plano, selecione Olá tipo de preço, local e outras opções. Para obter mais informações sobre planos de serviço de aplicativo, consulte o artigo Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Folha de novo aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Clique em **Criar**.
   
    ![folha de aplicativo Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Habilitar a publicação de Git para o novo aplicativo de web Olá
Git é um sistema de controle de versão distribuídos que você pode usar toodeploy seu aplicativo da web do serviço de aplicativo do Azure. Armazenar código Olá que gravar para seu aplicativo web em um repositório Git local e implantará seu código tooAzure enviando o repositório remoto tooa.   

1. Faça logon no hello [Portal do Azure](https://portal.azure.com).
2. Clique em **Procurar**.
3. Clique em **aplicativos Web** tooview uma lista de aplicativos da web de saudação associado à sua assinatura do Azure.
4. Selecione o aplicativo de web de saudação criado neste tutorial.
5. Na folha de saudação do aplicativo web, clique em **configurações** > **implantação contínua**. 
   
    ![host de aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Clique em **Escolher fonte > Repositório Git local**.
7. Clique em **OK**.
   
    ![Repositório Git Local do Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Se você não configurou previamente as credenciais de implantação para publicação de um Aplicativo Web ou outro aplicativo de Serviço de Aplicativo, configure-as agora:
   
   * Clique em **Configurações** > **Credenciais de implantação**. Olá **definir credenciais de implantação** folha será exibida.
   * Digite um nome de usuário e senha.  Você precisará dessa senha posteriormente ao configurar o Git.
   * Clique em **Salvar**.
9. Na folha de seu aplicativo Web, clique em **Configurações > Propriedades**. URL de saudação do repositório Git remoto Olá que você implantará toois mostrado em **URL do GIT**.
10. Saudação de cópia **URL do GIT** valor para uso posterior no tutorial de saudação.
    
    ![URL Git do Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publicar seu tooAzure de aplicativo web do serviço de aplicativo
Nesta seção, você criará um repositório Git local e enviar por push de toodeploy de tooAzure esse repositório seu tooAzure de aplicativo web.

1. No código VS, selecione Olá **Git** opção na barra de navegação à esquerda de saudação.
   
    ![Ícone do Git no Código do VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Selecione **inicializar o repositório do git** toomake-se de que seu espaço de trabalho está sob controle do código-fonte git. 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Abra Olá janela de comando e altere o diretório de toohello diretórios de seu aplicativo web. Em seguida, digite Olá comando a seguir:
   
        git config core.autocrlf false
   
    Esse comando previne um problema de texto envolvendo as terminações CRLF e LF.
4. No código VS, adicionar uma mensagem de confirmação e clique em Olá **confirmar todos** ícone de verificação.
   
    ![Confirmar Tudo do Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Depois de concluir o processamento Git, você verá que não existem arquivos listados na janela de Git de saudação em **alterações**. 
   
    ![Sem alterações do Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Altere toohello back janela de comando onde o prompt de comando Olá aponta toohello diretório onde o aplicativo web está localizado.
7. Crie uma referência remota para enviar atualizações tooyour web app usando Olá URL de Git (terminando em ".git") que você copiou anteriormente.
   
        git remote add azure [URL for remote repository]
8. Configure Git toosave suas credenciais localmente para que eles serão acrescentadas automaticamente tooyour comandos de push gerados a partir de código do VS.
   
        git config credential.helper store
9. Enviar por push o tooAzure alterações inserindo Olá comando a seguir. Após essa tooAzure push inicial, será toodo capaz de envio de saudação todos os comandos de código VS. 
   
        git push -u azure master
   
    Você será solicitado para senha Olá que você criou anteriormente no Azure. **Observação: a senha não será visível.**
   
    saída de saudação do hello acima comando termina com uma mensagem de que a implantação for bem-sucedida.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Se você fizer alterações tooyour aplicativo, você poderá republicar diretamente no código VS usando a funcionalidade interna de Git Olá selecionando Olá **confirmar todos os** opção seguido Olá **Push** opção. Você encontrará Olá **Push** opção disponível no hello menu suspenso próximo toohello **confirmar todos os** e **atualização** botões.
> 
> 

Se você precisar toocollaborate em um projeto, você deve considerar enviar por push tooGitHub entre tooAzure de envio por push.

## <a name="run-hello-app-in-azure"></a>Executar o aplicativo hello no Azure
Agora que você implantou seu aplicativo web, vamos executar o aplicativo hello enquanto hospedado no Azure. 

Isso pode ser feito de duas maneiras:

* Abra um navegador e insira o nome de saudação do seu aplicativo web da seguinte maneira.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Olá Portal do Azure, localize a folha de aplicativo web Olá para seu aplicativo web e clique no **procurar** tooview seu aplicativo 
* no navegador padrão.

![Aplicativo Web do Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Resumo
Neste tutorial, você aprendeu como toocreate um aplicativo web no código VS e implantá-lo tooAzure. Para obter mais informações sobre código VS, consulte o artigo Olá [por código do Visual Studio?](https://code.visualstudio.com/Docs/) Para obter informações sobre os aplicativos Web do Serviço de Aplicativo, consulte [Visão geral de Aplicativos Web](app-service-web-overview.md). 

