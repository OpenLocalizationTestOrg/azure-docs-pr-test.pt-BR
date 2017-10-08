---
title: "aaaGet iniciado com aplicativos de celular do serviço de aplicativo do Azure para aplicativos xamarin | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de aplicativos móveis para o desenvolvimento do xamarin."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Criar um aplicativo Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como tooadd um back-end baseado em nuvem serviço aplicativo móvel do xamarin tooa usando um back-end do aplicativo móvel do Azure.  Você cria um novo back-end do aplicativo móvel e um aplicativo Xamarin.iOS *Todo list* simples que armazena dados de aplicativo no Azure.

Concluir este tutorial é um pré-requisito para todos os outros tutoriais do xamarin sobre como usar o recurso de aplicativos móveis Olá no serviço de aplicativo do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* Uma conta ativa do Azure. Se você não tiver uma conta, inscreva-se para uma avaliação do Azure e começar a too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio com Xamarin. Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).
* Um Mac com Xcode v7.0 ou posterior e o Xamarin Studio Community instalados. Veja [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configuração, instalação e verificações para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end de aplicativo móvel do Azure
Siga essas etapas toocreate um back-end do aplicativo móvel.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurar o projeto do servidor de saudação
Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes. Em seguida, baixar um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.

Siga Olá seguindo as etapas tooconfigure Olá servidor projeto toouse ou Olá Node. js ou .NET back-end.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Baixe e execute o aplicativo de xamarin Olá
1. Olá abrir [portal do Azure] em uma janela do navegador.
2. Na folha de configurações de saudação para seu aplicativo móvel, clique em **começar** > **xamarin**. Na etapa 3, clique em **Criar um novo aplicativo** se essa opção ainda não tiver sido selecionada.  Em seguida clique Olá **baixar** botão.

      Um aplicativo cliente que se conecta de back-end do tooyour móvel é baixado. Salve o arquivo de projeto compactado de saudação em seu computador local e anote onde você salvá-lo.
3. Extraia o projeto Olá que você baixou e abra-o no Xamarin Studio (ou o Visual Studio).

    ![][9]

    ![][8]
4. Pressione projeto de Olá Olá F5 toobuild chave e iniciar o aplicativo hello no emulador do iPhone hello.
5. No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*e, em seguida, clique em Olá  **+**  botão.

    ![][10]

    Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação. Itens armazenados na tabela de saudação são retornados pelo back-end de aplicativo móvel hello e os dados são exibidos na lista de saudação.

> [!NOTE]
> Você pode examinar o código Olá que acessa o tooquery de back-end do aplicativo móvel e inserir dados em Olá arquivo QSTodoService.cs c#.
>
>

## <a name="next-steps"></a>Próximas etapas
* [Adicionar aplicativo de tooyour sincronização Offline](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Adicionar autenticação tooyour aplicativo](app-service-mobile-xamarin-ios-get-started-users.md)
* [Adicionar aplicativo de xamarin de tooyour de notificações por push](app-service-mobile-xamarin-ios-get-started-push.md)
* [Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portal do Azure]: https://portal.azure.com/
