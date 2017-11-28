---
title: aaaAzure AD Connect na Alemanha Microsoft Cloud
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure."
keywords: "Introdução tooAzure AD Connect, visão geral do Azure AD Connect, o que é o Azure AD Connect, instalar o active directory, Alemanha, preto floresta"
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
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="6b5f4-105">Azure AD Connect na Microsoft Cloud Alemanha - Visualização Pública</span><span class="sxs-lookup"><span data-stu-id="6b5f4-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="6b5f4-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="6b5f4-106">Introduction</span></span>
<span data-ttu-id="6b5f4-107">O Azure AD Connect fornece sincronização entre o Active Directory local e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="6b5f4-108">Atualmente, muitos dos cenários de saudação em [Microsoft Cloud Alemanha](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) deve ser feito por operador hello.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="6b5f4-109">Ao usar o Microsoft Cloud Alemanha, você deve estar ciente do seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6b5f4-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="6b5f4-110">Olá que URLs a seguir devem ser abertas em um servidor proxy para sincronização toooccur com êxito:</span><span class="sxs-lookup"><span data-stu-id="6b5f4-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="6b5f4-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="6b5f4-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="6b5f4-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="6b5f4-112">*.windows.net</span></span>
  * * <span data-ttu-id="6b5f4-113">Listas de Revogação de Certificados</span><span class="sxs-lookup"><span data-stu-id="6b5f4-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="6b5f4-114">Quando você entrar no diretório do AD do Azure tooyour, você deve usar uma conta no domínio de onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="6b5f4-115">Olá recursos a seguir não está disponível:</span><span class="sxs-lookup"><span data-stu-id="6b5f4-115">hello following features are not available:</span></span>
  * <span data-ttu-id="6b5f4-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="6b5f4-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="6b5f4-117">Atualizações automáticas</span><span class="sxs-lookup"><span data-stu-id="6b5f4-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="6b5f4-118">Baixar</span><span class="sxs-lookup"><span data-stu-id="6b5f4-118">Download</span></span>
<span data-ttu-id="6b5f4-119">Você pode baixar o Azure AD Connect da folha de conexão do AD do Azure hello dentro do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="6b5f4-120">Use as instruções de saudação abaixo folha do toolocate hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="6b5f4-121">saudação do Azure AD Connect-folha</span><span class="sxs-lookup"><span data-stu-id="6b5f4-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="6b5f4-122">Depois de ter entrado no toohello portal do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b5f4-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="6b5f4-123">Vá tooBrowse</span><span class="sxs-lookup"><span data-stu-id="6b5f4-123">Go tooBrowse</span></span>
2. <span data-ttu-id="6b5f4-124">Selecione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b5f4-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="6b5f4-125">Em seguida, selecione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6b5f4-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="6b5f4-126">Você verá a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6b5f4-126">You should see hello following:</span></span>

![Folha do Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="6b5f4-128">Hello tabela a seguir descreve os recursos de saudação mostrados na folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="6b5f4-129">Title</span><span class="sxs-lookup"><span data-stu-id="6b5f4-129">Title</span></span> | <span data-ttu-id="6b5f4-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="6b5f4-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b5f4-131">STATUS DA SINCRONIZAÇÃO</span><span class="sxs-lookup"><span data-stu-id="6b5f4-131">SYNC STATUS</span></span> |<span data-ttu-id="6b5f4-132">Informa se a sincronização está habilitada ou desabilitada.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="6b5f4-133">ÚLTIMA SINCRONIZAÇÃO</span><span class="sxs-lookup"><span data-stu-id="6b5f4-133">LAST SYNC</span></span> |<span data-ttu-id="6b5f4-134">Olá a última vez em que uma sincronização bem-sucedida foi concluída.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="6b5f4-135">DOMÍNIOS FEDERADOS</span><span class="sxs-lookup"><span data-stu-id="6b5f4-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="6b5f4-136">Mostra o número de saudação de domínios federados configurado no momento.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="6b5f4-137">Instalação</span><span class="sxs-lookup"><span data-stu-id="6b5f4-137">Installation</span></span>
<span data-ttu-id="6b5f4-138">tooinstall do Azure AD Connect, você pode usar a documentação de saudação [aqui](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="6b5f4-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="6b5f4-139">Recursos avançados e informações adicionais</span><span class="sxs-lookup"><span data-stu-id="6b5f4-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="6b5f4-140">Para obter informações adicionais e orientação sobre as configurações personalizadas ou configurações avançadas, comece em [Integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6b5f4-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="6b5f4-141">Esta página fornece informações e links tooadditional orientação.</span><span class="sxs-lookup"><span data-stu-id="6b5f4-141">This page provides information and links tooadditional guidance.</span></span>

