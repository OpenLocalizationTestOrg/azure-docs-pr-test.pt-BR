---
title: "Obtenha a mesma experiência do Office 365 em qualquer dispositivo com Azure RemoteApp | Microsoft Docs"
description: "Aprenda a compartilhar qualquer aplicativo de Office 365 com os usuários usando o RemoteApp do Azure."
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
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="6b2ba-103">Obter a mesma experiência de Office 365 em qualquer dispositivo com RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="6b2ba-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6b2ba-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6b2ba-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6b2ba-106">Este artigo abordará como implantar o Office 365 em qualquer dispositivo em sua empresa.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="6b2ba-107">Os usuários possam obter as mesmas capacidades e a experiência de interface de usuário em Android, Apple e Windows.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="6b2ba-108">Faremos isso usando o RemoteApp do Azure hospedando o Office 365 em máquinas virtuais com capacidade de dimensionamento no Azure, às quais os usuários possam se conectar.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="6b2ba-109">Chamamos esse conjunto de máquinas virtuais de uma “coleção nuvem”.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="6b2ba-110">Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="6b2ba-110">Create a cloud collection</span></span>
<span data-ttu-id="6b2ba-111">Pela primeira vez depois de criar uma conta do Azure, navegue até **RemoteApp** clicando no link no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="6b2ba-112">![Mostrando o Azure RemoteApp no Portal do Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="6b2ba-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="6b2ba-113">Depois, prossiga clicando em **novo** na parte inferior e fazendo a "criação rápida" de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="6b2ba-114">Forneça um nome, região, assinatura, plano e imagem "Office Professional 2013" que fornecemos.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="6b2ba-115">![Caixa de diálogo Criar](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="6b2ba-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="6b2ba-116">Depois de você concluir o formulário, o processo de criação de coleção deve começar.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="6b2ba-117">Isso pode levar até uma hora ou mais.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-117">This may take up to an hour or so.</span></span>

![Aguardando](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="6b2ba-119">Depois que o processo for concluído, ele terá a aparência a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="6b2ba-120">Se clicarmos em **Publicação** , podemos ver que a maioria dos aplicativos do Office já foram publicados para nós.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="6b2ba-121">![Coleção criada](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="6b2ba-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Aplicativos publicados](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="6b2ba-123">Nesse ponto você também pode adicionar mais usuários que têm acesso a esta coleção, clicando em **Acesso de usuário**.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="6b2ba-124">![Configurar o acesso do usuário](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="6b2ba-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="6b2ba-125">Agora vamos experimentar conectar ao Office 365!</span><span class="sxs-lookup"><span data-stu-id="6b2ba-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="6b2ba-126">Conectar ao Office 365</span><span class="sxs-lookup"><span data-stu-id="6b2ba-126">Connect to Office 365</span></span>
<span data-ttu-id="6b2ba-127">Vamos acessar [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), rolar para baixo e clicar em **Baixar clientes** para instalar o cliente do Azure RemoteApp no dispositivo no qual você está.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="6b2ba-128">As capturas de tela abaixo são para o Windows.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="6b2ba-129">Depois que o aplicativo for iniciado, você será solicitado a entrar com a conta da Microsoft (chamada anteriormente de “Live ID”), insira a mesma usada na sua conta do Azure por enquanto.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="6b2ba-130">Quando você tiver feito logon, você deve receber uma notificação sobre novos convites, clique nos mesmos e você deve ver uma lista como a mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="6b2ba-131">Aceite o convite que corresponde ao seu e-mail de proprietário de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-131">Accept the invitation that matches your Azure account owner email.</span></span>

![Novo convite](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="6b2ba-133">Abaixo, sua aparência quando há novos convites.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-133">What it looks like when there are new invitations.</span></span>

![Aceite um aplicativo](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="6b2ba-135">Depois de aceitar o convite, você deve ver todos os aplicativos do Office no cliente do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2ba-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![Lista de aplicativos](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="6b2ba-137">Quando você clica em qualquer um desses, o aplicativo deve ser iniciado na máquina virtual do Azure e você deve estar com tudo pronto!</span><span class="sxs-lookup"><span data-stu-id="6b2ba-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="6b2ba-138">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="6b2ba-138">Enjoy!</span></span>

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

