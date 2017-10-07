---
title: aplicativos do Azure Service Fabric aaaManage usando a CLI do Azure Service Fabric
description: Saiba como toodeploy e remova os aplicativos do Service Fabric do Azure de cluster usando a CLI do Azure Service Fabric
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure Service Fabric

Saiba como toocreate e exclua os aplicativos em execução em um cluster do Azure Service Fabric.

## <a name="prerequisites"></a>Pré-requisitos

* Implantar a CLI do Service Fabric. Em seguida, selecione o cluster do Service Fabric. Para obter mais informações, consulte [Introdução à CLI do Service Fabric](service-fabric-cli.md).

* Ter uma malha de serviço aplicativo pacote pronto toobe implantado. Para obter mais informações sobre como tooauthor e pacote de um aplicativo, leia sobre Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Visão geral

toodeploy um novo aplicativo, execute estas etapas:

1. Carregar um repositório de imagem do aplicativo pacote toohello Service Fabric.
2. Provisione um tipo de aplicativo.
3. Especifique e crie um aplicativo.
4. Especifique e crie serviços.

tooremove um aplicativo existente, execute estas etapas:

1. Exclua aplicativo hello.
2. Olá desconfiguração associados tipo de aplicativo.
3. Exclua conteúdo do repositório de imagem de saudação.

## <a name="deploy-a-new-application"></a>Implantar um novo aplicativo

toodeploy um novo aplicativo, completo Olá tarefas a seguir:

### <a name="upload-a-new-application-package-toohello-image-store"></a>Carregar um novo repositório de imagem de toohello de pacote de aplicativo

Antes de criar um aplicativo, carregue o repositório de imagens do hello aplicativo pacote toohello Service Fabric.

Por exemplo, se o seu pacote de aplicativo está em Olá `app_package_dir` diretório, use Olá diretório de saudação tooupload comandos a seguir:

```azurecli
sfctl application upload --path ~/app_package_dir
```

Para grandes pacotes de aplicativos, você pode especificar Olá `--show-progress` opção toodisplay progresso de saudação do carregamento de saudação.

### <a name="provision-hello-application-type"></a>Tipo de aplicativo hello provisão

Quando terminar de carregar Olá, provisione o aplicativo hello. aplicativo de hello tooprovision, use Olá comando a seguir:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

Olá valor `application-type-build-path` é Olá nome do diretório de saudação em que você carregou o pacote de aplicativo.

### <a name="create-an-application-from-an-application-type"></a>Criar um aplicativo com base em um tipo de aplicativo

Depois de provisionar o aplicativo hello, use Olá tooname de comando a seguir e crie seu aplicativo:

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`é o nome de saudação que você deseja toouse para instância do aplicativo hello. Você pode obter parâmetros adicionais no manifesto do aplicativo provisionado anteriormente.

nome do aplicativo Hello deve começar com o prefixo Olá `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Criar serviços para o novo aplicativo de saudação

Depois de criar um aplicativo, crie serviços de aplicativo hello. Saudação de exemplo a seguir, criamos um novo serviço sem monitoração de estado do nosso aplicativo. Serviços de saudação que você pode criar a partir de um aplicativo são definidos em um manifesto de serviço no pacote de aplicativo provisionado anteriormente hello.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Verificar a integridade e a implantação do aplicativo

tooverify tudo está íntegro, use Olá comandos de integridade a seguir:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

tooverify que serviço Olá esteja íntegro, use semelhante integridade de saudação tooretrieve de comandos do serviço de saudação e do aplicativo:

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.

## <a name="remove-an-existing-application"></a>Remover um aplicativo existente

tooremove um aplicativo hello concluir tarefas a seguir:

### <a name="delete-hello-application"></a>Excluir aplicativo hello

aplicativo de hello toodelete, use Olá comando a seguir:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Desconfigurar o tipo de aplicativo hello

Depois de excluir o aplicativo hello, você pode desconfigurar o tipo de aplicativo hello se você não precisar mais dela. tipo de aplicativo toounprovision hello, use Olá comando a seguir:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

versão de nome e o tipo do tipo Hello deve coincidir nome hello e versão no manifesto de aplicativo provisionado anteriormente hello.

### <a name="delete-hello-application-package"></a>Excluir o pacote de aplicativo hello

Após cancelou o provisionamento de tipo de aplicativo hello, você pode excluir o pacote de aplicativo hello saudação do repositório de imagens se você não precisar mais dela. A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco. 

pacote de aplicativo toodelete Olá Olá do repositório de imagens, use Olá comando a seguir:

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`deve ser o nome de saudação do diretório Olá carregado quando você criou o aplicativo hello.

## <a name="upgrade-application"></a>Atualizar aplicativo

Depois de criar seu aplicativo, você pode repetir Olá mesmo conjunto de etapas tooprovision uma segunda versão do seu aplicativo. Em seguida, com uma atualização de aplicativo do Service Fabric transição toorunning Olá segunda versão do aplicativo hello. Para obter mais informações, consulte a documentação do hello em [atualizações de aplicativo do Service Fabric](service-fabric-application-upgrade.md).

tooperform uma atualização, primeiro provisionar Olá próxima versão do aplicativo usando a saudação Olá comandos mesmo de antes:

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

É recomendável tooperform uma atualização automática monitorada, reinicie a atualização Olá executando o comando a seguir de saudação:

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

As atualizações substituem os parâmetros existentes por qualquer conjunto especificado. Parâmetros do aplicativo devem ser passados como um comando de atualização de toohello de argumentos, se necessário. Parâmetros do aplicativo devem ser codificados como um objeto JSON.

tooretrieve todos os parâmetros especificados anteriormente, você pode usar o hello `sfctl application info` comando.

Quando uma atualização do aplicativo está em andamento, o status de saudação podem ser recuperados usando o `sfctl application upgrade-status` comando.

Finalmente, se uma atualização está em andamento e precisa toobe cancelada, você pode usar Olá `sfctl application upgrade-rollback` tooroll volta Olá atualização.

## <a name="next-steps"></a>Próximas etapas

* [Noções básicas do Service Fabric](service-fabric-cli.md)
* [Introdução ao Service Fabric no Linux](service-fabric-get-started-linux.md)
* [Iniciar uma atualização de aplicativo do Service Fabric](service-fabric-application-upgrade.md)
