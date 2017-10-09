---
title: "aaaConnecting sua solução de auditoria e segurança produtos toohello segurança Operations Management Suite (OMS) | Microsoft Docs"
description: "Este documento ajuda você tooconnect sua tooOperations de produtos de segurança usando o formato de evento comuns de solução de auditoria e segurança do pacote de gerenciamento."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="9df8e-103">Conectar-se a sua solução de auditoria e segurança produtos toohello segurança Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="9df8e-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="9df8e-104">Este documento ajuda você a se conectar a seus produtos de segurança Olá segurança da OMS e solução de auditoria.</span><span class="sxs-lookup"><span data-stu-id="9df8e-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="9df8e-105">Olá as origens a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="9df8e-105">hello following sources are supported:</span></span>

- <span data-ttu-id="9df8e-106">Eventos de Formato de Evento Comum (CEF)</span><span class="sxs-lookup"><span data-stu-id="9df8e-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="9df8e-107">Eventos do Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="9df8e-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="9df8e-108">O que é CEF?</span><span class="sxs-lookup"><span data-stu-id="9df8e-108">What is CEF?</span></span>
<span data-ttu-id="9df8e-109">Formato de evento comuns (CEF) é um formato padrão da indústria sobre mensagens de Syslog, usado por muitos segurança fornecedores tooallow evento interoperabilidade entre plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="9df8e-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="9df8e-110">Suportam a ingestão de dados usando os produtos de segurança CEF, que permite que você tooconnect com segurança de OMS OMS solução de segurança e auditoria.</span><span class="sxs-lookup"><span data-stu-id="9df8e-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="9df8e-111">Conectando-se a tooOMS de fonte de dados, você está tootake capaz de aproveitar Olá recursos que fazem parte dessa plataforma a seguir:</span><span class="sxs-lookup"><span data-stu-id="9df8e-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="9df8e-112">Pesquisa e Correlação</span><span class="sxs-lookup"><span data-stu-id="9df8e-112">Search & Correlation</span></span>
- <span data-ttu-id="9df8e-113">Auditoria</span><span class="sxs-lookup"><span data-stu-id="9df8e-113">Auditing</span></span>
- <span data-ttu-id="9df8e-114">Alerta</span><span class="sxs-lookup"><span data-stu-id="9df8e-114">Alert</span></span>
- <span data-ttu-id="9df8e-115">Inteligência contra ameaças</span><span class="sxs-lookup"><span data-stu-id="9df8e-115">Threat Intelligence</span></span>
- <span data-ttu-id="9df8e-116">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="9df8e-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="9df8e-117">Coleção de logs da solução de segurança</span><span class="sxs-lookup"><span data-stu-id="9df8e-117">Collection of security solution logs</span></span>

