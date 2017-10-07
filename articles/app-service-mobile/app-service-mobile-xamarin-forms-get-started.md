---
title: "aaaGet iniciada com aplicativos móveis usando o xamarin. Forms"
description: "Siga este tutorial toostart usando aplicativos móveis para o desenvolvimento do xamarin. Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Criar um aplicativo Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como tooadd um aplicativo baseado em nuvem serviço de back-end tooa xamarin. Forms móvel usando Olá recurso de aplicativos móveis do serviço de aplicativo do Azure como back-end hello. Você cria um novo back-end do Aplicativo Móvel e um aplicativo de lista de tarefas pendentes Xamarin.Forms que armazena dados do aplicativo no Azure.

A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para o Xamarin.Forms.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se você não tiver uma conta, você pode inscrever-se para uma avaliação do Azure e obter o too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação. Para saber mais, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio com Xamarin. Para obter informações, consulte Olá [definido para cima e instalar o Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) página.

* Um Mac com Xcode v7.0 ou posterior e o Xamarin Studio Community instalados. Para saber mais, confira [Configurar e instalar o Visual Studio e o Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurar, instalar e verificar para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Criar um novo back-end de Aplicativos Móveis

toocreate terminar de volta um novos aplicativos móveis, Olá a seguir:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Você já configurou um back-end de Aplicativos Móveis que os aplicativos clientes móveis podem usar. Em seguida, você pode baixar um projeto de servidor para um simples tarefas lista back-end e, em seguida, publicá-lo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar o projeto do servidor de saudação

toouse de projeto de servidor tooconfigure Olá Olá back-end node. js ou .NET, Olá a seguir:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Baixe e execute a solução de xamarin. Forms Olá

Você pode baixar a solução de saudação de duas maneiras. Baixá-lo tooa Mac e abri-lo no Xamarin Studio, ou baixe-o computador com Windows tooa e abra-o no Visual Studio usando um Mac em rede para a criação de aplicativo do iOS hello. Para saber mais, confira a página [Configurar e instalar o Visual Studio e o Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

Em um computador Mac ou Windows, Olá a seguir:

1. Vá toohello [portal do Azure].

2. Em Olá **configurações** folha para seu aplicativo móvel, em **Mobile**, selecione **começar** > **xamarin. Forms**. Na **etapa 3**, selecione **Criar um novo aplicativo**e selecione **Baixar**.

   Essa ação baixa um projeto que contém um aplicativo cliente que é o aplicativo móvel tooyour conectado. Salvar o computador local do hello projeto compactado arquivo tooyour e anote onde você salvá-lo.

3. Extraia Olá projeto que você baixou e abra-o no Visual Studio (Windows) ou no Xamarin Studio (Mac).

   ![Projeto extraído no Xamarin Studio][9]

   ![Projeto extraído no Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Opcional) Execute o projeto do iOS Olá
Nesta seção, você executar o projeto do hello Xamarin iOS para dispositivos iOS. Você poderá ignorá-la se não estiver trabalhando com dispositivos iOS.

#### <a name="in-xamarin-studio"></a>No Xamarin Studio
1. Clique com botão direito Olá iOS e, em seguida, selecione **definir como projeto de inicialização**.

2. Em Olá **executar** menu, selecione **iniciar depuração** toobuild Olá projeto e iniciar o aplicativo hello no emulador do iPhone hello.

#### <a name="in-visual-studio"></a>No Visual Studio
1. Clique com botão direito Olá iOS e, em seguida, selecione **definir como projeto de inicialização**.

2. Em Olá **criar** menu, selecione **do Configuration Manager**.

3. Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próximo toohello iOS projeto.

4. toobuild Olá projeto e iniciar o aplicativo hello no emulador do iPhone hello, selecione Olá **F5** chave.

   > [!NOTE]
   > Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello. Projetos de início rápido podem ser lento tooupdate toohello últimas versões.    
   >
   >

5. No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).

    ![][10]

    Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure. Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação. Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.

    > [!NOTE]
    > Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Opcional) Execute o projeto Android Olá
Nesta seção, você executar o projeto de droid Xamarin Olá para Android. Você poderá ignorá-la se não estiver trabalhando com dispositivos Android.

#### <a name="in-xamarin-studio"></a>No Xamarin Studio

1. Projeto Android hello e, em seguida, selecione **definir como projeto de inicialização**.

2. toobuild Olá projeto e iniciar o aplicativo hello em um emulador Android, no hello **executar** menu, selecione **iniciar depuração**.

#### <a name="in-visual-studio"></a>No Visual Studio

1. Clique com botão direito Olá Android (Droid) e, em seguida, selecione **definir como projeto de inicialização**.

2. Em Olá **criar** menu, selecione **do Configuration Manager**.

3. Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próxima toohello Android do projeto.

4. toobuild Olá projeto e iniciar o aplicativo hello em um emulador Android, selecione Olá **F5** chave.

   > [!NOTE]
   > Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello. Projetos de início rápido podem ser lento tooupdate toohello últimas versões.    
   >
   >

5. No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).

    ![][11]
    
    Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure. Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação. Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.
    
    > [!NOTE]
    > Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Opcional) Execute o projeto do Windows hello

Nesta seção, você deve executar Olá Xamarin WinApp projeto para dispositivos Windows. Você poderá ignorá-la se não estiver trabalhando com dispositivos Windows.

#### <a name="in-visual-studio"></a>No Visual Studio

1. Qualquer um dos projetos do Windows hello e, em seguida, selecione **definir como projeto de inicialização**.

2. Em Olá **criar** menu, selecione **do Configuration Manager**.

3. Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próxima toohello projeto do Windows que você escolheu.

4. toobuild Olá projeto e iniciar o aplicativo hello em um emulador do Windows, selecione Olá **F5** chave.

   > [!NOTE]
   > Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello. Projetos de início rápido podem ser lento tooupdate toohello últimas versões.    
   >
   >

5. No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).

    Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure. Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação. Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.
    
    ![][12]
    
    > [!NOTE]
    > Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.
    >
    >

## <a name="next-steps"></a>Próximas etapas

* [Adicionar autenticação tooyour aplicativo](app-service-mobile-xamarin-forms-get-started-users.md)  
  Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.

* [Adicionar aplicativo de tooyour de notificações por push](app-service-mobile-xamarin-forms-get-started-push.md)  
  Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seus aplicativos móveis back-end toouse Hubs de notificação do Azure toosend Olá envio notificações por.

* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Saiba como tooadd de suporte off-line para seu aplicativo usando um aplicativos móveis do back-end. Com a sincronização offline, você pode exibir, adicionar ou modificar os dados do aplicativo móvel mesmo quando não há nenhuma conexão de rede.

* [Use o cliente gerenciado Olá para aplicativos móveis](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Saiba como toowork com hello gerenciada SDK de cliente em seu aplicativo Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portal do Azure]: https://portal.azure.com/
