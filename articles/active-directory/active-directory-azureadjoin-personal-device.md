---
title: "Ingressar em um dispositivo pessoal para sua organização| Microsoft Docs"
description: "Explica como os usuários podem registrar seus dispositivos Windows 10 pessoais em sua rede corporativa e fornece as etapas de implantação para um cenário BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="a2374-103">Ingressar em um dispositivo pessoal para sua organização</span><span class="sxs-lookup"><span data-stu-id="a2374-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="a2374-104">Para ingressar em um dispositivo Windows 10 para sua organização</span><span class="sxs-lookup"><span data-stu-id="a2374-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="a2374-105">No menu **Iniciar**, selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a2374-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="a2374-106">Selecione **Contas** e, em seguida, clique em **Sua conta**.</span><span class="sxs-lookup"><span data-stu-id="a2374-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="a2374-107">Clique em **Adicionar conta corporativa ou de estudante**e, em seguida, digite sua conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="a2374-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="a2374-108">Na página de credenciais da sua organização, insira seu nome de usuário e senha e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2374-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="a2374-109">Um desafio de Multi-Factor Authentication será apresentado a você.</span><span class="sxs-lookup"><span data-stu-id="a2374-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="a2374-110">(Esse desafio é configurável por um administrador de TI.)</span><span class="sxs-lookup"><span data-stu-id="a2374-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="a2374-111">O Azure Active Directory (Azure AD) verifica se o dispositivo requer o registro de gerenciamento de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="a2374-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="a2374-112">O Windows registra o dispositivo no diretório da organização no Azure AD e no gerenciamento de dispositivo móvel, se apropriado.</span><span class="sxs-lookup"><span data-stu-id="a2374-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="a2374-113">Se você for um usuário gerenciado, o Windows levará para a área de trabalho por meio da conexão automático.</span><span class="sxs-lookup"><span data-stu-id="a2374-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="a2374-114">Se você for um usuário federado, você será levado para a tela de logon do Windows para inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="a2374-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="a2374-115">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="a2374-115">Additional information</span></span>
* [<span data-ttu-id="a2374-116">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="a2374-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a2374-117">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a2374-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a2374-118">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="a2374-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="a2374-119">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2374-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a2374-120">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="a2374-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a2374-121">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2374-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

