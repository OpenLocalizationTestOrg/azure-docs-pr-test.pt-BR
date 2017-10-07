---
title: aplicativos do Azure Service Fabric aaaManage usando 2.0 do CLI do Azure
description: Saiba como toodeploy e remova os aplicativos do Service Fabric do Azure de cluster usando o Azure CLI 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure 2.0

Saiba como toocreate e exclua os aplicativos em execução em um cluster do Azure Service Fabric.

## <a name="prerequisites"></a>Pré-requisitos

* Instale a CLI do Azure 2.0. Em seguida, selecione o cluster do Service Fabric. Para obter mais informações, consulte [Introdução à CLI do Azure 2.0](service-fabric-azure-cli-2-0.md).

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

toodeploy um novo aplicativo, completo Olá tarefas a seguir.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Carregar um novo repositório de imagem de toohello de pacote de aplicativo

Antes de criar um aplicativo, carregue o repositório de imagens do hello aplicativo pacote toohello Service Fabric. 

Por exemplo, se o seu pacote de aplicativo está em Olá `app_package_dir` diretório, use Olá diretório de saudação tooupload comandos a seguir:

```azurecli
az sf application upload --path ~/app_package_dir
```

Para grandes pacotes de aplicativos, você pode especificar Olá `--show-progress` opção toodisplay progresso de saudação do carregamento de saudação.

### <a name="provision-hello-application-type"></a>Tipo de aplicativo hello provisão

Quando terminar de carregar Olá, provisione o aplicativo hello. aplicativo de hello tooprovision, use Olá comando a seguir:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Olá valor `application-type-build-path` é Olá nome do diretório de saudação em que você carregou o pacote de aplicativo.

### <a name="create-an-application-from-an-application-type"></a>Criar um aplicativo com base em um tipo de aplicativo

Depois de provisionar o aplicativo hello, use Olá tooname de comando a seguir e crie seu aplicativo:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`é o nome de saudação que você deseja toouse para instância do aplicativo hello. Você pode obter parâmetros adicionais do manifesto de aplicativo provisionado anteriormente hello.

nome do aplicativo Hello deve começar com o prefixo Olá `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Criar serviços para o novo aplicativo de saudação

Depois de criar um aplicativo, crie serviços de aplicativo hello. Saudação de exemplo a seguir, criamos um novo serviço sem monitoração de estado do nosso aplicativo. Serviços de saudação que você pode criar a partir de um aplicativo são definidos em um manifesto de serviço no pacote de aplicativo provisionado anteriormente hello.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Verificar a integridade e a implantação do aplicativo

tooverify que um aplicativo e o serviço foram implantados com êxito, verifique se o serviço e aplicativo hello estão listados:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify que serviço Olá esteja íntegro, use semelhante integridade de saudação tooretrieve de comandos de serviço hello e o aplicativo hello:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.

## <a name="remove-an-existing-application"></a>Remover um aplicativo existente

tooremove um aplicativo hello concluir tarefas a seguir.

### <a name="delete-hello-application"></a>Excluir aplicativo hello

aplicativo de hello toodelete, use Olá comando a seguir:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Desconfigurar o tipo de aplicativo hello

Depois de excluir o aplicativo hello, você pode desconfigurar o tipo de aplicativo hello se você não precisar mais dela. tipo de aplicativo toounprovision hello, use Olá comando a seguir:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

versão de nome e o tipo do tipo Hello deve coincidir nome hello e versão no manifesto de aplicativo provisionado anteriormente hello.

### <a name="delete-hello-application-package"></a>Excluir o pacote de aplicativo hello

Após cancelou o provisionamento de tipo de aplicativo hello, você pode excluir o pacote de aplicativo hello saudação do repositório de imagens se você não precisar mais dela. A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco. 

pacote de aplicativo toodelete Olá Olá do repositório de imagens, use Olá comando a seguir:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`deve ser o nome de saudação do diretório Olá carregado quando você criou o aplicativo hello.

## <a name="related-articles"></a>Artigos relacionados

* [Introdução ao Service Fabric e à CLI do Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Introdução à CLI XPlat do Service Fabric](service-fabric-azure-cli.md)
