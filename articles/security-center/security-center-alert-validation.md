---
title: "aaaAlerts validação na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajudará a alertas de segurança Olá toovalidate na Central de segurança do Azure."
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
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="ed5a4-103">Validação de alertas na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ed5a4-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="ed5a4-104">Este documento ajuda você a aprender como tooverify se o sistema está configurado corretamente para os alertas da Central de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="ed5a4-105">O que são alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="ed5a4-105">What are security alerts?</span></span>
<span data-ttu-id="ed5a4-106">Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros conectados, como soluções de proteção de firewall e de ponto de extremidade, toodetect e alerta você toothreats.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="ed5a4-107">Leitura [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para obter mais informações sobre alertas de segurança e ler [Noções básicas sobre alertas de segurança na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn mais sobre os diferentes tipos de alertas hello.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="ed5a4-108">Validação de alerta</span><span class="sxs-lookup"><span data-stu-id="ed5a4-108">Alert validation</span></span>
<span data-ttu-id="ed5a4-109">Depois que a Central de segurança é instalado em seu computador, siga as etapas de saudação abaixo do computador Olá onde você deseja toobe Olá atacado recursos de alerta de saudação:</span><span class="sxs-lookup"><span data-stu-id="ed5a4-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="ed5a4-110">Copie um toohello executável (por exemplo calc.exe) da área de trabalho ou outro diretório de sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="ed5a4-111">Renomear esse arquivo também**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="ed5a4-112">Abra o prompt de comando hello e execute este arquivo com um argumento (apenas um nome de argumento falsa), como: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="ed5a4-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="ed5a4-113">Aguarde 5 minutos too10 e abra alertas da Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="ed5a4-114">Lá, você deve encontrar um alerta toofollowing semelhante um:</span><span class="sxs-lookup"><span data-stu-id="ed5a4-114">There you should find an alert similar toofollowing one:</span></span>

    ![Validação de alerta](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="ed5a4-116">Ao revisar este alerta, certifique-se de campo Olá argumentos auditoria habilitada aparece como true.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="ed5a4-117">Se ele mostra falso, será necessário tooenable argumentos de linha de comando de auditoria.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="ed5a4-118">Você pode habilitar essa opção usando Olá linha de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed5a4-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="ed5a4-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="ed5a4-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="ed5a4-120">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ed5a4-120">See also</span></span>
<span data-ttu-id="ed5a4-121">Este artigo introduzido toohello processo de validação de alertas.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="ed5a4-122">Agora que você estiver familiarizado com esse tipo de validação, tente Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed5a4-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="ed5a4-123">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="ed5a4-124">Saiba como toomanage alertas e responder toosecurity incidentes na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="ed5a4-125">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="ed5a4-126">Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ed5a4-127">[Noções básicas de alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="ed5a4-128">Saiba mais sobre os diferentes tipos de saudação de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="ed5a4-129">[Guia de solução de problemas da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="ed5a4-130">Saiba como tootroubleshoot comum problemas na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="ed5a4-131">[Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="ed5a4-132">Localize as perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ed5a4-133">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="ed5a4-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="ed5a4-134">Encontre postagens no blog sobre a conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5a4-134">Find blog posts about Azure security and compliance.</span></span>

