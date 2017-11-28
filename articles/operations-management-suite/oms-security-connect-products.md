---
title: "Conectando seus produtos de segurança à Solução de Segurança e Auditoria do OMS (Operations Management Suite) | Microsoft Docs"
description: "Este documento ajudará você a conectar seus produtos de segurança à Solução de Segurança e Auditoria do OMS usando Formato de Evento Comum."
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
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="18462-103">Conectando seus produtos de segurança à Solução de Segurança e Auditoria do OMS (Operations Management Suite)</span><span class="sxs-lookup"><span data-stu-id="18462-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="18462-104">Este documento ajudará você a conectar seus produtos de segurança à Solução de Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="18462-105">Há suporte para as fontes a seguir:</span><span class="sxs-lookup"><span data-stu-id="18462-105">The following sources are supported:</span></span>

- <span data-ttu-id="18462-106">Eventos de Formato de Evento Comum (CEF)</span><span class="sxs-lookup"><span data-stu-id="18462-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="18462-107">Eventos do Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="18462-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="18462-108">O que é CEF?</span><span class="sxs-lookup"><span data-stu-id="18462-108">What is CEF?</span></span>
<span data-ttu-id="18462-109">O Formato de Evento Comum (CEF) é um formato padrão da indústria, além das mensagens Syslog, usado por muitos fornecedores de segurança para permitir a interoperabilidade de eventos entre diferentes plataformas.</span><span class="sxs-lookup"><span data-stu-id="18462-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="18462-110">A Solução de Segurança e Auditoria do OMS dá suporte à ingestão de dados usando CEF, o que permite que você conecte seus produtos de segurança com a Segurança do OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="18462-111">Ao conectar a fonte de dados com o OMS, você poderá tirar vantagem dos recursos a seguir, que fazem parte dessa plataforma:</span><span class="sxs-lookup"><span data-stu-id="18462-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="18462-112">Pesquisa e Correlação</span><span class="sxs-lookup"><span data-stu-id="18462-112">Search & Correlation</span></span>
- <span data-ttu-id="18462-113">Auditoria</span><span class="sxs-lookup"><span data-stu-id="18462-113">Auditing</span></span>
- <span data-ttu-id="18462-114">Alerta</span><span class="sxs-lookup"><span data-stu-id="18462-114">Alert</span></span>
- <span data-ttu-id="18462-115">Inteligência contra ameaças</span><span class="sxs-lookup"><span data-stu-id="18462-115">Threat Intelligence</span></span>
- <span data-ttu-id="18462-116">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="18462-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="18462-117">Coleção de logs da solução de segurança</span><span class="sxs-lookup"><span data-stu-id="18462-117">Collection of security solution logs</span></span>

