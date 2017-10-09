---
title: "aaaAzure serviço Central de segurança e o banco de dados do SQL Azure | Microsoft Docs"
description: "Este artigo mostra como a Central de Segurança pode ajudar você a proteger seus bancos de dados no Banco de Dados SQL."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Central de Segurança do Azure e serviço do Banco de Dados SQL
[Central de segurança do Azure](https://azure.microsoft.com/documentation/services/security-center/) ajuda a evitar, detectar e responder toothreats. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Este artigo mostra como a Central de Segurança pode ajudar você a proteger seus bancos de dados no Banco de Dados SQL.

## <a name="why-use-security-center"></a>Por que usar a Central de Segurança?
Central de segurança ajuda a proteger os dados no banco de dados SQL, fornecendo a visibilidade de segurança de saudação de todos os servidores e bancos de dados. Com a Central de Segurança, você pode:

* Definir políticas de criptografia e auditoria do Banco de Dados SQL.
* Monitorar a segurança de saudação de recursos de banco de dados SQL em todas as suas assinaturas.
* Identifique e corrija rapidamente problemas de segurança.
* Integre os alertas da [detecção de ameaças do Banco de Dados SQL](../sql-database/sql-database-threat-detection.md).

Além disso, toohelping proteger seus recursos de banco de dados SQL, a Central de segurança também fornece monitoramento de segurança e gerenciamento de máquinas virtuais do Azure, serviços de nuvem, serviços de aplicativos, redes virtuais e muito mais. Saiba mais sobre a Central de Segurança [aqui](security-center-intro.md).

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado com a Central de segurança, você deve ter um tooMicrosoft de assinatura do Azure. a camada gratuita Olá da Central de segurança está habilitada com a sua assinatura. Para saber mais sobre as camadas Gratuito e Standard da Central de Segurança, confira [Preços da Central de Segurança](https://azure.microsoft.com/pricing/details/security-center/).

A Central de segurança dá suporte ao acesso baseado em função. toolearn mais sobre o controle de acesso baseado em função (RBAC) no Azure, consulte [controle de acesso baseado em função do Azure Active Directory](../active-directory/role-based-access-control-configure.md). Olá perguntas frequentes sobre o Centro de segurança fornece informações sobre [como as permissões são tratadas na Central de segurança](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Acessar a Central de Segurança
Acessar a Central de segurança do hello [portal do Azure](https://azure.microsoft.com/features/azure-portal/). [Entrar no portal de toohello](https://portal.azure.com/) e selecione hello **opção central de segurança**.

![Opção da Central de Segurança][1]

Olá **Central de segurança** folha é aberta.
![Folha Central de Segurança][2]

## <a name="set-security-policy"></a>Definir políticas de segurança
Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura ou grupo de recursos. Central de segurança, você define para suas assinaturas ou grupos de recursos da empresa tooyour as necessidades de segurança e tipo de saudação de aplicativos ou confidencialidade dos dados de saudação em cada assinatura de acordo com as políticas.

Você pode definir uma política tooshow recomendações para a auditoria do SQL e criptografia de dados transparente (TDE) do SQL.

* Quando você ativa **detecção de ameaças e a auditoria do SQL**, Central de segurança recomenda que a auditoria de acesso tooAzure banco de dados esteja habilitada para conformidade, avançados de detecção e fins de investigação.
* Quando você ativa a **Transparent Data Encryption do SQL**, a Central de Segurança recomenda que a criptografia em repouso seja habilitada para o Banco de Dados SQL, backups associados e arquivos do log de transação.

tooset uma política de segurança, selecione Olá **política** lado a lado na folha da Central de segurança de saudação. Em Olá **política de segurança** folha, no qual você deseja tooenable política de segurança de saudação de assinatura de Olá select. Selecione **política de prevenção de** e ativar **em** Olá recomendações de segurança que você deseja toouse esta assinatura.
![Política de segurança][3]

mais, consulte toolearn [definir políticas de segurança](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Gerenciar recomendações de segurança
Central de segurança periodicamente analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações. recomendações de saudação orientará você durante processo de saudação do configurando controles de saudação necessário.

Depois de definir uma política de segurança, Central de segurança analisa o estado de segurança Olá seus recursos tooidentify as vulnerabilidades potenciais. recomendações de saudação são exibidas em um formato de tabela em que cada linha representa uma recomendação específica. Use Olá a tabela a seguir como um toohelp referência que entender recomendações de saudação disponível para o banco de dados do SQL Azure, e que cada recomendação não se aplicar. Selecionar uma recomendação leva tooan artigo que explica como tooimplement Olá recomendação na Central de segurança.

| Recomendações | Descrição |
| --- | --- |
| [Habilitar a detecção de ameaças e auditoria em servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomenda que você ative a detecção de ameaças e a auditoria para servidores do Banco de Dados SQL. (Somente o serviço do Banco de Dados SQL. Não inclui o Microsoft SQL Server em execução nas máquinas virtuais.) |
| [Habilitar a detecção de ameaças e auditoria em Bancos de Dados SQL](security-center-enable-auditing-on-sql-databases.md) |Recomenda que você ative a detecção de ameaças e a auditoria para bancos de dados do Banco de Dados SQL. (Somente o serviço do Banco de Dados SQL. Não inclui o Microsoft SQL Server em execução nas máquinas virtuais.) |
| [Habilitar Transparent Data Encryption](security-center-enable-transparent-data-encryption.md) |Recomenda que você habilite a criptografia para bancos de dados SQL. (Somente o serviço do Banco de Dados SQL.) |

recomendações de toosee para seus recursos do Azure, selecione Olá **recomendações** lado a lado na folha da Central de segurança de saudação. Em Olá **recomendações** folha, selecione os detalhes de toosee uma recomendação. Neste exemplo, vamos selecionar **Habilitar Auditoria e Detecção de ameaça em servidores SQL**.

![Recomendações][4]

Como mostrado abaixo, Central de segurança mostra Olá servidores SQL em que a detecção de ameaças e auditoria não estão habilitados. Após você ativa a auditoria, você pode definir as configurações de detecção de ameaças e alertas de segurança de tooreceive de configurações de email. A detecção de ameaças alerta quando detecta atividades anômalas de banco de dados que indicam as ameaças de segurança potencial toohello dados. Olá alertas são exibidos no painel de Central de segurança hello.
![Auditoria e detecção de ameaças][5]

Siga as etapas de saudação em [detecção de ameaças do banco de dados SQL no portal do Azure de saudação](../sql-database/sql-database-threat-detection-portal.md) tooturn em e configurar a detecção de ameaças e lista de saudação tooconfigure de endereços de email que receberão alertas de segurança após a detecção de atividades anormais.

toolearn mais informações sobre recomendações, consulte [Gerenciando recomendações de segurança](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Monitorar integridade da segurança
Depois de habilitar [políticas de segurança](security-center-policies.md) para recursos de uma assinatura, a Central de segurança analisará segurança Olá das vulnerabilidades potenciais tooidentify recursos.  Você pode exibir o estado de segurança de saudação de seus recursos no hello **integridade da segurança do recurso** lado a lado. Quando você clica em **dados** em Olá **integridade da segurança do recurso** lado a lado, hello **dados recursos** folha é aberta com as recomendações do SQL para problemas como a auditoria e transparente criptografia de dados não está habilitada. Ele também apresenta recomendações para estado de integridade geral de saudação do banco de dados de saudação.
![Integridade da segurança de recursos][6]

mais, consulte toolearn [monitoramento de integridade de segurança](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Gerenciar e responder a alertas de toosecurity
Central de segurança automaticamente coleta, analisa e integra dados de log de [detecção de ameaças do SQL Azure](../sql-database/sql-database-threat-detection.md), bem como outros recursos do Azure, ameaças reais toodetect e reduzir falsos positivos. É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema hello e recomendações sobre como tooremediate um ataque.

toosee alertas, selecione Olá **alertas de segurança** lado a lado na folha da Central de segurança de saudação. Em Olá **alertas de segurança** folha, selecione um alerta toolearn mais informações sobre eventos de saudação que disparou o alerta hello e, se houver, etapas que você precisa tootake tooremediate um ataque. Neste exemplo, vamos selecionar **Possível injeção de SQL**.
![Alertas de segurança][7]

Conforme mostrado abaixo, a Central de segurança fornece detalhes adicionais que oferecem informações sobre quais alerta disparado Olá, hello destino recursos, quando aplicável Olá fonte de endereço IP e recomendações sobre como tooremediate.
![Possível injeção de SQL][8]

mais, consulte toolearn [está respondendo e gerenciar alertas de toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Próximas etapas
* [Perguntas frequentes sobre o Centro de segurança](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Guia de planejamento e operações da Central de segurança](security-center-planning-and-operations-guide.md) - seguem um conjunto de etapas e tarefas toooptimize o uso da Central de segurança com base em requisitos de segurança da sua organização e o modelo de gerenciamento de nuvem.
* [Segurança de dados da Central de Segurança](security-center-data-security.md) - Saiba como a Central de Segurança coleta e processa dados sobre os recursos do Azure, incluindo informações da configuração, metadados, logs de eventos, arquivos de despejo corrompidos e mais.
* [Lidar com incidentes de segurança](security-center-incident.md) -Saiba como segurança de saudação toouse alerta recurso na Central de segurança tooassist você lidar com incidentes de segurança.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
