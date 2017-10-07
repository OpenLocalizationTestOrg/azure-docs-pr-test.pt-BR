---
title: aaaManage seus aplicativos no Visual Studio | Microsoft Docs
description: "Usar o Visual Studio toocreate, desenvolver, pacotes, implantar e depurar seus aplicativos de serviço de malha e serviços."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Use a gravação de toosimplify do Visual Studio e gerenciar seus aplicativos do Service Fabric
É possível gerenciar os serviços e aplicativos do Service Fabric do Azure por meio do Visual Studio. Depois que você [configurar seu ambiente de desenvolvimento](service-fabric-get-started.md), usar os aplicativos do Visual Studio toocreate Service Fabric, adicionar um registro de serviços ou pacote e implantar aplicativos em seu cluster de desenvolvimento local.

## <a name="deploy-your-service-fabric-application"></a>Implantar o aplicativo do Service Fabric
Por padrão, implantando um aplicativo combina Olá seguindo as etapas em uma operação simple:

1. Criar pacote de aplicativo hello
2. Carregando o repositório de imagens toohello do pacote de aplicativo hello
3. Registrando o tipo de aplicativo hello
4. Remover as instâncias de aplicativo em execução
5. Criando uma instância do aplicativo

No Visual Studio, pressionando **F5** anexar instâncias do aplicativo hello depurador tooall e implanta seu aplicativo. Você pode usar **Ctrl + F5** toodeploy um aplicativo sem depuração ou você pode publicar tooa local ou cluster remoto usando Olá perfil de publicação. Para obter mais informações, consulte [publicar um cluster remoto de tooa do aplicativo usando o Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Modo de Depuração do Aplicativo
Visual Studio fornece uma propriedade chamada **o modo de depuração de aplicativo**, que controla como deseja que a implantação de aplicativos do Visual estúdios toohandle como parte da depuração.

#### <a name="tooset-hello-application-debug-mode-property"></a>Olá tooset propriedade modo de depuração de aplicativo
1. Em Olá Service Fabric do projeto de aplicação (*. sfproj) menu de atalho, escolha **propriedades** (ou pressione hello **F4** chave).
2. Em Olá **propriedades** janela, Olá conjunto **o modo de depuração de aplicativo** propriedade.

![Definir a Propriedade Modo de Depuração do Aplicativo][debugmodeproperty]

#### <a name="application-debug-modes"></a>Modos de depuração do aplicativo

1. **Atualizar aplicativo** esse modo permite que você altere tooquickly e depurar seu código e dá suporte à edição de arquivos de estático da web durante a depuração. Esse modo funciona apenas se o cluster de desenvolvimento local está em [Modo 1 Nó](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Remover aplicativo** causas Olá toobe aplicativo removido quando a sessão de depuração Olá termina.
3. **Auto atualização** aplicativo hello continua toorun quando a sessão de depuração Olá termina. Olá próxima sessão de depuração tratará implantação hello como uma atualização. o processo de atualização Olá preserva todos os dados inseridos em uma sessão de depuração anterior.
4. **Manter o aplicativo** Olá aplicativo mantém em execução no cluster hello quando hello término da sessão de depuração. Olá começo da saudação próxima sessão de depuração, aplicativo hello será removido.

Para **atualização automática** os dados são preservados, aplicando a capacidade de atualização de aplicativo hello do Service Fabric. Para obter mais informações sobre como atualizar aplicativos e como executar uma atualização em um ambiente real, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Adicionar um serviço tooyour aplicativo do Service Fabric
Você pode adicionar novos serviços tooyour aplicativo tooextend sua funcionalidade.  tooensure que o serviço de saudação está incluído em seu pacote de aplicativo, adicione o serviço de Olá por meio de saudação **novo Service Fabric...**  item de menu.

![Adicionar um novo serviço Service Fabric][newservice]

Selecione um aplicativo do Service Fabric projetos tipo tooadd tooyour e especifique um nome para o serviço de saudação.  Consulte [escolher uma estrutura para seu serviço](service-fabric-choose-framework.md) toohelp decidir qual serviço digite toouse.

![Selecione um aplicativo do Service Fabric service projeto tipo tooadd tooyour][addserviceproject]

novo serviço de saudação é adicionado à solução tooyour e pacote de aplicativo existente. Olá referências de serviço e uma instância de serviço padrão será adicionado toohello o manifesto do aplicativo, causando toobe de serviço Olá criada e iniciada Olá próxima vez que você implantar o aplicativo hello.

![Olá novo serviço é adicionado, o manifesto do aplicativo tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Empacotar o aplicativo do Service Fabric
aplicativo de hello toodeploy e seu cluster tooa de serviços, é necessário toocreate um pacote de aplicativo.  pacote de saudação organiza o manifesto do aplicativo hello, manifestos do serviço e outros arquivos necessários em um layout específico.  Visual Studio configura e gerencia Olá pacote na pasta do projeto de aplicativo hello, no diretório de 'pkg' hello.  Clicando em **pacote** de saudação **aplicativo** cria do menu de contexto ou atualizações Olá pacote de aplicativo.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Remover aplicativos e tipos de aplicativo usando o Gerenciador de Nuvem
Você pode executar operações de gerenciamento de cluster básico do Visual Studio usando o Gerenciador de nuvem, que você pode iniciar de saudação **exibição** menu. Por exemplo, você pode excluir aplicativos e desprovisionar tipos de aplicativos em clusters locais ou remotos.

![Remover um aplicativo][removeapplication]

> [!TIP]
> Para funcionalidade de gerenciamento de cluster mais avançada, confira [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
* [Modelo de aplicativo da Malha do Serviço](service-fabric-application-model.md)
* [Implantação de aplicativo da Malha do Serviço](service-fabric-deploy-remove-applications.md)
* [Gerenciando parâmetros do aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md)
* [Depurando o aplicativo da Malha do Serviço](service-fabric-debugging-your-application.md)
* [Visualização do cluster usando o Gerenciador do Service Fabric](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png