<span data-ttu-id="18462-118">A Segurança do OMS dá suporte à coleta de logs usando CEF em Syslogs e de logs do [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="18462-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="18462-119">Neste exemplo, a origem (computador que gera os logs) é um computador Linux executando o daemon syslog-ng e o destino é a Segurança do OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="18462-120">Para preparar o computador Linux, você precisará executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="18462-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="18462-121">Baixe o Agente do OMS para Linux, versão 1.2.0-25 ou superior.</span><span class="sxs-lookup"><span data-stu-id="18462-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="18462-122">Siga a seção **Guia de Instalação Rápida** [deste artigo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) para instalar e carregar o agente em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="18462-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="18462-123">Normalmente, o agente é instalado em um computador diferente do qual os logs são gerados.</span><span class="sxs-lookup"><span data-stu-id="18462-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="18462-124">O encaminhamento dos logs para o computador agente geralmente exigirá as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="18462-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="18462-125">Configure o produto/máquina de logs para encaminhar os eventos necessários para o daemon syslog (rsyslog ou syslo-ng) no computador agente.</span><span class="sxs-lookup"><span data-stu-id="18462-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="18462-126">Habilite o daemon syslog no computador agente para receber mensagens de um sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="18462-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="18462-127">No computador agente, os eventos precisam ser enviados do daemon syslog para a porta UDP local 25226.</span><span class="sxs-lookup"><span data-stu-id="18462-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="18462-128">O agente está ouvindo eventos de entrada nessa porta.</span><span class="sxs-lookup"><span data-stu-id="18462-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="18462-129">A seguir está um exemplo de configuração para o envio de todos os eventos do sistema local para o agente (você pode modificar a configuração para se ajustar às suas configurações locais):</span><span class="sxs-lookup"><span data-stu-id="18462-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="18462-130">Abra a janela do terminal e vá para o diretório */etc/syslog-ng/*</span><span class="sxs-lookup"><span data-stu-id="18462-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="18462-131">Crie um novo arquivo *security-config-omsagent.conf* e adicione o seguinte conteúdo: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="18462-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="18462-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="18462-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="18462-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="18462-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="18462-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="18462-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="18462-135">Baixe o arquivo *security_events.conf* e coloque-o em */etc/opt/microsoft/omsagent/conf/omsagent.d/* no computador agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="18462-136">Digite o comando a seguir para reiniciar o daemon do syslog: *para syslog-ng executar:*</span><span class="sxs-lookup"><span data-stu-id="18462-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="18462-137">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="18462-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="18462-138">Digite o comando abaixo para reiniciar o Agente OMS:</span><span class="sxs-lookup"><span data-stu-id="18462-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="18462-139">*For syslog-ng run:*</span><span class="sxs-lookup"><span data-stu-id="18462-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="18462-140">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="18462-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="18462-141">Digite o comando abaixo e examine o resultado para confirmar que não há erros no log do Agente do OMS:</span><span class="sxs-lookup"><span data-stu-id="18462-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="18462-142">Revisando os eventos de segurança coletados</span><span class="sxs-lookup"><span data-stu-id="18462-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="18462-143">Após terminar configuração, o evento de segurança começará a ser processado pela Segurança do OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="18462-144">Para visualizar esses eventos, abra a Pesquisa de Log, digite o comando *Type=CommonSecurityLog* no campo de pesquisa e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="18462-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="18462-145">O exemplo a seguir mostra o resultado desse comando. Observe que, nesse caso, a Segurança do OMS já incluiu logs de segurança de vários fornecedores:</span><span class="sxs-lookup"><span data-stu-id="18462-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Avaliação de Linha de Base de Auditoria e Segurança do OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="18462-147">Você pode refinar a pesquisa para um único fornecedor, por exemplo, para visualizar logs Cisco online, digite: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="18462-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="18462-148">"CommonSecurityLog" tem campos predefinidos para qualquer cabeçalho CEF, incluindo as extensões básicas, sendo que qualquer outra extensão, seja "Extensão Personalizada" ou não, será inserida no campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="18462-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="18462-149">Você pode usar o recurso de Campos Personalizados para obter campos dedicados.</span><span class="sxs-lookup"><span data-stu-id="18462-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="18462-150">Acessando computadores sem avaliação de linha de base</span><span class="sxs-lookup"><span data-stu-id="18462-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="18462-151">O OMS dá suporte ao perfil de linha de base de membro do domínio do Windows Server 2008 R2 até o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18462-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="18462-152">A linha de base do Windows Server 2016 ainda não é final e será adicionada assim que for publicada.</span><span class="sxs-lookup"><span data-stu-id="18462-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="18462-153">Todos os outros sistemas operacionais examinados por meio da avaliação de linha de base da Segurança e Auditoria do OMS estão na seção **Computadores sem avaliação de linha de base**.</span><span class="sxs-lookup"><span data-stu-id="18462-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="18462-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="18462-154">See also</span></span>
<span data-ttu-id="18462-155">Neste documento, você aprendeu como conectar sua solução CEF ao OMS.</span><span class="sxs-lookup"><span data-stu-id="18462-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="18462-156">Para saber mais sobre a Segurança do OMS, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="18462-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="18462-157">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="18462-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="18462-158">Monitorando e respondendo a alertas de segurança na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="18462-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="18462-159">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="18462-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

