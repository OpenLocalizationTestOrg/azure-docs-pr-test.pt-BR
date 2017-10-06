---
title: "passa por dispositivos que ingressaram no domínio de aaaConnect tooAzure AD para Windows 10 | Microsoft Docs"
description: "Explica como os administradores podem configurar a rede da empresa política de grupo tooenable dispositivos toobe toohello ingressado no domínio."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="74871-103">Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="74871-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="74871-104">Ingresso no domínio é organizações de maneira tradicional de saudação conectou dispositivos para o trabalho para Olá últimos 15 anos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="74871-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="74871-105">Permitiu que usuários toosign tootheir dispositivos por meio de seu trabalho do Windows Server Active Directory (Active Directory) ou contas de estudante e toofully IT permitido gerenciam esses dispositivos.</span><span class="sxs-lookup"><span data-stu-id="74871-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="74871-106">As organizações normalmente dependem de métodos tooprovision dispositivos toousers de geração de imagens e geralmente usam toomanage de diretiva de grupo ou System Center Configuration Manager (SCCM)-los.</span><span class="sxs-lookup"><span data-stu-id="74871-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="74871-107">Ingresso no domínio no Windows 10 fornece Olá benefícios a seguir depois de conectar dispositivos tooAzure do Active Directory (AD do Azure):</span><span class="sxs-lookup"><span data-stu-id="74871-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="74871-108">Único sign-on (SSO) tooAzure AD recursos em qualquer lugar</span><span class="sxs-lookup"><span data-stu-id="74871-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="74871-109">Acessar toohello empresa da Windows Store usando o trabalho ou escola contas (nenhuma conta da Microsoft necessários)</span><span class="sxs-lookup"><span data-stu-id="74871-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="74871-110">Roaming de configurações de usuário entre dispositivos compatível com a empresa usando a conta corporativa ou de estudante (sem a exigência de conta da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="74871-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="74871-111">Autenticação forte e entrada conveniente para a conta corporativa ou de estudante com o Windows Hello for Business e o Windows Hello</span><span class="sxs-lookup"><span data-stu-id="74871-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="74871-112">Capacidade toorestrict acessar apenas toodevices que estão em conformidade com as configurações de política de grupo do dispositivo organizacional</span><span class="sxs-lookup"><span data-stu-id="74871-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74871-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74871-113">Prerequisites</span></span>
<span data-ttu-id="74871-114">Ingresso no domínio continua toobe útil.</span><span class="sxs-lookup"><span data-stu-id="74871-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="74871-115">No entanto, tooget benefícios de saudação do AD do Azure do SSO, roaming de configurações com ou escolar contas e acessar o armazenamento de tooWindows com o trabalho ou de estudante contas, você precisará Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="74871-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="74871-116">Assinatura do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74871-116">Azure AD subscription</span></span>
* <span data-ttu-id="74871-117">Saudação de tooextend do Azure AD Connect tooAzure diretório AD local</span><span class="sxs-lookup"><span data-stu-id="74871-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="74871-118">Diretiva que definiu tooconnect tooAzure de dispositivos que ingressaram no domínio AD</span><span class="sxs-lookup"><span data-stu-id="74871-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="74871-119">Compilação do Windows 10 (compilação 10551 ou mais recente) para dispositivos</span><span class="sxs-lookup"><span data-stu-id="74871-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="74871-120">tooenable Windows Hello for Business e o Windows Hello, também será necessário seguir hello:</span><span class="sxs-lookup"><span data-stu-id="74871-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="74871-121">**Infraestrutura de chave pública (PKI)** para a emissão de certificados de usuário.</span><span class="sxs-lookup"><span data-stu-id="74871-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="74871-122">**Ramificação atual do System Center Configuration Manager** -você precisa tooinstall versão 1606 ou melhor.</span><span class="sxs-lookup"><span data-stu-id="74871-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="74871-123">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="74871-123">For more information, see:</span></span> 
    - [<span data-ttu-id="74871-124">Documentação para o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="74871-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="74871-125">Blog da Equipe do System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="74871-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="74871-126">Configurações do Windows Hello for Business no System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="74871-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="74871-127">Como um requisito de implantação de PKI toohello alternativa, você pode fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="74871-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="74871-128">Ter alguns controladores de domínio com os Serviços de Domínio do Active Directory do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="74871-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="74871-129">tooenable o acesso condicional, você pode criar configurações de diretiva de grupo que permitem que dispositivos que ingressaram no toodomain acesso com nenhuma implantações adicionais.</span><span class="sxs-lookup"><span data-stu-id="74871-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="74871-130">toomanage controle de acesso com base na conformidade de dispositivo hello, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="74871-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="74871-131">Ramificação Atual do System Center Configuration Manager (1606 ou posterior) para cenários do Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="74871-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="74871-132">Instruções de implantação</span><span class="sxs-lookup"><span data-stu-id="74871-132">Deployment instructions</span></span>

<span data-ttu-id="74871-133">toodeploy, siga as etapas de Olá listadas na [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="74871-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="74871-134">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="74871-134">Next step</span></span>
* [<span data-ttu-id="74871-135">Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho</span><span class="sxs-lookup"><span data-stu-id="74871-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="74871-136">Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="74871-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="74871-137">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74871-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="74871-138">Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="74871-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="74871-139">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74871-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

