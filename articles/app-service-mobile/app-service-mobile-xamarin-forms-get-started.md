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
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="beba7-103">Criar um aplicativo Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="beba7-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="beba7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="beba7-104">Overview</span></span>
<span data-ttu-id="beba7-105">Este tutorial mostra como tooadd um aplicativo baseado em nuvem serviço de back-end tooa xamarin. Forms móvel usando Olá recurso de aplicativos móveis do serviço de aplicativo do Azure como back-end hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="beba7-106">Você cria um novo back-end do Aplicativo Móvel e um aplicativo de lista de tarefas pendentes Xamarin.Forms que armazena dados do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="beba7-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="beba7-107">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para o Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="beba7-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="beba7-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="beba7-108">Prerequisites</span></span>
<span data-ttu-id="beba7-109">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="beba7-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="beba7-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="beba7-110">An active Azure account.</span></span> <span data-ttu-id="beba7-111">Se você não tiver uma conta, você pode inscrever-se para uma avaliação do Azure e obter o too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação.</span><span class="sxs-lookup"><span data-stu-id="beba7-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="beba7-112">Para saber mais, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="beba7-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="beba7-113">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="beba7-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="beba7-114">Para obter informações, consulte Olá [definido para cima e instalar o Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="beba7-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="beba7-115">Um Mac com Xcode v7.0 ou posterior e o Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="beba7-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="beba7-116">Para saber mais, confira [Configurar e instalar o Visual Studio e o Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurar, instalar e verificar para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="beba7-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="beba7-117">Criar um novo back-end de Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="beba7-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="beba7-118">toocreate terminar de volta um novos aplicativos móveis, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="beba7-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="beba7-119">Você já configurou um back-end de Aplicativos Móveis que os aplicativos clientes móveis podem usar.</span><span class="sxs-lookup"><span data-stu-id="beba7-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="beba7-120">Em seguida, você pode baixar um projeto de servidor para um simples tarefas lista back-end e, em seguida, publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="beba7-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="beba7-121">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="beba7-121">Configure hello server project</span></span>

