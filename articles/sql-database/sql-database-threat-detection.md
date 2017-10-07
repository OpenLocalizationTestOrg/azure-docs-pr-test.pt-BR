---
title: "aaaThreat detecção - banco de dados do SQL Azure | Microsoft Docs"
description: "Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>Detecção de Ameaças do Banco de Dados SQL

SQL a detecção de ameaças detecta atividades anormais indicando tentativas incomuns e potencialmente prejudiciais tooaccess ou exploração bancos de dados.

## <a name="overview"></a>Visão geral

Detecção de ameaças SQL fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais.  Os usuários receberão um alerta mediante atividades suspeitas em bancos de dados, possíveis vulnerabilidades e ataques de injeção de SQL, bem como padrões anômalos de acesso ao banco de dados. Alertas de detecção de ameaças SQL fornecer detalhes de atividade suspeita e recomendarão a ação sobre como tooinvestigate e atenuar a ameaça de saudação. Os usuários podem explorar eventos suspeitos de saudação usando [auditoria de banco de dados SQL](sql-database-auditing.md) toodetermine se eles são provenientes de uma tentativa tooaccess, violação ou explorar dados no banco de dados de saudação. A detecção de ameaças torna simples tooaddress potenciais ameaças toohello banco de dados sem a necessidade de saudação toobe um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançada.

Por exemplo, injeção de SQL é um Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados. Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, serem violados ou modificar dados no banco de dados de saudação.

Detecção de ameaças SQL integra alertas com [Central de segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/), e, cada servidor de banco de dados SQL protegido será cobrado com hello mesmo preço como camada padrão do Centro de segurança do Azure, em r $15/nó/mês, onde cada protegido SQL Servidor de banco de dados é contado como um nó. Você está convidado tootry-lo por 60 dias para liberar. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Configurar a detecção de ameaças do banco de dados em Olá portal do Azure
1. Iniciar hello Azure portal em [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello folha de configuração de saudação deseja toomonitor do banco de dados do SQL. Na folha de configurações hello, selecione **auditoria e detecção de ameaças**. 
    ![Painel de navegação][1]
3. Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibe as configurações de detecção de ameaças hello.
  
    ![Painel de navegação][2]
4. **ATIVE** a Detecção de ameaças.
5. Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades anormais de banco de dados.
6. Clique em **salvar** em Olá **detecção de auditoria e ameaças** toosave folha Olá novas ou atualizadas configurações de detecção de ameaças e auditoria.
       
    ![Painel de navegação][3]

## <a name="set-up-threat-detection-using-powershell"></a>Configurar a detecção de ameaças usando o PowerShell

Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Explore as atividades anormais do banco de dados na detecção de um evento suspeito
1. Você receberá uma notificação por email na detecção das atividades anormais do banco de dados. <br/>
   email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, nome do servidor, nome do aplicativo e tempo de evento de saudação. Além disso, email Olá fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de.<br/>
     
    ![Painel de navegação][4]
2. alerta de email Olá inclui um log de auditoria do SQL toohello vínculo direto. Clicando em Olá de inicia esse link do Azure portal e abre Olá SQL registros de auditoria em torno de tempo de saudação do evento suspeitas hello. Clique em um tooview de registro de auditoria para obter mais detalhes sobre as atividades de banco de dados suspeito hello, tornando mais fácil toofind Olá instruções que foram executadas (quem acessou, o que eles fizeram e quando) e determinar se o evento Olá foi legítimo ou mal-intencionados (por exemplo, aplicativo injeção de tooSQL vulnerabilidade é explorada, alguém violado dados confidenciais, etc.).<br/>
   ![Painel de navegação][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Explore os alertas de detecção de ameaças do banco de dados no portal do Azure de saudação

A Detecção de Ameaças do Banco de Dados SQL integra seus alertas à [Central de Segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/). Um bloco dinâmico de segurança do SQL na folha do banco de dados de saudação no status de Olá Olá rastreia portal do Azure de ameaças ativas. 

   ![Painel de navegação][6]
   
1. Clicando no bloco de segurança do SQL Olá inicia a folha de alertas Olá Central de segurança do Azure e fornece uma visão geral do active SQL as ameaças detectadas no banco de dados de saudação. 

  ![Painel de navegação][7]

2. Clicar em um alerta específico fornece detalhes adicionais e ações para investigar essa ameaça e corrigir futuras ameaças.

  ![Painel de navegação][8]


## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre a detecção de ameaças, visite Olá [blog do Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Saiba mais sobre a [Auditoria do Banco de Dados SQL do Azure](sql-database-auditing.md)
* Saiba mais sobre a [Central de Segurança do Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Para obter mais detalhes sobre preços, consulte Olá [página de preços de banco de dados SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Para obter um exemplo de script do PowerShell, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


