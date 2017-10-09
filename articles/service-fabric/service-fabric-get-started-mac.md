---
title: aaaSet seu ambiente de desenvolvimento em toowork do Mac OS X com o Azure Service Fabric | Microsoft Docs
description: "Instalar o tempo de execução hello, SDK e as ferramentas e criar um cluster de desenvolvimento local. Depois de concluir esta instalação, você será aplicativos toobuild pronto no Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Configurar seu ambiente de desenvolvimento no Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Você pode criar toorun de aplicativos do Service Fabric em clusters do Linux usando o Mac OS X. Este artigo aborda como tooset o Mac para o desenvolvimento.

## <a name="prerequisites"></a>Pré-requisitos
Serviço de malha não executar nativamente OS X. toorun um cluster local do serviço de malha, fornecemos uma máquina de virtual pré-configurado Ubuntu usando Vagrant e VirtualBox. Antes de começar, você precisa do:

* [Vagrant (v1.8.4 ou posterior)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Você precisa toouse mutuamente suporte para versões de Vagrant e VirtualBox. O Vagrant pode se comportar incorretamente em uma versão sem suporte do VirtualBox.
>

## <a name="create-hello-local-vm"></a>Criar hello VM local
toocreate Olá VM local que contém um cluster do Service Fabric 5 nós, execute Olá etapas a seguir:

1. Saudação de clone `Vagrantfile` repositório

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Esta etapa é colocar análises Olá arquivo `Vagrantfile` contendo Olá VM configuração junto com a saudação de local de saudação VM é baixada do.

2. Navegue toohello clone de local de repositório de saudação

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Opcional) Modificar configurações de VM saudação padrão

    Por padrão, Olá VM local está configurado da seguinte maneira:

   * 3 GB de memória alocada
   * Rede privada host configurado no IP 192.168.50.50 habilitando a passagem de tráfego de host de Mac Olá

     Você pode alterar qualquer uma dessas configurações ou adicionar outros toohello configuração VM em Olá `Vagrantfile`. Consulte Olá [documentação Vagrant](http://www.vagrantup.com/docs) para obter a lista completa Olá das opções de configuração.
4. Criar hello VM

    ```bash
    vagrant up
    ```

   Esta etapa baixa a imagem de VM de Olá pré-configurado, inicialização-o localmente e em seguida, configure uma malha local do serviço de cluster nele. Você deve esperar que ele tootake alguns minutos. Se a instalação for concluída com êxito, você verá uma mensagem na saída de hello indicando a que esse cluster hello está sendo inicializado.

    ![A configuração do cluster começa após o provisionamento da VM][cluster-setup-script]

    >[!TIP]
    > Se o download VM hello está demorando muito tempo, você pode baixá-lo usando wget ou Ondulação ou por meio de um navegador, navegando toohello link especificado por **config.vm.box_url** no arquivo hello `Vagrantfile`. Depois de baixar localmente, editar `Vagrantfile` toopoint toohello caminho local onde você baixou a imagem de saudação. Por exemplo se você baixou Olá imagem too/home/users/test/azureservicefabric.tp8.box, em seguida, definir **config.vm.box_url** toothat caminho.
    >

5. Testar esse Olá cluster foi configurado corretamente, navegando tooService Fabric Explorer no http://192.168.50.50:19080/Explorer (supondo que mantidos IP de rede privada de padrão de saudação).

    ![Service Fabric Explorer exibido a partir do host de saudação Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Criar um aplicativo Mac usando Yeoman
O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo do Service Fabric no terminal usando gerador de modelos Yeoman. Siga as etapas de saudação abaixo tooensure que têm o gerador de modelo yeoman Service Fabric Olá trabalhando em seu computador.

1. Você precisará toohave Node. js e NPM mac é instalado. Se não é possível instalar Node. js e NPM usando Homebrew usando os seguintes hello. versões de saudação do toocheck do Node. js e NPM instalado no seu Mac, você pode usar o hello ``-v`` opção.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM

  ```bash
  npm install -g yo
  ```
3. Instalar Olá Yeoman gerador você deseja toouse, seguindo as etapas de Olá Olá Introdução [documentação](service-fabric-get-started-linux.md). Aplicativos de malha do serviço toocreate usando Yeoman, execute as etapas de saudação-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild um aplicativo de serviço do Fabric Java no Mac, você precisaria - JDK 1.8 e instalado na máquina de saudação do Gradle.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Instalar o plug-in do Service Fabric Olá para Eclipse Neon

Serviço de malha fornece um plug-in para Olá **Neon Eclipse para Java IDE** que pode simplificar o processo de saudação de criar, compilar e implantar serviços de Java. Você pode seguir etapas de instalação Olá mencionadas neste geral [documentação](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sobre como instalar ou atualizar o plug-in do Eclipse de malha do serviço.

>[!TIP]
> Por padrão oferecemos suporte a saudação padrão IP conforme mencionado em Olá ``Vagrantfile`` em Olá ``Local.json`` do aplicativo hello gerado. No caso de você alterá-la e implantar Vagrant com um IP diferente, atualize o IP de saudação correspondente no ``Local.json`` do seu aplicativo.

## <a name="next-steps"></a>Próximas etapas
<!-- Links -->
* [Criar e implantar seu primeiro aplicativo Java de do Service Fabric no Linux usando Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in do Service Fabric para o Eclipse](service-fabric-get-started-eclipse.md)
* [Criar um cluster do Service Fabric no hello portal do Azure](service-fabric-cluster-creation-via-portal.md)
* [Criar um cluster do Service Fabric usando hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Entender o modelo de aplicativo do Service Fabric Olá](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
