---
title: "Introdução à Detecção de Ameaças do SQL Data Warehouse"
description: "Introdução à detecção de ameaças"
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
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="7fb8b-103">Introdução à detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="7fb8b-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fb8b-104">Auditoria</span><span class="sxs-lookup"><span data-stu-id="7fb8b-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="7fb8b-105">Detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="7fb8b-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7fb8b-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7fb8b-106">Overview</span></span>
<span data-ttu-id="7fb8b-107">A Detecção de Ameaças detecta as atividades anormais do banco de dados que indicam possíveis ameaças de segurança ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="7fb8b-108">Detecção de ameaças está em visualização e tem suporte para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="7fb8b-109">A Detecção de Ameaças fornece uma nova camada de segurança, que permite que os clientes detectem e respondam às ameaças potenciais conforme elas ocorrem, fornecendo alertas de segurança nas atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="7fb8b-110">Os usuários podem explorar os eventos suspeitos usando a [Auditoria do Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) para determinar se eles resultam de uma tentativa de acesso, violação ou exploração dos dados no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="7fb8b-111">A Detecção de Ameaças torna simples lidar com possíveis ameaças no data warehouse sem a necessidade de ser uma especialista em segurança ou gerenciar sistemas avançados de monitoramento de segurança.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="7fb8b-112">Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="7fb8b-113">A injeção de SQL é um dos problemas comuns de segurança do aplicativo da Web na Internet, usada para atacar os aplicativos controlados por dados.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="7fb8b-114">Os invasores aproveitam as vulnerabilidades do aplicativo para inserir instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para violar ou modificar os dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="7fb8b-115">Configurar a detecção de ameaças para seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="7fb8b-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="7fb8b-116">Inicie o Portal do Azure em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7fb8b-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7fb8b-117">Navegue até a folha de configuração do SQL Data Warehouse que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="7fb8b-118">Na folha Configurações, selecione **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Painel de navegação][1]
3. <span data-ttu-id="7fb8b-120">Na folha de configuração **Auditoria e Detecção de Ameaças**, **ATIVE** a auditoria, que exibirá as configurações de Detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Painel de navegação][2]
4. <span data-ttu-id="7fb8b-122">**ATIVE** a Detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="7fb8b-123">Configure a lista de emails que receberão alertas de segurança após a detecção de atividades de depósito de dados anormais.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="7fb8b-124">Clique em **Salvar** na folha de configuração **Auditoria e detecção de ameaças** para salvar a auditoria nova ou atualizada e a política de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Painel de navegação][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="7fb8b-126">Explore as atividades de depósito de dados anômalos após a detecção de um evento suspeito</span><span class="sxs-lookup"><span data-stu-id="7fb8b-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="7fb8b-127">Você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="7fb8b-128">O email fornecerá informações sobre o evento de segurança suspeito, incluindo a natureza das atividades anormais, nome do banco de dados, nome do servidor e a hora do evento.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="7fb8b-129">Além disso, ele fornecerá informações sobre as possíveis causas e ações recomendadas para investigar e atenuar a ameaça em potencial no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Painel de navegação][4]
2. <span data-ttu-id="7fb8b-131">No email, clique no link **Log de Auditoria do SQL do Azure** , que iniciará o portal clássico do Azure e mostrará os registros de Auditoria relevantes na época do evento suspeito.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Painel de navegação][5]
3. <span data-ttu-id="7fb8b-133">Clique nos registros de auditoria para exibir mais detalhes sobre as atividades suspeitas do banco de dados, como a instrução SQL, motivo da falha e IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Painel de navegação][6]
4. <span data-ttu-id="7fb8b-135">Na folha Registros de Auditoria, clique em **Abrir no Excel** para abrir um modelo pré-configurado do Excel para importar e executar uma análise mais profunda do log de auditoria na época do evento suspeito.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="7fb8b-136">
   **Observação:** no Excel 2010 ou posterior, o Power Query e a configuração **Combinação Rápida** são necessários</span><span class="sxs-lookup"><span data-stu-id="7fb8b-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Painel de navegação][7]
5. <span data-ttu-id="7fb8b-138">Para definir a configuração **Combinação Rápida**: na guia de faixa de opções **POWER QUERY**, selecione **Opções** para exibir a caixa de diálogo Opções.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="7fb8b-139">Selecione a seção Privacidade e escolha a segunda opção - 'Ignorar os Níveis de Privacidade e melhorar potencialmente o desempenho':</span><span class="sxs-lookup"><span data-stu-id="7fb8b-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Painel de navegação][8]
6. <span data-ttu-id="7fb8b-141">Para carregar os logs de auditoria do SQL, verifique se os parâmetros na guia de configurações estão definidos corretamente e, em seguida, selecione a faixa de opções 'Dados' e clique no botão 'Atualizar Tudo'.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Painel de navegação][9]
7. <span data-ttu-id="7fb8b-143">Os resultados aparecem na folha **Logs de Auditoria do SQL** , que permite executar uma análise mais profunda das atividades anormais detectadas e minimizar o impacto do evento de segurança em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7fb8b-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

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
