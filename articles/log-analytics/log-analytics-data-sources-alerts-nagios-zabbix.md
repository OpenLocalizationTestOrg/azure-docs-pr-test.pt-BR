---
title: Coletar alertas do Nagios e do Zabbix no OMS Log Analytics | Microsoft Docs
description: "O Nagios e o Zabbix são ferramentas de monitoramento de software livre. Você pode coletar alertas dessas ferramentas para o Log Analytics para analisá-los junto com os alertas de outras fontes.  Este artigo descreve como configurar o Agente do OMS para Linux para coletar alertas desses sistemas."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="c2afa-105">Coletar alertas do Nagios e do Zabbix no Log Analytics do Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="c2afa-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="c2afa-106">O [Nagios](https://www.nagios.org/) e o [Zabbix](http://www.zabbix.com/) são ferramentas de monitoramento de software livre.</span><span class="sxs-lookup"><span data-stu-id="c2afa-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="c2afa-107">Você pode coletar alertas dessas ferramentas para o Log Analytics para analisá-los junto com os [alertas de outras fontes](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c2afa-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="c2afa-108">Este artigo descreve como configurar o Agente do OMS para Linux para coletar alertas desses sistemas.</span><span class="sxs-lookup"><span data-stu-id="c2afa-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="c2afa-109">Configurar coleta de alertas</span><span class="sxs-lookup"><span data-stu-id="c2afa-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="c2afa-110">Configurar coleta de alertas do Nagios</span><span class="sxs-lookup"><span data-stu-id="c2afa-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="c2afa-111">Execute as etapas a seguir no servidor Nagios para coletar alertas.</span><span class="sxs-lookup"><span data-stu-id="c2afa-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="c2afa-112">Conceda ao usuário **omsagent** acesso de leitura ao arquivo de log do Nagios (ou seja, `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="c2afa-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="c2afa-113">Supondo que o arquivo nagios.log pertença ao grupo `nagios`, você poderá adicionar o usuário **omsagent** ao grupo **nagios**.</span><span class="sxs-lookup"><span data-stu-id="c2afa-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="c2afa-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="c2afa-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="c2afa-115">Modificar o arquivo de configuração em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="c2afa-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="c2afa-116">Verifique se as entradas a seguir estão presentes e se não foram comentadas:</span><span class="sxs-lookup"><span data-stu-id="c2afa-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="c2afa-117">Reinicie o daemon omsagent</span><span class="sxs-lookup"><span data-stu-id="c2afa-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="c2afa-118">Configurar coleta de alertas do Zabbix</span><span class="sxs-lookup"><span data-stu-id="c2afa-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="c2afa-119">Para obter alertas de um servidor do Zabbix, você precisa especificar um usuário e senha com *texto não criptografado*.</span><span class="sxs-lookup"><span data-stu-id="c2afa-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="c2afa-120">Isso não é o ideal, mas recomendamos que você crie o usuário e conceda permissões somente para monitorar.</span><span class="sxs-lookup"><span data-stu-id="c2afa-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="c2afa-121">Execute as etapas a seguir no servidor Nagios para coletar alertas.</span><span class="sxs-lookup"><span data-stu-id="c2afa-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="c2afa-122">Modificar o arquivo de configuração em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="c2afa-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="c2afa-123">Verifique se as entradas a seguir estão presentes e se não foram comentadas.</span><span class="sxs-lookup"><span data-stu-id="c2afa-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="c2afa-124">Altere o nome de usuário e senha para valores para o seu ambiente do Zabbix.</span><span class="sxs-lookup"><span data-stu-id="c2afa-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="c2afa-125">Reinicie o daemon omsagent</span><span class="sxs-lookup"><span data-stu-id="c2afa-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="c2afa-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="c2afa-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="c2afa-127">Registros de alerta</span><span class="sxs-lookup"><span data-stu-id="c2afa-127">Alert records</span></span>
<span data-ttu-id="c2afa-128">Você pode recuperar registros de alerta do Nagios e do Zabbix usando [pesquisas de logs](log-analytics-log-searches.md) no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c2afa-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="c2afa-129">Registros de alerta do Nagios</span><span class="sxs-lookup"><span data-stu-id="c2afa-129">Nagios Alert records</span></span>

<span data-ttu-id="c2afa-130">Registros de alerta coletados pelo Nagios têm **Type** definido como **Alert** e **SourceSystem** definido como **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="c2afa-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="c2afa-131">Eles têm as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2afa-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="c2afa-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c2afa-132">Property</span></span> | <span data-ttu-id="c2afa-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2afa-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c2afa-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="c2afa-134">Type</span></span> |<span data-ttu-id="c2afa-135">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="c2afa-135">*Alert*</span></span> |
| <span data-ttu-id="c2afa-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c2afa-136">SourceSystem</span></span> |<span data-ttu-id="c2afa-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="c2afa-137">*Nagios*</span></span> |
| <span data-ttu-id="c2afa-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="c2afa-138">AlertName</span></span> |<span data-ttu-id="c2afa-139">Nome do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-139">Name of the alert.</span></span> |
| <span data-ttu-id="c2afa-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="c2afa-140">AlertDescription</span></span> | <span data-ttu-id="c2afa-141">Descrição do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-141">Description of the alert.</span></span> |
| <span data-ttu-id="c2afa-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="c2afa-142">AlertState</span></span> | <span data-ttu-id="c2afa-143">Status do serviço ou do host.</span><span class="sxs-lookup"><span data-stu-id="c2afa-143">Status of the service or host.</span></span><br><br><span data-ttu-id="c2afa-144">OK</span><span class="sxs-lookup"><span data-stu-id="c2afa-144">OK</span></span><br><span data-ttu-id="c2afa-145">AVISO</span><span class="sxs-lookup"><span data-stu-id="c2afa-145">WARNING</span></span><br><span data-ttu-id="c2afa-146">PARA CIMA</span><span class="sxs-lookup"><span data-stu-id="c2afa-146">UP</span></span><br><span data-ttu-id="c2afa-147">PARA BAIXO</span><span class="sxs-lookup"><span data-stu-id="c2afa-147">DOWN</span></span> |
| <span data-ttu-id="c2afa-148">HostName</span><span class="sxs-lookup"><span data-stu-id="c2afa-148">HostName</span></span> | <span data-ttu-id="c2afa-149">Nome do host que criou o alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="c2afa-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="c2afa-150">PriorityNumber</span></span> | <span data-ttu-id="c2afa-151">Nível de prioridade do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="c2afa-152">StateType</span><span class="sxs-lookup"><span data-stu-id="c2afa-152">StateType</span></span> | <span data-ttu-id="c2afa-153">O tipo de estado do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="c2afa-154">SUAVE – problema que não foi verificado novamente.</span><span class="sxs-lookup"><span data-stu-id="c2afa-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="c2afa-155">GRAVE – problema que foi verificado novamente um número especificado de vezes.</span><span class="sxs-lookup"><span data-stu-id="c2afa-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="c2afa-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="c2afa-156">TimeGenerated</span></span> |<span data-ttu-id="c2afa-157">Data e hora em que o alerta foi criado.</span><span class="sxs-lookup"><span data-stu-id="c2afa-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="c2afa-158">Registros de alerta do Zabbix</span><span class="sxs-lookup"><span data-stu-id="c2afa-158">Zabbix alert records</span></span>
<span data-ttu-id="c2afa-159">Registros de alerta coletados pelo Zabbix têm **Type** definido como **Alert** e **SourceSystem** definido como **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="c2afa-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="c2afa-160">Eles têm as propriedades indicadas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2afa-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="c2afa-161">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c2afa-161">Property</span></span> | <span data-ttu-id="c2afa-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2afa-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c2afa-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="c2afa-163">Type</span></span> |<span data-ttu-id="c2afa-164">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="c2afa-164">*Alert*</span></span> |
| <span data-ttu-id="c2afa-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c2afa-165">SourceSystem</span></span> |<span data-ttu-id="c2afa-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="c2afa-166">*Zabbix*</span></span> |
| <span data-ttu-id="c2afa-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="c2afa-167">AlertName</span></span> | <span data-ttu-id="c2afa-168">Nome do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-168">Name of the alert.</span></span> |
| <span data-ttu-id="c2afa-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="c2afa-169">AlertPriority</span></span> | <span data-ttu-id="c2afa-170">Severidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-170">Severity of the alert.</span></span><br><br><span data-ttu-id="c2afa-171">não classificado</span><span class="sxs-lookup"><span data-stu-id="c2afa-171">not classified</span></span><br><span data-ttu-id="c2afa-172">informações</span><span class="sxs-lookup"><span data-stu-id="c2afa-172">information</span></span><br><span data-ttu-id="c2afa-173">Aviso</span><span class="sxs-lookup"><span data-stu-id="c2afa-173">warning</span></span><br><span data-ttu-id="c2afa-174">média</span><span class="sxs-lookup"><span data-stu-id="c2afa-174">average</span></span><br><span data-ttu-id="c2afa-175">alto</span><span class="sxs-lookup"><span data-stu-id="c2afa-175">high</span></span><br><span data-ttu-id="c2afa-176">desastre</span><span class="sxs-lookup"><span data-stu-id="c2afa-176">disaster</span></span>  |
| <span data-ttu-id="c2afa-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="c2afa-177">AlertState</span></span> | <span data-ttu-id="c2afa-178">Estado do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-178">State of the alert.</span></span><br><br><span data-ttu-id="c2afa-179">0 – estado está atualizado.</span><span class="sxs-lookup"><span data-stu-id="c2afa-179">0 - State is up to date.</span></span><br><span data-ttu-id="c2afa-180">1 – o estado é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="c2afa-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="c2afa-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="c2afa-181">AlertTypeNumber</span></span> | <span data-ttu-id="c2afa-182">Especifica se o alerta pode ou não gerar vários eventos de problema.</span><span class="sxs-lookup"><span data-stu-id="c2afa-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="c2afa-183">0 – estado está atualizado.</span><span class="sxs-lookup"><span data-stu-id="c2afa-183">0 - State is up to date.</span></span><br><span data-ttu-id="c2afa-184">1 – o estado é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="c2afa-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="c2afa-185">Comentários</span><span class="sxs-lookup"><span data-stu-id="c2afa-185">Comments</span></span> | <span data-ttu-id="c2afa-186">Comentários adicionais para o alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="c2afa-187">HostName</span><span class="sxs-lookup"><span data-stu-id="c2afa-187">HostName</span></span> | <span data-ttu-id="c2afa-188">Nome do host que criou o alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="c2afa-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="c2afa-189">PriorityNumber</span></span> | <span data-ttu-id="c2afa-190">Valor que indica a gravidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="c2afa-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="c2afa-191">0 – não classificado</span><span class="sxs-lookup"><span data-stu-id="c2afa-191">0 - not classified</span></span><br><span data-ttu-id="c2afa-192">1 – informações</span><span class="sxs-lookup"><span data-stu-id="c2afa-192">1 - information</span></span><br><span data-ttu-id="c2afa-193">2 – aviso</span><span class="sxs-lookup"><span data-stu-id="c2afa-193">2 - warning</span></span><br><span data-ttu-id="c2afa-194">3 – média</span><span class="sxs-lookup"><span data-stu-id="c2afa-194">3 - average</span></span><br><span data-ttu-id="c2afa-195">4 – alta</span><span class="sxs-lookup"><span data-stu-id="c2afa-195">4 - high</span></span><br><span data-ttu-id="c2afa-196">5 – desastre</span><span class="sxs-lookup"><span data-stu-id="c2afa-196">5 - disaster</span></span> |
| <span data-ttu-id="c2afa-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="c2afa-197">TimeGenerated</span></span> |<span data-ttu-id="c2afa-198">Data e hora em que o alerta foi criado.</span><span class="sxs-lookup"><span data-stu-id="c2afa-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="c2afa-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="c2afa-199">TimeLastModified</span></span> |<span data-ttu-id="c2afa-200">Data e hora em que o estado do alerta foi alterado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="c2afa-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c2afa-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2afa-201">Next steps</span></span>
* <span data-ttu-id="c2afa-202">Aprenda sobre [alertas](log-analytics-alerts.md) no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c2afa-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="c2afa-203">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) para analisar os dados coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="c2afa-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
