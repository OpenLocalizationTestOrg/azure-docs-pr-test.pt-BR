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
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="a2eb2-103">Azure AD Connect: considerações especiais para instâncias</span><span class="sxs-lookup"><span data-stu-id="a2eb2-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="a2eb2-104">Conexão do AD do Azure é mais comumente usado com a instância do hello world-wide do AD do Azure e o Office 365.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="a2eb2-105">Mas também existem outras instâncias que têm requisitos diferentes para URLs e outras considerações especiais.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="a2eb2-106">Microsoft Cloud Alemanha</span><span class="sxs-lookup"><span data-stu-id="a2eb2-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="a2eb2-107">Olá [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) é uma nuvem soberana operada por um objeto de confiança dados alemão.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="a2eb2-108">Tooopen de URLs no servidor proxy</span><span class="sxs-lookup"><span data-stu-id="a2eb2-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="a2eb2-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="a2eb2-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="a2eb2-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="a2eb2-110">\*.windows.net</span></span> |
| <span data-ttu-id="a2eb2-111">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="a2eb2-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="a2eb2-112">Quando você entrar no locatário do AD do Azure tooyour, você deve usar uma conta no domínio de onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="a2eb2-113">Recursos atualmente não está presentes na Alemanha do Microsoft Cloud hello:</span><span class="sxs-lookup"><span data-stu-id="a2eb2-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="a2eb2-114">O **Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="a2eb2-115">As **Atualizações automáticas** não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="a2eb2-116">O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="a2eb2-117">Outros serviços do Azure AD Premium não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="a2eb2-118">Nuvem do Microsoft Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="a2eb2-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="a2eb2-119">Olá [nuvem do Microsoft Azure Government](https://azure.microsoft.com/features/gov/) é uma nuvem para o governo dos EUA.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="a2eb2-120">Esta nuvem teve suporte em versões mais antigas do DirSync.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="a2eb2-121">Compilação 1.1.180 do Azure AD Connect, Olá próxima geração da nuvem de saudação é suportada.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="a2eb2-122">Essa geração está usando pontos de extremidade com base somente nos EUA e tem uma lista de URLs tooopen diferente no servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="a2eb2-123">Tooopen de URLs no servidor proxy</span><span class="sxs-lookup"><span data-stu-id="a2eb2-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="a2eb2-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a2eb2-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="a2eb2-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="a2eb2-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="a2eb2-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a2eb2-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="a2eb2-127">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="a2eb2-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="a2eb2-128">Conexão do AD do Azure não é capaz de tooautomatically detectar que o seu locatário do AD do Azure está localizado na nuvem do governo hello.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="a2eb2-129">Em vez disso, você precisa de saudação tootake ações a seguir quando você instala o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="a2eb2-130">Inicie a instalação do Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="a2eb2-131">Quando você vir a página primeiro hello, onde você deve tooaccept Olá EULA, não continuar, mas deixar o Assistente de instalação de saudação em execução.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="a2eb2-132">Inicie o regedit e alterar a chave de registro de saudação `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="a2eb2-133">Voltar Assistente de instalação toohello do Azure AD Connect, aceite o EULA de saudação e continuar.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="a2eb2-134">Durante a instalação, verifique se Olá de toouse **configuração personalizada** caminho de instalação (e não a instalação expressa).</span><span class="sxs-lookup"><span data-stu-id="a2eb2-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="a2eb2-135">Em seguida, continue a instalação do hello como de costume.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="a2eb2-136">Recursos atualmente não está presentes na nuvem do Microsoft Azure Government Olá:</span><span class="sxs-lookup"><span data-stu-id="a2eb2-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="a2eb2-137">O **Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="a2eb2-138">As **Atualizações automáticas** não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="a2eb2-139">O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="a2eb2-140">Outros serviços do Azure AD Premium não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a2eb2-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2eb2-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2eb2-141">Next steps</span></span>
<span data-ttu-id="a2eb2-142">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="a2eb2-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
