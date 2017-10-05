---
title: "Encontrando aplicativos em nuvem não gerenciados com o Cloud App Discovery | Microsoft Docs"
description: "Fornece informações sobre a localização e o gerenciamento de aplicativos com o Cloud App Discovery, quais são seus benefícios e como ele funciona."
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="a08dd-104">Encontrando aplicativos em nuvem não gerenciados com o Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="a08dd-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="a08dd-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a08dd-105">Overview</span></span>
<span data-ttu-id="a08dd-106">Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos em nuvem que os membros de sua organização usam para realizar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="a08dd-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="a08dd-107">É fácil ver por que os administradores teriam preocupações sobre o acesso não autorizado aos dados corporativos, perda de dados e outros riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="a08dd-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="a08dd-108">Essa falta de reconhecimento pode fazer com que a criação de um plano para lidar com esses riscos de segurança pareça assustadora.</span><span class="sxs-lookup"><span data-stu-id="a08dd-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="a08dd-109">O Cloud App Discovery é um recurso Premium do Active Directory (AD) do Azure que permite descobrir os aplicativos em nuvem usados pelas pessoas em sua organização.</span><span class="sxs-lookup"><span data-stu-id="a08dd-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="a08dd-110">**Com o Cloud App Discovery é possível:**</span><span class="sxs-lookup"><span data-stu-id="a08dd-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="a08dd-111">Descubra os aplicativos em nuvem usados e meça o uso pelo número de usuários, volume de tráfego ou número de solicitações Web para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a08dd-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="a08dd-112">Identificar os usuários que estão usando um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a08dd-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="a08dd-113">Exporte os dados para a análise offline.</span><span class="sxs-lookup"><span data-stu-id="a08dd-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="a08dd-114">Coloque esses aplicativos sob controle da TI e habilite o logon único para o gerenciamento de usuário.</span><span class="sxs-lookup"><span data-stu-id="a08dd-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a08dd-115">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="a08dd-115">How it works</span></span>
1. <span data-ttu-id="a08dd-116">Os agentes de uso dos aplicativos são instalados nos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="a08dd-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="a08dd-117">As informações de uso do aplicativo coletadas pelos agentes são enviadas por um canal criptografado seguro para o serviço Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="a08dd-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="a08dd-118">O serviço Cloud App Discovery avalia os dados e gera relatórios.</span><span class="sxs-lookup"><span data-stu-id="a08dd-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Diagrama do Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="a08dd-120">Para iniciar com o Cloud App Discovery, confira [Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="a08dd-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="a08dd-121">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="a08dd-121">Related articles</span></span>
* [<span data-ttu-id="a08dd-122">Considerações de privacidade e segurança no Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="a08dd-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="a08dd-123">Guia de Implantação da Política de Grupo do Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="a08dd-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="a08dd-124">Guia de Implantação do System Center do Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="a08dd-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="a08dd-125">Configurações de Registro do Cloud App Discovery para Servidores Proxy com Portas Personalizadas</span><span class="sxs-lookup"><span data-stu-id="a08dd-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="a08dd-126">Cloud App Discovery - Log de Alteração de Agente </span><span class="sxs-lookup"><span data-stu-id="a08dd-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="a08dd-127">Cloud App Discovery - Perguntas Frequentes</span><span class="sxs-lookup"><span data-stu-id="a08dd-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="a08dd-128">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a08dd-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

