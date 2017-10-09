---
title: "aaaGet iniciado o Azure MFA na nuvem Olá | Microsoft Docs"
description: "Isso é página de autenticação do Microsoft Azure multi-Factor Olá que descreve como tooget iniciada com o Azure MFA na nuvem hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="a299c-103">Guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="a299c-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="a299c-104">Este artigo explica como tooget iniciado usando o Azure multi-Factor Authentication na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="a299c-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="a299c-105">Olá documentação a seguir fornece informações sobre como os usuários tooenable usando Olá **Portal clássico do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a299c-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="a299c-106">Se você estiver procurando informações sobre como tooset o Azure multi-Factor Authentication para usuários do O365, consulte [configurar autenticação multifator para Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="a299c-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA na nuvem de saudação](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="a299c-108">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="a299c-108">Prerequisite</span></span>
<span data-ttu-id="a299c-109">[Inscreva-se para uma assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/) -se você não tiver uma assinatura do Azure, você precisa toosign-up para um.</span><span class="sxs-lookup"><span data-stu-id="a299c-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="a299c-110">Se você estiver apenas começando a usar o Azure MFA, poderá usar uma assinatura de avaliação.</span><span class="sxs-lookup"><span data-stu-id="a299c-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="a299c-111">Habilitar a Autenticação Multifator do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a299c-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="a299c-112">Como os usuários tiverem licenças que incluem autenticação multifator do Azure, não há nada que você precisa tooturn toodo no Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="a299c-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="a299c-113">Você pode começar solicitando uma verificação em duas etapas em base de usuário individual.</span><span class="sxs-lookup"><span data-stu-id="a299c-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="a299c-114">Olá licenças que habilitar a MFA do Azure são:</span><span class="sxs-lookup"><span data-stu-id="a299c-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="a299c-115">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="a299c-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="a299c-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="a299c-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="a299c-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="a299c-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="a299c-118">Se você não tiver uma dessas três licenças, ou você não tem suficiente toocover licenças todos os usuários, que okey muito.</span><span class="sxs-lookup"><span data-stu-id="a299c-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="a299c-119">Você que toodo uma etapa extra e [criar um provedor de autenticação multifator](multi-factor-authentication-get-started-auth-provider.md) em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="a299c-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="a299c-120">Ativar a verificação em duas etapas para usuários</span><span class="sxs-lookup"><span data-stu-id="a299c-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="a299c-121">Use um dos procedimentos de saudação listados na [como verificacao toorequire para um usuário ou grupo](multi-factor-authentication-get-started-user-states.md) toostart usando o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="a299c-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="a299c-122">Você pode escolher tooenforce verificação de duas etapas para todas as entradas ou você pode criar a verificação de duas etapas de toorequire de políticas de acesso condicional somente quando é importante tooyou.</span><span class="sxs-lookup"><span data-stu-id="a299c-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a299c-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a299c-123">Next Steps</span></span>
<span data-ttu-id="a299c-124">Agora que você configurou o Azure multi-Factor Authentication na nuvem hello, você pode configurar e configurar sua implantação.</span><span class="sxs-lookup"><span data-stu-id="a299c-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="a299c-125">Confira [Configurr a autenticação multifator do Azure](multi-factor-authentication-whats-next.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a299c-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

