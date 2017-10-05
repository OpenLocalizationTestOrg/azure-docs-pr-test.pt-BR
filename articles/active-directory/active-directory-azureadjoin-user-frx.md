---
title: "Configurar um novo dispositivo com o Azure AD durante a Instalação | Microsoft Docs"
description: "Um tópico que explica como os usuários podem configurar a Junção do Azure AD durante sua experiência de primeira execução."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="c6721-103">Configurar um novo dispositivo com o AD do Azure durante a instalação</span><span class="sxs-lookup"><span data-stu-id="c6721-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="c6721-104">No Windows 10, os usuários podem ingressar seus dispositivos no Azure AD (Azure Active Directory) na FRX (tela de apresentação).</span><span class="sxs-lookup"><span data-stu-id="c6721-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="c6721-105">Isso permite que as organizações distribuam dispositivos reduzidos e encapsulados para seus funcionários ou alunos ou deixem que eles tenham uma experiência CYOD (escolha seus próprios dispositivos).</span><span class="sxs-lookup"><span data-stu-id="c6721-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="c6721-106">Se o Windows 10 Professional ou Windows 10 Enterprise Edition estiver instalado em um dispositivo, a experiência usará como padrão o processo de instalação de dispositivos de propriedade da empresa.</span><span class="sxs-lookup"><span data-stu-id="c6721-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="c6721-107">Para adicionar um dispositivo ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c6721-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="c6721-108">Ao ligar o novo dispositivo e iniciar o processo de instalação, você deverá ver a mensagem **Preparando-se** .</span><span class="sxs-lookup"><span data-stu-id="c6721-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="c6721-109">Siga os prompts para configurar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6721-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="c6721-110">Inicie personalizando a região e o idioma.</span><span class="sxs-lookup"><span data-stu-id="c6721-110">Start by customizing your region and language.</span></span> <span data-ttu-id="c6721-111">Em seguida, aceite os Termos de Licença para Software Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6721-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="c6721-112">![Personalizar a região](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="c6721-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="c6721-113">Selecione a rede que deseja usar para se conectar à Internet.</span><span class="sxs-lookup"><span data-stu-id="c6721-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="c6721-114">Selecione se está usando um dispositivo pessoal ou de propriedade da empresa.</span><span class="sxs-lookup"><span data-stu-id="c6721-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="c6721-115">Se ele for de propriedade da empresa, clique em **Este dispositivo pertence à minha organização**.</span><span class="sxs-lookup"><span data-stu-id="c6721-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="c6721-116">Isso inicia a experiência de junção do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6721-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="c6721-117">Apresentamos a seguir uma tela que será exibida se estiver usando o Windows 10 Professional.</span><span class="sxs-lookup"><span data-stu-id="c6721-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="c6721-118"><center>
   ![Tela Quem é o proprietário deste computador?](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="c6721-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="c6721-119">Insira as credenciais que foram fornecidas a você por sua organização.</span><span class="sxs-lookup"><span data-stu-id="c6721-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="c6721-120"><center>
   ![Tela de entrada](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="c6721-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="c6721-121">Depois de inserir seu nome de usuário, um locatário correspondente estará localizado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6721-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="c6721-122">Se estiver em um domínio federado, você será redirecionado para o servidor local do STS (Serviço de Token Seguro) – por exemplo, o AD FS (Serviços de Federação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c6721-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="c6721-123">Se você for um usuário em um domínio não federado, será necessário inserir suas credenciais diretamente na página hospedada pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6721-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="c6721-124">Você também verá o logotipo de sua organização e um texto de suporte se a identidade visual da empresa tiver sido configurada.</span><span class="sxs-lookup"><span data-stu-id="c6721-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="c6721-125">Um desafio da autenticação multifator será apresentado a você.</span><span class="sxs-lookup"><span data-stu-id="c6721-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="c6721-126">Esse desafio é configurável por um administrador de TI.</span><span class="sxs-lookup"><span data-stu-id="c6721-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="c6721-127">O Azure AD verifica se esse usuário/dispositivo exige registro no gerenciamento de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="c6721-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="c6721-128">O Windows registra o dispositivo no diretório da organização no Azure AD e no gerenciamento de dispositivo móvel, se apropriado.</span><span class="sxs-lookup"><span data-stu-id="c6721-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="c6721-129">Se você for um usuário gerenciado, o Windows o levará para a área de trabalho por meio do processo de entrada automática.</span><span class="sxs-lookup"><span data-stu-id="c6721-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="c6721-130">Se você for um usuário federado, será direcionado para a tela de entrada do Windows para inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="c6721-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="c6721-131">Não há suporte para o ingresso em um domínio local do Active Directory do Windows Server na tela de apresentação do Windows.</span><span class="sxs-lookup"><span data-stu-id="c6721-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="c6721-132">Portanto, se pretende adicionar um computador a um domínio, é necessário selecionar o link **Configurar o Windows com uma conta local** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="c6721-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="c6721-133">Em seguida, é possível ingressar no domínio através das configurações do computador, como você fez antes.</span><span class="sxs-lookup"><span data-stu-id="c6721-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="c6721-134">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="c6721-134">Additional information</span></span>
* [<span data-ttu-id="c6721-135">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="c6721-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="c6721-136">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c6721-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="c6721-137">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="c6721-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="c6721-138">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6721-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="c6721-139">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="c6721-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="c6721-140">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6721-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