<span data-ttu-id="beba7-122">toouse de projeto de servidor tooconfigure Olá Olá back-end node. js ou .NET, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="beba7-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="beba7-123">Baixe e execute a solução de xamarin. Forms Olá</span><span class="sxs-lookup"><span data-stu-id="beba7-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="beba7-124">Você pode baixar a solução de saudação de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="beba7-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="beba7-125">Baixá-lo tooa Mac e abri-lo no Xamarin Studio, ou baixe-o computador com Windows tooa e abra-o no Visual Studio usando um Mac em rede para a criação de aplicativo do iOS hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="beba7-126">Para saber mais, confira a página [Configurar e instalar o Visual Studio e o Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="beba7-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="beba7-127">Em um computador Mac ou Windows, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="beba7-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="beba7-128">Vá toohello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="beba7-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="beba7-129">Em Olá **configurações** folha para seu aplicativo móvel, em **Mobile**, selecione **começar** > **xamarin. Forms**.</span><span class="sxs-lookup"><span data-stu-id="beba7-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="beba7-130">Na **etapa 3**, selecione **Criar um novo aplicativo**e selecione **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="beba7-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="beba7-131">Essa ação baixa um projeto que contém um aplicativo cliente que é o aplicativo móvel tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="beba7-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="beba7-132">Salvar o computador local do hello projeto compactado arquivo tooyour e anote onde você salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="beba7-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="beba7-133">Extraia Olá projeto que você baixou e abra-o no Visual Studio (Windows) ou no Xamarin Studio (Mac).</span><span class="sxs-lookup"><span data-stu-id="beba7-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Projeto extraído no Xamarin Studio][9]

   ![Projeto extraído no Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="beba7-136">(Opcional) Execute o projeto do iOS Olá</span><span class="sxs-lookup"><span data-stu-id="beba7-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="beba7-137">Nesta seção, você executar o projeto do hello Xamarin iOS para dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="beba7-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="beba7-138">Você poderá ignorá-la se não estiver trabalhando com dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="beba7-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="beba7-139">No Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="beba7-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="beba7-140">Clique com botão direito Olá iOS e, em seguida, selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="beba7-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="beba7-141">Em Olá **executar** menu, selecione **iniciar depuração** toobuild Olá projeto e iniciar o aplicativo hello no emulador do iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="beba7-142">No Visual Studio</span><span class="sxs-lookup"><span data-stu-id="beba7-142">In Visual Studio</span></span>
1. <span data-ttu-id="beba7-143">Clique com botão direito Olá iOS e, em seguida, selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="beba7-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="beba7-144">Em Olá **criar** menu, selecione **do Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="beba7-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="beba7-145">Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próximo toohello iOS projeto.</span><span class="sxs-lookup"><span data-stu-id="beba7-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="beba7-146">toobuild Olá projeto e iniciar o aplicativo hello no emulador do iPhone hello, selecione Olá **F5** chave.</span><span class="sxs-lookup"><span data-stu-id="beba7-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="beba7-147">Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="beba7-148">Projetos de início rápido podem ser lento tooupdate toohello últimas versões.</span><span class="sxs-lookup"><span data-stu-id="beba7-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="beba7-149">No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="beba7-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="beba7-150">Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="beba7-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="beba7-151">Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="beba7-152">Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="beba7-153">Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.</span><span class="sxs-lookup"><span data-stu-id="beba7-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="beba7-154">(Opcional) Execute o projeto Android Olá</span><span class="sxs-lookup"><span data-stu-id="beba7-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="beba7-155">Nesta seção, você executar o projeto de droid Xamarin Olá para Android.</span><span class="sxs-lookup"><span data-stu-id="beba7-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="beba7-156">Você poderá ignorá-la se não estiver trabalhando com dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="beba7-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="beba7-157">No Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="beba7-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="beba7-158">Projeto Android hello e, em seguida, selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="beba7-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="beba7-159">toobuild Olá projeto e iniciar o aplicativo hello em um emulador Android, no hello **executar** menu, selecione **iniciar depuração**.</span><span class="sxs-lookup"><span data-stu-id="beba7-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="beba7-160">No Visual Studio</span><span class="sxs-lookup"><span data-stu-id="beba7-160">In Visual Studio</span></span>

1. <span data-ttu-id="beba7-161">Clique com botão direito Olá Android (Droid) e, em seguida, selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="beba7-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="beba7-162">Em Olá **criar** menu, selecione **do Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="beba7-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="beba7-163">Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próxima toohello Android do projeto.</span><span class="sxs-lookup"><span data-stu-id="beba7-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="beba7-164">toobuild Olá projeto e iniciar o aplicativo hello em um emulador Android, selecione Olá **F5** chave.</span><span class="sxs-lookup"><span data-stu-id="beba7-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="beba7-165">Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="beba7-166">Projetos de início rápido podem ser lento tooupdate toohello últimas versões.</span><span class="sxs-lookup"><span data-stu-id="beba7-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="beba7-167">No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="beba7-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="beba7-168">Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="beba7-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="beba7-169">Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="beba7-170">Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="beba7-171">Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.</span><span class="sxs-lookup"><span data-stu-id="beba7-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="beba7-172">(Opcional) Execute o projeto do Windows hello</span><span class="sxs-lookup"><span data-stu-id="beba7-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="beba7-173">Nesta seção, você deve executar Olá Xamarin WinApp projeto para dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="beba7-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="beba7-174">Você poderá ignorá-la se não estiver trabalhando com dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="beba7-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="beba7-175">No Visual Studio</span><span class="sxs-lookup"><span data-stu-id="beba7-175">In Visual Studio</span></span>

1. <span data-ttu-id="beba7-176">Qualquer um dos projetos do Windows hello e, em seguida, selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="beba7-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="beba7-177">Em Olá **criar** menu, selecione **do Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="beba7-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="beba7-178">Em Olá **do Configuration Manager** caixa de diálogo, selecione Olá **criar** e **implantar** caixas de seleção próxima toohello projeto do Windows que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="beba7-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="beba7-179">toobuild Olá projeto e iniciar o aplicativo hello em um emulador do Windows, selecione Olá **F5** chave.</span><span class="sxs-lookup"><span data-stu-id="beba7-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="beba7-180">Se você tiver problemas de compilação de projeto hello, execute Olá Gerenciador e atualização toohello mais recente versão do pacote NuGet de pacotes de suporte de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="beba7-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="beba7-181">Projetos de início rápido podem ser lento tooupdate toohello últimas versões.</span><span class="sxs-lookup"><span data-stu-id="beba7-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="beba7-182">No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*, e, em seguida, selecione Olá sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="beba7-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="beba7-183">Essa ação envia um toohello de solicitação post que novos aplicativos móveis back-end que está hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="beba7-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="beba7-184">Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="beba7-185">Itens que são armazenados na tabela de saudação são retornados por Olá novamente os aplicativos móveis terminar e Olá dados são exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="beba7-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="beba7-186">Você encontrará o código de saudação que acessa seu back-end de aplicativos móveis no hello TodoItemManager.cs C# arquivo de projeto de biblioteca de classes portátil Olá de sua solução.</span><span class="sxs-lookup"><span data-stu-id="beba7-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="beba7-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="beba7-187">Next steps</span></span>

* [<span data-ttu-id="beba7-188">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="beba7-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="beba7-189">Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="beba7-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="beba7-190">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="beba7-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="beba7-191">Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seus aplicativos móveis back-end toouse Hubs de notificação do Azure toosend Olá envio notificações por.</span><span class="sxs-lookup"><span data-stu-id="beba7-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="beba7-192">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="beba7-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="beba7-193">Saiba como tooadd de suporte off-line para seu aplicativo usando um aplicativos móveis do back-end.</span><span class="sxs-lookup"><span data-stu-id="beba7-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="beba7-194">Com a sincronização offline, você pode exibir, adicionar ou modificar os dados do aplicativo móvel mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="beba7-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="beba7-195">Use o cliente gerenciado Olá para aplicativos móveis</span><span class="sxs-lookup"><span data-stu-id="beba7-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="beba7-196">Saiba como toowork com hello gerenciada SDK de cliente em seu aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="beba7-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

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
