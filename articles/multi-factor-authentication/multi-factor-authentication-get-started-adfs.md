---
title: "Verificação em duas etapas e AD FS - Azure MFA | Microsoft Docs"
description: "Esta é a página do Azure Multi-Factor Authentication que descreve como começar a usar o Azure MFA e o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="92287-103">Introdução ao Azure Multi-Factor Authentication e aos Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="92287-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="92287-104"><center>![Nuvem](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="92287-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="92287-105">Caso organização tenha federado seu Active Directory local com o Azure Active Directory usando o AD FS, existem duas opções para usar a Autenticação Multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="92287-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="92287-106">Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication ou os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="92287-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="92287-107">Proteger os recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="92287-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="92287-108">A tabela a seguir resume a experiência de verificação entre a proteção dos recursos com a Autenticação Multifator do Azure e o AD FS</span><span class="sxs-lookup"><span data-stu-id="92287-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="92287-109">Experiência de verificação – Aplicativos baseados em navegador</span><span class="sxs-lookup"><span data-stu-id="92287-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="92287-110">Experiência de verificação – Aplicativos não baseados em navegador</span><span class="sxs-lookup"><span data-stu-id="92287-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="92287-111">Protegendo os recursos do AD do Azure usando o Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="92287-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="92287-112">A primeira etapa de verificação é executada localmente usando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="92287-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="92287-113">A segunda etapa é um método baseado em telefone executado com a autenticação na nuvem.</span><span class="sxs-lookup"><span data-stu-id="92287-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="92287-114">Protegendo recursos do AD do Azure usando os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="92287-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="92287-115">A primeira etapa de verificação é executada localmente usando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="92287-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="92287-116">A segunda etapa é realizada localmente, cumprindo a declaração.</span><span class="sxs-lookup"><span data-stu-id="92287-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="92287-117">Advertências sobre senhas de aplicativo para usuários federados:</span><span class="sxs-lookup"><span data-stu-id="92287-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="92287-118">Senhas de aplicativo são verificadas usando a autenticação na nuvem e, portanto, ignora as federações.</span><span class="sxs-lookup"><span data-stu-id="92287-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="92287-119">A federação só é usada ativamente ao configurar a senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92287-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="92287-120">As configurações do Controle de Acesso do Cliente local não são consideradas pela Senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92287-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="92287-121">Você perde a capacidade de registro de autenticação local para senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92287-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="92287-122">A desabilitação/exclusão da conta pode levar até três horas para a sincronização do diretório, atrasando a desabilitação/exclusão da senha de aplicativo na identidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="92287-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92287-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92287-123">Next steps</span></span>
<span data-ttu-id="92287-124">Para obter informações sobre como configurar a Autenticação Multifator do Azure ou o Servidor de Autenticação Multifator do Azure com o AD FS, consulte os artigos:</span><span class="sxs-lookup"><span data-stu-id="92287-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="92287-125">Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS</span><span class="sxs-lookup"><span data-stu-id="92287-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="92287-126">Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com o AD FS do Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="92287-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="92287-127">Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="92287-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
