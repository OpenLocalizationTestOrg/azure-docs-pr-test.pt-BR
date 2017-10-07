---
title: "Windows 10 para a empresa Olá: dispositivos de toouse maneiras para trabalho | Microsoft Docs"
description: "Visão geral da implantação de dispositivos Windows 10 para empresas e como toointegrate com o Active Directory do Azure para Olá Windows nuvem. Diferente de maneiras diferentes de saudação um dispositivo pode ser provisionado e usado em uma empresa por meio de saudação portal do Azure."
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
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="d4798-105">Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho</span><span class="sxs-lookup"><span data-stu-id="d4798-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="d4798-106">Permite que o Windows 10 Olá tooleverage de capacidade do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d4798-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d4798-107">Você pode conectar o Windows 10 dispositivos tooAzure AD para que os usuários possam entrar em tooWindows usando as contas do AD do Azure ou adicionando seus aplicativos do Azure IDs toogain acesso toobusiness e recursos.</span><span class="sxs-lookup"><span data-stu-id="d4798-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Active Directory do Azure com a nuvem do Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="d4798-109">Integração de dispositivos do Windows 10 com o Active Directory do Azure - um mapa de conteúdo</span><span class="sxs-lookup"><span data-stu-id="d4798-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="d4798-110">Olá tópicos a seguir fornece informações sobre os diferentes recursos de dispositivos Windows 10 em sua organização.</span><span class="sxs-lookup"><span data-stu-id="d4798-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="d4798-111">Tópicos</span><span class="sxs-lookup"><span data-stu-id="d4798-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="d4798-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="d4798-112">Getting started</span></span> |[<span data-ttu-id="d4798-113">Usando dispositivos com Windows 10 no local de trabalho</span><span class="sxs-lookup"><span data-stu-id="d4798-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="d4798-114">Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d4798-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="d4798-115">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="d4798-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="d4798-116">Implantação</span><span class="sxs-lookup"><span data-stu-id="d4798-116">Deployment</span></span> |[<span data-ttu-id="d4798-117">Cenários de uso e considerações de implantação para a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4798-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="d4798-118">Experiências de se conectar a dispositivos que ingressaram no domínio tooAzure AD, para Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4798-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="d4798-119">Habilitar o Microsoft Passport for work na organização Olá</span><span class="sxs-lookup"><span data-stu-id="d4798-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="d4798-120">Habilitando o Roaming de Estado da Empresa para Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4798-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="d4798-121">Tarefas do usuário</span><span class="sxs-lookup"><span data-stu-id="d4798-121">User tasks</span></span> |[<span data-ttu-id="d4798-122">Configurando um novo dispositivo com Windows 10 com o Azure AD durante a instalação</span><span class="sxs-lookup"><span data-stu-id="d4798-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="d4798-123">Configurar um dispositivo Windows 10 com o Azure AD no menu de configurações de saudação</span><span class="sxs-lookup"><span data-stu-id="d4798-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="d4798-124">Ingressar em uma organização de tooyour de dispositivo pessoal do Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4798-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

