---
title: "aaaGet iniciado com aplicativos móveis do Azure para aplicativos xamarin"
description: "Siga este tutorial tooget iniciado usando aplicativos móveis do Azure para o desenvolvimento do Xamarin Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Criar um Aplicativo Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como tooadd um back-end baseado em nuvem tooa xamarin aplicativo de serviço. Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md).

É uma captura de tela do aplicativo hello concluída abaixo:

![][0]

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos Xamarin.Android.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* Uma conta ativa do Azure. Se você não tiver uma conta, inscreva-se para um avaliação do Azure e começar a aplicativos móveis livre de too10. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio com Xamarin. Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end de aplicativo móvel do Azure
Siga essas etapas toocreate um back-end do aplicativo móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes. Em seguida, baixar um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar o projeto do servidor de saudação
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Baixe e execute o aplicativo de xamarin Olá
1. Em **baixar e executar o projeto xamarin**, clique em Olá **baixar** botão.

      Salvar o computador local do hello projeto compactado arquivo tooyour e anote onde você salvá-lo.
2. Olá pressione **F5** chave projeto de saudação toobuild e iniciar o aplicativo hello.
3. No aplicativo hello, digite o texto significativo, como *tutorial completo Olá* e, em seguida, clique em Olá **adicionar** botão.

    ![][10]

    Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação. Itens armazenados na tabela de saudação são retornados pelo back-end de aplicativo móvel hello e os dados aparecem na lista de saudação.

   > [!NOTE]
   > Você pode examinar o código Olá que acessa o tooquery de back-end do aplicativo móvel e inserir dados, que são encontrados no hello arquivo ToDoActivity.cs c#.
   >
   >

## <a name="next-steps"></a>Próximas etapas
* [Adicionar aplicativo de tooyour sincronização Offline](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Adicionar autenticação tooyour aplicativo](app-service-mobile-xamarin-android-get-started-users.md)
* [Adicionar aplicativo de xamarin de tooyour de notificações por push](app-service-mobile-xamarin-android-get-started-push.md)
* [Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
