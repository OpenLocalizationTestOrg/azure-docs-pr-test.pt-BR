---
title: "Azure Active Directory B2C: criar um locatário do Azure Active Directory B2C | Microsoft Docs"
description: "Um tópico sobre como toocreate um B2C do Azure Active Directory de locatário"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="69076-103">Criar um locatário do Azure Active Directory B2C no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="69076-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="69076-104">Editado por Sipi.</span><span class="sxs-lookup"><span data-stu-id="69076-104">Edited by Sipi.</span></span>

<span data-ttu-id="69076-105">Este Guia de início rápido ajuda a criar um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="69076-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="69076-106">Quando você terminar, você tem um toouse de locatário B2C para registrar aplicativos B2C.</span><span class="sxs-lookup"><span data-stu-id="69076-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69076-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="69076-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="69076-108">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="69076-108">Log in tooAzure</span></span>

<span data-ttu-id="69076-109">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="69076-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="69076-110">Criar um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="69076-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="69076-111">Os recursos B2C não podem ser habilitados em seus locatários existentes.</span><span class="sxs-lookup"><span data-stu-id="69076-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="69076-112">É necessário toocreate um locatário Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="69076-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="69076-113">Parabéns, você criou um locatário do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="69076-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="69076-114">Você é um Administrador Global do locatário hello.</span><span class="sxs-lookup"><span data-stu-id="69076-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="69076-115">Você pode adicionar outros Administradores Globais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="69076-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="69076-116">tooswitch tooyour novo locatário, clique em Olá *gerenciar seu novo link de locatário*.</span><span class="sxs-lookup"><span data-stu-id="69076-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Gerenciar seu novo link de locatário](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="69076-118">Se você estiver planejando toouse um locatário B2C para um aplicativo de produção, leia o artigo de saudação em [escala de produção versus locatários visualização B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="69076-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="69076-119">Há conhecidos problemas quando você excluir um existente B2C do locatário e recriá-la com hello mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="69076-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="69076-120">É necessário toocreate um locatário B2C com um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="69076-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="69076-121">Vincular sua assinatura do locatário tooyour</span><span class="sxs-lookup"><span data-stu-id="69076-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="69076-122">Você precisa toolink seu B2C do AD do Azure locatário tooyour assinatura do Azure tooenable todas as funcionalidades de B2C e pagar pelos encargos de uso.</span><span class="sxs-lookup"><span data-stu-id="69076-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="69076-123">mais, leia toolearn [neste artigo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="69076-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="69076-124">Se você não vincular seu tooyour de locatário do Azure AD B2C assinatura do Azure, alguma funcionalidade será bloqueada e, você verá uma mensagem de aviso ("nenhuma assinatura toothis vinculados B2C locatário ou Olá assinatura precisa de atenção.") nas configurações de saudação B2C.</span><span class="sxs-lookup"><span data-stu-id="69076-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="69076-125">É importante que você execute esta etapa antes de enviar seus aplicativos para produção.</span><span class="sxs-lookup"><span data-stu-id="69076-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="69076-126">Acesso fácil toosettings</span><span class="sxs-lookup"><span data-stu-id="69076-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="69076-127">Você também pode acessar a folha de saudação inserindo `Azure AD B2C` na **pesquisar recursos** na parte superior de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="69076-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="69076-128">Na lista de resultados de saudação, selecione **do Azure AD B2C** tooaccess Olá B2C folha de configurações.</span><span class="sxs-lookup"><span data-stu-id="69076-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69076-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69076-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69076-130">Registrar seu aplicativo B2C em um locatário B2C</span><span class="sxs-lookup"><span data-stu-id="69076-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
