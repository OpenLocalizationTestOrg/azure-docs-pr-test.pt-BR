---
title: Como configurar um aplicativo de Application Proxy para usar o PingAccess | Microsoft Docs
description: "Saiba como usar o PingAccess para estender os benefícios do Application Proxy em aplicativos que usam autenticação baseada em cabeçalho"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="4ef62-103">Como configurar um aplicativo de Application Proxy para usar o PingAccess</span><span class="sxs-lookup"><span data-stu-id="4ef62-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="4ef62-104">Nossa colaboração com PingAccess agora permite que você estenda os benefícios do Application Proxy para aplicativos que usam autenticação baseada em cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="4ef62-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="4ef62-105">Se seus aplicativos não usam cabeçalhos, consulte nossa [Documentação de Logon único](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) para obter detalhes sobre outras opções.</span><span class="sxs-lookup"><span data-stu-id="4ef62-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="4ef62-106">Visão geral das etapas e documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="4ef62-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="4ef62-107">Para configurar um aplicativo com PingAccess, há quatro etapas:</span><span class="sxs-lookup"><span data-stu-id="4ef62-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="4ef62-108">Configurar conectores de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="4ef62-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="4ef62-109">Criar um aplicativo de Application Proxy do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef62-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="4ef62-110">Baixar e configurar PingAccess</span><span class="sxs-lookup"><span data-stu-id="4ef62-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="4ef62-111">Configurar aplicativos no PingAccess</span><span class="sxs-lookup"><span data-stu-id="4ef62-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="4ef62-112">Para obter detalhes sobre cada uma dessas etapas, consulte nossa [Documentação de Logon único com cabeçalhos](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="4ef62-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
