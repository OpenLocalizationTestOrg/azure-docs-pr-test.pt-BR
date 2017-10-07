---
title: "aaaDeploy um aplicativo .NET em um contêiner de tooAzure Service Fabric | Microsoft Docs"
description: "Ensina como toopackage um aplicativo .NET no Visual Studio em um contêiner do Docker. Esse novo aplicativo de \"contêiner\", em seguida, é implantado cluster do Service Fabric tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Implantar um aplicativo .NET em um contêiner de Windows tooAzure Service Fabric

Este tutorial mostra como toodeploy um aplicativo ASP.NET existente em um contêiner do Windows no Azure.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um projeto do Docker no Visual Studio
> * Colocar um aplicativo existente em um contêiner
> * Configurar a integração contínua com o Visual Studio e o VSTS

## <a name="prerequisites"></a>Pré-requisitos

1. Instalar o [Docker CE para Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) de forma que você possa executar contêineres no Windows 10.
2. Familiarize-se com hello [início rápido de contêineres do Windows 10][link-container-quickstart].
3. Baixar Olá [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicativo de exemplo.
4. Instalar o [Azure PowerShell][link-azure-powershell-install]
5. Instalar Olá [extensão de ferramentas de entrega contínua para 2017 do Visual Studio][link-visualstudio-cd-extension]
6. Criar uma [assinatura do Azure][link-azure-subscription] e uma [conta do Visual Studio Team Services][link-vsts-account]. 
7. [Criar um cluster no Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Coloca o aplicativo hello

Agora que você tem um [cluster do Service Fabric está em execução no Azure](service-fabric-tutorial-create-cluster-azure-ps.md) são toocreate pronto e implantar um aplicativo em contêineres. toostart executar o aplicativo em um contêiner, é preciso tooadd **Docker suporte** toohello projeto no Visual Studio. Quando você adiciona **suporte Docker** toohello aplicativo, duas coisas acontecem. Primeiro, um _Dockerfile_ é adicionado toohello projeto. Esse novo arquivo descreve como a imagem de contêiner de saudação é toobe criado. Em seguida, segundo, um novo _compor docker_ projeto é adicionado toohello solução. Olá, novo projeto contém alguns arquivos de compor docker. Compor docker arquivos podem ser usado toodescribe como contêiner Olá é executado.

Mais informações sobre como trabalhar com as [Ferramentas de Contêiner do Visual Studio][link-visualstudio-container-tools].

>[!NOTE]
>Se for Olá primeira vez que você está executando a imagens de contêiner do Windows em seu computador, Docker CE deve suspenso imagens de base Olá para os contêineres. imagens de saudação usadas neste tutorial são 14 GB. Vá em frente e execute Olá base imagens do comando terminal toopull Olá a seguir:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Adicionar suporte ao Docker

Olá abrir [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] arquivo no Visual Studio.

Saudação de atalho **FabrikamFiber.Web** projeto > **adicionar** > **Docker suporte**.

### <a name="add-support-for-sql"></a>Adicionar suporte para SQL

Este aplicativo usa SQL como provedor de dados Olá, para que um SQL server é necessário toorun Olá aplicativo. Referencie uma imagem de contêiner do SQL Server em nosso arquivo docker-compose.override.yml.

No Visual Studio, abra **Gerenciador de soluções**, localizar **compor docker**e o arquivo aberto Olá **compose.override.yml docker**.

Navegue toohello `services:` nó, adicionar um nó denominado `db:` que define a entrada do SQL Server Olá para o contêiner de saudação.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Você pode usar qualquer SQL Server que preferir para a depuração local, desde que ele seja acessível no host. No entanto, **localdb** não dá suporte à comunicação `container -> host`.

>[!WARNING]
>A execução do SQL Server em um contêiner não dá suporte a dados persistentes. Quando o contêiner de saudação for interrompida, seus dados são apagados. Não use essa configuração para produção.

Navegue toohello `fabrikamfiber.web:` nó e adicionar um nó filho denominado `depends_on:`. Isso garante que Olá `db` serviço (contêiner de saudação do SQL Server) é iniciado antes de nosso aplicativo web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Atualizar a configuração de web Olá

Em Olá **FabrikamFiber.Web** projeto, a cadeia de caracteres de conexão Olá de atualização em hello **Web. config** de arquivos toopoint toohello do SQL Server no contêiner de saudação.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Se você quiser toouse um SQL Server diferente durante a criação de uma versão de compilação do seu aplicativo web, adicione outro arquivo de web.release.config do tooyour cadeia de conexão.

### <a name="test-your-container"></a>Testar o contêiner

Pressione **F5** toorun e depurar aplicativo hello em seu contêiner.

Borda abre a página de inicialização definido do seu aplicativo usando o endereço IP de saudação do contêiner Olá na rede interna de NAT hello (geralmente 172.x.x.x). toolearn mais sobre a depuração de aplicativos em contêineres com o Visual Studio de 2017, consulte [neste artigo][link-debug-container].

![exemplo de fabrikam em um contêiner][image-web-preview]

contêiner de saudação agora está pronto toobe criados e empacotados em um aplicativo de malha do serviço. Uma vez que a imagem de contêiner Olá criada no seu computador, você pode por push do registro de contêiner tooany e levante-o para baixo tooany toorun de host.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Preparar o aplicativo hello para nuvem Olá

aplicativo de hello tooget pronto para execução na malha do serviço no Azure, é preciso toocomplete duas etapas:

1. Expor porta Olá onde desejamos tooreach capaz de toobe nosso aplicativo web no cluster do Service Fabric hello.
2. Fornecer um banco de dados SQL pronto para produção para nosso aplicativo.

### <a name="expose-hello-port-for-hello-app"></a>Expor porta Olá para o aplicativo hello
cluster do Service Fabric Olá configuramos, tem porta *80* aberta por padrão no hello balanceador de carga do Azure, que equilibra a entrada cluster toohello de tráfego. É possível expor o contêiner nessa porta por meio do arquivo docker-compose.yml.

No Visual Studio, abra **Gerenciador de soluções**, localizar **compor docker**e o arquivo aberto Olá **compose.override.yml docker**.

Modificar Olá `fabrikamfiber.web:` nó, adicionar um nó filho denominado `ports:`.

Adicione uma entrada de cadeia de caracteres `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Usar um banco de dados SQL de produção
Ao executar em produção, precisamos que os dados sejam persistidos em nosso banco de dados. Atualmente há nenhum dado persistente de tooguarantee de maneira em um contêiner, portanto você não pode armazenar dados de produção no SQL Server em um contêiner.

Recomendamos o uso de um Banco de Dados SQL do Azure. tooset backup e executar um servidor gerenciado do SQL no Azure, visite Olá [início rápido de banco de dados do SQL Azure] [ link-azure-sql] artigo.

>[!NOTE]
>Lembre-se de toochange Olá conexão cadeias de caracteres toohello do SQL server no hello **web.release.config** arquivo hello **FabrikamFiber.Web** projeto.
>
>Esse aplicativo falha normalmente se nenhum banco de dados SQL está acessível. Você pode escolher toogo em frente e implantar o aplicativo hello com nenhum SQL server.

## <a name="deploy-with-visual-studio-team-services"></a>Implantar com o Visual Studio Team Services

tooset a implantação usando o Visual Studio Team Services, você precisa Olá tooinstall [extensão de ferramentas de entrega contínua para Visual Studio de 2017][link-visualstudio-cd-extension]. Essa extensão torna fácil toodeploy tooAzure por meio da configuração do Visual Studio Team Services e obter o cluster do aplicativo implantado tooyour Service Fabric.

tooget iniciado, seu código deve ser hospedado no controle de origem. assume restante desta seção Olá **git** está sendo usado.

### <a name="set-up-a-vsts-repo"></a>Configurar um repositório do VSTS
No canto inferior direito de saudação do Visual Studio, clique em **adicionar tooSource controle** > **Git** (ou qualquer opção que você preferir).

![Pressione o botão de controle do código-fonte Olá][image-source-control]

Em Olá _Team Explorer_ painel, pressione **publicar o repositório do Git**.

Selecione o nome do repositório VSTS e pressione **Repositório**.

![publicar o repositório tooVSTS][image-publish-repo]

Agora que seu código está sincronizado com um repositório de origem do VSTS, você pode configurar a integração e a entrega contínuas.

### <a name="setup-continuous-delivery"></a>Configurar a entrega contínua

Em _Solution Explorer_, Olá do botão direito do mouse **solução** > **configurar fornecimento contínuo**.

Selecione Olá assinatura do Azure.

Definir **tipo de Host** muito**Cluster do Service Fabric**.

Definir **Host de destino** toohello cluster do service fabric você criou na seção anterior hello.

Escolha um **registro de contêiner** toopublish seu recipiente.

>[!TIP]
>Saudação de uso **editar** botão toocreate um registro de contêiner.

Pressione **OK**.

![configurar a integração contínua do service fabric][image-setup-ci]
   
   Concluída a configuração Olá, o contêiner é implantado tooService malha. Sempre que você enviar por push o repositório de toohello atualizações uma nova compilação e a versão é executado.
   
   >[!NOTE]
   >Imagens de contêiner de saudação de construção levar aproximadamente 15 minutos.
   >Olá primeiro implantação toohello Service Fabric cluster faz com que Olá base Windows Server Core contêiner imagens toobe baixado. download de saudação leva toocomplete mais de 5 a 10 minutos.

Navegar no aplicativo de Call Center de Fabrikam toohello usando a url de saudação do cluster: por exemplo, *http://mycluster.westeurope.cloudapp.azure.com*

Agora que você tem em contêineres e implantado Olá Fabrikam Call Center solução, você pode abrir Olá [portal do Azure] [ link-azure-portal] e ver o aplicativo hello em execução no serviço de malha. aplicativo de hello tootry, abra um navegador da web e vá toohello URL do cluster do Service Fabric.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Criar um projeto do Docker no Visual Studio
> * Colocar um aplicativo existente em um contêiner
> * Configurar a integração contínua com o Visual Studio e o VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
