---
title: "aaaSet um dispositivo Windows 10 com o Azure AD de configurações | Microsoft Docs"
description: "Explica como os usuários podem ingressar tooAzure AD por meio do menu de configurações de saudação."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="87241-103">Configurar um dispositivo Windows 10 com o Azure AD nas Configurações</span><span class="sxs-lookup"><span data-stu-id="87241-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="87241-104">Se você já estiver usar o Windows 7 ou Windows 8 e seu computador ou dispositivo foi atualizado tooWindows 10, você pode ingressar em tooAzure do Active Directory (AD do Azure) por meio do menu de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="87241-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="87241-105">toojoin tooAzure AD no menu de configurações de saudação</span><span class="sxs-lookup"><span data-stu-id="87241-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="87241-106">De saudação **iniciar** menu, clique em Olá **configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="87241-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="87241-107">Em **Configurações**, escolha    **Sistema**->**Sobre**->**Ingressar no Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="87241-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="87241-108"><center>
   ![Ingressar no menu de configurações de saudação do AD do Azure](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="87241-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="87241-109">Clique em **continuar** na janela de mensagem de junção do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="87241-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="87241-110"><center>
   ![Janela de mensagem de ingresso no Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="87241-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="87241-111">Forneça suas credenciais de entrada.</span><span class="sxs-lookup"><span data-stu-id="87241-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="87241-112">Essa experiência de logon incluirá todas as etapas de saudação toocomplete necessária autenticação.</span><span class="sxs-lookup"><span data-stu-id="87241-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="87241-113">Se você fizer parte de um locatário federado, o administrador fornecerá experiência de Federação Olá que é hospedada pela sua organização.</span><span class="sxs-lookup"><span data-stu-id="87241-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="87241-114"><center>
   ![Fornecer suas credenciais de entrada](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="87241-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="87241-115">Se sua organização tiver configurado o Azure multi-Factor Authentication para ingresso tooAzure AD, forneça o segundo fator Olá antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="87241-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="87241-116">Clique em **aceitar** em Olá **permitir esta toobe dispositivo gerenciado** tela.</span><span class="sxs-lookup"><span data-stu-id="87241-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="87241-117">Você deve ver a mensagem de saudação "o dispositivo agora está unido tooyour organização no AD do Azure".</span><span class="sxs-lookup"><span data-stu-id="87241-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="87241-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="87241-118">Additional information</span></span>
* [<span data-ttu-id="87241-119">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="87241-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="87241-120">Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="87241-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="87241-121">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="87241-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="87241-122">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="87241-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

