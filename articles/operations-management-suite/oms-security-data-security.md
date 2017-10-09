---
title: "aaaOperations segurança do pacote de gerenciamento e segurança de dados de solução de auditoria | Microsoft Docs"
description: "Este documento explica como os dados são gerenciados e protegidos na Solução de Segurança e Auditoria do Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="2b140-103">Segurança de dados da solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2b140-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="2b140-104">impedir que clientes toohelp, detectar e responder toothreats, [Operations Management Suite (OMS) solução de segurança e auditoria](operations-management-suite-overview.md) coleta e processa os dados sobre seus recursos, que inclui:</span><span class="sxs-lookup"><span data-stu-id="2b140-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="2b140-105">Log de eventos de segurança</span><span class="sxs-lookup"><span data-stu-id="2b140-105">Security event log</span></span>
* <span data-ttu-id="2b140-106">Eventos de ETW (Rastreamento de Eventos para Windows)</span><span class="sxs-lookup"><span data-stu-id="2b140-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="2b140-107">Eventos de auditoria do AppLocker</span><span class="sxs-lookup"><span data-stu-id="2b140-107">AppLocker auditing events</span></span>
* <span data-ttu-id="2b140-108">Log do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="2b140-108">Windows Firewall log</span></span>
* <span data-ttu-id="2b140-109">Eventos de Análise de Ameaças Avançadas</span><span class="sxs-lookup"><span data-stu-id="2b140-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="2b140-110">Resultados da avaliação de linha de base</span><span class="sxs-lookup"><span data-stu-id="2b140-110">Results of baseline assessment</span></span>
* <span data-ttu-id="2b140-111">Resultados da avaliação antimalware</span><span class="sxs-lookup"><span data-stu-id="2b140-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="2b140-112">Resultados da avaliação de atualização/patch</span><span class="sxs-lookup"><span data-stu-id="2b140-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="2b140-113">Fluxos de syslogs explicitamente habilitados no agente Olá</span><span class="sxs-lookup"><span data-stu-id="2b140-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="2b140-114">Oferecemos a privacidade de saudação do investimento forte tooprotect e a segurança dos dados.</span><span class="sxs-lookup"><span data-stu-id="2b140-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="2b140-115">A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço.</span><span class="sxs-lookup"><span data-stu-id="2b140-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="2b140-116">Este artigo explica como os dados são gerenciados e protegidos na Solução de Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="2b140-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="2b140-117">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="2b140-117">Data sources</span></span>
<span data-ttu-id="2b140-118">OMS solução de segurança e auditoria analisam dados de suas máquinas virtuais e computadores físicos onde Olá agente do OMS está instalado.</span><span class="sxs-lookup"><span data-stu-id="2b140-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="2b140-119">A Solução de Segurança e Auditoria do OMS pode coletar informações de configuração sobre eventos de segurança, como eventos do Windows, logs de auditoria, logs do IIS e mensagens de syslog.</span><span class="sxs-lookup"><span data-stu-id="2b140-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="2b140-120">Exemplos desses dados são: tipo e versão de sistema operacional, processos em execução, nome do computador, endereços IP, usuário conectado e ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="2b140-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="2b140-121">Proteção de dados</span><span class="sxs-lookup"><span data-stu-id="2b140-121">Data protection</span></span>
<span data-ttu-id="2b140-122">**Diferenciação de dados**: dados são mantidos separados logicamente em cada componente serviço hello.</span><span class="sxs-lookup"><span data-stu-id="2b140-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="2b140-123">Todos os dados são marcados por organização.</span><span class="sxs-lookup"><span data-stu-id="2b140-123">All data is tagged per organization.</span></span> <span data-ttu-id="2b140-124">Essa marcação persiste em todo o ciclo de vida de dados de saudação e é imposta em cada camada de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="2b140-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="2b140-125">**Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="2b140-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="2b140-126">Cumprimento toohello [termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), que de estado que o Microsoft não usam dados do cliente ou derivar informações dele para qualquer anúncio ou semelhante fins comerciais.</span><span class="sxs-lookup"><span data-stu-id="2b140-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="2b140-127">recomendações de segurança tooprovide e investigar potenciais ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="2b140-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="2b140-128">Somente usamos os dados do cliente como necessário tooprovide você com o Azure de serviços, incluindo fins compatível com o fornecimento desses serviços.</span><span class="sxs-lookup"><span data-stu-id="2b140-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="2b140-129">Você manter todos os direitos tooyour próprios dados.</span><span class="sxs-lookup"><span data-stu-id="2b140-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="2b140-130">**Use dados**: a Microsoft usa os padrões e inteligência de ameaça Vista em vários locatários tooenhance nossos recursos de detecção e prevenção; fazemos acordo com os compromissos de privacidade de saudação descritos em nosso [privacidade Instrução](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b140-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2b140-131">Local de dados é configurado no nível de espaço de trabalho do OMS hello, durante a criação de espaço de trabalho hello, que faz parte da saudação inicial OMS segurança e auditoria processo de configuração.</span><span class="sxs-lookup"><span data-stu-id="2b140-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="2b140-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2b140-132">See also</span></span>
<span data-ttu-id="2b140-133">Neste documento, você aprendeu como os dados são gerenciados e protegidos no OMS.</span><span class="sxs-lookup"><span data-stu-id="2b140-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="2b140-134">toolearn mais sobre o OMS solução de segurança e auditoria, consulte:</span><span class="sxs-lookup"><span data-stu-id="2b140-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="2b140-135">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="2b140-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="2b140-136">Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria</span><span class="sxs-lookup"><span data-stu-id="2b140-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="2b140-137">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2b140-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

