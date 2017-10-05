---
title: "Validação de alertas na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento ajuda a validar os alertas de segurança na Central de Segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="837f3-103">Validação de alertas na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="837f3-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="837f3-104">Este documento ensina você a verificar se o sistema está configurado corretamente para os alertas da Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f3-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="837f3-105">O que são alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="837f3-105">What are security alerts?</span></span>
<span data-ttu-id="837f3-106">A Central de Segurança coleta, analisa e integra automaticamente os dados de registro de seus recursos do Azure, da rede e das soluções de parceiros conectados, como firewall e soluções de proteção de ponto de extremidade, a fim de detectar e alertar sobre ameaças.</span><span class="sxs-lookup"><span data-stu-id="837f3-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="837f3-107">Leia [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para saber mais sobre alertas de segurança e [Noções básicas sobre alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) para saber mais sobre os diferentes tipos de alertas.</span><span class="sxs-lookup"><span data-stu-id="837f3-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="837f3-108">Validação de alerta</span><span class="sxs-lookup"><span data-stu-id="837f3-108">Alert validation</span></span>
<span data-ttu-id="837f3-109">Depois que o agente da Central de Segurança for instalado no seu computador, siga as etapas abaixo no computador alvo do alerta:</span><span class="sxs-lookup"><span data-stu-id="837f3-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="837f3-110">Copie um arquivo executável (por exemplo, calc.exe) para a área de trabalho do computador ou outro diretório desejado.</span><span class="sxs-lookup"><span data-stu-id="837f3-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="837f3-111">Renomeie o arquivo como **ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="837f3-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="837f3-112">Abra o prompt de comando e execute o arquivo com um argumento (apenas um nome de argumento falso), como: *ASC_AlertTest_662jfi039N.exe -foo*</span><span class="sxs-lookup"><span data-stu-id="837f3-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="837f3-113">Aguarde 5 a 10 minutos e abra Alertas da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="837f3-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="837f3-114">Lá você deve encontrar um alerta semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="837f3-114">There you should find an alert similar to following one:</span></span>

    ![Validação de alerta](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="837f3-116">Ao revisar o alerta, verifique se o campo Auditoria de Argumentos Habilitada aparece como true.</span><span class="sxs-lookup"><span data-stu-id="837f3-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="837f3-117">Se ele mostra false, você precisa habilitar a auditoria de argumentos na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="837f3-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="837f3-118">Você pode habilitar essa opção usando a seguinte linha de comando:</span><span class="sxs-lookup"><span data-stu-id="837f3-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="837f3-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="837f3-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="837f3-120">Consulte também</span><span class="sxs-lookup"><span data-stu-id="837f3-120">See also</span></span>
<span data-ttu-id="837f3-121">Este artigo apresentou a você o processo de validação de alertas.</span><span class="sxs-lookup"><span data-stu-id="837f3-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="837f3-122">Agora que você está familiarizado com esse tipo de validação, experimente os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="837f3-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="837f3-123">[Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="837f3-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="837f3-124">Saiba como gerenciar alertas e responder a incidentes de segurança na Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="837f3-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="837f3-125">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="837f3-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="837f3-126">Saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f3-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="837f3-127">[Noções básicas de alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="837f3-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="837f3-128">Saiba mais sobre os diferentes tipos de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="837f3-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="837f3-129">[Guia de solução de problemas da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="837f3-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="837f3-130">Saiba como solucionar problemas comuns na Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="837f3-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="837f3-131">[Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="837f3-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="837f3-132">Encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="837f3-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="837f3-133">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="837f3-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="837f3-134">Encontre postagens no blog sobre a conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="837f3-134">Find blog posts about Azure security and compliance.</span></span>

