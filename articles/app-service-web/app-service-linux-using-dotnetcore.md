---
title: aaaUse .NET Core no aplicativo Web no Linux | Microsoft Docs
description: Usar o .NET Core em aplicativo Web no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Usar o .NET Core em um aplicativo Web do Azure no Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Aplicativo da Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) no Linux fornece um serviço de hospedagem na web altamente escalonável, aplicação de patch automática usando o sistema de operacional Linux Olá. Este tutorial contém instruções passo a passo mostra como toocreate uma [.NET Core](https://docs.microsoft.com/aspnet/core/) aplicativo no aplicativo web do Azure no Linux. 

![Aplicativo Web no Linux][10]

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.

## <a name="prerequisites"></a>Pré-requisitos ##

toocomplete este tutorial: 

* Instalar Olá [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Instale o [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Criar um aplicativo .NET Core local ##

Inicie uma nova sessão de terminal. Crie um diretório chamado `hellodotnetcore`e alterar Olá tooit de diretório atual. Em seguida, digite o seguinte hello: 

```
dotnet new web
``` 

  Este comando cria três arquivos (*hellodotnetcore.csproj*, *Program.cs*, e *Startup.cs*) e uma pasta vazia (*wwwroot /*) no diretório atual da saudação. Olá conteúdo de `.csproj` arquivo deve ser semelhante Olá seguinte: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Como esse aplicativo é um aplicativo web, um tooan de referência do pacote ASP.NET Core foi automaticamente adicionada toohello *hellodotnetcore.csproj* arquivo. número de versão de saudação do pacote de saudação é definido toohello escolhido do framework de acordo com. Este exemplo faz referência à versão 1.1.2 do ASP.NET Core porque o .NET Core 1.1 é usado.

## <a name="build-and-test-hello-application-locally"></a>Compilar e testar o aplicativo hello localmente ##

Você pode compilar e executar seu aplicativo .NET Core com hello `dotnet restore` comando seguido Olá `dotnet run` de comando, conforme mostrado aqui:

```
dotnet restore
dotnet run
```


Quando o aplicativo hello é iniciado, ele exibe uma mensagem indicando que o aplicativo hello está escutando as solicitações de tooincoming em uma porta. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Testá-lo navegando muito`http://localhost:5000/` com seu navegador. Se tudo estiver funcionando bem, você verá "Olá, Mundo!" como o texto de saudação do resultado.

![Testar com um navegador][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Criar um aplicativo .NET Core em Olá Portal do Azure ##

Primeiro, é necessário toocreate um aplicativo web vazio. Faça logon no toohello [portal do Azure](https://portal.azure.com/) e criar um novo [Web App no Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Criar um aplicativo Web][1]

Olá quando **criar** página será aberta, forneça detalhes sobre seu aplicativo web:

![Escolher uma pilha de tempo de execução do .NET Core][2]

Tabela a seguir de saudação uso como um toofill guia saída Olá **criar** página e, em seguida, selecione **Okey** e **criar** toocreate Olá aplicativo.

| Configuração      | Valor sugerido  | Descrição                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nome do aplicativo | hellodotnetcore  | nome de saudação do seu aplicativo. Esse nome deve ser exclusivo. |
| Assinatura | Escolher uma assinatura existente | Olá assinatura do Azure. |
| Grupo de recursos | myResourceGroup |  aplicativo Hello recursos do Azure grupo toocontain Olá web. |
| Plano do Serviço de Aplicativo | Nome do plano do Serviço de Aplicativo existente |  saudação do plano de serviço de aplicativo.  |
| Configurar o contêiner | .NET Core 1.1 | Olá tipo de contêiner para este aplicativo web: registro internas, Docker ou privada. |
| Origem da imagem  | Interno  |  origem de saudação da imagem de saudação. |
| Pilha de tempo de execução  | .NET Core 1.1  | pilha de tempo de execução Hello e versão.  |

## <a name="deploy-your-application-via-git"></a>Implantar seu aplicativo por meio do Git ##

Use Git toodeploy Olá .NET Core aplicativo tooAzure aplicativo Web do serviço de aplicativo no Linux.

novo aplicativo web do Azure e Olá já tem Git implantação configurada. Você encontrará uma URL de implantação do Git Olá navegando toohello URL a seguir depois de inserir o nome do aplicativo web:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Olá URL de Git tem Olá formulário com base no nome do aplicativo da web a seguir:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Execute Olá aplicativo web do Azure tooyour de aplicativo local do comandos toodeploy Olá a seguir: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Não é necessário toopush todos os arquivos no *bin /* ou *obj /* diretórios porque seu aplicativo é criado na nuvem Olá Olá do aplicativo quando os arquivos de origem são enviados por push tooAzure. Após a conclusão do processo de compilação hello, arquivos binários são copiados para o diretório do aplicativo hello em *inicial/site/wwwroot/*.

Confirme que o relatório de operações de implantação remota Olá sucesso. Operações de envio podem levar um tempo desde a resolução de pacote e executado na nuvem de saudação do processo de compilação. Você verá várias mensagens de status, inclusive algumas informando que os arquivos foram copiados. saída de Hello deve ser a seguir toohello semelhante:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Após a conclusão da implantação Olá, reinicie seu aplicativo web para efeito de tootake implantação hello. toodo isso, vá toohello portal do Azure e navegue toohello **visão geral** página do seu aplicativo web. Selecione Olá **reiniciar** botão na página de saudação. Quando uma janela pop-up aparece, selecione **Sim** tooconfirm. Em seguida, você pode procurar o aplicativo Web, conforme mostrado aqui:

![Pesquisa no .NET Core aplicativo implantado tooAzure do serviço de aplicativo no Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Próximas etapas
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
