---
title: "aaaCreate um Windows UWP (plataforma Universal) que usa em aplicativos móveis | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de back-ends dos aplicativos móveis do Azure para desenvolvimento de aplicativos do Windows UWP (plataforma Universal) no c#, Visual Basic ou JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Criar um aplicativo do Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como tooadd um back-end baseado em nuvem tooa Windows UWP (plataforma Universal) aplicativo de serviço. Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md). Olá seguem capturas de tela do aplicativo hello concluída:

![Aplicativo de área de trabalho concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
em execução em uma área de trabalho.

![Aplicativo de telefone concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
em execução em um telefone

A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos UWP.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se você não tiver uma conta, você pode inscrever-se para uma avaliação do Azure e obter o too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] ou uma versão posterior.

## <a name="create-a-new-azure-mobile-app-backend"></a>Criar um novo back-end de aplicativo móvel do Azure
Siga essas etapas toocreate um novo back-end do aplicativo móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes. Em seguida, você baixará um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar o projeto do servidor de saudação
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Baixe e execute o projeto de saudação do cliente
Quando você tiver configurado seu back-end do aplicativo móvel, você pode criar um novo aplicativo de cliente ou modificar um tooAzure de tooconnect de aplicativo existente. Nesta seção, você baixar um projeto de modelo de aplicativo UWP que é o back-end de aplicativo móvel de tooyour tooconnect personalizado.

1. Em Olá **início rápido** folha para seu back-end do aplicativo móvel, clique em **criar um novo aplicativo** > **baixar**, extraia os arquivos de projeto Olá compactado tooyour de computador local.

    ![Baixar o projeto de início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Opcional) Adicionar toohello de projeto de aplicativo UWP Olá mesma solução que o projeto do servidor de saudação. Isso facilita toodebug e teste ambos Olá Olá e aplicativos back-end em Olá mesma solução do Visual Studio, se você escolher toodo isso. tooadd uma solução de toohello de projeto de aplicativo UWP, você deve estar usando o Visual Studio 2015 ou posterior.
3. Com o aplicativo UWP hello como projeto de inicialização hello, pressione Olá F5 chave toodeploy e aplicativo hello execução.
4. No aplicativo hello, digite o texto significativo, como *tutorial completo Olá*, em Olá **inserir um TodoItem** caixa de texto e clique **salvar**.

    ![Área de trabalho completa do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Isso envia um POST solicitação toohello novo aplicativo móvel back-end que está hospedado no Azure.
5. (Opcional) Interromper um aplicativo hello e reiniciá-lo em outro dispositivo ou emulador móvel.

    ![Telefone completo do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Observe que os dados salvos da etapa anterior Olá seja carregados do Azure após o início do aplicativo UWP de saudação.

## <a name="next-steps"></a>Próximas etapas
* [Adicionar autenticação tooyour aplicativo](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.
* [Adicionar aplicativo de tooyour de notificações por push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.
* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel. Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
