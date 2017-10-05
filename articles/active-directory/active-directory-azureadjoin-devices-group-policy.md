---
title: "Conectar dispositivos ingressados no domínio ao Azure AD para experiências com Windows 10 | Microsoft Docs"
description: "Explica como os administradores podem configurar a Política de Grupo para permitir que dispositivos ingressem no domínio da rede corporativa."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="cea6b-103">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="cea6b-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="cea6b-104">O ingresso no domínio é a maneira tradicional usada pelas organizações para conectar dispositivos de trabalho pelo menos nos últimos 15 anos.</span><span class="sxs-lookup"><span data-stu-id="cea6b-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="cea6b-105">Esse recurso permitiu que os usuários entrassem em seus dispositivos usando suas contas corporativas ou de estudante do Windows Server Active Directory (Active Directory) e permitiu que a TI gerenciasse totalmente esses dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cea6b-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="cea6b-106">As organizações geralmente dependem de métodos de geração de imagens para provisionar dispositivos aos usuários e geralmente usam o SCCM (System Center Configuration Manager) ou política de grupo para gerenciá-los.</span><span class="sxs-lookup"><span data-stu-id="cea6b-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="cea6b-107">O ingresso no domínio no Windows 10 fornece os seguintes benefícios depois de conectar os dispositivos ao Azure Active Directory do Azure (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="cea6b-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="cea6b-108">SSO (logon único) para recursos do AD do Azure em qualquer lugar</span><span class="sxs-lookup"><span data-stu-id="cea6b-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="cea6b-109">Acesso à Windows Store corporativa usando contas corporativas ou de estudante (sem a exigência de conta da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="cea6b-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="cea6b-110">Roaming de configurações de usuário entre dispositivos compatível com a empresa usando a conta corporativa ou de estudante (sem a exigência de conta da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="cea6b-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="cea6b-111">Autenticação forte e entrada conveniente para a conta corporativa ou de estudante com o Windows Hello for Business e o Windows Hello</span><span class="sxs-lookup"><span data-stu-id="cea6b-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="cea6b-112">Capacidade de restringir o acesso apenas aos dispositivos que estão em conformidade com as configurações da Política de Grupo do dispositivo organizacional</span><span class="sxs-lookup"><span data-stu-id="cea6b-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cea6b-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cea6b-113">Prerequisites</span></span>
<span data-ttu-id="cea6b-114">O ingresso no domínio continua a ser útil.</span><span class="sxs-lookup"><span data-stu-id="cea6b-114">Domain join continues to be useful.</span></span> <span data-ttu-id="cea6b-115">No entanto, para obter os benefícios que o AD do Azure pode oferecer, por exemplo, SSO, roaming de configurações com conta corporativa ou de estudante, acesso ao Windows Store com conta corporativa ou de estudante, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="cea6b-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="cea6b-116">Assinatura do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cea6b-116">Azure AD subscription</span></span>
* <span data-ttu-id="cea6b-117">Azure AD Connect para estender o diretório local ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cea6b-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="cea6b-118">Política definida para conectar dispositivos ingressados no domínio ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cea6b-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="cea6b-119">Compilação do Windows 10 (compilação 10551 ou mais recente) para dispositivos</span><span class="sxs-lookup"><span data-stu-id="cea6b-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="cea6b-120">Para habilitar o Windows Hello for Business e o Windows Hello, você precisará também do seguinte:</span><span class="sxs-lookup"><span data-stu-id="cea6b-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="cea6b-121">**Infraestrutura de chave pública (PKI)** para a emissão de certificados de usuário.</span><span class="sxs-lookup"><span data-stu-id="cea6b-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="cea6b-122">**Ramificação atual do System Center Configuration Manager** - Você precisa instalar a versão 1606 ou superior.</span><span class="sxs-lookup"><span data-stu-id="cea6b-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="cea6b-123">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="cea6b-123">For more information, see:</span></span> 
    - [<span data-ttu-id="cea6b-124">Documentação para o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="cea6b-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="cea6b-125">Blog da Equipe do System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="cea6b-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="cea6b-126">Configurações do Windows Hello for Business no System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="cea6b-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="cea6b-127">Como alternativa ao requisito de implantação de PKI, você pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cea6b-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="cea6b-128">Ter alguns controladores de domínio com os Serviços de Domínio do Active Directory do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="cea6b-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="cea6b-129">Para habilitar o acesso condicional, você pode criar configurações de Política de Grupo que permitam acesso a dispositivos ingressados no domínio sem implantações adicionais.</span><span class="sxs-lookup"><span data-stu-id="cea6b-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="cea6b-130">Para gerenciar o controle de acesso baseado na conformidade do dispositivo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="cea6b-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="cea6b-131">Ramificação Atual do System Center Configuration Manager (1606 ou posterior) para cenários do Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="cea6b-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="cea6b-132">Instruções de implantação</span><span class="sxs-lookup"><span data-stu-id="cea6b-132">Deployment instructions</span></span>

<span data-ttu-id="cea6b-133">Para implantar, siga as etapas listadas em [Registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="cea6b-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="cea6b-134">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="cea6b-134">Next step</span></span>
* [<span data-ttu-id="cea6b-135">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="cea6b-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="cea6b-136">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cea6b-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="cea6b-137">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cea6b-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="cea6b-138">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="cea6b-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="cea6b-139">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cea6b-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

