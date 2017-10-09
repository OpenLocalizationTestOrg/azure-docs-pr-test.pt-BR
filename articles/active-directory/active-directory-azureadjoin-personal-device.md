---
title: "aaaJoin uma organização de tooyour dispositivo pessoal | Microsoft Docs"
description: "Explica como os usuários podem registrar suas redes corporativas pessoal do Windows 10 dispositivos tootheir e fornece as etapas de implantação para um cenário de BYOD."
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
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="27d4d-103">Ingressar em uma organização de tooyour dispositivo pessoal</span><span class="sxs-lookup"><span data-stu-id="27d4d-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="27d4d-104">organização de tooyour dispositivo toojoin um Windows 10</span><span class="sxs-lookup"><span data-stu-id="27d4d-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="27d4d-105">De saudação **iniciar** menu, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="27d4d-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="27d4d-106">Selecione **Contas** e, em seguida, clique em **Sua conta**.</span><span class="sxs-lookup"><span data-stu-id="27d4d-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="27d4d-107">Clique em **Adicionar conta corporativa ou de estudante**e, em seguida, digite sua conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="27d4d-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="27d4d-108">Na saudação página de entrada para a sua organização, insira seu nome de usuário e senha e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="27d4d-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="27d4d-109">Um desafio de Multi-Factor Authentication será apresentado a você.</span><span class="sxs-lookup"><span data-stu-id="27d4d-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="27d4d-110">(Esse desafio é configurável por um administrador de TI.)</span><span class="sxs-lookup"><span data-stu-id="27d4d-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="27d4d-111">Azure Active Directory (AD do Azure) verifica se o dispositivo Olá requer registro de gerenciamento de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="27d4d-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="27d4d-112">Windows registra o dispositivo Olá no diretório da organização Olá no AD do Azure e se registra no gerenciamento de dispositivos móveis, se apropriado.</span><span class="sxs-lookup"><span data-stu-id="27d4d-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="27d4d-113">Se você for um usuário gerenciado, o Windows usa toohello desktop por meio de entrada automática hello.</span><span class="sxs-lookup"><span data-stu-id="27d4d-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="27d4d-114">Se você for um usuário federado, você será levado tooa entrar no Windows tela tooenter suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="27d4d-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="27d4d-115">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="27d4d-115">Additional information</span></span>
* [<span data-ttu-id="27d4d-116">Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho</span><span class="sxs-lookup"><span data-stu-id="27d4d-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="27d4d-117">Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="27d4d-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="27d4d-118">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="27d4d-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="27d4d-119">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d4d-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="27d4d-120">Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="27d4d-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="27d4d-121">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d4d-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

