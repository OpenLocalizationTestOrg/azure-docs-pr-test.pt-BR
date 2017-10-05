---
title: Configurar um dispositivo Windows 10 com o Azure AD de Settings| Microsoft Docs
description: "Explica como os usuários podem unir-se ao Azure AD por meio do menu Configurações."
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="89020-103">Configurar um dispositivo Windows 10 com o Azure AD nas Configurações</span><span class="sxs-lookup"><span data-stu-id="89020-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="89020-104">Se já estiver usando o Windows 7 ou Windows 8 e o computador ou dispositivo tiver sido atualizado para o Windows 10, você poderá uni-lo ao Azure AD (Azure Active Directory) por meio do menu Configurações.</span><span class="sxs-lookup"><span data-stu-id="89020-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="89020-105">Para realizar a junção ao Azure AD no menu Configurações</span><span class="sxs-lookup"><span data-stu-id="89020-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="89020-106">No menu **Iniciar**, clique no botão **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="89020-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="89020-107">Em **Configurações**, escolha    **Sistema**->**Sobre**->**Ingressar no Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="89020-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="89020-108"><center>
   ![Ingressar no Azure AD no menu Configurações](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="89020-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="89020-109">Clique em **Continuar** na janela de mensagem da Junção do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89020-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="89020-110"><center>
   ![Janela de mensagem de ingresso no Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="89020-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="89020-111">Forneça suas credenciais de entrada.</span><span class="sxs-lookup"><span data-stu-id="89020-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="89020-112">Esta experiência de entrada incluirá todas as etapas necessárias concluir a autenticação.</span><span class="sxs-lookup"><span data-stu-id="89020-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="89020-113">Se você fizer parte de um locatário federado, seu administrador fornecerá uma experiência de federação hospedado pela sua organização.</span><span class="sxs-lookup"><span data-stu-id="89020-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="89020-114"><center>
   ![Fornecer suas credenciais de entrada](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="89020-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="89020-115">Se a sua organização tiver configurado a Azure Multi-Factor Authentication para unir-se ao Azure AD, forneça o segundo fator para continuar.</span><span class="sxs-lookup"><span data-stu-id="89020-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="89020-116">Clique em **Aceitar** na tela **Permitir que este dispositivo seja gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="89020-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="89020-117">Você deverá ver a mensagem "O dispositivo agora faz parte de sua organização no Azure AD".</span><span class="sxs-lookup"><span data-stu-id="89020-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="89020-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="89020-118">Additional information</span></span>
* [<span data-ttu-id="89020-119">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="89020-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="89020-120">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="89020-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="89020-121">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="89020-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="89020-122">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="89020-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

