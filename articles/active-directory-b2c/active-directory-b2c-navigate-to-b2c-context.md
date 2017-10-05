---
title: "Azure Active Directory B2C: Alternar para um locatário B2C | Microsoft Docs"
description: "Como alternar para o contexto do seu locatário do Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="2ba20-103">Alternar para o locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2ba20-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="2ba20-104">Para configurar o Azure AD B2C, você precisa estar no contexto do seu locatário Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2ba20-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="2ba20-105">Faça logon no locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2ba20-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="2ba20-106">Para navegar até seu locatário do Azure AD B2C, você deve estar conectado ao portal do Azure como um administrador global do locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2ba20-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="2ba20-107">Faça logon no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ba20-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="2ba20-108">Alternar locatários clicando em seu endereço de email ou na imagem no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="2ba20-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="2ba20-109">Na lista `Directory` que aparece, selecione o locatário do Azure AD B2C que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="2ba20-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="2ba20-110">O Portal do Azure será atualizado.</span><span class="sxs-lookup"><span data-stu-id="2ba20-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="2ba20-111">Agora você está conectado ao portal do Azure no contexto do locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2ba20-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="2ba20-112">Navegue até a folha de recursos do B2C</span><span class="sxs-lookup"><span data-stu-id="2ba20-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="2ba20-113">Clique em **Procurar** na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2ba20-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="2ba20-114">Clique em **> Mais serviços** e, em seguida, pesquise por `Azure AD B2C` no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="2ba20-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="2ba20-115">(Para fixar ao seu quadro inicial à esquerda, clique na estrela à esquerda do Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="2ba20-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="2ba20-116">Clique em **Azure AD B2C** para acessar a folha de recursos do B2C.</span><span class="sxs-lookup"><span data-stu-id="2ba20-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Captura de tela de Navegar para a folha de recursos do B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="2ba20-118">Você precisa ser um Administrador Global do locatário do B2C para ser capaz de acessar a folha de recursos do B2C.</span><span class="sxs-lookup"><span data-stu-id="2ba20-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="2ba20-119">Um Administrador Global de qualquer outro locatário ou um Usuário de qualquer outro locatário não pode acessá-la.</span><span class="sxs-lookup"><span data-stu-id="2ba20-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="2ba20-120">Você pode alternar para o locatário B2C usando o seletor de locatário no canto superior direito do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba20-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
