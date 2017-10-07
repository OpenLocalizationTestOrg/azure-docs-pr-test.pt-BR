---
title: "aaaGet Olá a mesma experiência do Office 365 em qualquer dispositivo com o Azure RemoteApp | Microsoft Docs"
description: "Saiba como tooshare qualquer aplicativo do Office 365 com seus usuários usando o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="c7a47-103">Get hello a mesma experiência do Office 365 em qualquer dispositivo com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c7a47-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c7a47-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="c7a47-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c7a47-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c7a47-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c7a47-106">Este artigo abordará como toodeploy Office 365 em qualquer dispositivo em sua empresa.</span><span class="sxs-lookup"><span data-stu-id="c7a47-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="c7a47-107">Os usuários podem obter Olá mesmos recursos e experiência de interface do usuário no Android, Apple e no Windows.</span><span class="sxs-lookup"><span data-stu-id="c7a47-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="c7a47-108">Faremos isso usando o RemoteApp do Azure hospedando o Office 365 em máquinas virtuais com capacidade de dimensionamento no Azure, às quais os usuários possam se conectar.</span><span class="sxs-lookup"><span data-stu-id="c7a47-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="c7a47-109">Chamamos esse conjunto de máquinas virtuais de uma “coleção nuvem”.</span><span class="sxs-lookup"><span data-stu-id="c7a47-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="c7a47-110">Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="c7a47-110">Create a cloud collection</span></span>
<span data-ttu-id="c7a47-111">Navega pela primeira vez depois de criar uma conta do Azure, muito**RemoteApp** clicando no link Olá no lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a47-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="c7a47-112">![Mostrando o Azure RemoteApp em Olá Portal do Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="c7a47-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="c7a47-113">Continue clicando em **novo** inferior hello e "Criando rápida" uma coleção.</span><span class="sxs-lookup"><span data-stu-id="c7a47-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="c7a47-114">Forneça um nome, região hello, assinatura hello, plano hello e imagem hello "Proffesional do Office 2013" que fornecemos.</span><span class="sxs-lookup"><span data-stu-id="c7a47-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="c7a47-115">![Caixa de diálogo Criar](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="c7a47-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="c7a47-116">Depois de concluir o processo de criação de coleção do hello formulário Olá deve começar.</span><span class="sxs-lookup"><span data-stu-id="c7a47-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="c7a47-117">Isso pode levar horas tooan mais ou menos.</span><span class="sxs-lookup"><span data-stu-id="c7a47-117">This may take up tooan hour or so.</span></span>

![Aguardando](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="c7a47-119">Depois de processo hello, terá aparência semelhante a esta.</span><span class="sxs-lookup"><span data-stu-id="c7a47-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="c7a47-120">Se clicarmos em **Publicação** , podemos ver que a maioria dos aplicativos do Office já foram publicados para nós.</span><span class="sxs-lookup"><span data-stu-id="c7a47-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="c7a47-121">![Coleção criada](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="c7a47-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Aplicativos publicados](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="c7a47-123">Agora você também pode adicionar mais usuários que têm acesso toothis coleção clicando **acesso de usuário**.</span><span class="sxs-lookup"><span data-stu-id="c7a47-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="c7a47-124">![Configurar o acesso do usuário](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="c7a47-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="c7a47-125">Agora vamos testar conexão tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="c7a47-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="c7a47-126">Conecte-se tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="c7a47-126">Connect tooOffice 365</span></span>
<span data-ttu-id="c7a47-127">Podemos entrará em muito[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), role para baixo e clique em **baixar clientes** tooinstall cliente de Azure RemoteApp Olá no dispositivo Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="c7a47-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="c7a47-128">Olá capturas de tela abaixo são para Windows.</span><span class="sxs-lookup"><span data-stu-id="c7a47-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="c7a47-129">Depois que o aplicativo hello inicia deverá toosign com sua conta da Microsoft (anteriormente chamada de "Live ID"), use Olá mesmo que sua conta do Azure agora.</span><span class="sxs-lookup"><span data-stu-id="c7a47-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="c7a47-130">Quando você tiver feito logon, você deve receber uma notificação sobre novos convites, clique nos mesmos e você deve ver uma lista como a mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="c7a47-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="c7a47-131">Aceite o convite de saudação que corresponde a seu email do proprietário de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a47-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Novo convite](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="c7a47-133">Abaixo, sua aparência quando há novos convites.</span><span class="sxs-lookup"><span data-stu-id="c7a47-133">What it looks like when there are new invitations.</span></span>

![Aceite um aplicativo](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="c7a47-135">Depois de aceitar o convite hello, você deve ver todos os aplicativos do Office Olá no cliente do Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="c7a47-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Lista de aplicativos](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="c7a47-137">Quando você clicar em qualquer um desses aplicativos, Olá deve começar em Olá máquina virtual do Azure e devem ser definidos!</span><span class="sxs-lookup"><span data-stu-id="c7a47-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="c7a47-138">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="c7a47-138">Enjoy!</span></span>

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

