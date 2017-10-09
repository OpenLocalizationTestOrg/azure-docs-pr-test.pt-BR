---
title: aaaSet seu ambiente de desenvolvimento no Linux | Microsoft Docs
description: "Instalar o tempo de execução de saudação e SDK e criar um cluster de desenvolvimento local no Linux. Depois de concluir esta instalação, você será aplicativos toobuild pronto."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Preparar seu ambiente de desenvolvimento no Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy e executar [aplicativos do Azure Service Fabric](service-fabric-application-model.md) em sua máquina de desenvolvimento do Linux, instalar o runtime do hello e SDK comuns. Você também pode instalar os SDKs opcionais para Java e .NET Core.

## <a name="prerequisites"></a>Pré-requisitos

Olá versões de sistemas operacionais a seguir têm suporte para desenvolvimento:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Atualizar suas fontes APT
tooinstall Olá SDK e hello em tempo de execução associado pacote por meio da ferramenta de linha de comando de apt get hello, primeiro você deve atualizar suas fontes de ferramenta de empacotamento avançadas (APT).

1. Abra um terminal.
2. Adicione lista de fontes de saudação do Service Fabric repositório tooyour.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Adicionar Olá `dotnet` lista de fontes de tooyour do repositório.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Adicionar Olá APT tooyour de token de autenticação de chave de nova proteção de privacidade do Gnu (GnuPG ou GPG).

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Adicione Olá oficial GPG Docker tooyour chave APT token de autenticação.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Configure o repositório de Docker hello.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. O pacote de atualização de lista com base nas Olá recentemente adicionado repositórios.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Instalar e configurar o hello SDK para a instalação de cluster local

Depois de atualizar as fontes, você pode instalar Olá SDK. Instalar o pacote do SDK do Service Fabric hello, Confirmar instalação hello e aceitar o contrato de licença de toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Olá, comandos a seguir automatizam aceitando licença Olá para pacotes de malha do serviço:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Configurar um cluster local
  Se Olá instalação for bem-sucedida, você deve ser capaz de toostart um cluster local.

  1. Execute o script de instalação de cluster hello.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Abra um navegador da web e vá muito[Service Fabric Explorer](http://localhost:19080/Explorer). Se Olá cluster foi iniciado, você deverá ver o painel do Gerenciador do Service Fabric hello.

      ![Service Fabric Explorer no Linux][sfx-linux]

  Neste ponto, você é capaz de implantar os pacotes do aplicativo Service Fabric predefinidos ou novos com base nos contêineres ou executáveis do convidado. toobuild novos serviços usando Olá Java ou .NET Core SDKs, execute as etapas de configuração opcional de saudação que são fornecidas nas seções subsequentes.


  > [!NOTE]
  > Não há suporte para os clusters autônomos no Linux. Olá visualização dá suporte a apenas uma caixa e clusters de vários computadores Linux do Azure.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Configurar Olá CLI de malha do serviço

Olá [CLI de malha do serviço](service-fabric-cli.md) tem comandos para interagir com entidades de malha do serviço, incluindo clusters e aplicativos. Ela se baseia em python, portanto, se toohave python e pip instalado antes de prosseguir com hello comando a seguir:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Instalar e configurar os geradores de saudação para contêineres e executáveis de convidado
O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo do Service Fabric no terminal usando gerador de modelos Yeoman. Siga as etapas de saudação abaixo tooensure que têm o gerador de modelo yeoman Olá Service Fabric para trabalhar em seu computador.

1. Instalar o nodejs e o NPM em seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar gerador de contêiner de serviço malha Yeo hello e gerador de execuatble guest de NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Depois que você instalou Olá acima geradores, você deve ser capaz de toocreate aplicativos com serviços de contêiner ou um executável de convidado executando `yo azuresfguest` ou `yo azuresfcontainer` respectivamente.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Instalar Olá Java artefatos necessários (opcionais, se você quiser toouse Olá Java modelos de programação)

Serviços de malha do serviço toobuild usando Java, certifique-se de ter 1.8 JDK instalado junto com o Gradle que é usado para executar tarefas de compilação. saudação de trecho de código a seguir instala abrir 1.8 JDK junto com Gradle. bibliotecas do Service Fabric Java Olá são extraídas da Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Instalar Olá Eclipse Neon plug-in (opcional)

Você pode instalar Olá plug-in do Eclipse para a malha do serviço de dentro de saudação **IDE do Eclipse para desenvolvedores de Java**. Você pode usar aplicativos executáveis do Eclipse toocreate Service Fabric convidado e aplicativos de contêiner em aplicativos de malha Java tooService adição.

1. No Eclipse, certifique-se de ter Neon mais recente do Eclipse e Olá a versão mais recente do Buildship (1.0.17 ou posterior) instalado. Você pode verificar as versões de saudação dos componentes instalados selecionando **ajuda** > **detalhes da instalação**. Você pode atualizar Buildship usando instruções Olá em [Buildship Eclipse: Plug-ins do Eclipse para Gradle][buildship-update].

2. tooinstall Olá selecione plug-in do Service Fabric **ajuda** > **instalar novo Software**.

3. Em Olá **trabalhar com** , digite **http://dl.microsoft.com/eclipse**.

4. Clique em **Adicionar**.

    ![página de Software disponíveis Olá][sf-eclipse-plugin]

5. Selecione Olá **ServiceFabric** plug-in e, em seguida, clique em **próximo**.

6. Conclua as etapas de instalação hello e, em seguida, aceite o contrato de licença de usuário final de saudação.

Se você já tiver Olá plug-in Eclipse de malha do serviço instalado, verifique se você tem a versão mais recente do hello. Você pode verificar selecionando **ajuda** > **detalhes da instalação** e procurando Service Fabric na lista de saudação do instalado plug-ins. Se uma versão mais recente estiver disponível, selecione **Atualizar**.

Para obter mais informações, consulte [Plug-in Service Fabric para o desenvolvimento de aplicativos Java do Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Instalar Olá .NET Core SDK (opcional, se desejar que os modelos de programação toouse Olá .NET Core)
Olá .NET Core SDK fornece bibliotecas hello e modelos de serviços do Service Fabric toobuild necessária com .NET Core. Instalar pacote do SDK do .NET Core Olá em execução a seguir Olá-

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Saudação de atualização SDK e o tempo de execução

versão mais recente do tooupdate toohello de saudação SDK e o tempo de execução, execute Olá comandos a seguir (desmarque Olá SDKs que você não deseja):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
binários do Java SDK tooupdate saudação do Maven, você precisa tooupdate detalhes de versão de saudação do binário correspondente de saudação em hello ``build.gradle`` versão mais recente do arquivo toopoint toohello. tooknow exatamente onde você precisa de tooupdate Olá versão, você pode consultar tooany ``build.gradle`` arquivo nos exemplos de guia de Introdução do Service Fabric [aqui](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Atualizando pacotes de saudação pode causar o toostop de cluster de desenvolvimento local em execução. Reinicie o cluster local após uma atualização seguindo as instruções de saudação nesta página.

## <a name="next-steps"></a>Próximas etapas

* [Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in Service Fabric para o Eclipse](service-fabric-get-started-eclipse.md)
* [Criar seu primeiro aplicativo do CSharp no Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Preparar seu ambiente de desenvolvimento no OSX](service-fabric-get-started-mac.md)
* [Usar Olá CLI de malha do serviço toomanage seus aplicativos](service-fabric-application-lifecycle-sfctl.md)
* [Diferenças Windows/Linux do Service Fabric](service-fabric-linux-windows-differences.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
