---
title: "integração de log de alertas do aaaIntegrating Central de segurança do Azure com o Azure | Microsoft Docs"
description: "Este artigo ajuda você a integrar alertas da Central de Segurança com a integração de log do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Integração de alertas da Central de Segurança do Azure com a integração de log do Azure
Muitas operações de segurança e as equipes de resposta a incidentes se baseiam em uma solução de gerenciamento de eventos (SIEM) e informações de segurança Olá ponto de partida para separação e investigando os alertas de segurança. Com a Integração de Log do Azure, você pode integrar alertas da Central de Segurança do Azure com sua solução SIEM.

A Integração de Log do Azure atualmente dá suporte a HP ArcSight, Splunk e QRadar da IBM.

## <a name="what-logs-can-i-integrate"></a>Quais logs posso integrar?
Azure produz um log abrangente para cada serviço. Esses logs são categorizados como:

* **Logs de gerenciamento do controle** que ofereçam visibilidade em Olá operações do Azure Resource Manager CREATE, UPDATE e DELETE. Esses eventos de plano de controle são apresentados em Olá Logs de atividade do Azure
* **Logs do plano de dados** que ofereçam visibilidade em eventos Olá gerado ao usar um recurso do Azure. Um exemplo é o log de eventos do Windows hello, onde você pode obter informações sobre eventos de segurança de canal de segurança do Visualizador de eventos hello. Eventos de plano de dados (que são gerados por uma máquina virtual ou um serviço do Azure) são exibidos pelos Logs de Diagnóstico do Azure.

Integração do log do Azure atualmente oferece suporte à integração de saudação do:

* Logs da VM do Azure
* Logs de Auditoria do Azure
* Alertas da Central de Segurança do Azure

## <a name="install-azure-log-integration"></a>Instalar a integração do log do Azure
Baixe a [integração do log do Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Olá serviço de integração do Azure log coleta dados de telemetria do computador de saudação no qual ele está instalado.  Os dados de telemetria coletados são:

* Exceções que ocorrem durante a execução da integração do log do Azure
* Métricas sobre o número de saudação de consultas e eventos processados
* Estatísticas sobre quais opções da linha de comando do Azlog.exe estão sendo usadas

> [!NOTE]
> Você pode desativar a coleta dos dados de telemetria desmarcando essa opção.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integrar os Logs de Auditoria do Azure e os alertas da Central de Segurança
1. Prompt de comando aberta hello e **cd** em **c:\Program Files\Microsoft Azure Log integração**.
2. Executar Olá **azlog createazureid** comando toocreate um [entidade de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md) em hello Azure AD (Active Directory) locatários que hospedam Olá assinaturas do Azure.

    Você deverá inserir seu logon do Azure.

   > [!NOTE]
   > Você deve ser o proprietário de assinatura de saudação ou um Coadministrador de assinatura de saudação.
   >
   >

    Autenticação tooAzure é feito por meio do AD do Azure.  Criar uma entidade de serviço para a integração do Azure log cria a identidade do AD do Azure Olá recebe acesso tooread de assinaturas do Azure.
3. Executar Olá **azlog autorizar <SubscriptionID>**  comando acesso de leitor de tooassign na entidade de serviço Olá assinatura toohello criado na etapa 2. Se você não especificar um **SubscriptionID**, entidade de serviço Olá será atribuído Olá leitor função tooall assinaturas toowhich você tem acesso.

   > [!NOTE]
   > Você pode ver avisos se você executar Olá **autorizar** comando imediatamente após Olá **createazureid** comando. Há alguma latência entre quando a conta de saudação do AD do Azure é criada e quando a conta de saudação está disponível para uso. Se você esperar cerca de 10 segundos depois de executar Olá **createazureid** saudação do comando toorun **autorizar** de comando, em seguida, você não deve ver esses avisos.
   >
   >
4. Verificar Olá tooconfirm pastas que Olá log de auditoria arquivos JSON a seguir existem:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Verificar Olá tooconfirm pastas alertas da Central de segurança existentes no-los a seguir:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Configure Olá SIEM arquivo encaminhador conector toohello pasta apropriada. procedimento Olá irão variar dependendo da saudação SIEM que você está usando.

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre Logs de atividades do Azure e definições de propriedade, consulte:

* [Operações de auditoria com o Gerenciador de Recursos](../azure-resource-manager/resource-group-audit.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — Obtenha notícias mais recentes de segurança do Azure hello e informações.
