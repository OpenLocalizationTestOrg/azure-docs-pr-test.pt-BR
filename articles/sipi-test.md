---
title: Arquivo de teste Sipi | Microsoft Docs
description: "Arquivo de teste para verificar dependências de ReadyForTest"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="a3e69-103">Arquivo de teste Sipi</span><span class="sxs-lookup"><span data-stu-id="a3e69-103">Sipi test file</span></span>

<span data-ttu-id="a3e69-104">Este Guia de início rápido ajuda você a registrar um aplicativo em um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="a3e69-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="a3e69-105">Quando terminar, seu aplicativo estará registrado para uso no locatário B2C do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e69-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3e69-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3e69-106">Prerequisites</span></span>

<span data-ttu-id="a3e69-107">Para compilar um aplicativo que aceite a inscrição e a entrada do consumidor, primeiro será necessário registrar o aplicativo em um locatário do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a3e69-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="a3e69-108">Obtenha seu próprio locatário usando as etapas descritas em [Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3e69-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="a3e69-109">Os aplicativos criados da folha Azure AD B2C no portal do Azure devem ser gerenciados do mesmo local.</span><span class="sxs-lookup"><span data-stu-id="a3e69-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="a3e69-110">Se você editar os aplicativos B2C usando o PowerShell ou outro portal, eles deixarão de ter suporte e não funcionarão com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a3e69-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="a3e69-111">Consulte os detalhes da seção [aplicativos com falha](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="a3e69-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="a3e69-112">Navegue até as configurações de B2C</span><span class="sxs-lookup"><span data-stu-id="a3e69-112">Navigate to B2C settings</span></span>

<span data-ttu-id="a3e69-113">Entre no [Portal do Azure](https://portal.azure.com/) como Administrador Global do locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="a3e69-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="a3e69-114">Escolha as próximas etapas com base no tipo de aplicativo que você está registrando:</span><span class="sxs-lookup"><span data-stu-id="a3e69-114">Choose next steps based on the application type you are registering:</span></span>
