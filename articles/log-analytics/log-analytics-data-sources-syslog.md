---
title: Coletar e analisar mensagens do Syslog no Log Analytics do OMS | Microsoft Docs
description: "O Syslog é um protocolo de registro de eventos em log que é comum para o Linux. Este artigo descreve como configurar a coleta de mensagens do Syslog no Log Analytics e os detalhes dos registros que eles criam no repositório do OMS."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="cbd02-104">Fontes de dados de Syslog no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cbd02-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="cbd02-105">O Syslog é um protocolo de registro de eventos em log que é comum para o Linux.</span><span class="sxs-lookup"><span data-stu-id="cbd02-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="cbd02-106">Os aplicativos enviarão mensagens que podem ser armazenadas no computador local ou entregues a um coletor de Syslog.</span><span class="sxs-lookup"><span data-stu-id="cbd02-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="cbd02-107">Quando o agente do OMS para Linux é instalado, ele configura o daemon do Syslog local para encaminhar mensagens para o agente.</span><span class="sxs-lookup"><span data-stu-id="cbd02-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="cbd02-108">O agente então envia a mensagem para o Log Analytics, no qual um registro correspondente é criado no repositório OMS.</span><span class="sxs-lookup"><span data-stu-id="cbd02-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="cbd02-109">O Log Analytics dá suporte à coleta de mensagens enviadas por rsyslog ou syslog-ng, em que rsyslog é o daemon padrão.</span><span class="sxs-lookup"><span data-stu-id="cbd02-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="cbd02-110">O daemon syslog padrão na versão 5 do Red Hat Enterprise Linux, CentOS e na versão Oracle Linux (sysklog) não tem suporte para a coleta de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="cbd02-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="cbd02-111">Para coletar dados de syslog nessa versão das distribuições, o [daemon rsyslog](http://rsyslog.com) deverá ser instalado e configurado para substituir sysklog.</span><span class="sxs-lookup"><span data-stu-id="cbd02-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Coleção do Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="cbd02-113">Configurando Syslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-113">Configuring Syslog</span></span>
<span data-ttu-id="cbd02-114">O Agente do OMS para Linux coletará apenas os eventos com os recursos e severidades especificadas em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="cbd02-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="cbd02-115">Você pode configurar o Syslog por meio do portal do OMS ou gerenciando arquivos de configuração em seus agentes do Linux.</span><span class="sxs-lookup"><span data-stu-id="cbd02-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="cbd02-116">Configurar o Syslog no portal do OMS</span><span class="sxs-lookup"><span data-stu-id="cbd02-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="cbd02-117">Configure o Syslog do menu [Dados nas Configurações do Log Analytics](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="cbd02-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="cbd02-118">Essa configuração é entregue ao arquivo de configuração em cada agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="cbd02-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="cbd02-119">Você pode adicionar um novo recurso, digitando seu nome e clicando em **+**.</span><span class="sxs-lookup"><span data-stu-id="cbd02-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="cbd02-120">Para cada recurso, somente mensagens com as severidades selecionadas serão coletados.</span><span class="sxs-lookup"><span data-stu-id="cbd02-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="cbd02-121">Marque as severidades para o recurso específico que você deseja coletar.</span><span class="sxs-lookup"><span data-stu-id="cbd02-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="cbd02-122">Você não pode fornecer quaisquer critérios adicionais para filtrar mensagens.</span><span class="sxs-lookup"><span data-stu-id="cbd02-122">You cannot provide any additional criteria to filter messages.</span></span>

![Configurar Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="cbd02-124">Por padrão, todas as alterações de configuração são automaticamente envidas por push para todos os agentes.</span><span class="sxs-lookup"><span data-stu-id="cbd02-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="cbd02-125">Se você quiser configurar o Syslog manualmente em cada agente do Linux, desmarque a caixa *Aplicar as configurações abaixo aos computadores Linux*.</span><span class="sxs-lookup"><span data-stu-id="cbd02-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="cbd02-126">Configurar o Syslog no agente do Linux</span><span class="sxs-lookup"><span data-stu-id="cbd02-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="cbd02-127">Quando o [agente do OMS é instalado em um cliente Linux](log-analytics-linux-agents.md), ele instala um arquivo de configuração de Syslog padrão, que define o recurso e a severidade das mensagens que são coletadas.</span><span class="sxs-lookup"><span data-stu-id="cbd02-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="cbd02-128">Você pode modificar esse arquivo para alterar a configuração.</span><span class="sxs-lookup"><span data-stu-id="cbd02-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="cbd02-129">O arquivo de configuração é diferente, dependendo do daemon do Syslog que o cliente tem instalado.</span><span class="sxs-lookup"><span data-stu-id="cbd02-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="cbd02-130">Se você editar a configuração de syslog, deverá reiniciar o daemon syslog para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="cbd02-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="cbd02-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-131">rsyslog</span></span>
<span data-ttu-id="cbd02-132">O arquivo de configuração para rsyslog está localizado em **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="cbd02-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="cbd02-133">Seu conteúdo padrão é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cbd02-133">Its default contents are shown below.</span></span>  <span data-ttu-id="cbd02-134">Isso coleta mensagens do syslog enviadas do agente local para todos os recursos com um nível de aviso ou superior.</span><span class="sxs-lookup"><span data-stu-id="cbd02-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="cbd02-135">Você pode remover um recurso removendo sua seção do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="cbd02-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="cbd02-136">Você pode limitar as severidades coletadas para um recurso específico, modificando a entrada desse recurso.</span><span class="sxs-lookup"><span data-stu-id="cbd02-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="cbd02-137">Por exemplo, para limitar o recurso do usuário a mensagens com uma severidade de erro ou superior, você modificaria essa linha do arquivo de configuração para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cbd02-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="cbd02-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="cbd02-138">syslog-ng</span></span>
<span data-ttu-id="cbd02-139">O arquivo de configuração para syslog-ng é a localização em **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="cbd02-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="cbd02-140">Seu conteúdo padrão é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cbd02-140">Its default contents are shown below.</span></span>  <span data-ttu-id="cbd02-141">Isso coleta mensagens do syslog enviadas do agente local para todos os recursos e todas as severidades.</span><span class="sxs-lookup"><span data-stu-id="cbd02-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="cbd02-142">Você pode remover um recurso removendo sua seção do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="cbd02-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="cbd02-143">Você pode limitar as severidades coletadas para um recurso específico, removendo-as de sua lista.</span><span class="sxs-lookup"><span data-stu-id="cbd02-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="cbd02-144">Por exemplo, para limitar o recurso exclusivamente a mensagens críticas e de alerta, você modificaria essa seção do arquivo de configuração para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cbd02-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="cbd02-145">Coletar dados de portas de Syslog adicionais</span><span class="sxs-lookup"><span data-stu-id="cbd02-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="cbd02-146">O agente do OMS escuta as mensagens do Syslog no cliente local na porta 25224.</span><span class="sxs-lookup"><span data-stu-id="cbd02-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="cbd02-147">Quando o agente é instalado, uma configuração de syslog padrão é aplicada e encontra o seguinte local:</span><span class="sxs-lookup"><span data-stu-id="cbd02-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="cbd02-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="cbd02-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="cbd02-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="cbd02-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="cbd02-150">Você pode alterar o número da porta criando dois arquivos de configuração: um arquivo de configuração FluentD, e um arquivo rsyslog-or-syslog-ng, dependendo do daemon do Syslog que você instalou.</span><span class="sxs-lookup"><span data-stu-id="cbd02-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="cbd02-151">O arquivo de configuração FluentD deve ser um novo arquivo localizado em: `/etc/opt/microsoft/omsagent/conf/omsagent.d` e substituir o valor na entrada da **porta** por seu número da porta personalizado.</span><span class="sxs-lookup"><span data-stu-id="cbd02-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="cbd02-152">Para rsyslog, você deve criar um novo arquivo de configuração localizado em: `/etc/rsyslog.d/` e substituir o valor % SYSLOG_PORT % pelo número da porta personalizada.</span><span class="sxs-lookup"><span data-stu-id="cbd02-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cbd02-153">Se você modificar esse valor no arquivo de configuração `95-omsagent.conf`, ele será substituído quando o agente aplicar a uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="cbd02-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="cbd02-154">A configuração de syslog-ng deve ser modificada por meio da cópia da configuração de exemplo mostrada abaixo e adicionando as configurações modificadas personalizadas ao final do arquivo de configuração syslog ng.conf localizado em `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="cbd02-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="cbd02-155">**Não** use o rótulo padrão **% WORKSPACE_ID %_oms** ou **% WORKSPACE_ID_OMS**, defina um rótulo personalizado para ajudar a distinguir as alterações.</span><span class="sxs-lookup"><span data-stu-id="cbd02-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cbd02-156">Se você modificar os valores padrão no arquivo de configuração, eles serão substituídos quando o agente aplicar uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="cbd02-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="cbd02-157">Depois de concluir as alterações, o Syslog e o serviço do agente do OMS precisarão ser reiniciados para garantir que as alterações de configuração entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="cbd02-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="cbd02-158">Propriedades de registro do syslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-158">Syslog record properties</span></span>
<span data-ttu-id="cbd02-159">Os registros do syslog têm um tipo de **Syslog** e têm as propriedades na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cbd02-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="cbd02-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbd02-160">Property</span></span> | <span data-ttu-id="cbd02-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbd02-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cbd02-162">Computador</span><span class="sxs-lookup"><span data-stu-id="cbd02-162">Computer</span></span> |<span data-ttu-id="cbd02-163">Computador do qual o evento foi coletado.</span><span class="sxs-lookup"><span data-stu-id="cbd02-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="cbd02-164">Recurso</span><span class="sxs-lookup"><span data-stu-id="cbd02-164">Facility</span></span> |<span data-ttu-id="cbd02-165">Define a parte do sistema que gerou a mensagem.</span><span class="sxs-lookup"><span data-stu-id="cbd02-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="cbd02-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="cbd02-166">HostIP</span></span> |<span data-ttu-id="cbd02-167">Endereço IP do sistema que envia a mensagem.</span><span class="sxs-lookup"><span data-stu-id="cbd02-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="cbd02-168">HostName</span><span class="sxs-lookup"><span data-stu-id="cbd02-168">HostName</span></span> |<span data-ttu-id="cbd02-169">Nome do sistema enviando a mensagem.</span><span class="sxs-lookup"><span data-stu-id="cbd02-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="cbd02-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="cbd02-170">SeverityLevel</span></span> |<span data-ttu-id="cbd02-171">Nível de severidade do evento.</span><span class="sxs-lookup"><span data-stu-id="cbd02-171">Severity level of the event.</span></span> |
| <span data-ttu-id="cbd02-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="cbd02-172">SyslogMessage</span></span> |<span data-ttu-id="cbd02-173">Texto da mensagem.</span><span class="sxs-lookup"><span data-stu-id="cbd02-173">Text of the message.</span></span> |
| <span data-ttu-id="cbd02-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="cbd02-174">ProcessID</span></span> |<span data-ttu-id="cbd02-175">A ID do processo que gerou a mensagem.</span><span class="sxs-lookup"><span data-stu-id="cbd02-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="cbd02-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="cbd02-176">EventTime</span></span> |<span data-ttu-id="cbd02-177">Data e hora em que o alerta foi gerado.</span><span class="sxs-lookup"><span data-stu-id="cbd02-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="cbd02-178">Consultas do log com registros do Syslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-178">Log queries with Syslog records</span></span>
<span data-ttu-id="cbd02-179">A tabela a seguir fornece diferentes exemplos de consultas de log que recuperam registros do Syslog.</span><span class="sxs-lookup"><span data-stu-id="cbd02-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="cbd02-180">Consultar</span><span class="sxs-lookup"><span data-stu-id="cbd02-180">Query</span></span> | <span data-ttu-id="cbd02-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbd02-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cbd02-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-182">Type=Syslog</span></span> |<span data-ttu-id="cbd02-183">Todos os Syslogs.</span><span class="sxs-lookup"><span data-stu-id="cbd02-183">All Syslogs.</span></span> |
| <span data-ttu-id="cbd02-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="cbd02-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="cbd02-185">Todos os registros do Syslog com a severidade de erro.</span><span class="sxs-lookup"><span data-stu-id="cbd02-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="cbd02-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="cbd02-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="cbd02-187">Contagem de registros do Syslog por computador.</span><span class="sxs-lookup"><span data-stu-id="cbd02-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="cbd02-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="cbd02-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="cbd02-189">Contagem de registros do Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="cbd02-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="cbd02-190">Se o seu espaço de trabalho fosse atualizado para a [nova linguagem de consulta do Log Analytics](log-analytics-log-search-upgrade.md), as consultas acima seriam alteradas para o demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="cbd02-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="cbd02-191">Consultar</span><span class="sxs-lookup"><span data-stu-id="cbd02-191">Query</span></span> | <span data-ttu-id="cbd02-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbd02-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cbd02-193">syslog</span><span class="sxs-lookup"><span data-stu-id="cbd02-193">Syslog</span></span> |<span data-ttu-id="cbd02-194">Todos os Syslogs.</span><span class="sxs-lookup"><span data-stu-id="cbd02-194">All Syslogs.</span></span> |
| <span data-ttu-id="cbd02-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="cbd02-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="cbd02-196">Todos os registros do Syslog com a severidade de erro.</span><span class="sxs-lookup"><span data-stu-id="cbd02-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="cbd02-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="cbd02-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="cbd02-198">Contagem de registros do Syslog por computador.</span><span class="sxs-lookup"><span data-stu-id="cbd02-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="cbd02-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="cbd02-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="cbd02-200">Contagem de registros do Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="cbd02-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cbd02-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cbd02-201">Next steps</span></span>
* <span data-ttu-id="cbd02-202">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) para analisar os dados coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="cbd02-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="cbd02-203">Use [campos personalizados](log-analytics-custom-fields.md) para analisar dados dos registros do syslog em campos individuais.</span><span class="sxs-lookup"><span data-stu-id="cbd02-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="cbd02-204">[Configure Agentes do Linux](log-analytics-linux-agents.md) para coletar outros tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="cbd02-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
