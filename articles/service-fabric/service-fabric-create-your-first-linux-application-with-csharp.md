---
title: aaaCreate seu primeiro aplicativo do Azure microservices no Linux usando o c# | Microsoft Docs
description: Criar e implantar um aplicativo do Service Fabric usando C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Criar seu primeiro aplicativo do Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

O Service Fabric fornece SDKs para compilação de serviços no Linux em .NET Core e Java. Neste tutorial, vamos examinar como toocreate um aplicativo para Linux e criar um serviço usando o c# (.NET Core).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, verifique se você [configurar o ambiente de desenvolvimento Linux](service-fabric-get-started-linux.md). Se você estiver usando Mac OS X, poderá [configurar um ambiente de uma caixa do Linux em uma máquina virtual usando Vagrant](service-fabric-get-started-mac.md).

Você também pode tooinstall Olá [CLI de malha do serviço](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Instalar e configurar os geradores de saudação para CSharp
O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo em CSharp do Service Fabric no terminal usando gerador de modelos Yeoman. Siga as etapas de saudação abaixo tooensure que ter gerador de modelo yeoman Olá Service Fabric para CSharp trabalhando em seu computador.
1. Instalar o nodejs e o NPM em seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar o gerador de aplicativo de serviço do Fabric Yeo Java Olá do NPM

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Criar um aplicativo hello
Um aplicativo de malha do serviço pode conter um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade do aplicativo hello. Olá Service Fabric [Yeoman](http://yeoman.io/) gerador para CSharp, que é instalado na última etapa, torna fácil toocreate seu primeiro serviço e tooadd mais mais tarde. Vamos usar Yeoman toocreate um aplicativo com um único serviço.

1. Em um terminal, digite Olá toostart comando compilar scaffolding Olá a seguir:`yo azuresfcsharp`
2. Nome do seu aplicativo.
3. Escolha o tipo de saudação do seu primeiro serviço e nomeie-o. Para fins de saudação deste tutorial, escolhemos um serviço de ator confiável.

   ![Gerador de Yeoman do Service Fabric para C#][sf-yeoman]

> [!NOTE]
> Para obter mais informações sobre opções de hello, consulte [visão geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Criar um aplicativo hello
modelos de serviço do Fabric Yeoman Olá incluem um script de compilação que você pode usar o aplicativo de Olá de toobuild de saudação terminal (depois de navegar toohello pasta de aplicativo).

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a>Implantar o aplicativo hello

Depois que o aplicativo hello é criado, você pode implantar cluster local toohello.

1. Conecte-se toohello cluster de malha do serviço local.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Execute o script de instalação de Olá fornecido no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.

    ```bash
    ./install.sh
    ```

Implantando aplicativo de hello criado é Olá mesmo como qualquer outro aplicativo de malha do serviço. Consulte a documentação de saudação em [gerenciar um aplicativo de malha do serviço com hello CLI de malha do serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.

Comandos de toothese de parâmetros podem ser encontrados nos manifestos de saudação gerado dentro do pacote de aplicativo hello.

Depois que o aplicativo hello foi implantado, abra um navegador e navegue até [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer). Em seguida, expanda Olá **aplicativos** nó e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Inicie o cliente de teste hello e executar um failover
Projetos de atores não fazem nada por conta própria. Eles exigem outro toosend de serviço ou cliente mensagens-los. modelo de ator Olá inclui um script de teste simples que você pode usar toointeract com o serviço de ator hello.

1. Execute script hello usando Olá inspecionar utilitário toosee Olá saída do serviço de ator hello.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. No Service Fabric Explorer, localize o nó que hospeda a réplica primária Olá para o serviço de ator hello. Olá captura de tela abaixo, é o nó 3.

    ![Localizar a réplica primária Olá no Gerenciador do Service Fabric][sfx-primary]
3. Clique no nó Olá encontrado na etapa anterior Olá, e selecione **desativar (reinicialização)** no menu de ações de saudação. Essa ação reinicia um nó no cluster local forçar uma réplica secundária de failover tooa em execução em outro nó. Ao executar esta ação, preste saída de toohello atenção de cliente de teste hello e anote que esse contador Olá continua tooincrement apesar Olá failover.

## <a name="adding-more-services-tooan-existing-application"></a>Adicionar mais serviços tooan aplicativo

tooadd outro tooan aplicativo de serviço já criado usando `yo`, executar Olá etapas a seguir:
1. Alterar o diretório raiz de toohello do aplicativo existente hello.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.
2. Execute o `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>Migrando do Project too.csproj
1. Executar 'dotnet migrar' no diretório raiz do projeto, todos os formato do hello Project toocsproj serão migrados.
2. Atualização Olá projeto faz referência a arquivos toocsproj em arquivos de projeto adequadamente.
3. Atualize Olá arquivo nomes toocsproj arquivos de projeto build.sh.

## <a name="next-steps"></a>Próximas etapas

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interagir com clusters de malha do serviço usando Olá CLI de malha do serviço](service-fabric-cli.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
