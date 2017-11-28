---
title: "aaaCollect e analisar as mensagens de Syslog na análise de logs do OMS | Microsoft Docs"
description: "Syslog é um protocolo de registro em log de eventos é tooLinux comuns. Este artigo descreve como tooconfigure coleção de mensagens de Syslog na análise de Log e os detalhes de registros de saudação criado no repositório do OMS hello."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="029c5-104">Fontes de dados de Syslog no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="029c5-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="029c5-105">Syslog é um protocolo de registro em log de eventos é tooLinux comuns.</span><span class="sxs-lookup"><span data-stu-id="029c5-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="029c5-106">Aplicativos enviará mensagens que podem ser armazenadas no computador local hello ou entregues tooa Syslog coletor.</span><span class="sxs-lookup"><span data-stu-id="029c5-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="029c5-107">Olá agente do OMS para Linux for instalado, ele configura Olá Syslog daemon tooforward mensagens toohello agente local.</span><span class="sxs-lookup"><span data-stu-id="029c5-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="029c5-108">Olá agente envia mensagem de saudação tooLog Analytics onde um registro correspondente é criado no repositório do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="029c5-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="029c5-109">Análise de log dá suporte a coleção de mensagens enviadas por rsyslog ou syslog-ng, onde rsyslog é o daemon saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="029c5-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="029c5-110">Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="029c5-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="029c5-111">Olá toocollect dados de syslog dessa versão de distribuições, [daemon de rsyslog](http://rsyslog.com) deve ser instalado e configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="029c5-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Coleção do Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="029c5-113">Configurando Syslog</span><span class="sxs-lookup"><span data-stu-id="029c5-113">Configuring Syslog</span></span>
<span data-ttu-id="029c5-114">Olá agente do OMS para Linux coletará apenas eventos com instalações de saudação e gravidades especificadas em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="029c5-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="029c5-115">Você pode configurar o Syslog por meio do portal do OMS hello ou por meio do gerenciamento de arquivos de configuração em seus agentes do Linux.</span><span class="sxs-lookup"><span data-stu-id="029c5-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="029c5-116">Configurar o Syslog no portal do OMS Olá</span><span class="sxs-lookup"><span data-stu-id="029c5-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="029c5-117">Configurar o Syslog Olá [menu dados nas configurações de análise de Log](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="029c5-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="029c5-118">Essa configuração é entregue toohello o arquivo de configuração em cada agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="029c5-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="029c5-119">Você pode adicionar um novo recurso, digitando seu nome e clicando em **+**.</span><span class="sxs-lookup"><span data-stu-id="029c5-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="029c5-120">Para cada recurso, apenas as mensagens com severidades de saudação selecionada serão coletadas.</span><span class="sxs-lookup"><span data-stu-id="029c5-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="029c5-121">Verifique severidades Olá para que você deseja toocollect de recurso específico do hello.</span><span class="sxs-lookup"><span data-stu-id="029c5-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="029c5-122">Você não pode fornecer qualquer critérios adicionais toofilter mensagens.</span><span class="sxs-lookup"><span data-stu-id="029c5-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Configurar Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="029c5-124">Por padrão, todas as alterações de configuração são enviadas automaticamente tooall agentes.</span><span class="sxs-lookup"><span data-stu-id="029c5-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="029c5-125">Se você quiser tooconfigure Syslog manualmente em cada agente do Linux, em seguida, desmarque a caixa Olá *aplicar abaixo máquinas de Linux toomy configuração*.</span><span class="sxs-lookup"><span data-stu-id="029c5-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="029c5-126">Configurar o Syslog no agente do Linux</span><span class="sxs-lookup"><span data-stu-id="029c5-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="029c5-127">Olá quando [agente do OMS é instalado em um cliente Linux](log-analytics-linux-agents.md), ele instala um arquivo de configuração de syslog padrão que define o recurso de saudação e gravidade da saudação mensagens que são coletados.</span><span class="sxs-lookup"><span data-stu-id="029c5-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="029c5-128">Você pode modificar essa configuração de saudação do arquivo toochange.</span><span class="sxs-lookup"><span data-stu-id="029c5-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="029c5-129">arquivo de configuração de saudação é diferente dependendo Olá Syslog daemon que Olá cliente foi instalado.</span><span class="sxs-lookup"><span data-stu-id="029c5-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="029c5-130">Se você editar configuração de syslog Olá, você deve reiniciar o daemon do syslog Olá Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="029c5-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="029c5-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="029c5-131">rsyslog</span></span>
<span data-ttu-id="029c5-132">Olá arquivo de configuração para rsyslog está localizado em **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="029c5-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="029c5-133">Seu conteúdo padrão é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="029c5-133">Its default contents are shown below.</span></span>  <span data-ttu-id="029c5-134">Isso reúne mensagens de syslog enviadas do agente local Olá para todos os recursos com um nível de aviso ou superior.</span><span class="sxs-lookup"><span data-stu-id="029c5-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="029c5-135">Você pode remover um recurso, removendo sua seção saudação do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="029c5-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="029c5-136">Você pode limitar severidades Olá que são coletadas para um recurso específico, modificando entrada desse recurso.</span><span class="sxs-lookup"><span data-stu-id="029c5-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="029c5-137">Por exemplo, toolimit Olá usuário recurso toomessages com uma severidade de erro ou maior que modificaria essa linha de saudação toohello de arquivo de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="029c5-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="029c5-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="029c5-138">syslog-ng</span></span>
<span data-ttu-id="029c5-139">arquivo de configuração de saudação do syslog-ng é local em **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="029c5-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="029c5-140">Seu conteúdo padrão é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="029c5-140">Its default contents are shown below.</span></span>  <span data-ttu-id="029c5-141">Isso reúne mensagens de syslog enviadas de agente local Olá para todos os recursos e todas as gravidades.</span><span class="sxs-lookup"><span data-stu-id="029c5-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="029c5-142">Você pode remover um recurso, removendo sua seção saudação do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="029c5-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="029c5-143">Você pode limitar severidades Olá que são coletadas para um recurso específico, removendo-as da sua lista.</span><span class="sxs-lookup"><span data-stu-id="029c5-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="029c5-144">Por exemplo, toolimit Olá usuário recurso toojust mensagens de alerta e críticas, deverá modificar essa seção do hello toohello de arquivo de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="029c5-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="029c5-145">Coletar dados de portas de Syslog adicionais</span><span class="sxs-lookup"><span data-stu-id="029c5-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="029c5-146">agente do OMS Olá escuta mensagens de Syslog no cliente local de saudação na porta 25224.</span><span class="sxs-lookup"><span data-stu-id="029c5-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="029c5-147">Quando Olá agente é instalado, uma configuração de syslog padrão é aplicada e encontrada no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="029c5-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="029c5-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="029c5-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="029c5-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="029c5-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="029c5-150">Você pode alterar o número da porta Olá criando dois arquivos de configuração: um arquivo de configuração FluentD e um arquivo de ng de rsyslog ou syslog dependendo de ter instalado o daemon Syslog hello.</span><span class="sxs-lookup"><span data-stu-id="029c5-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="029c5-151">arquivo de configuração do Hello FluentD deve ser um novo arquivo localizado em: `/etc/opt/microsoft/omsagent/conf/omsagent.d` e substitua o valor Olá Olá **porta** entrada com o número da porta personalizada.</span><span class="sxs-lookup"><span data-stu-id="029c5-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="029c5-152">Para rsyslog, você deve criar um novo arquivo de configuração localizado em: `/etc/rsyslog.d/` e substitua Olá valor % SYSLOG_PORT % com o número da porta personalizada.</span><span class="sxs-lookup"><span data-stu-id="029c5-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="029c5-153">Se você modificar esse valor no arquivo de configuração de saudação `95-omsagent.conf`, ele será substituído quando o agente de saudação aplica uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="029c5-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="029c5-154">Hello syslog-ng config deve ser modificado, copiando a configuração de exemplo hello mostrada abaixo e adicionando Olá personalizado configurações modificadas toohello final do arquivo de configuração de syslog ng.conf Olá localizado em `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="029c5-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="029c5-155">Fazer **não** usar saudação padrão rótulo **% WORKSPACE_ID % _oms** ou **% WORKSPACE_ID_OMS**, definir um personalizado toohelp rótulo distinguir as alterações.</span><span class="sxs-lookup"><span data-stu-id="029c5-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="029c5-156">Se você modificar os valores padrão de saudação no arquivo de configuração de hello, eles serão substituídos quando o agente de saudação aplica uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="029c5-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="029c5-157">Depois de concluir as alterações hello, Olá Syslog e hello o serviço de agente do OMS precisa toobe reiniciado tooensure Olá configuração alterações entrarão em vigor.</span><span class="sxs-lookup"><span data-stu-id="029c5-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="029c5-158">Propriedades de registro do syslog</span><span class="sxs-lookup"><span data-stu-id="029c5-158">Syslog record properties</span></span>
<span data-ttu-id="029c5-159">Registros de syslog têm um tipo de **Syslog** e têm propriedades de saudação em Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="029c5-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="029c5-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="029c5-160">Property</span></span> | <span data-ttu-id="029c5-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="029c5-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="029c5-162">Computador</span><span class="sxs-lookup"><span data-stu-id="029c5-162">Computer</span></span> |<span data-ttu-id="029c5-163">Computador que Olá evento foi coletado do.</span><span class="sxs-lookup"><span data-stu-id="029c5-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="029c5-164">Recurso</span><span class="sxs-lookup"><span data-stu-id="029c5-164">Facility</span></span> |<span data-ttu-id="029c5-165">Define a parte de saudação do sistema de saudação que gerou a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="029c5-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="029c5-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="029c5-166">HostIP</span></span> |<span data-ttu-id="029c5-167">Endereço IP do sistema Olá enviar mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="029c5-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="029c5-168">HostName</span><span class="sxs-lookup"><span data-stu-id="029c5-168">HostName</span></span> |<span data-ttu-id="029c5-169">Nome do sistema de saudação enviar mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="029c5-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="029c5-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="029c5-170">SeverityLevel</span></span> |<span data-ttu-id="029c5-171">Nível de severidade do evento hello.</span><span class="sxs-lookup"><span data-stu-id="029c5-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="029c5-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="029c5-172">SyslogMessage</span></span> |<span data-ttu-id="029c5-173">Texto da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="029c5-173">Text of hello message.</span></span> |
| <span data-ttu-id="029c5-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="029c5-174">ProcessID</span></span> |<span data-ttu-id="029c5-175">ID do processo de saudação que gerou a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="029c5-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="029c5-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="029c5-176">EventTime</span></span> |<span data-ttu-id="029c5-177">Data e hora em que Olá evento foi gerado.</span><span class="sxs-lookup"><span data-stu-id="029c5-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="029c5-178">Consultas do log com registros do Syslog</span><span class="sxs-lookup"><span data-stu-id="029c5-178">Log queries with Syslog records</span></span>
<span data-ttu-id="029c5-179">Olá tabela a seguir fornece exemplos de diferentes de consultas de log que recuperam registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="029c5-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="029c5-180">Consultar</span><span class="sxs-lookup"><span data-stu-id="029c5-180">Query</span></span> | <span data-ttu-id="029c5-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="029c5-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="029c5-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="029c5-182">Type=Syslog</span></span> |<span data-ttu-id="029c5-183">Todos os Syslogs.</span><span class="sxs-lookup"><span data-stu-id="029c5-183">All Syslogs.</span></span> |
| <span data-ttu-id="029c5-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="029c5-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="029c5-185">Todos os registros do Syslog com a severidade de erro.</span><span class="sxs-lookup"><span data-stu-id="029c5-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="029c5-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="029c5-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="029c5-187">Contagem de registros do Syslog por computador.</span><span class="sxs-lookup"><span data-stu-id="029c5-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="029c5-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="029c5-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="029c5-189">Contagem de registros do Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="029c5-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="029c5-190">Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="029c5-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="029c5-191">Consultar</span><span class="sxs-lookup"><span data-stu-id="029c5-191">Query</span></span> | <span data-ttu-id="029c5-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="029c5-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="029c5-193">syslog</span><span class="sxs-lookup"><span data-stu-id="029c5-193">Syslog</span></span> |<span data-ttu-id="029c5-194">Todos os Syslogs.</span><span class="sxs-lookup"><span data-stu-id="029c5-194">All Syslogs.</span></span> |
| <span data-ttu-id="029c5-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="029c5-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="029c5-196">Todos os registros do Syslog com a severidade de erro.</span><span class="sxs-lookup"><span data-stu-id="029c5-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="029c5-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="029c5-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="029c5-198">Contagem de registros do Syslog por computador.</span><span class="sxs-lookup"><span data-stu-id="029c5-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="029c5-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="029c5-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="029c5-200">Contagem de registros do Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="029c5-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="029c5-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="029c5-201">Next steps</span></span>
* <span data-ttu-id="029c5-202">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="029c5-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="029c5-203">Use [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registros de syslog em campos individuais.</span><span class="sxs-lookup"><span data-stu-id="029c5-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="029c5-204">[Configurar agentes do Linux](log-analytics-linux-agents.md) toocollect outros tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="029c5-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
