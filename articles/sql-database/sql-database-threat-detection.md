---
title: "Detecção de ameaças – Banco de Dados SQL do Azure | Microsoft Docs"
description: "A Detecção de Ameaças detecta as atividades anormais do banco de dados que indicam possíveis ameaças de segurança ao banco de dados."
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="b8bf3-103">Detecção de Ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="b8bf3-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="b8bf3-104">A Detecção de Ameaças do SQL detecta atividades anômalas, indicando tentativas incomuns e potencialmente prejudiciais de acessar ou explorar bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="b8bf3-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b8bf3-105">Overview</span></span>

<span data-ttu-id="b8bf3-106">A Detecção de Ameaças do SQL fornece uma nova camada de segurança, que permite que os clientes detectem e respondam às ameaças potenciais conforme elas ocorrem, fornecendo alertas de segurança sobre atividades anômalas.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="b8bf3-107">Os usuários receberão um alerta mediante atividades suspeitas em bancos de dados, possíveis vulnerabilidades e ataques de injeção de SQL, bem como padrões anômalos de acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="b8bf3-108">Os alertas da Detecção de Ameaças do SQL fornecem detalhes de atividades suspeitas e recomendam ação de como investigar e atenuar a ameaça.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="b8bf3-109">Os usuários podem explorar os eventos suspeitos usando a [Auditoria do Banco de Dados SQL](sql-database-auditing.md) para determinar se eles resultam de uma tentativa de acesso, violação ou exploração dos dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="b8bf3-110">A Detecção de Ameaças torna simples tratar as possíveis ameaças no banco de dados sem a necessidade de ser um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="b8bf3-111">Por exemplo, a injeção de SQL é um dos problemas comuns de segurança do aplicativo da Web na Internet, usada para atacar os aplicativos orientados a dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="b8bf3-112">Os invasores aproveitam as vulnerabilidades do aplicativo para inserir instruções SQL mal-intencionadas nos campos de entrada do aplicativo, violando ou modificando os dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="b8bf3-113">A Detecção de Ameaças do SQL integra alertas à [Central de Segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/) e, de cada servidor de Banco de Dados SQL protegido será cobrado o mesmo preço cobrado pela camada Standard da Central de Segurança do Azure, que é US$ 15 por nó ao mês, em que cada servidor de banco de dados SQL protegido será contado como um nó.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="b8bf3-114">Convidamos você a testar o recurso por 60 dias gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="b8bf3-115">Configurar a detecção de ameaças para seu banco de dados no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8bf3-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="b8bf3-116">Inicie o Portal do Azure em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8bf3-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8bf3-117">Navegue até a folha de configuração do Banco de Dados SQL que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="b8bf3-118">Na folha Configurações, selecione **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="b8bf3-119">![Painel de navegação][1]</span><span class="sxs-lookup"><span data-stu-id="b8bf3-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="b8bf3-120">Na folha de configuração **Auditoria e Detecção de Ameaças**, **ATIVE** a Auditoria, o que exibirá as configurações de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![Painel de navegação][2]
4. <span data-ttu-id="b8bf3-122">**ATIVE** a Detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="b8bf3-123">Configure a lista de emails que receberão os alertas de segurança após a detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="b8bf3-124">Clique em **Salvar** na folha **Auditoria e Detecção de ameaças** para salvar a auditoria nova ou atualizada, bem como as configurações de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![Painel de navegação][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="b8bf3-126">Configurar a detecção de ameaças usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8bf3-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="b8bf3-127">Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b8bf3-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="b8bf3-128">Explore as atividades anormais do banco de dados na detecção de um evento suspeito</span><span class="sxs-lookup"><span data-stu-id="b8bf3-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="b8bf3-129">Você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="b8bf3-130">O email fornecerá informações sobre o evento de segurança suspeito, incluindo a natureza das atividades anômalas, o nome do banco de dados, o nome do servidor, o nome do aplicativo e a hora do evento.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="b8bf3-131">Além disso, o email fornecerá informações sobre as possíveis causas e as ações recomendadas para investigar e atenuar a ameaça em potencial no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![Painel de navegação][4]
2. <span data-ttu-id="b8bf3-133">O alerta por email inclui um link direto para o log de Auditoria do SQL.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="b8bf3-134">Clicar nesse link inicia o Portal do Azure e abre os registros de Auditoria do SQL próximos ao horário do evento suspeito.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="b8bf3-135">Clique em um registro de auditoria para exibir mais detalhes sobre as atividades suspeitas no banco de dados, o que facilita encontrar as instruções SQL que foram executadas (quem acessou, o que foi feito e quando) e determinar se o evento foi legítimo ou mal-intencionado (por exemplo, a vulnerabilidade do aplicativo para injeção de SQL foi explorada, alguém violou dados confidenciais, etc.).</span><span class="sxs-lookup"><span data-stu-id="b8bf3-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="b8bf3-136">
   ![Painel de navegação][5]</span><span class="sxs-lookup"><span data-stu-id="b8bf3-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="b8bf3-137">Explorar os alertas de detecção de ameaças para seu banco de dados no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8bf3-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="b8bf3-138">A Detecção de Ameaças do Banco de Dados SQL integra seus alertas à [Central de Segurança do Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="b8bf3-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="b8bf3-139">Um bloco de segurança SQL dinâmico na folha de banco de dados no Portal do Azure rastreia o status das ameaças ativas.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![Painel de navegação][6]
   
1. <span data-ttu-id="b8bf3-141">Clicar no bloco de segurança SQL inicia a folha de alertas da Central de Segurança do Azure e fornece uma visão geral das ameaças SQL ativas detectadas no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![Painel de navegação][7]

2. <span data-ttu-id="b8bf3-143">Clicar em um alerta específico fornece detalhes adicionais e ações para investigar essa ameaça e corrigir futuras ameaças.</span><span class="sxs-lookup"><span data-stu-id="b8bf3-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Painel de navegação][8]


## <a name="next-steps"></a><span data-ttu-id="b8bf3-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8bf3-145">Next steps</span></span>

* <span data-ttu-id="b8bf3-146">Saiba mais sobre a Detecção de Ameaças, visite o [blog do Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="b8bf3-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="b8bf3-147">Saiba mais sobre a [Auditoria do Banco de Dados SQL do Azure](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="b8bf3-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="b8bf3-148">Saiba mais sobre a [Central de Segurança do Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="b8bf3-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="b8bf3-149">Para obter mais detalhes sobre preços, visite a [página de Preços do Banco de Dados SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="b8bf3-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="b8bf3-150">Para obter um exemplo de script do PowerShell, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b8bf3-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


