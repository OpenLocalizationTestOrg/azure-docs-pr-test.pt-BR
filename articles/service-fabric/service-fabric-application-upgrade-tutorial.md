---
title: "tutorial de atualização aaaService malha aplicativo | Microsoft Docs"
description: "Este artigo o orienta através da experiência de saudação de implantar um aplicativo de malha do serviço, alterar o código de saudação e implantar uma atualização usando o Visual Studio."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Tutorial de atualização do aplicativo Service Fabric usando o Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Malha do serviço do Azure simplifica o processo de saudação da atualização de aplicativos em nuvem, garantindo que somente os serviços alterados são atualizados e que a integridade de aplicativos é monitorada em todo o processo de atualização de saudação. Ele também será revertida automaticamente versão anterior do hello aplicativo toohello ao encontrar problemas. As atualizações de aplicativo de malha do serviço são *tempo de inatividade Zero*, uma vez que o aplicativo hello pode ser atualizado sem tempo de inatividade. Este tutorial aborda como toocomplete uma atualização sem interrupção do Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Etapa 1: Criar e publicar o exemplo de objetos visuais hello
Primeiro, baixe o hello [objetos visuais](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) aplicativo do GitHub. Em seguida, criar e publicar o aplicativo hello clicando no projeto de aplicativo hello, **VisualObjects**e selecionando Olá **publicar** comando no item de menu Olá Service Fabric.

![Menu de contexto para um aplicativo do Service Fabric][image1]

Selecionando **publicar** abre um janela pop-up, e você pode definir Olá **perfil de destino** muito**PublishProfiles\Local.xml**. Olá janela deve ter aparência Olá a seguir antes de clicar em **publicar**.

![Publicar um aplicativo do Service Fabric][image2]

Agora você pode clicar em **publicar** na caixa de diálogo de saudação. Você pode usar [Service Fabric Explorer tooview Olá cluster e Olá o aplicativo](service-fabric-visualizing-your-cluster.md). Olá aplicativo Visual objetos tem um serviço web que você pode ir digitando tooby [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) na barra de endereços de saudação do seu navegador.  Você deve ver os 10 objetos visual flutuantes mover-se na tela hello.

**Observação:** se Implantando muito`Cloud.xml` perfil (Service Fabric do Azure), aplicativo hello, deve estar disponível em **http://{ServiceFabricName}. { Region}.cloudapp.Azure.com:8081/visualobjects/**. Verifique se você tem `8081/TCP` configurado no balanceador de carga da saudação (Localizar Olá balanceador de carga no hello mesmo grupo de recursos como instância do Service Fabric Olá).

## <a name="step-2-update-hello-visual-objects-sample"></a>Etapa 2: Atualizar exemplo de objetos visuais hello
Você pode notar que com a versão de saudação que foi implantado na etapa 1, objetos visuais Olá não gire. Vamos atualizar esse tooone aplicativo onde objetos visuais Olá também girar.

Selecione o projeto VisualObjects.ActorService Olá Olá VisualObjects solução e abra Olá **VisualObjectActor.cs** arquivo. Dentro desse arquivo, vá toohello método `MoveObject`, comente `visualObject.Move(false)`e remova os `visualObject.Move(true)`. Essa alteração de código gira objetos Olá depois que o serviço de saudação é atualizado.  **Agora você pode criar (não a recriação) Olá solução**, que compila Olá modificado projetos. Se você selecionar *recompilar tudo*, você tem versões de saudação tooupdate para todos os projetos de hello.

Também precisamos tooversion nosso aplicativo. versão de hello toomake alterações depois que você clica em Olá **VisualObjects** projeto, você pode usar o Visual Studio de saudação **Editar manifesto versões** opção. A seleção dessa opção abre caixa de diálogo Olá para versões de edição da seguinte maneira:

![Caixa de diálogo Controle de Versão][image3]

Versões de saudação de atualização para Olá modificado projetos e seus pacotes de código, juntamente com hello aplicativo tooversion 2.0.0. Depois que forem feitas alterações Olá, manifesto Olá deve ter aparência a seguir Olá (negrito partes mostram alterações Olá):

![Atualizando versões][image4]

ferramentas do Visual Studio Olá podem fazer pacotes cumulativos de atualizações automáticas de versões ao selecionar **atualizar automaticamente o aplicativo e as versões de serviço**. Se você usar [SemVer](http://www.semver.org), você precisa tooupdate Olá código e/ou configuração pacote versão somente se essa opção for selecionada.

Salvar alterações de saudação e verificar agora Olá **atualização Olá aplicativo** caixa.

## <a name="step-3--upgrade-your-application"></a>Etapa 3: Atualizar seu aplicativo
Familiarize-se com hello [parâmetros de atualização de aplicativo](service-fabric-application-upgrade-parameters.md) e hello [processo de atualização](service-fabric-application-upgrade.md) tooget um bom entendimento da saudação vários atualizar parâmetros, tempos limite e critérios de integridade que pode ser aplicada. Para este passo a passo, critério de avaliação de integridade de serviço de saudação é definido toohello padrão (modo de não monitorado). Você pode definir essas configurações selecionando **configurar configurações de atualização** e, em seguida, modificar parâmetros de saudação conforme desejado.

Agora, estamos todos os aplicativos de saudação do conjunto toostart atualização selecionando **publicar**. Essa opção atualiza tooversion seu aplicativo 2.0.0, no qual os objetos de saudação girar. Serviço malha atualiza um domínio de atualização de cada vez (alguns objetos são atualizados primeiro, seguido por outras pessoas) e serviço Olá permanece acessível durante a atualização de saudação. O serviço de acesso toohello pode ser verificado por meio de seu cliente (navegador).  

Agora, como hello prossegue de atualização do aplicativo, você poderá monitorá-lo com o Gerenciador do Service Fabric usando Olá **atualizações em andamento** guia em aplicativos de saudação.

Em alguns minutos, todos os domínios de atualização devem ser atualizados (concluído) e janela de saída do Visual Studio Olá também deve indicar que a atualização Olá é concluída. E você deve notar que *todos os* objetos visuais de saudação na janela do navegador estão girando agora!

Você pode desejar tootry alterando versões hello e mudança de versão 2.0.0 tooversion 3.0.0 como um exercício ou mesmo da versão 2.0.0 fazer tooversion 1.0.0. Experimentar tempos limite e toomake de diretivas de integridade por conta própria familiarizados com eles. Ao implantar tooan Azure cluster como oposição cluster local tooa, parâmetros de saudação usados podem ter toodiffer. É recomendável que você definir tempos limite de saudação impedidas.

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

Controle como seu aplicativo é atualizado usando [parâmetros de atualização](service-fabric-application-upgrade-parameters.md).

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [Solucionando problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
