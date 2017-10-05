---
title: Azure AD Connect na Microsoft Cloud Alemanha
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory. Isso permite que você forneça uma identidade comum para os aplicativos do Office 365, Azure e SaaS integrados ao AD do Azure."
keywords: "introdução ao Azure AD Connect, visão geral do Azure AD Connect, o que é o Azure AD Connect, instalar o active directory, Alemanha, Floresta Negra"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="fcddd-105">Azure AD Connect na Microsoft Cloud Alemanha - Visualização Pública</span><span class="sxs-lookup"><span data-stu-id="fcddd-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="fcddd-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="fcddd-106">Introduction</span></span>
<span data-ttu-id="fcddd-107">O Azure AD Connect fornece sincronização entre o Active Directory local e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcddd-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="fcddd-108">Atualmente, muitos dos cenários em [Microsoft Cloud Alemanha](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) devem ser realizados pela operadora.</span><span class="sxs-lookup"><span data-stu-id="fcddd-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="fcddd-109">Ao usar o Microsoft Cloud Alemanha, você deve estar ciente do seguinte:</span><span class="sxs-lookup"><span data-stu-id="fcddd-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="fcddd-110">As URLs a seguir devem ser abertas em um servidor proxy para que a sincronização tenha êxito:</span><span class="sxs-lookup"><span data-stu-id="fcddd-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="fcddd-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="fcddd-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="fcddd-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="fcddd-112">*.windows.net</span></span>
  * * <span data-ttu-id="fcddd-113">Listas de Revogação de Certificados</span><span class="sxs-lookup"><span data-stu-id="fcddd-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="fcddd-114">Quando você entrar em seu diretório do Azure AD, deverá usar uma conta com o domínio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="fcddd-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="fcddd-115">Os seguintes recursos não estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="fcddd-115">The following features are not available:</span></span>
  * <span data-ttu-id="fcddd-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="fcddd-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="fcddd-117">Atualizações automáticas</span><span class="sxs-lookup"><span data-stu-id="fcddd-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="fcddd-118">Baixar</span><span class="sxs-lookup"><span data-stu-id="fcddd-118">Download</span></span>
<span data-ttu-id="fcddd-119">Você pode baixar o Azure AD Connect da folha do Azure AD Connect no portal.</span><span class="sxs-lookup"><span data-stu-id="fcddd-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="fcddd-120">Use as instruções abaixo para localizar a folha do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fcddd-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="fcddd-121">A folha do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="fcddd-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="fcddd-122">Depois que você entrar no portal do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fcddd-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="fcddd-123">Vá para Procurar</span><span class="sxs-lookup"><span data-stu-id="fcddd-123">Go to Browse</span></span>
2. <span data-ttu-id="fcddd-124">Selecione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcddd-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="fcddd-125">Em seguida, selecione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="fcddd-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="fcddd-126">Você deve ver o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fcddd-126">You should see the following:</span></span>

![Folha do Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="fcddd-128">A tabela a seguir descreve os recursos mostrados na folha.</span><span class="sxs-lookup"><span data-stu-id="fcddd-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="fcddd-129">Title</span><span class="sxs-lookup"><span data-stu-id="fcddd-129">Title</span></span> | <span data-ttu-id="fcddd-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcddd-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fcddd-131">STATUS DA SINCRONIZAÇÃO</span><span class="sxs-lookup"><span data-stu-id="fcddd-131">SYNC STATUS</span></span> |<span data-ttu-id="fcddd-132">Informa se a sincronização está habilitada ou desabilitada.</span><span class="sxs-lookup"><span data-stu-id="fcddd-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="fcddd-133">ÚLTIMA SINCRONIZAÇÃO</span><span class="sxs-lookup"><span data-stu-id="fcddd-133">LAST SYNC</span></span> |<span data-ttu-id="fcddd-134">A última vez que uma sincronização bem-sucedida foi concluída.</span><span class="sxs-lookup"><span data-stu-id="fcddd-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="fcddd-135">DOMÍNIOS FEDERADOS</span><span class="sxs-lookup"><span data-stu-id="fcddd-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="fcddd-136">Mostra o número de domínios federados configurado no momento.</span><span class="sxs-lookup"><span data-stu-id="fcddd-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="fcddd-137">Instalação</span><span class="sxs-lookup"><span data-stu-id="fcddd-137">Installation</span></span>
<span data-ttu-id="fcddd-138">Para instalar o Azure AD Connect, você pode usar a documentação [aqui](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="fcddd-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="fcddd-139">Recursos avançados e informações adicionais</span><span class="sxs-lookup"><span data-stu-id="fcddd-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="fcddd-140">Para obter informações adicionais e orientação sobre as configurações personalizadas ou configurações avançadas, comece em [Integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="fcddd-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="fcddd-141">Esta página fornece informações e links para orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="fcddd-141">This page provides information and links to additional guidance.</span></span>

