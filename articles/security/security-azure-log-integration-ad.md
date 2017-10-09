---
title: "aaaAzure integração de Log com os logs de auditoria do Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooinstall Olá serviço de integração de Log do Azure e integrar os logs de logs de auditoria do Azure"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integrar o Azure Active Directory a logs de auditoria

Eventos de auditoria do Azure AD (Azure Active Directory) ajudam a identificar ações privilegiadas que ocorreram no Azure Active Directory. Você pode ver Olá tipos de eventos que você pode acompanhar revisando [eventos de relatório de auditoria do Active Directory do Azure](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Antes de tentar etapas Olá neste artigo, você deve revisar Olá [começar](security-azure-log-integration-get-started.md) artigo e concluir as etapas hello.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Logs de auditoria do Azure Active directory do etapas toointegrate

1. Abra o prompt de comando hello e execute este comando:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Execute este comando: 
 
   ``azlog createazureid``

   Esse comando solicitará o logon do Azure. Olá comando cria um Azure Active Directory entidade de serviço nos locatários de saudação do AD do Azure que hospedam Olá no qual Olá usuário conectado é um administrador, um coadministrador ou um proprietário de assinaturas do Azure. comando Olá falhará se o usuário que fez logon Olá é apenas um usuário convidado no locatário do AD do Azure hello. Autenticação tooAzure é feito por meio do AD do Azure. Criar uma entidade de serviço para a integração do Azure Log cria Olá identidade do AD do Azure que recebe acesso tooread de assinaturas do Azure.

3. Comando a seguir de execução Olá tooprovide sua ID de locatário. Você precisa de membro toobe do comando de Olá Olá locatário admin função toorun.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Exemplo:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Verificar Olá tooconfirm pastas que Olá arquivos de JSON de log de auditoria do Azure Active Directory a seguir é criada no-los:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hello vídeo a seguir demonstra as etapas de saudação abordadas neste artigo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Para obter instruções específicas sobre colocar informações de saudação nos arquivos de JSON de saudação em seu sistema de gerenciamento (SIEM) de eventos e informações de segurança, contate o fornecedor do SIEM.

Ajuda da comunidade está disponível por meio de saudação [Fórum do MSDN de integração do Azure Log](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Este fórum permite que as pessoas em hello Azure Log integração da comunidade toosupport uns aos outros com perguntas, respostas, dicas e truques. Além disso, a equipe de integração do Azure Log Olá monitora este fórum e ajuda sempre que possível.

Você também pode abrir uma [solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md). Selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a integração de Log do Azure, consulte:

* [Integração de Logs do Microsoft Azure para os logs do Azure](https://www.microsoft.com/download/details.aspx?id=53324): a página Centro de Download oferece os detalhes, os requisitos de sistema e as instruções de instalação da Integração de Logs do Azure.
* [Introdução tooAzure Log integração](security-azure-log-integration-overview.md): Este artigo apresenta tooAzure integração de Log, seus principais recursos e como ele funciona.
* [Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta postagem de blog mostra como o tooconfigure toowork de integração de Log do Azure com soluções Splunk, HP ArcSight e IBM QRadar de parceiros.
* [Perguntas frequentes sobre a Integração do Log do Azure](security-azure-log-integration-faq.md): este artigo responde perguntas sobre a Integração do Log do Azure.
* [Integração de alertas da Central de segurança com a integração do Azure Log](../security-center/security-center-integrating-alerts-with-log-integration.md): Este artigo mostra como alertas da Central de segurança toosync, juntamente com coletados pelo diagnóstico do Azure e logs de auditoria do Azure, com a análise de log de eventos de segurança de máquina virtual ou Solução SIEM.
* [Logs de auditoria de novos recursos de diagnóstico do Azure e o Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta postagem de blog apresenta tooAzure os logs de auditoria e outros recursos que ajudarão a obtém ideias sobre operações de saudação de seus recursos do Azure.
