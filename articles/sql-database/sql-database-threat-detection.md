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
# <a name="sql-database-threat-detection"></a><span data-ttu-id="88f12-103">Detecção de Ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="88f12-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="88f12-104">SQL a detecção de ameaças detecta atividades anormais indicando tentativas incomuns e potencialmente prejudiciais tooaccess ou exploração bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="88f12-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="88f12-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="88f12-105">Overview</span></span>

<span data-ttu-id="88f12-106">Detecção de ameaças SQL fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="88f12-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="88f12-107">Os usuários receberão um alerta mediante atividades suspeitas em bancos de dados, possíveis vulnerabilidades e ataques de injeção de SQL, bem como padrões anômalos de acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="88f12-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="88f12-108">Alertas de detecção de ameaças SQL fornecer detalhes de atividade suspeita e recomendarão a ação sobre como tooinvestigate e atenuar a ameaça de saudação.</span><span class="sxs-lookup"><span data-stu-id="88f12-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="88f12-109">Os usuários podem explorar eventos suspeitos de saudação usando [auditoria de banco de dados SQL](sql-database-auditing.md) toodetermine se eles são provenientes de uma tentativa tooaccess, violação ou explorar dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="88f12-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="88f12-110">A detecção de ameaças torna simples tooaddress potenciais ameaças toohello banco de dados sem a necessidade de saudação toobe um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançada.</span><span class="sxs-lookup"><span data-stu-id="88f12-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="88f12-111">Por exemplo, injeção de SQL é um Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados.</span><span class="sxs-lookup"><span data-stu-id="88f12-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="88f12-112">Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, serem violados ou modificar dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="88f12-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="88f12-113">Detecção de ameaças SQL integra alertas com [Central de segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/), e, cada servidor de banco de dados SQL protegido será cobrado com hello mesmo preço como camada padrão do Centro de segurança do Azure, em r $15/nó/mês, onde cada protegido SQL Servidor de banco de dados é contado como um nó.</span><span class="sxs-lookup"><span data-stu-id="88f12-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="88f12-114">Você está convidado tootry-lo por 60 dias para liberar.</span><span class="sxs-lookup"><span data-stu-id="88f12-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="88f12-115">Configurar a detecção de ameaças do banco de dados em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="88f12-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="88f12-116">Iniciar hello Azure portal em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88f12-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="88f12-117">Navegue toohello folha de configuração de saudação deseja toomonitor do banco de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="88f12-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="88f12-118">Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="88f12-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="88f12-119">![Painel de navegação][1]</span><span class="sxs-lookup"><span data-stu-id="88f12-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="88f12-120">Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibe as configurações de detecção de ameaças hello.</span><span class="sxs-lookup"><span data-stu-id="88f12-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Painel de navegação][2]
4. <span data-ttu-id="88f12-122">**ATIVE** a Detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="88f12-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="88f12-123">Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades anormais de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="88f12-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="88f12-124">Clique em **salvar** em Olá **detecção de auditoria e ameaças** toosave folha Olá novas ou atualizadas configurações de detecção de ameaças e auditoria.</span><span class="sxs-lookup"><span data-stu-id="88f12-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Painel de navegação][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="88f12-126">Configurar a detecção de ameaças usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="88f12-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="88f12-127">Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="88f12-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="88f12-128">Explore as atividades anormais do banco de dados na detecção de um evento suspeito</span><span class="sxs-lookup"><span data-stu-id="88f12-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="88f12-129">Você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="88f12-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="88f12-130">email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, nome do servidor, nome do aplicativo e tempo de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="88f12-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="88f12-131">Além disso, email Olá fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de.</span><span class="sxs-lookup"><span data-stu-id="88f12-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Painel de navegação][4]
2. <span data-ttu-id="88f12-133">alerta de email Olá inclui um log de auditoria do SQL toohello vínculo direto.</span><span class="sxs-lookup"><span data-stu-id="88f12-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="88f12-134">Clicando em Olá de inicia esse link do Azure portal e abre Olá SQL registros de auditoria em torno de tempo de saudação do evento suspeitas hello.</span><span class="sxs-lookup"><span data-stu-id="88f12-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="88f12-135">Clique em um tooview de registro de auditoria para obter mais detalhes sobre as atividades de banco de dados suspeito hello, tornando mais fácil toofind Olá instruções que foram executadas (quem acessou, o que eles fizeram e quando) e determinar se o evento Olá foi legítimo ou mal-intencionados (por exemplo, aplicativo injeção de tooSQL vulnerabilidade é explorada, alguém violado dados confidenciais, etc.).</span><span class="sxs-lookup"><span data-stu-id="88f12-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="88f12-136">
   ![Painel de navegação][5]</span><span class="sxs-lookup"><span data-stu-id="88f12-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="88f12-137">Explore os alertas de detecção de ameaças do banco de dados no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="88f12-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="88f12-138">A Detecção de Ameaças do Banco de Dados SQL integra seus alertas à [Central de Segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="88f12-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="88f12-139">Um bloco dinâmico de segurança do SQL na folha do banco de dados de saudação no status de Olá Olá rastreia portal do Azure de ameaças ativas.</span><span class="sxs-lookup"><span data-stu-id="88f12-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Painel de navegação][6]
   
1. <span data-ttu-id="88f12-141">Clicando no bloco de segurança do SQL Olá inicia a folha de alertas Olá Central de segurança do Azure e fornece uma visão geral do active SQL as ameaças detectadas no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="88f12-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Painel de navegação][7]

2. <span data-ttu-id="88f12-143">Clicar em um alerta específico fornece detalhes adicionais e ações para investigar essa ameaça e corrigir futuras ameaças.</span><span class="sxs-lookup"><span data-stu-id="88f12-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Painel de navegação][8]


## <a name="next-steps"></a><span data-ttu-id="88f12-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88f12-145">Next steps</span></span>

* <span data-ttu-id="88f12-146">Saiba mais sobre a detecção de ameaças, visite Olá [blog do Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="88f12-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="88f12-147">Saiba mais sobre a [Auditoria do Banco de Dados SQL do Azure](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="88f12-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="88f12-148">Saiba mais sobre a [Central de Segurança do Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="88f12-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="88f12-149">Para obter mais detalhes sobre preços, consulte Olá [página de preços de banco de dados SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="88f12-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="88f12-150">Para obter um exemplo de script do PowerShell, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="88f12-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


