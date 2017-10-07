---
title: "aplicativos de aaaDebugging em um contêiner de Docker local | Microsoft Docs"
description: "Saiba como toomodify um aplicativo que é executado em um contêiner de Docker local, atualizar o contêiner de saudação por meio de editar e atualizar e definir pontos de interrupção de depuração"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Depuração de aplicativos em um contêiner de Docker local
## <a name="overview"></a>Visão geral
Olá Visual Studio Tools para o Docker fornece uma toodevelop de maneira consistente em e validar seu aplicativo localmente em um contêiner do Docker do Linux.
Você não tem contêiner de saudação toorestart cada vez que você faz com que um código de alteração.
Este artigo ilustra como toostart de recurso de "Editar e atualizar" hello toouse um aplicativo Web do ASP.NET Core em um contêiner de Docker local, faça as alterações necessárias e, em seguida, atualizar Olá navegador toosee essas alterações.
Este artigo também mostra como tooset pontos de interrupção de depuração.

> [!NOTE]
> O suporte do Contêiner do Windows estará disponível em uma versão futura
>
>

## <a name="prerequisites"></a>Pré-requisitos
Olá ferramentas a seguir deve ser instalado.

* [Versão mais recente do Visual Studio](https://www.visualstudio.com/downloads/)
* [SDK do Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)

toorun localmente contêineres do Docker, será necessário um cliente do docker local.
Você pode usar o hello [caixa de ferramentas do Docker](https://www.docker.com/products/docker-toolbox), que requer o Hyper-V toobe desabilitado ou você pode usar [Docker para Windows](https://www.docker.com/get-docker), que usa o Hyper-V e requer o Windows 10.

Se usar a caixa de ferramentas do Docker, será necessário muito[configurar o cliente do Docker Olá](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Criar um aplicativo Web
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Adicionar suporte ao Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Editar seu código e atualizar
tooquickly iterar alterações, você pode iniciar o aplicativo em um contêiner e continuar toomake alterações, exibi-los como faria com o IIS Express.

1. Definir Olá configuração da solução muito`Debug` e pressione  **&lt;CTRL + F5 >** toobuild o docker de imagens e executá-lo localmente.

    Depois que a imagem de contêiner Olá foi criada e está em execução em um contêiner do Docker, o Visual Studio iniciará Olá Web app no navegador padrão.
    Se você estiver usando o navegador Microsoft Edge de saudação ou detêm erros, consulte [solução de problemas](vs-azure-tools-docker-troubleshooting-docker-errors.md) seção.
2. Vá toohello sobre a página, que é aqui que vamos toomake nossas alterações.
3. Retornar tooVisual Studio e abra `Views\Home\About.cshtml`.
4. Adicionar Olá seguindo HTML toohello conteúdo final do arquivo hello e salve as alterações de saudação.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Exibir janela de saída de hello, quando Olá compilação .NET é concluída e você vê essas linhas, alterne tooyour back navegador e Olá sobre a página de atualização.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. As alterações foram aplicadas.

## <a name="4-debug-with-breakpoints"></a>4. Depurar com pontos de interrupção
Geralmente, as alterações serão necessário mais inspeção, aproveitando Olá depuração de recursos do Visual Studio.

1. Retornar tooVisual Studio e abra`Controllers\HomeController.cs`
2. Substitua o conteúdo de saudação do método do hello About () com os seguintes hello:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Definir um ponto de interrupção toohello à esquerda da saudação `string message`... linha.
4. Acertos  **&lt;F5 >** toostart depuração.
5. Navegue toohello sobre página toohit seu ponto de interrupção.
6. Alternar ponto de interrupção da saudação tooview tooVisual Studio e inspecionar o valor de saudação da mensagem.

   ![][2]

## <a name="summary"></a>Resumo
Com [ferramentas do Visual Studio 2015 para Docker](https://aka.ms/DockerToolsForVS), você pode obter produtividade de saudação do trabalhando localmente, com realismo de produção de hello de desenvolvimento em um contêiner do Docker.

## <a name="troubleshooting"></a>Solucionar problemas
[Troubleshooting Visual Studio Docker Development (Solucionar Problemas de Desenvolvimento do Docker do Visual Studio)](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Mais informações sobre o Docker com o Visual Studio, Windows e Azure
* [Ferramentas do Docker para Visual Studio](http://aka.ms/dockertoolsforvs) – Desenvolvendo seu código do .NET Core em um contêiner
* [Ferramentas do Docker para o Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) – Criar e Implantar contêineres do docker
* [Ferramentas do Docker para Visual Studio Code](http://aka.ms/dockertoolsforvscode) – Serviços de linguagem para editar arquivos do docker, com futuros cenários e2e
* [Informações do Contêiner do Windows](http://aka.ms/containers)– Informações sobre Windows Server e Nano Server
* [Serviço de Contêiner do Azure](https://azure.microsoft.com/services/container-service/) - [Conteúdo do Serviço de Contêiner do Azure](http://aka.ms/AzureContainerService)
* Para obter mais exemplos de como trabalhar com o Docker, consulte [trabalhando com o Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de saudação [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 conectar [demonstração](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Para mais guias de início rápido de demonstração de HealthClinic.biz hello, consulte [início rápido do Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Várias ferramentas do Docker
[Algumas ótimas ferramentas do Docker (blog de Steve Lasker)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Bons artigos
[Introdução tooMicroservices de NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Apresentações
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Steve Lasker: VS ao vivo de Las Vegas 2016 - Docker e2e)](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Introdução tooASP.NET núcleos @ 2016 - onde você na demonstração de compilação](https://channel9.msdn.com/Events/Build/2016/B810)
* [Developing .NET apps in containers, Channel 9 (Desenvolvendo aplicativos .NET em contêineres, Channel 9)](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
