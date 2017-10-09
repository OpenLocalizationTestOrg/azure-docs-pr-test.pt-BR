---
title: "verificação de aaaTwo etapa e o AD FS - Azure MFA | Microsoft Docs"
description: "Esta é hello Azure multi-Factor authentication página que descreve como tooget iniciada com o Azure MFA e AD FS."
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
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="c2590-103">Introdução ao Azure Multi-Factor Authentication e aos Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2590-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="c2590-104"><center>![Nuvem](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="c2590-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="c2590-105">Caso organização tenha federado seu Active Directory local com o Azure Active Directory usando o AD FS, existem duas opções para usar a Autenticação Multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2590-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="c2590-106">Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication ou os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2590-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="c2590-107">Proteger os recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c2590-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="c2590-108">Olá a tabela a seguir resume a experiência de verificação de saudação entre a captação de recursos com autenticação multifator do Azure e o AD FS</span><span class="sxs-lookup"><span data-stu-id="c2590-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="c2590-109">Experiência de verificação – Aplicativos baseados em navegador</span><span class="sxs-lookup"><span data-stu-id="c2590-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="c2590-110">Experiência de verificação – Aplicativos não baseados em navegador</span><span class="sxs-lookup"><span data-stu-id="c2590-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c2590-111">Protegendo os recursos do AD do Azure usando o Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c2590-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="c2590-112">Olá a primeira etapa de verificação é realizada usando o AD FS no local.</span><span class="sxs-lookup"><span data-stu-id="c2590-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="c2590-113">Olá segunda etapa é um método baseado em telefone realizado usando a autenticação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c2590-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="c2590-114">Protegendo recursos do AD do Azure usando os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2590-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="c2590-115">Olá a primeira etapa de verificação é realizada usando o AD FS no local.</span><span class="sxs-lookup"><span data-stu-id="c2590-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="c2590-116">Olá segunda etapa é realizado no local, cumprindo a declaração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2590-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="c2590-117">Advertências sobre senhas de aplicativo para usuários federados:</span><span class="sxs-lookup"><span data-stu-id="c2590-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="c2590-118">Senhas de aplicativo são verificadas usando a autenticação na nuvem e, portanto, ignora as federações.</span><span class="sxs-lookup"><span data-stu-id="c2590-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="c2590-119">A federação só é usada ativamente ao configurar a senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2590-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="c2590-120">As configurações do Controle de Acesso do Cliente local não são consideradas pela Senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2590-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="c2590-121">Você perde a capacidade de registro de autenticação local para senha de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2590-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="c2590-122">Desabilitar/excluir a conta pode levar horas toothree para sincronização de diretórios, atrasando o desabilitar/excluir das senhas de aplicativo na identidade de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c2590-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2590-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2590-123">Next steps</span></span>
<span data-ttu-id="c2590-124">Para obter informações sobre como configurar a autenticação multifator do Azure ou Olá servidor Azure multi-Factor Authentication com o AD FS, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2590-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="c2590-125">Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS</span><span class="sxs-lookup"><span data-stu-id="c2590-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="c2590-126">Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com o AD FS do Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c2590-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="c2590-127">Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="c2590-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
