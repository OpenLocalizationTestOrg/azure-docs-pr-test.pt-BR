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
# <a name="alerts-validation-in-azure-security-center"></a>Validação de alertas na Central de Segurança do Azure
Este documento ajuda você a aprender como tooverify se o sistema está configurado corretamente para os alertas da Central de segurança do Azure.

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros conectados, como soluções de proteção de firewall e de ponto de extremidade, toodetect e alerta você toothreats. Leitura [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para obter mais informações sobre alertas de segurança e ler [Noções básicas sobre alertas de segurança na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn mais sobre os diferentes tipos de alertas hello.

## <a name="alert-validation"></a>Validação de alerta
Depois que a Central de segurança é instalado em seu computador, siga as etapas de saudação abaixo do computador Olá onde você deseja toobe Olá atacado recursos de alerta de saudação:

1. Copie um toohello executável (por exemplo calc.exe) da área de trabalho ou outro diretório de sua conveniência.
2. Renomear esse arquivo também**ASC_AlertTest_662jfi039N.exe**.
3. Abra o prompt de comando hello e execute este arquivo com um argumento (apenas um nome de argumento falsa), como: *ASC_AlertTest_662jfi039N.exe - foo*
4. Aguarde 5 minutos too10 e abra alertas da Central de segurança. Lá, você deve encontrar um alerta toofollowing semelhante um:

    ![Validação de alerta](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Ao revisar este alerta, certifique-se de campo Olá argumentos auditoria habilitada aparece como true. Se ele mostra falso, será necessário tooenable argumentos de linha de comando de auditoria. Você pode habilitar essa opção usando Olá linha de comando a seguir:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Consulte também
Este artigo introduzido toohello processo de validação de alertas. Agora que você estiver familiarizado com esse tipo de validação, tente Olá artigos a seguir:

* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Saiba como toomanage alertas e responder toosecurity incidentes na Central de segurança.
* [Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md). Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Noções básicas de alertas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Saiba mais sobre os diferentes tipos de saudação de alertas de segurança.
* [Guia de solução de problemas da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Saiba como tootroubleshoot comum problemas na Central de segurança. 
* [Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md). Localize as perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre postagens no blog sobre a conformidade e segurança do Azure.

