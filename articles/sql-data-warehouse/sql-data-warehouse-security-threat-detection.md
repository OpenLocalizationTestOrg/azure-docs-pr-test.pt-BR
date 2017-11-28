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
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="31fce-103">Introdução à detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="31fce-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31fce-104">Auditoria</span><span class="sxs-lookup"><span data-stu-id="31fce-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="31fce-105">Detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="31fce-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="31fce-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="31fce-106">Overview</span></span>
<span data-ttu-id="31fce-107">Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança.</span><span class="sxs-lookup"><span data-stu-id="31fce-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="31fce-108">Detecção de ameaças está em visualização e tem suporte para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="31fce-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="31fce-109">A detecção de ameaças fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="31fce-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="31fce-110">Os usuários podem explorar eventos suspeitos de saudação usando [auditoria do Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) toodetermine se eles são provenientes de uma tentativa tooaccess, violação ou explorar dados no data warehouse do hello.</span><span class="sxs-lookup"><span data-stu-id="31fce-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="31fce-111">A detecção de ameaças torna simples tooaddress possíveis ameaças toohello dados do data warehouse sem Olá necessidade toobe um especialista em segurança ou gerenciam sistemas de monitoramento de segurança avançada.</span><span class="sxs-lookup"><span data-stu-id="31fce-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="31fce-112">Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL.</span><span class="sxs-lookup"><span data-stu-id="31fce-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="31fce-113">Injeção de SQL é um dos Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados.</span><span class="sxs-lookup"><span data-stu-id="31fce-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="31fce-114">Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para serem violados ou modificar dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="31fce-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="31fce-115">Configurar a detecção de ameaças para seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="31fce-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="31fce-116">Iniciar Olá Portal do Azure em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31fce-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31fce-117">Navegue toohello folha de configuração de saudação SQL Data Warehouse, você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="31fce-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="31fce-118">Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="31fce-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Painel de navegação][1]
3. <span data-ttu-id="31fce-120">Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibirá as configurações de detecção de ameaças hello.</span><span class="sxs-lookup"><span data-stu-id="31fce-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Painel de navegação][2]
4. <span data-ttu-id="31fce-122">**ATIVE** a Detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="31fce-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="31fce-123">Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades de depósito de dados anômalos.</span><span class="sxs-lookup"><span data-stu-id="31fce-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="31fce-124">Clique em **salvar** em Olá **detecção de auditoria e ameaças** configuração folha toosave Olá nova ou atualizada política de detecção de ameaças e auditoria.</span><span class="sxs-lookup"><span data-stu-id="31fce-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Painel de navegação][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="31fce-126">Explore as atividades de depósito de dados anômalos após a detecção de um evento suspeito</span><span class="sxs-lookup"><span data-stu-id="31fce-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="31fce-127">Você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="31fce-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="31fce-128">email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, a hora de evento de nome e hello do servidor.</span><span class="sxs-lookup"><span data-stu-id="31fce-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="31fce-129">Além disso, ele fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de.</span><span class="sxs-lookup"><span data-stu-id="31fce-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Painel de navegação][4]
2. <span data-ttu-id="31fce-131">No email de saudação, clique em Olá **o Log de auditoria do SQL Azure** link, o que iniciará Olá Portal clássico do Azure e Mostrar registros de auditoria relevantes Olá em torno de tempo de saudação do evento suspeitas hello.</span><span class="sxs-lookup"><span data-stu-id="31fce-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Painel de navegação][5]
3. <span data-ttu-id="31fce-133">Clique em tooview de registros de auditoria hello mais detalhes sobre atividades de banco de dados suspeito hello, como a instrução SQL, IP de cliente e o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="31fce-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Painel de navegação][6]
4. <span data-ttu-id="31fce-135">Na folha de registros de auditoria de saudação, clique em **abrir no Excel** tooopen previamente configurada do excel tooimport de modelo e executar uma análise mais profunda do log de auditoria Olá em torno de tempo de saudação do evento suspeitas hello.</span><span class="sxs-lookup"><span data-stu-id="31fce-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="31fce-136">
   **Observação:** no Excel 2010 ou posterior, o Power Query e Olá **combinação rápida** configuração é necessária</span><span class="sxs-lookup"><span data-stu-id="31fce-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Painel de navegação][7]
5. <span data-ttu-id="31fce-138">Olá tooconfigure **combinação rápida** configuração - no hello **POWER QUERY** guia de faixa de opções, selecione **opções** toodisplay caixa de diálogo de opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="31fce-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="31fce-139">Selecione a seção de privacidade hello e escolha Olá segunda opção - 'Ignorar Olá níveis de privacidade e potencialmente melhorar o desempenho':</span><span class="sxs-lookup"><span data-stu-id="31fce-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Painel de navegação][8]
6. <span data-ttu-id="31fce-141">logs de auditoria do SQL tooload, verifique se Olá parâmetros na guia Configurações de saudação estão definidos corretamente e, em seguida, selecione a faixa de opções de 'Dados' hello e clique o botão 'Atualizar tudo' hello.</span><span class="sxs-lookup"><span data-stu-id="31fce-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Painel de navegação][9]
7. <span data-ttu-id="31fce-143">resultados de saudação aparecem na Olá **os Logs de auditoria do SQL** folha que permite que você toorun uma análise mais profunda de atividades anormais de saudação que foram detectadas e reduzir o impacto de saudação do evento de segurança de saudação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31fce-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
