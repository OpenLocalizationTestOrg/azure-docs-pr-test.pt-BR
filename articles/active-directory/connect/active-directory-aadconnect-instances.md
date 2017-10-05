---
title: "Azure AD Connect: instâncias do serviço de sincronização | Microsoft Docs"
description: "Esta página documenta considerações especiais para instâncias do Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="ab6e0-103">Azure AD Connect: considerações especiais para instâncias</span><span class="sxs-lookup"><span data-stu-id="ab6e0-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="ab6e0-104">O Azure AD Connect é mais comumente usado com a instância mundial do Azure AD e o Office 365.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="ab6e0-105">Mas também existem outras instâncias que têm requisitos diferentes para URLs e outras considerações especiais.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="ab6e0-106">Microsoft Cloud Alemanha</span><span class="sxs-lookup"><span data-stu-id="ab6e0-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="ab6e0-107">O [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) é uma nuvem soberana operada por uma administradora de dados alemã.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="ab6e0-108">URLs para abrir no servidor proxy</span><span class="sxs-lookup"><span data-stu-id="ab6e0-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="ab6e0-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="ab6e0-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="ab6e0-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="ab6e0-110">\*.windows.net</span></span> |
| <span data-ttu-id="ab6e0-111">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="ab6e0-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="ab6e0-112">Ao entrar em seu locatário do Azure AD, você deverá usar uma conta com o domínio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="ab6e0-113">Recursos atualmente indisponíveis no Microsoft Cloud Alemanha:</span><span class="sxs-lookup"><span data-stu-id="ab6e0-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="ab6e0-114">O **Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="ab6e0-115">As **Atualizações automáticas** não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="ab6e0-116">O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="ab6e0-117">Outros serviços do Azure AD Premium não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="ab6e0-118">Nuvem do Microsoft Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="ab6e0-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="ab6e0-119">A [Nuvem do Microsoft Azure Governamental](https://azure.microsoft.com/features/gov/) é uma nuvem para o governo dos EUA.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="ab6e0-120">Esta nuvem teve suporte em versões mais antigas do DirSync.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="ab6e0-121">A partir da build 1.1.180 do Azure AD Connect, há suporte para a próxima geração da nuvem.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="ab6e0-122">Essa geração está usando pontos de extremidade com base somente nos EUA e tem uma lista de URLs diferente para abrir em seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="ab6e0-123">URLs para abrir no servidor proxy</span><span class="sxs-lookup"><span data-stu-id="ab6e0-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="ab6e0-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ab6e0-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="ab6e0-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="ab6e0-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="ab6e0-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ab6e0-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="ab6e0-127">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="ab6e0-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="ab6e0-128">O Azure AD Connect não é capaz de detectar automaticamente que o locatário do Azure AD está localizado na nuvem Governamental.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="ab6e0-129">Em vez disso, você precisa executar as seguintes ações ao instalar o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="ab6e0-130">Inicie a instalação do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="ab6e0-131">Quando você consultar a primeira página na qual recebe uma solicitação para aceitar o EULA, não continue, mas deixe o assistente de instalação em execução.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="ab6e0-132">Inicie o regedit e altere a chave do registro `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` para o valor `2`.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="ab6e0-133">Vá para o assistente de instalação do Azure AD Connect, aceite o EULA e continue.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="ab6e0-134">Durante a instalação, certifique-se de usar o caminho de instalação **configuração personalizada** (e não a instalação Expressa).</span><span class="sxs-lookup"><span data-stu-id="ab6e0-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="ab6e0-135">Em seguida, continue a instalação como de costume.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="ab6e0-136">Recursos atualmente indisponíveis na nuvem do Microsoft Azure Governamental:</span><span class="sxs-lookup"><span data-stu-id="ab6e0-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="ab6e0-137">O **Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="ab6e0-138">As **Atualizações automáticas** não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="ab6e0-139">O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="ab6e0-140">Outros serviços do Azure AD Premium não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ab6e0-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab6e0-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab6e0-141">Next steps</span></span>
<span data-ttu-id="ab6e0-142">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ab6e0-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