<span data-ttu-id="9df8e-118">A Segurança do OMS dá suporte à coleta de logs usando CEF em Syslogs e de logs do [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="9df8e-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="9df8e-119">Neste exemplo, origem hello (computador que gera logs de saudação) é um computador Linux executando o daemon do syslog-ng e destino de saudação é segurança do OMS.</span><span class="sxs-lookup"><span data-stu-id="9df8e-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="9df8e-120">tarefas do computador com Linux tooprepare Olá que precisará Olá tooperform a seguir:</span><span class="sxs-lookup"><span data-stu-id="9df8e-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="9df8e-121">Baixe Olá agente do OMS para Linux, versão 1.2.0-25 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9df8e-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="9df8e-122">Siga a seção de saudação **guia de instalação rápida** de [neste artigo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall e Olá integrar agente tooyour espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9df8e-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="9df8e-123">Normalmente, Olá é instalado em um computador diferente da saudação um no qual logs Olá são gerados.</span><span class="sxs-lookup"><span data-stu-id="9df8e-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="9df8e-124">O computador de agente do encaminhamento Olá logs toohello geralmente exigirá Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9df8e-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="9df8e-125">Configure Olá log produto/máquina tooforward Olá eventos necessários toohello o syslog daemon (rsyslog ou syslog-ng) no computador do agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="9df8e-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="9df8e-126">Habilite o daemon do syslog Olá em mensagens de tooreceive de máquina de agente de saudação de um sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="9df8e-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="9df8e-127">No computador do agente hello, eventos de saudação necessário toobe enviado do hello syslog daemon toolocal a porta UDP 25226.</span><span class="sxs-lookup"><span data-stu-id="9df8e-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="9df8e-128">Olá agente está escutando para eventos de entrada nessa porta.</span><span class="sxs-lookup"><span data-stu-id="9df8e-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="9df8e-129">a seguir Olá é um exemplo de configuração para envio de todos os eventos do agente de toohello do sistema local hello (você pode modificar Olá configuração toofit as configurações locais):</span><span class="sxs-lookup"><span data-stu-id="9df8e-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="9df8e-130">Janela do terminal Olá aberta e vá toohello directory */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="9df8e-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="9df8e-131">Criar um novo arquivo *omsagent de configuração de segurança* e adicione Olá conteúdo a seguir: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="9df8e-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="9df8e-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="9df8e-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="9df8e-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="9df8e-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="9df8e-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="9df8e-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="9df8e-135">Baixe o arquivo hello *security_events.conf* e colocar em */etc/opt/microsoft/omsagent/conf/omsagent.d/* no computador do agente do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9df8e-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="9df8e-136">Digite comando Olá abaixo daemon do syslog Olá toorestart: *para syslog-ng executar:*</span><span class="sxs-lookup"><span data-stu-id="9df8e-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="9df8e-137">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="9df8e-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="9df8e-138">Digite o comando abaixo toorestart Olá agente do OMS hello:</span><span class="sxs-lookup"><span data-stu-id="9df8e-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="9df8e-139">*For syslog-ng run:*</span><span class="sxs-lookup"><span data-stu-id="9df8e-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="9df8e-140">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="9df8e-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="9df8e-141">Digite o comando de saudação abaixo e revise Olá tooconfirm de resultado que não há nenhum erro no log de agente do OMS hello:</span><span class="sxs-lookup"><span data-stu-id="9df8e-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="9df8e-142">Revisando os eventos de segurança coletados</span><span class="sxs-lookup"><span data-stu-id="9df8e-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="9df8e-143">Após hello configuração, eventos de segurança Olá iniciará toobe incluído por segurança do OMS.</span><span class="sxs-lookup"><span data-stu-id="9df8e-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="9df8e-144">toovisualize esses eventos, abra Olá pesquisa de Log, digite o comando de saudação *tipo = CommonSecurityLog* em Olá campo de pesquisa e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="9df8e-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="9df8e-145">Olá, exemplo a seguir mostra Olá resultado desse comando, observe que nesse caso OMS segurança já incluídos logs de segurança de vários fornecedores:</span><span class="sxs-lookup"><span data-stu-id="9df8e-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Avaliação de Linha de Base de Auditoria e Segurança do OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="9df8e-147">Você pode refinar essa pesquisa para um único fornecedor, por exemplo, toovisualize Cisco online logs, digite: *tipo = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="9df8e-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="9df8e-148">Olá "CommonSecurityLog" possui predefinido campos para qualquer cabeçalho CEF incluindo extensios básica hello, durante qualquer outra extensão seja "Extensão personalizada" ou não, será inserido no campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="9df8e-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="9df8e-149">Você pode usar campos de tooget dedicado de recurso de campos personalizados de saudação dele.</span><span class="sxs-lookup"><span data-stu-id="9df8e-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="9df8e-150">Acessando computadores sem avaliação de linha de base</span><span class="sxs-lookup"><span data-stu-id="9df8e-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="9df8e-151">OMS dá suporte para perfil de linha de base de membro de domínio Olá no Windows Server 2008 R2 até tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9df8e-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="9df8e-152">A linha de base do Windows Server 2016 ainda não é final e será adicionada assim que for publicada.</span><span class="sxs-lookup"><span data-stu-id="9df8e-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="9df8e-153">Todos os outros sistemas operacionais verificados por meio de avaliação de linha de base de segurança da OMS e auditoria aparecem sob Olá **computadores ausente avaliação de linha de base** seção.</span><span class="sxs-lookup"><span data-stu-id="9df8e-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="9df8e-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9df8e-154">See also</span></span>
<span data-ttu-id="9df8e-155">Neste documento, você aprendeu como tooconnect seu tooOMS de solução CEF.</span><span class="sxs-lookup"><span data-stu-id="9df8e-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="9df8e-156">toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9df8e-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="9df8e-157">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="9df8e-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="9df8e-158">Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria</span><span class="sxs-lookup"><span data-stu-id="9df8e-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="9df8e-159">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9df8e-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

