---
title: 'Windows 10 para a empresa: maneiras de usar dispositivos para trabalho | Microsoft Docs'
description: "Visão geral da implantação de dispositivos Windows 10 para empresas e como integrar-se com o Active Directory do Azure para a nuvem do Windows. Compara as diferentes maneiras que um dispositivo pode ser provisionado e usado em uma empresa por meio do portal do Azure."
keywords: nuvem do Windows, Windows no Active Directory do Azure, dispositivos Windows 10 no Azure, dispositivos Windows no Azure
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="52095-105">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="52095-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="52095-106">O Windows 10 fornece a capacidade de aproveitar o Active Directory do Azure (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="52095-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="52095-107">Você pode conectar os dispositivos Windows 10 ao AD do Azure e, assim, os usuários podem entrar no Windows usando contas do AD do Azure ou adicionando as IDs do Azure para obter acesso aos recursos e aplicativos de negócios.</span><span class="sxs-lookup"><span data-stu-id="52095-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Active Directory do Azure com a nuvem do Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="52095-109">Integração de dispositivos do Windows 10 com o Active Directory do Azure - um mapa de conteúdo</span><span class="sxs-lookup"><span data-stu-id="52095-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="52095-110">Os tópicos a seguir fornecem informações sobre recursos diferentes de dispositivos Windows 10 em sua organização.</span><span class="sxs-lookup"><span data-stu-id="52095-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="52095-111">Tópicos</span><span class="sxs-lookup"><span data-stu-id="52095-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="52095-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="52095-112">Getting started</span></span> |[<span data-ttu-id="52095-113">Usando dispositivos com Windows 10 no local de trabalho</span><span class="sxs-lookup"><span data-stu-id="52095-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="52095-114">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52095-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="52095-115">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="52095-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="52095-116">Implantação</span><span class="sxs-lookup"><span data-stu-id="52095-116">Deployment</span></span> |[<span data-ttu-id="52095-117">Cenários de uso e considerações de implantação para a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52095-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="52095-118">Conectando dispositivos ingressados no domínio ao Azure AD para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="52095-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="52095-119">Habilitando o Microsoft Passport for Work na organização</span><span class="sxs-lookup"><span data-stu-id="52095-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="52095-120">Habilitando o Roaming de Estado da Empresa para Windows 10</span><span class="sxs-lookup"><span data-stu-id="52095-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="52095-121">Tarefas do usuário</span><span class="sxs-lookup"><span data-stu-id="52095-121">User tasks</span></span> |[<span data-ttu-id="52095-122">Configurando um novo dispositivo com Windows 10 com o Azure AD durante a instalação</span><span class="sxs-lookup"><span data-stu-id="52095-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="52095-123">Configurando um dispositivo com Windows 10 com o Azure AD no menu de configurações</span><span class="sxs-lookup"><span data-stu-id="52095-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="52095-124">Ingressar um dispositivo Windows 10 pessoal na sua organização</span><span class="sxs-lookup"><span data-stu-id="52095-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

