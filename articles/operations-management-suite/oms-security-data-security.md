---
title: "Segurança de Dados de Solução de Segurança e Auditoria do Operations Management Suite | Microsoft Docs"
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
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="851cf-103">Segurança de dados da solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="851cf-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="851cf-104">Para ajudar os clientes a evitar, detectar e responder a ameaças, a [solução de Segurança e Auditoria do OMS (Operations Management Suite)](operations-management-suite-overview.md) coleta e processa dados sobre seus recursos, o que inclui:</span><span class="sxs-lookup"><span data-stu-id="851cf-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="851cf-105">Log de eventos de segurança</span><span class="sxs-lookup"><span data-stu-id="851cf-105">Security event log</span></span>
* <span data-ttu-id="851cf-106">Eventos de ETW (Rastreamento de Eventos para Windows)</span><span class="sxs-lookup"><span data-stu-id="851cf-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="851cf-107">Eventos de auditoria do AppLocker</span><span class="sxs-lookup"><span data-stu-id="851cf-107">AppLocker auditing events</span></span>
* <span data-ttu-id="851cf-108">Log do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="851cf-108">Windows Firewall log</span></span>
* <span data-ttu-id="851cf-109">Eventos de Análise de Ameaças Avançadas</span><span class="sxs-lookup"><span data-stu-id="851cf-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="851cf-110">Resultados da avaliação de linha de base</span><span class="sxs-lookup"><span data-stu-id="851cf-110">Results of baseline assessment</span></span>
* <span data-ttu-id="851cf-111">Resultados da avaliação antimalware</span><span class="sxs-lookup"><span data-stu-id="851cf-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="851cf-112">Resultados da avaliação de atualização/patch</span><span class="sxs-lookup"><span data-stu-id="851cf-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="851cf-113">Fluxos de Syslogs habilitados explicitamente no agente</span><span class="sxs-lookup"><span data-stu-id="851cf-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="851cf-114">Estamos comprometidos com a proteção da privacidade e da segurança dos dados.</span><span class="sxs-lookup"><span data-stu-id="851cf-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="851cf-115">A Microsoft obedece às diretrizes rígidas de conformidade e segurança — da codificação à operação de um serviço.</span><span class="sxs-lookup"><span data-stu-id="851cf-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="851cf-116">Este artigo explica como os dados são gerenciados e protegidos na Solução de Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="851cf-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="851cf-117">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="851cf-117">Data sources</span></span>
<span data-ttu-id="851cf-118">A Solução de Segurança e Auditoria do OMS analisa dados de máquinas virtuais e computadores físicos em que o Agente do OMS está instalado.</span><span class="sxs-lookup"><span data-stu-id="851cf-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="851cf-119">A Solução de Segurança e Auditoria do OMS pode coletar informações de configuração sobre eventos de segurança, como eventos do Windows, logs de auditoria, logs do IIS e mensagens de syslog.</span><span class="sxs-lookup"><span data-stu-id="851cf-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="851cf-120">Exemplos desses dados são: tipo e versão de sistema operacional, processos em execução, nome do computador, endereços IP, usuário conectado e ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="851cf-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="851cf-121">Proteção de dados</span><span class="sxs-lookup"><span data-stu-id="851cf-121">Data protection</span></span>
<span data-ttu-id="851cf-122">**Segregação dos dados**: os dados são mantidos separados logicamente em cada componente em todo o serviço.</span><span class="sxs-lookup"><span data-stu-id="851cf-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="851cf-123">Todos os dados são marcados por organização.</span><span class="sxs-lookup"><span data-stu-id="851cf-123">All data is tagged per organization.</span></span> <span data-ttu-id="851cf-124">Essa marcação persiste em todo o ciclo de vida dos dados e é imposta em cada camada do serviço.</span><span class="sxs-lookup"><span data-stu-id="851cf-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="851cf-125">**Acesso a dados**: para fornecer recomendações de segurança e investigar possíveis ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="851cf-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="851cf-126">Seguimos os [Termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e a [Política de Privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), que determinam que a Microsoft não usará os Dados do Cliente nem obterá as informações para fins comerciais ou de propaganda semelhantes.</span><span class="sxs-lookup"><span data-stu-id="851cf-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="851cf-127">Para fornecer recomendações de segurança e investigar possíveis ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços.</span><span class="sxs-lookup"><span data-stu-id="851cf-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="851cf-128">Somente usamos os Dados do Cliente conforme o necessário para fornecer os serviços do Azure, inclusive para fins compatíveis com o fornecimento desses serviços.</span><span class="sxs-lookup"><span data-stu-id="851cf-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="851cf-129">Você mantém todos os direitos a seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="851cf-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="851cf-130">**Uso dos dados**: A Microsoft usa os padrões e a inteligência de ameaças vistos em vários locatários para aprimorar os recursos de detecção e prevenção. Fazemos isso de acordo com os compromissos de privacidade descritos em nossa [Política de Privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="851cf-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="851cf-131">O local dos dados é configurado no nível do espaço de trabalho do OMS, durante a criação do espaço de trabalho, que faz parte do processo de configuração inicial de Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="851cf-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="851cf-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="851cf-132">See also</span></span>
<span data-ttu-id="851cf-133">Neste documento, você aprendeu como os dados são gerenciados e protegidos no OMS.</span><span class="sxs-lookup"><span data-stu-id="851cf-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="851cf-134">Para saber mais sobre a solução de Segurança e Auditoria do OMS, confira:</span><span class="sxs-lookup"><span data-stu-id="851cf-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="851cf-135">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="851cf-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="851cf-136">Monitorando e respondendo a alertas de segurança na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="851cf-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="851cf-137">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="851cf-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

