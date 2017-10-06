---
title: "alertas de Nagios e Zabbix aaaCollect na análise de Log do OMS | Microsoft Docs"
description: "O Nagios e o Zabbix são ferramentas de monitoramento de software livre. Você pode coletar de alertas essas ferramentas para análise de Log na ordem tooanalyze-los junto com os alertas de outras fontes.  Este artigo descreve como tooconfigure Olá agente do OMS para Linux toocollect alertas desses sistemas."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="00542-105">Coletar alertas do Nagios e do Zabbix no Log Analytics do Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="00542-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="00542-106">O [Nagios](https://www.nagios.org/) e o [Zabbix](http://www.zabbix.com/) são ferramentas de monitoramento de software livre.</span><span class="sxs-lookup"><span data-stu-id="00542-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="00542-107">Você pode coletar de alertas essas ferramentas para análise de Log na ordem tooanalyze-os junto com [alertas de outras fontes](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="00542-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="00542-108">Este artigo descreve como tooconfigure Olá agente do OMS para Linux toocollect alertas desses sistemas.</span><span class="sxs-lookup"><span data-stu-id="00542-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="00542-109">Configurar coleta de alertas</span><span class="sxs-lookup"><span data-stu-id="00542-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="00542-110">Configurar coleta de alertas do Nagios</span><span class="sxs-lookup"><span data-stu-id="00542-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="00542-111">Execute Olá seguindo as etapas em alertas de toocollect Olá Nagios server.</span><span class="sxs-lookup"><span data-stu-id="00542-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="00542-112">Usuário de saudação Grant **omsagent** arquivo de log do acesso de leitura toohello Nagios (ou seja, `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="00542-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="00542-113">Supondo que o arquivo nagios.log de saudação pertencem ao grupo Olá `nagios`, você pode adicionar usuário Olá **omsagent** toohello **nagios** grupo.</span><span class="sxs-lookup"><span data-stu-id="00542-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="00542-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="00542-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="00542-115">Modificar o arquivo de configuração de saudação em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="00542-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="00542-116">Certifique-se de saudação entradas a seguir está presentes e sem comentários:</span><span class="sxs-lookup"><span data-stu-id="00542-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="00542-117">Reiniciar o daemon omsagent Olá</span><span class="sxs-lookup"><span data-stu-id="00542-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="00542-118">Configurar coleta de alertas do Zabbix</span><span class="sxs-lookup"><span data-stu-id="00542-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="00542-119">toocollect alertas de um servidor Zabbix, você precisa toospecify um usuário e senha em *limpar texto*.</span><span class="sxs-lookup"><span data-stu-id="00542-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="00542-120">Isso não é ideal, mas é recomendável que você crie Olá usuário e conceda permissões toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="00542-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="00542-121">Execute Olá seguindo as etapas em alertas de toocollect Olá Nagios server.</span><span class="sxs-lookup"><span data-stu-id="00542-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="00542-122">Modificar o arquivo de configuração de saudação em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="00542-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="00542-123">Certifique-se de saudação entradas a seguir está presentes e sem comentários.  Alterar os toovalues Olá nome e senha de usuário para o seu ambiente Zabbix.</span><span class="sxs-lookup"><span data-stu-id="00542-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="00542-124">Reiniciar o daemon omsagent Olá</span><span class="sxs-lookup"><span data-stu-id="00542-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="00542-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="00542-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="00542-126">Registros de alerta</span><span class="sxs-lookup"><span data-stu-id="00542-126">Alert records</span></span>
<span data-ttu-id="00542-127">Você pode recuperar registros de alerta do Nagios e do Zabbix usando [pesquisas de logs](log-analytics-log-searches.md) no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="00542-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="00542-128">Registros de alerta do Nagios</span><span class="sxs-lookup"><span data-stu-id="00542-128">Nagios Alert records</span></span>

<span data-ttu-id="00542-129">Registros de alerta coletados pelo Nagios têm **Type** definido como **Alert** e **SourceSystem** definido como **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="00542-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="00542-130">Eles têm propriedades Olá no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="00542-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="00542-131">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00542-131">Property</span></span> | <span data-ttu-id="00542-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="00542-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="00542-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="00542-133">Type</span></span> |<span data-ttu-id="00542-134">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="00542-134">*Alert*</span></span> |
| <span data-ttu-id="00542-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="00542-135">SourceSystem</span></span> |<span data-ttu-id="00542-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="00542-136">*Nagios*</span></span> |
| <span data-ttu-id="00542-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="00542-137">AlertName</span></span> |<span data-ttu-id="00542-138">Nome do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-138">Name of hello alert.</span></span> |
| <span data-ttu-id="00542-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="00542-139">AlertDescription</span></span> | <span data-ttu-id="00542-140">Descrição do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-140">Description of hello alert.</span></span> |
| <span data-ttu-id="00542-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="00542-141">AlertState</span></span> | <span data-ttu-id="00542-142">Status do serviço de saudação ou host.</span><span class="sxs-lookup"><span data-stu-id="00542-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="00542-143">OK</span><span class="sxs-lookup"><span data-stu-id="00542-143">OK</span></span><br><span data-ttu-id="00542-144">AVISO</span><span class="sxs-lookup"><span data-stu-id="00542-144">WARNING</span></span><br><span data-ttu-id="00542-145">PARA CIMA</span><span class="sxs-lookup"><span data-stu-id="00542-145">UP</span></span><br><span data-ttu-id="00542-146">PARA BAIXO</span><span class="sxs-lookup"><span data-stu-id="00542-146">DOWN</span></span> |
| <span data-ttu-id="00542-147">HostName</span><span class="sxs-lookup"><span data-stu-id="00542-147">HostName</span></span> | <span data-ttu-id="00542-148">Nome do host de saudação que criou o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="00542-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="00542-149">PriorityNumber</span></span> | <span data-ttu-id="00542-150">Nível de prioridade de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="00542-151">StateType</span><span class="sxs-lookup"><span data-stu-id="00542-151">StateType</span></span> | <span data-ttu-id="00542-152">tipo de saudação do estado de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="00542-153">SUAVE – problema que não foi verificado novamente.</span><span class="sxs-lookup"><span data-stu-id="00542-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="00542-154">GRAVE – problema que foi verificado novamente um número especificado de vezes.</span><span class="sxs-lookup"><span data-stu-id="00542-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="00542-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="00542-155">TimeGenerated</span></span> |<span data-ttu-id="00542-156">Alerta de saudação de data e hora foi criado.</span><span class="sxs-lookup"><span data-stu-id="00542-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="00542-157">Registros de alerta do Zabbix</span><span class="sxs-lookup"><span data-stu-id="00542-157">Zabbix alert records</span></span>
<span data-ttu-id="00542-158">Registros de alerta coletados pelo Zabbix têm **Type** definido como **Alert** e **SourceSystem** definido como **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="00542-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="00542-159">Eles têm propriedades Olá no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="00542-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="00542-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00542-160">Property</span></span> | <span data-ttu-id="00542-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="00542-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="00542-162">Tipo</span><span class="sxs-lookup"><span data-stu-id="00542-162">Type</span></span> |<span data-ttu-id="00542-163">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="00542-163">*Alert*</span></span> |
| <span data-ttu-id="00542-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="00542-164">SourceSystem</span></span> |<span data-ttu-id="00542-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="00542-165">*Zabbix*</span></span> |
| <span data-ttu-id="00542-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="00542-166">AlertName</span></span> | <span data-ttu-id="00542-167">Nome do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-167">Name of hello alert.</span></span> |
| <span data-ttu-id="00542-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="00542-168">AlertPriority</span></span> | <span data-ttu-id="00542-169">Severidade do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="00542-170">não classificado</span><span class="sxs-lookup"><span data-stu-id="00542-170">not classified</span></span><br><span data-ttu-id="00542-171">informações</span><span class="sxs-lookup"><span data-stu-id="00542-171">information</span></span><br><span data-ttu-id="00542-172">Aviso</span><span class="sxs-lookup"><span data-stu-id="00542-172">warning</span></span><br><span data-ttu-id="00542-173">média</span><span class="sxs-lookup"><span data-stu-id="00542-173">average</span></span><br><span data-ttu-id="00542-174">alto</span><span class="sxs-lookup"><span data-stu-id="00542-174">high</span></span><br><span data-ttu-id="00542-175">desastre</span><span class="sxs-lookup"><span data-stu-id="00542-175">disaster</span></span>  |
| <span data-ttu-id="00542-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="00542-176">AlertState</span></span> | <span data-ttu-id="00542-177">Estado de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-177">State of hello alert.</span></span><br><br><span data-ttu-id="00542-178">0 - estado é toodate.</span><span class="sxs-lookup"><span data-stu-id="00542-178">0 - State is up toodate.</span></span><br><span data-ttu-id="00542-179">1 – o estado é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="00542-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="00542-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="00542-180">AlertTypeNumber</span></span> | <span data-ttu-id="00542-181">Especifica se o alerta pode ou não gerar vários eventos de problema.</span><span class="sxs-lookup"><span data-stu-id="00542-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="00542-182">0 - estado é toodate.</span><span class="sxs-lookup"><span data-stu-id="00542-182">0 - State is up toodate.</span></span><br><span data-ttu-id="00542-183">1 – o estado é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="00542-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="00542-184">Comentários</span><span class="sxs-lookup"><span data-stu-id="00542-184">Comments</span></span> | <span data-ttu-id="00542-185">Comentários adicionais para o alerta.</span><span class="sxs-lookup"><span data-stu-id="00542-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="00542-186">HostName</span><span class="sxs-lookup"><span data-stu-id="00542-186">HostName</span></span> | <span data-ttu-id="00542-187">Nome do host de saudação que criou o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="00542-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="00542-188">PriorityNumber</span></span> | <span data-ttu-id="00542-189">Valor que indica a severidade do alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="00542-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="00542-190">0 – não classificado</span><span class="sxs-lookup"><span data-stu-id="00542-190">0 - not classified</span></span><br><span data-ttu-id="00542-191">1 – informações</span><span class="sxs-lookup"><span data-stu-id="00542-191">1 - information</span></span><br><span data-ttu-id="00542-192">2 – aviso</span><span class="sxs-lookup"><span data-stu-id="00542-192">2 - warning</span></span><br><span data-ttu-id="00542-193">3 – média</span><span class="sxs-lookup"><span data-stu-id="00542-193">3 - average</span></span><br><span data-ttu-id="00542-194">4 – alta</span><span class="sxs-lookup"><span data-stu-id="00542-194">4 - high</span></span><br><span data-ttu-id="00542-195">5 – desastre</span><span class="sxs-lookup"><span data-stu-id="00542-195">5 - disaster</span></span> |
| <span data-ttu-id="00542-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="00542-196">TimeGenerated</span></span> |<span data-ttu-id="00542-197">Alerta de saudação de data e hora foi criado.</span><span class="sxs-lookup"><span data-stu-id="00542-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="00542-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="00542-198">TimeLastModified</span></span> |<span data-ttu-id="00542-199">Estado de saudação de data e hora de alerta de saudação última alteração.</span><span class="sxs-lookup"><span data-stu-id="00542-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="00542-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00542-200">Next steps</span></span>
* <span data-ttu-id="00542-201">Aprenda sobre [alertas](log-analytics-alerts.md) no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="00542-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="00542-202">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="00542-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
