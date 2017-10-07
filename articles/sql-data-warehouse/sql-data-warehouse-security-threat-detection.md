---
title: "aaaGet iniciado com detecção de ameaças do SQL Data Warehouse"
description: "Como tooget iniciada com detecção de ameaças"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>Introdução à detecção de ameaças
> [!div class="op_single_selector"]
> * [Auditoria](sql-data-warehouse-auditing-overview.md)
> * [Detecção de ameaças](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Visão geral
Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança. Detecção de ameaças está em visualização e tem suporte para o SQL Data Warehouse.

A detecção de ameaças fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais. Os usuários podem explorar eventos suspeitos de saudação usando [auditoria do Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) toodetermine se eles são provenientes de uma tentativa tooaccess, violação ou explorar dados no data warehouse do hello.
A detecção de ameaças torna simples tooaddress possíveis ameaças toohello dados do data warehouse sem Olá necessidade toobe um especialista em segurança ou gerenciam sistemas de monitoramento de segurança avançada.

Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL. Injeção de SQL é um dos Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados. Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para serem violados ou modificar dados no banco de dados de saudação.

## <a name="set-up-threat-detection-for-your-database"></a>Configurar a detecção de ameaças para seu banco de dados
1. Iniciar Olá Portal do Azure em [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello folha de configuração de saudação SQL Data Warehouse, você deseja toomonitor. Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.
   
    ![Painel de navegação][1]
3. Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibirá as configurações de detecção de ameaças hello.
   
    ![Painel de navegação][2]
4. **ATIVE** a Detecção de ameaças.
5. Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades de depósito de dados anômalos.
6. Clique em **salvar** em Olá **detecção de auditoria e ameaças** configuração folha toosave Olá nova ou atualizada política de detecção de ameaças e auditoria.
   
    ![Painel de navegação][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Explore as atividades de depósito de dados anômalos após a detecção de um evento suspeito
1. Você receberá uma notificação por email na detecção das atividades anormais do banco de dados. <br/>
   email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, a hora de evento de nome e hello do servidor. Além disso, ele fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de.<br/>
   
    ![Painel de navegação][4]
2. No email de saudação, clique em Olá **o Log de auditoria do SQL Azure** link, o que iniciará Olá Portal clássico do Azure e Mostrar registros de auditoria relevantes Olá em torno de tempo de saudação do evento suspeitas hello.
   
    ![Painel de navegação][5]
3. Clique em tooview de registros de auditoria hello mais detalhes sobre atividades de banco de dados suspeito hello, como a instrução SQL, IP de cliente e o motivo da falha.
   
    ![Painel de navegação][6]
4. Na folha de registros de auditoria de saudação, clique em **abrir no Excel** tooopen previamente configurada do excel tooimport de modelo e executar uma análise mais profunda do log de auditoria Olá em torno de tempo de saudação do evento suspeitas hello.<br/>
   **Observação:** no Excel 2010 ou posterior, o Power Query e Olá **combinação rápida** configuração é necessária
   
    ![Painel de navegação][7]
5. Olá tooconfigure **combinação rápida** configuração - no hello **POWER QUERY** guia de faixa de opções, selecione **opções** toodisplay caixa de diálogo de opções de saudação. Selecione a seção de privacidade hello e escolha Olá segunda opção - 'Ignorar Olá níveis de privacidade e potencialmente melhorar o desempenho':
   
    ![Painel de navegação][8]
6. logs de auditoria do SQL tooload, verifique se Olá parâmetros na guia Configurações de saudação estão definidos corretamente e, em seguida, selecione a faixa de opções de 'Dados' hello e clique o botão 'Atualizar tudo' hello.
   
    ![Painel de navegação][9]
7. resultados de saudação aparecem na Olá **os Logs de auditoria do SQL** folha que permite que você toorun uma análise mais profunda de atividades anormais de saudação que foram detectadas e reduzir o impacto de saudação do evento de segurança de saudação em seu aplicativo.

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
