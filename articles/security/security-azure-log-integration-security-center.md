---
title: "aaaAzure integração de Log com a Central de segurança | Microsoft Docs"
description: "Saiba como tooget segurança do Azure center trabalhando com a integração do Log de alertas"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Como tooget a Central de segurança alertas na integração de log do Azure
Este artigo fornece serviço Olá etapas tooenable necessário Olá integração do Azure Log toopull informações de alerta de segurança geradas pelo Centro de segurança do Azure. Você deve ter concluído com êxito etapas Olá Olá [começar](security-azure-log-integration-get-started.md) artigo antes de executar as etapas de saudação neste artigo.

## <a name="detailed-steps"></a>Etapas detalhadas
Olá etapas a seguir criará Olá necessário entidade de serviço do Azure Active Directory e permissões de leitura do atribuir Olá SPN toohello assinatura:
1. Abra o prompt de comando hello e navegue muito**c:\Program Files\Microsoft Azure Log integração**
2. Execute o comando Olá``azlog createazureid``

    Esse comando solicitará o logon do Azure. comando Hello, em seguida, cria um [entidade de serviço do Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) em Olá locatários do AD do Azure que hospedam Olá no qual Olá usuário conectado no é um administrador, um Coadministrador ou um proprietário de assinaturas do Azure. comando Olá falhará se Olá usuário conectado no é apenas um usuário convidado em Olá locatário do AD do Azure. Autenticação tooAzure é feito por meio do Azure AD (Active Directory). Criar uma entidade de serviço para a integração de Azlog cria Olá identidade do AD do Azure que terá acesso tooread de assinaturas do Azure.

2. Em seguida, você executará um comando que atribui acesso leitor na entidade de serviço Olá assinatura toohello criado na etapa 2. Se você não especificar um SubscriptionID, o comando Olá tentará tooassign Olá serviço principal leitor função tooall assinaturas toowhich tenha acesso. </br></br>
``azlog authorize <SubscriptionID>`` </br> por exemplo </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Você pode ver avisos se você executar Olá autorizar comando imediatamente após o comando de createazureid hello. Há alguma latência entre quando a conta de saudação do AD do Azure é criada e quando a conta de saudação está disponível para uso. Se você Espere cerca de 60 segundos após a execução de saudação do hello createazureid comando toorun autorizar o comando, você não deve ver esses avisos.

4. Verificar Olá tooconfirm pastas que Olá log de auditoria arquivos JSON a seguir existem:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Verificar Olá tooconfirm pastas alertas da Central de segurança existentes no-los a seguir:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Se você tiver algum problema durante a saudação de instalação e configuração, abra um [solicitação de suporte](/azure-supportability/how-to-create-azure-support-request.md), selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a integração de Log do Azure, consulte Olá documentos a seguir:

* [Integração de log do Microsoft Azure para os logs do Azure](https://www.microsoft.com/download/details.aspx?id=53324) – visite o Centro de Download para obter os detalhes, os requisitos de sistema e as instruções de instalação da integração de log do Azure.
* [Integração do log de Introdução tooAzure](security-azure-log-integration-overview.md) – este documento apresenta a integração do registro tooAzure, seus principais recursos e como ele funciona.
* [Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – esta postagem de blog mostra como tooconfigure Azure log toowork integração com soluções de parceiros Splunk, HP ArcSight e IBM QRadar.
* [Perguntas frequentes sobre o log de integração do Azure](security-azure-log-integration-faq.md) – encontre as respostas para as perguntas frequentes sobre a integração de log do Azure.
* [Integração Central de segurança do log de alertas com o Azure Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – este documento mostra como alertas da Central de segurança toosync, juntamente com coletados pelo diagnóstico do Azure e os Logs de auditoria do Azure, com a análise de log de eventos de segurança de máquina virtual ou Solução SIEM.
* [Novos recursos de diagnóstico do Azure e os Logs de auditoria do Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – esta postagem de blog apresenta tooAzure os Logs de auditoria e outros recursos que ajudarão a obtém ideias sobre operações de saudação de seus recursos do Azure.
