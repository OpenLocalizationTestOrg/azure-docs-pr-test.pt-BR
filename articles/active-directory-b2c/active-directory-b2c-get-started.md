---
title: "Azure Active Directory B2C: criar um locatário do Azure Active Directory B2C | Microsoft Docs"
description: "Um tópico sobre como criar um locatário zure Active Directory B2C"
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
ms.openlocfilehash: 8a1d4935397f59e5813afc6f04559e471187a779
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="d2f32-103">Crie um locatário do Azure Active Directory B2C no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2f32-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="d2f32-104">Este Guia de início rápido ajuda a criar um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="d2f32-104">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="d2f32-105">Quando você terminar, terá um locatário B2C a ser usado para registrar aplicativos B2C.</span><span class="sxs-lookup"><span data-stu-id="d2f32-105">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2f32-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2f32-106">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="d2f32-107">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="d2f32-107">Log in to Azure</span></span>

<span data-ttu-id="d2f32-108">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2f32-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d2f32-109">Criar um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d2f32-109">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="d2f32-110">Os recursos B2C não podem ser habilitados em seus locatários existentes.</span><span class="sxs-lookup"><span data-stu-id="d2f32-110">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="d2f32-111">Você precisa um locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2f32-111">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="d2f32-112">Parabéns, você criou um locatário do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d2f32-112">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d2f32-113">Você é um Administrador Global do locatário.</span><span class="sxs-lookup"><span data-stu-id="d2f32-113">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="d2f32-114">Você pode adicionar outros Administradores Globais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d2f32-114">You can add other Global Administrators as required.</span></span> <span data-ttu-id="d2f32-115">Para alternar para o novo locatário, clique no *link gerenciar seu novo locatário*.</span><span class="sxs-lookup"><span data-stu-id="d2f32-115">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Gerenciar seu novo link de locatário](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="d2f32-117">Se você está planejando usar um locatário B2C para um aplicativo de produção, leia o artigo sobre [escala de produção versus locatários de visualização do B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="d2f32-117">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="d2f32-118">Há problemas conhecidos quando você exclui um locatário B2C existente e o recria com o mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="d2f32-118">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="d2f32-119">Você precisa criar um locatário B2C com um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="d2f32-119">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="d2f32-120">Vincular seu locatário à sua assinatura</span><span class="sxs-lookup"><span data-stu-id="d2f32-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="d2f32-121">Você precisa vincular o seu locatário do Azure AD B2C à sua assinatura do Azure para habilitar todas as funcionalidades do B2C e pagar pelos encargos de uso.</span><span class="sxs-lookup"><span data-stu-id="d2f32-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="d2f32-122">Para saber mais, leia este [artigo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="d2f32-122">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="d2f32-123">Se você não vincular seu locatário do Azure AD B2C à sua assinatura do Azure, alguma funcionalidade será bloqueada e você verá uma mensagem de aviso ("Nenhuma assinatura vinculada a este locatário B2C ou A assinatura precisa de sua atenção.") nas configurações do B2C.</span><span class="sxs-lookup"><span data-stu-id="d2f32-123">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="d2f32-124">É importante que você execute esta etapa antes de enviar seus aplicativos para produção.</span><span class="sxs-lookup"><span data-stu-id="d2f32-124">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="d2f32-125">Acesso fácil a configurações</span><span class="sxs-lookup"><span data-stu-id="d2f32-125">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="d2f32-126">Você também pode acessar a folha digitando `Azure AD B2C` em **Pesquisar recursos** na parte superior do portal.</span><span class="sxs-lookup"><span data-stu-id="d2f32-126">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="d2f32-127">Na lista de resultados, selecione **Azure AD B2C** para acessar a folha de configurações do B2C.</span><span class="sxs-lookup"><span data-stu-id="d2f32-127">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2f32-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2f32-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2f32-129">Registrar seu aplicativo B2C em um locatário B2C</span><span class="sxs-lookup"><span data-stu-id="d2f32-129">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)