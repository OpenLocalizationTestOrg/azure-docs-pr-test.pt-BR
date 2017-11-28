---
title: "aplicativos de nuvem com o Cloud App Discovery não gerenciado aaaFinding | Microsoft Docs"
description: "Fornece informações sobre como localizar e gerenciar aplicativos com o Cloud App Discovery, quais são os benefícios de saudação e como ele funciona."
services: active-directory
keywords: cloud app discovery, gerenciamento de aplicativos
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="5aa2f-104">Encontrando aplicativos em nuvem não gerenciados com o Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5aa2f-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="5aa2f-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5aa2f-105">Overview</span></span>
<span data-ttu-id="5aa2f-106">Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos de nuvem Olá que membros de sua organização usam toodo seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="5aa2f-107">É fácil toosee por que os administradores terão preocupações sobre dados de toocorporate de acesso não autorizado, perda de dados e outros riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="5aa2f-108">Essa falta de reconhecimento pode fazer com que a criação de um plano para lidar com esses riscos de segurança pareça assustadora.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="5aa2f-109">Cloud App Discovery é um recurso Premium do Azure AD (Active Directory) que permite que você toodiscover aplicativos em nuvem que estão sendo usados por pessoas de saudação em sua organização.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="5aa2f-110">**Com o Cloud App Discovery é possível:**</span><span class="sxs-lookup"><span data-stu-id="5aa2f-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="5aa2f-111">Localizar aplicativos em nuvem hello está sendo usados e que o uso de medidas por número de usuários, volume de tráfego ou número de solicitações toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="5aa2f-112">Identificar usuários Olá que estão usando um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="5aa2f-113">Exporte os dados para a análise offline.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="5aa2f-114">Coloque esses aplicativos sob controle da TI e habilite o logon único para o gerenciamento de usuário.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5aa2f-115">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="5aa2f-115">How it works</span></span>
1. <span data-ttu-id="5aa2f-116">Os agentes de uso dos aplicativos são instalados nos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="5aa2f-117">informações de uso do aplicativo Hello capturadas por agentes de saudação são enviadas por um serviço do canal seguro, criptografado toohello cloud app discovery.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="5aa2f-118">Olá serviço Cloud App Discovery avalia Olá dados e gera relatórios.</span><span class="sxs-lookup"><span data-stu-id="5aa2f-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Diagrama do Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="5aa2f-120">tooget Introdução ao Cloud App Discovery, consulte [guia de Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="5aa2f-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="5aa2f-121">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="5aa2f-121">Related articles</span></span>
* [<span data-ttu-id="5aa2f-122">Considerações de privacidade e segurança no Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5aa2f-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="5aa2f-123">Guia de Implantação da Política de Grupo do Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5aa2f-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="5aa2f-124">Guia de Implantação do System Center do Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5aa2f-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="5aa2f-125">Configurações de Registro do Cloud App Discovery para Servidores Proxy com Portas Personalizadas</span><span class="sxs-lookup"><span data-stu-id="5aa2f-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="5aa2f-126">Cloud App Discovery - Log de Alteração de Agente </span><span class="sxs-lookup"><span data-stu-id="5aa2f-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="5aa2f-127">Cloud App Discovery - Perguntas Frequentes</span><span class="sxs-lookup"><span data-stu-id="5aa2f-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="5aa2f-128">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5aa2f-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

