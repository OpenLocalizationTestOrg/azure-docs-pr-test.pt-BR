---
title: Conectar computadores Linux ao OMS (Operations Management Suite) | Microsoft Docs
description: Este artigo descreve como conectar computadores Linux hospedados no Azure, em outra nuvem ou localmente ao OMS usando o Agente do OMS para Linux.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a><span data-ttu-id="9dedf-103">Conectar computadores Linux ao OMS (Operations Management Suite)</span><span class="sxs-lookup"><span data-stu-id="9dedf-103">Connect your Linux Computers to Operations Management Suite (OMS)</span></span> 

<span data-ttu-id="9dedf-104">Com o OMS (Microsoft Operations Management Suite), você pode coletar e agir sobre os dados gerados em computadores Linux e soluções de contêiner como o Docker, residindo em seu data center local como servidores físicos ou máquinas virtuais, máquinas virtuais em um serviço hospedado em nuvem como AWS (Amazon Web Services) ou Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9dedf-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="9dedf-105">Você também pode usar soluções de gerenciamento disponíveis no OMS, como Controle de Alterações, para identificar alterações de configuração e Gerenciamento de Atualizações para gerenciar atualizações de software para gerenciar proativamente o ciclo de vida das VMs Linux.</span><span class="sxs-lookup"><span data-stu-id="9dedf-105">You can also use management solutions available in OMS such as Change Tracking, to identify configuration changes, and Update Management to manage software updates to proactively manage the lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="9dedf-106">O Agente do OMS para Linux se comunica na saída com o serviço OMS na porta TCP 443. Caso o computador se conecte a um firewall ou servidor proxy para se comunicar pela Internet, examine [Configurando o agente para uso com um servidor proxy HTTP ou Gateway do OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) para entender quais alterações de configuração precisarão ser aplicadas.</span><span class="sxs-lookup"><span data-stu-id="9dedf-106">The OMS Agent for Linux communicates outbound with the OMS service over TCP port 443, and if the computer connects to a firewall or proxy server to communicate over the Internet, review [Configuring the agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) to understand what configuration changes will need to be applied.</span></span>  <span data-ttu-id="9dedf-107">Se você estiver monitorando o computador com o System Center 2016 – Operations Manager ou Operations Manager 2012 R2, ele poderá ser multihomed com o serviço OMS para coletar dados e encaminhe para o serviço e ainda ser monitorado pelo Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="9dedf-107">If you are monitoring the computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with the OMS service to collect data and forward to the service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="9dedf-108">Os computadores Linux monitorados por um grupo de gerenciamento do Operations Manager integrado ao OMS não recebem a configuração de fontes de dados e encaminham os dados coletados pelo grupo de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="9dedf-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through the management group.</span></span>  <span data-ttu-id="9dedf-109">O agente do OMS não pode ser configurado para se reportar a mais de um espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9dedf-109">The OMS agent cannot be configured to report to more than one workspace.</span></span>  

<span data-ttu-id="9dedf-110">Se suas políticas de segurança não permitem que computadores em sua rede se conectem à Internet, o agente pode ser configurado para se conectar ao Gateway do OMS para receber informações de configuração e enviar os dados coletados dependendo da solução habilitada.</span><span class="sxs-lookup"><span data-stu-id="9dedf-110">If your IT security policies do not allow computers on your network to connect to the Internet, the agent can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span> <span data-ttu-id="9dedf-111">Para obter mais informações e etapas sobre como configurar o Agente do OMS para Linux para se comunicar através de um Gateway do OMS ao serviço OMS, consulte [Conectar computadores ao OMS usando o Gateway do OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9dedf-111">For more information and steps on how to configure your OMS Linux Agent to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="9dedf-112">O diagrama a seguir ilustra a conexão entre os computadores Linux gerenciados por agente e o OMS, incluindo a direção e as portas.</span><span class="sxs-lookup"><span data-stu-id="9dedf-112">The following diagram depicts the connection between the agent-managed Linux computers and OMS, including the direction and ports.</span></span>

![diagrama Comunicação do agente direto com o OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="9dedf-114">Requisitos do sistema</span><span class="sxs-lookup"><span data-stu-id="9dedf-114">System requirements</span></span>
<span data-ttu-id="9dedf-115">Antes de começar, examine os detalhes a seguir para verificar se você atende aos pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="9dedf-115">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="9dedf-116">Sistemas operacionais Linux com suporte</span><span class="sxs-lookup"><span data-stu-id="9dedf-116">Supported Linux operating systems</span></span>
<span data-ttu-id="9dedf-117">As seguintes distribuições Linux têm suporte oficialmente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-117">The following Linux distributions are officially supported.</span></span>  <span data-ttu-id="9dedf-118">No entanto, o Agente do OMS para Linux também pode ser executado em outras distribuições não listadas.</span><span class="sxs-lookup"><span data-stu-id="9dedf-118">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="9dedf-119">Amazon Linux 2012.09 a 2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-119">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="9dedf-120">CentOS Linux 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="9dedf-121">Oracle Linux 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="9dedf-122">Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="9dedf-123">Debian GNU/Linux 6, 7 e 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="9dedf-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="9dedf-125">SUSE Linux Enterprise Server 11 e 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9dedf-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="9dedf-126">Rede</span><span class="sxs-lookup"><span data-stu-id="9dedf-126">Network</span></span>
<span data-ttu-id="9dedf-127">As informações abaixo listam as informações de configuração de proxy e firewall necessárias para que o agente do Linux se comunique com o OMS.</span><span class="sxs-lookup"><span data-stu-id="9dedf-127">The information below list the proxy and firewall configuration information required for the Linux agent to communicate with OMS.</span></span> <span data-ttu-id="9dedf-128">O tráfego é de saída da rede para o serviço OMS.</span><span class="sxs-lookup"><span data-stu-id="9dedf-128">Traffic is outbound from your network to the OMS service.</span></span> 

|<span data-ttu-id="9dedf-129">Recurso de agente</span><span class="sxs-lookup"><span data-stu-id="9dedf-129">Agent Resource</span></span>| <span data-ttu-id="9dedf-130">Portas</span><span class="sxs-lookup"><span data-stu-id="9dedf-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="9dedf-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9dedf-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="9dedf-132">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-132">Port 443</span></span>|   
|<span data-ttu-id="9dedf-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9dedf-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="9dedf-134">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-134">Port 443</span></span>|   
|<span data-ttu-id="9dedf-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9dedf-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="9dedf-136">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-136">Port 443</span></span>|   
|<span data-ttu-id="9dedf-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="9dedf-137">*.azure-automation.net</span></span> | <span data-ttu-id="9dedf-138">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="9dedf-139">Requisitos do pacote</span><span class="sxs-lookup"><span data-stu-id="9dedf-139">Package requirements</span></span>

 <span data-ttu-id="9dedf-140">**Pacote necessário**</span><span class="sxs-lookup"><span data-stu-id="9dedf-140">**Required package**</span></span>   | <span data-ttu-id="9dedf-141">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="9dedf-141">**Description**</span></span>   | <span data-ttu-id="9dedf-142">**Versão mínima**</span><span class="sxs-lookup"><span data-stu-id="9dedf-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="9dedf-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="9dedf-143">Glibc</span></span> | <span data-ttu-id="9dedf-144">Biblioteca GNU C</span><span class="sxs-lookup"><span data-stu-id="9dedf-144">GNU C Library</span></span>   | <span data-ttu-id="9dedf-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="9dedf-145">2.5-12</span></span> 
<span data-ttu-id="9dedf-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="9dedf-146">Openssl</span></span> | <span data-ttu-id="9dedf-147">Bibliotecas OpenSSL</span><span class="sxs-lookup"><span data-stu-id="9dedf-147">OpenSSL Libraries</span></span> | <span data-ttu-id="9dedf-148">0.9.8e ou 1.0</span><span class="sxs-lookup"><span data-stu-id="9dedf-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="9dedf-149">Curl</span><span class="sxs-lookup"><span data-stu-id="9dedf-149">Curl</span></span> | <span data-ttu-id="9dedf-150">cliente Web cURL</span><span class="sxs-lookup"><span data-stu-id="9dedf-150">cURL web client</span></span> | <span data-ttu-id="9dedf-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="9dedf-151">7.15.5</span></span>
<span data-ttu-id="9dedf-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="9dedf-152">Python-ctypes</span></span> | | 
<span data-ttu-id="9dedf-153">PAM</span><span class="sxs-lookup"><span data-stu-id="9dedf-153">PAM</span></span> | <span data-ttu-id="9dedf-154">Módulos de autenticação conectáveis</span><span class="sxs-lookup"><span data-stu-id="9dedf-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="9dedf-155">Rsyslog ou syslog-ng são necessários para coletar mensagens de syslog.</span><span class="sxs-lookup"><span data-stu-id="9dedf-155">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="9dedf-156">O daemon syslog padrão na versão 5 do Red Hat Enterprise Linux, CentOS e na versão Oracle Linux (sysklog) não tem suporte para a coleta de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="9dedf-156">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9dedf-157">Para coletar dados de syslog nessa versão dessas distribuições, o daemon rsyslog deve ser instalado e configurado para substituir sysklog.</span><span class="sxs-lookup"><span data-stu-id="9dedf-157">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog,</span></span> 

<span data-ttu-id="9dedf-158">O agente inclui vários pacotes.</span><span class="sxs-lookup"><span data-stu-id="9dedf-158">The agent includes multiple packages.</span></span> <span data-ttu-id="9dedf-159">O arquivo de versão contém os seguintes pacotes, disponíveis por meio da execução do pacote do shell com `--extract`:</span><span class="sxs-lookup"><span data-stu-id="9dedf-159">The release file contains the following packages, available by running the shell bundle with `--extract`:</span></span>

<span data-ttu-id="9dedf-160">**Pacote**</span><span class="sxs-lookup"><span data-stu-id="9dedf-160">**Package**</span></span> | <span data-ttu-id="9dedf-161">**Versão**</span><span class="sxs-lookup"><span data-stu-id="9dedf-161">**Version**</span></span> | <span data-ttu-id="9dedf-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="9dedf-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="9dedf-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="9dedf-163">omsagent</span></span> | <span data-ttu-id="9dedf-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="9dedf-164">1.4.0</span></span> | <span data-ttu-id="9dedf-165">O Agente do Operations Management Suite para Linux</span><span class="sxs-lookup"><span data-stu-id="9dedf-165">The Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="9dedf-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="9dedf-166">omsconfig</span></span> | <span data-ttu-id="9dedf-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9dedf-167">1.1.1</span></span> | <span data-ttu-id="9dedf-168">Agente de configuração para o Agente do OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-168">Configuration agent for the OMS Agent</span></span>
<span data-ttu-id="9dedf-169">omi</span><span class="sxs-lookup"><span data-stu-id="9dedf-169">omi</span></span> | <span data-ttu-id="9dedf-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9dedf-170">1.2.0</span></span> | <span data-ttu-id="9dedf-171">OMI (Open Management Infrastructure) – um servidor CIM leve</span><span class="sxs-lookup"><span data-stu-id="9dedf-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="9dedf-172">scx</span><span class="sxs-lookup"><span data-stu-id="9dedf-172">scx</span></span> | <span data-ttu-id="9dedf-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="9dedf-173">1.6.3</span></span> | <span data-ttu-id="9dedf-174">Provedores de CIM OMI para métricas de desempenho do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="9dedf-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="9dedf-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="9dedf-175">apache-cimprov</span></span> | <span data-ttu-id="9dedf-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9dedf-176">1.0.1</span></span> | <span data-ttu-id="9dedf-177">Provedor de monitoramento de desempenho do Servidor HTTP Apache para OMI.</span><span class="sxs-lookup"><span data-stu-id="9dedf-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9dedf-178">Instalado se o Servidor HTTP Apache for detectado.</span><span class="sxs-lookup"><span data-stu-id="9dedf-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="9dedf-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="9dedf-179">mysql-cimprov</span></span> | <span data-ttu-id="9dedf-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9dedf-180">1.0.1</span></span> | <span data-ttu-id="9dedf-181">Provedor de monitoramento de desempenho do Servidor MySQL para OMI.</span><span class="sxs-lookup"><span data-stu-id="9dedf-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9dedf-182">Instalado se o servidor MySQL/MariaDB for detectado.</span><span class="sxs-lookup"><span data-stu-id="9dedf-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="9dedf-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="9dedf-183">docker-cimprov</span></span> | <span data-ttu-id="9dedf-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9dedf-184">1.0.0</span></span> | <span data-ttu-id="9dedf-185">Provedor do Docker para OMI.</span><span class="sxs-lookup"><span data-stu-id="9dedf-185">Docker provider for OMI.</span></span> <span data-ttu-id="9dedf-186">Instalado se o Docker for detectado.</span><span class="sxs-lookup"><span data-stu-id="9dedf-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="9dedf-187">Compatibilidade com o System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9dedf-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="9dedf-188">O Agente do OMS para Linux compartilha arquivos binários de agente com o agente do System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="9dedf-188">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="9dedf-189">Se você instalar o Agente do OMS para Linux em um sistema atualmente gerenciado pelo Operations Manager, atualiza os pacotes OMI e SCX no computador para uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-189">If you install the OMS Agent for Linux on a system currently managed by Operations Manager, it the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="9dedf-190">Nesta versão, o OMS e o System Center 2016 – agentes do Operations Manager/Operations Manager 2012 R2 para Linux são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="9dedf-190">In this release, the OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="9dedf-191">O System Center 2012 SP1 e versões anteriores atualmente não são compatíveis com o Agente do OMS para Linux ou não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="9dedf-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="9dedf-192">Se o Agente do OMS para Linux for instalado em um computador que não é monitorado pelo Operations Manager no momento e você desejar monitorar o computador com o Operations Manager, será necessário modificar a [configuração do OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) antes de descobrir o computador.</span><span class="sxs-lookup"><span data-stu-id="9dedf-192">If the OMS Agent for Linux is installed to a computer that is not currently monitored by Operations Manager, and you then wish to monitor the computer with Operations Manager, you must modify the [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior to discovering the computer.</span></span> <span data-ttu-id="9dedf-193">**Esta etapa não *será* necessária se o agente do Operations Manager for instalado antes do Agente do OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="9dedf-193">**This step is *not* needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="9dedf-194">Alterações de configuração do sistema</span><span class="sxs-lookup"><span data-stu-id="9dedf-194">System configuration changes</span></span>
<span data-ttu-id="9dedf-195">Após a instalação dos pacotes do Agente do OMS para Linux, serão aplicadas as seguintes alterações de configuração adicionais em todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="9dedf-195">After installing the OMS Agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="9dedf-196">Esses artefatos serão removidos quando o pacote omsagent for desinstalado.</span><span class="sxs-lookup"><span data-stu-id="9dedf-196">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="9dedf-197">Um usuário sem privilégios chamado: `omsagent` é criado.</span><span class="sxs-lookup"><span data-stu-id="9dedf-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="9dedf-198">O daemon omsagent é executado como essa conta.</span><span class="sxs-lookup"><span data-stu-id="9dedf-198">This is the account the omsagent daemon runs as.</span></span>
* <span data-ttu-id="9dedf-199">Um arquivo "include" sudoers é criado em /etc/sudoers.d/omsagent.</span><span class="sxs-lookup"><span data-stu-id="9dedf-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="9dedf-200">Isso autoriza o omsagent a reiniciar os daemons syslog e omsagent.</span><span class="sxs-lookup"><span data-stu-id="9dedf-200">This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="9dedf-201">Se o sudo incluir diretivas sem suporte na versão instalada do sudo, essas entradas serão gravadas em /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="9dedf-201">If sudo “include” directives are not supported in the installed version of sudo, these entries are written to /etc/sudoers.</span></span>
* <span data-ttu-id="9dedf-202">A configuração de syslog é modificada para encaminhar um subconjunto de eventos para o agente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-202">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="9dedf-203">Para saber mais, confira a seção **Configuração da Coleta de Dados** abaixo</span><span class="sxs-lookup"><span data-stu-id="9dedf-203">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="9dedf-204">Atualizar de uma versão anterior</span><span class="sxs-lookup"><span data-stu-id="9dedf-204">Upgrade from a previous release</span></span>
<span data-ttu-id="9dedf-205">A atualização de versões anteriores à 1.0.0-47 tem suporte nesta versão.</span><span class="sxs-lookup"><span data-stu-id="9dedf-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="9dedf-206">Executar a instalação com o comando `--upgrade` atualizará todos os componentes do agente para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-206">Performing the installation with the `--upgrade` command upgrades all components of the agent to the latest version.</span></span>

## <a name="installing-the-agent"></a><span data-ttu-id="9dedf-207">Instalando o agente</span><span class="sxs-lookup"><span data-stu-id="9dedf-207">Installing the agent</span></span>

<span data-ttu-id="9dedf-208">Esta seção descreve como instalar o agente do OMS para Linux usando um pacote, que contém pacotes Debian e RPM para cada um dos componentes do agente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-208">This section describes how to install the OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of the agent components.</span></span>  <span data-ttu-id="9dedf-209">Ele pode ser instalado diretamente ou extraído para recuperar os pacotes individuais.</span><span class="sxs-lookup"><span data-stu-id="9dedf-209">It can be installed directly or extracted to retrieve the individual packages.</span></span>  

<span data-ttu-id="9dedf-210">Primeiro, você precisa da ID e chave de seu espaço de trabalho do OMS, que podem ser encontradas alternando para o [Portal Clássico do OMS](https://mms.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9dedf-210">First you need your OMS workspace ID and key, which you can find by switching to the [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="9dedf-211">Na página **Visão geral**, no menu superior, selecione **Configurações** e, em seguida, navegue até **Fontes Conectadas\Servidores Linux**.</span><span class="sxs-lookup"><span data-stu-id="9dedf-211">On the **Overview** page, from the top menu select **Settings**, and then navigate to **Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="9dedf-212">Você verá o valor à direita da **ID do Espaço de Trabalho** e **Chave Primária**.</span><span class="sxs-lookup"><span data-stu-id="9dedf-212">You see the value to the right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="9dedf-213">Copie e cole os dois em seu editor favorito.</span><span class="sxs-lookup"><span data-stu-id="9dedf-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="9dedf-214">Baixe o versão mais recente [agente do OMS para Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) ou [agente do OMS para Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9dedf-214">Download the latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="9dedf-215">Transfira o pacote apropriado (x86 ou x64) para seu computador Linux usando scp/sftp.</span><span class="sxs-lookup"><span data-stu-id="9dedf-215">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="9dedf-216">Instale o pacote usando o argumento `--install` ou `--upgrade`.</span><span class="sxs-lookup"><span data-stu-id="9dedf-216">Install the bundle by using the `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9dedf-217">Se houver qualquer pacote existente instalado, como quando o agente do System Center Operations Manager para Linux já está instalado, use o argumento `--upgrade`.</span><span class="sxs-lookup"><span data-stu-id="9dedf-217">If any existing packages are installed such as when the System Center Operations Manager agent for Linux is already installed, use the `--upgrade` argument.</span></span> <span data-ttu-id="9dedf-218">Para se conectar ao Operations Management Suite durante a instalação, forneça os parâmetros `-w <WorkspaceID>` e `-s <Shared Key>`.</span><span class="sxs-lookup"><span data-stu-id="9dedf-218">To connect to Operations Management Suite during installation, provide the `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="to-install-and-onboard-directly"></a><span data-ttu-id="9dedf-219">Para instalar e integrar diretamente</span><span class="sxs-lookup"><span data-stu-id="9dedf-219">To install and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a><span data-ttu-id="9dedf-220">Para atualizar o pacote do agente</span><span class="sxs-lookup"><span data-stu-id="9dedf-220">To upgrade the agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a><span data-ttu-id="9dedf-221">Para instalar e integrar para um espaço de trabalho no Nuvem do Governo dos EUA</span><span class="sxs-lookup"><span data-stu-id="9dedf-221">To install and onboard to a workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="9dedf-222">Configurando o agente para uso com um servidor proxy HTTP ou Gateway do OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-222">Configuring the agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="9dedf-223">O Agente do OMS para Linux dá suporte para a comunicação por meio de um servidor proxy HTTP, HTTPS ou Gateway do OMS para o serviço OMS.</span><span class="sxs-lookup"><span data-stu-id="9dedf-223">The OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway to the OMS service.</span></span>  <span data-ttu-id="9dedf-224">Há suporte para a autenticação anônima e básica (nome de usuário/senha).</span><span class="sxs-lookup"><span data-stu-id="9dedf-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="9dedf-225">Configuração de Proxy</span><span class="sxs-lookup"><span data-stu-id="9dedf-225">Proxy configuration</span></span>
<span data-ttu-id="9dedf-226">O valor de configuração de proxy tem a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="9dedf-226">The proxy configuration value has the following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="9dedf-227">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9dedf-227">Property</span></span>|<span data-ttu-id="9dedf-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="9dedf-228">Description</span></span>
-|-
<span data-ttu-id="9dedf-229">Protocolo</span><span class="sxs-lookup"><span data-stu-id="9dedf-229">Protocol</span></span>|<span data-ttu-id="9dedf-230">http ou https</span><span class="sxs-lookup"><span data-stu-id="9dedf-230">http or https</span></span>
<span data-ttu-id="9dedf-231">usuário</span><span class="sxs-lookup"><span data-stu-id="9dedf-231">user</span></span>|<span data-ttu-id="9dedf-232">Nome de usuário opcional para autenticação de proxy</span><span class="sxs-lookup"><span data-stu-id="9dedf-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="9dedf-233">Senha</span><span class="sxs-lookup"><span data-stu-id="9dedf-233">password</span></span>|<span data-ttu-id="9dedf-234">Senha opcional para autenticação de proxy</span><span class="sxs-lookup"><span data-stu-id="9dedf-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="9dedf-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="9dedf-235">proxyhost</span></span>|<span data-ttu-id="9dedf-236">Endereço ou FQDN do servidor proxy/Gateway do OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-236">Address or FQDN of the proxy server/OMS Gateway</span></span>
<span data-ttu-id="9dedf-237">porta</span><span class="sxs-lookup"><span data-stu-id="9dedf-237">port</span></span>|<span data-ttu-id="9dedf-238">Número da porta opcional para o servidor proxy/OMS do Gateway</span><span class="sxs-lookup"><span data-stu-id="9dedf-238">Optional port number for the proxy server/OMS Gateway</span></span>

<span data-ttu-id="9dedf-239">Por exemplo: `http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="9dedf-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="9dedf-240">O servidor proxy pode ser especificado durante a instalação ou modificando o arquivo de configuração proxy.conf após a instalação.</span><span class="sxs-lookup"><span data-stu-id="9dedf-240">The proxy server can be specified during installation or by modifying the proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="9dedf-241">Especificar a configuração de proxy durante a instalação</span><span class="sxs-lookup"><span data-stu-id="9dedf-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="9dedf-242">O argumento `-p` ou `--proxy` para o pacote de instalação omsagent especifica a configuração de proxy a ser usada.</span><span class="sxs-lookup"><span data-stu-id="9dedf-242">The `-p` or `--proxy` argument for the omsagent installation bundle specifies the proxy configuration to use.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a><span data-ttu-id="9dedf-243">Definir a configuração de proxy em um arquivo</span><span class="sxs-lookup"><span data-stu-id="9dedf-243">Define the proxy configuration in a file</span></span>
<span data-ttu-id="9dedf-244">A configuração de proxy pode ser definida nos arquivos `/etc/opt/microsoft/omsagent/proxy.conf` e `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span><span class="sxs-lookup"><span data-stu-id="9dedf-244">The proxy configuration can be set in the files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="9dedf-245">Os arquivos podem ser criados ou editados diretamente, mas as permissões devem ser atualizadas para conceder ao usuário omiuser as permissões de leitura nos arquivos.</span><span class="sxs-lookup"><span data-stu-id="9dedf-245">The files can be directly created or edited, but their permissions must be updated to grant the omiuser user read permission on the files.</span></span> <span data-ttu-id="9dedf-246">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9dedf-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a><span data-ttu-id="9dedf-247">Removendo a configuração de proxy</span><span class="sxs-lookup"><span data-stu-id="9dedf-247">Removing the proxy configuration</span></span>
<span data-ttu-id="9dedf-248">Para remover uma configuração de proxy definida anteriormente e reverter para a conectividade direta, remova o arquivo proxy.conf:</span><span class="sxs-lookup"><span data-stu-id="9dedf-248">To remove a previously defined proxy configuration and revert to direct connectivity, remove the proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="9dedf-249">Integração com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9dedf-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="9dedf-250">Se uma ID e chave do espaço de trabalho não foram fornecidas durante a instalação do pacote, o agente deve ser subsequentemente registrado com o Operations Manager Suite.</span><span class="sxs-lookup"><span data-stu-id="9dedf-250">If a workspace ID and key were not provided during the bundle installation, the agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-the-command-line"></a><span data-ttu-id="9dedf-251">Integração usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="9dedf-251">Onboarding using the command line</span></span>
<span data-ttu-id="9dedf-252">Execute o comando omsadmin.sh fornecendo a ID e a chave do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9dedf-252">Run the omsadmin.sh command supplying the workspace id and key for your workspace.</span></span> <span data-ttu-id="9dedf-253">Este comando deve ser executado como raiz (com elevação sudo):</span><span class="sxs-lookup"><span data-stu-id="9dedf-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="9dedf-254">Integração usando um arquivo</span><span class="sxs-lookup"><span data-stu-id="9dedf-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="9dedf-255">Crie o arquivo `/etc/omsagent-onboard.conf`.</span><span class="sxs-lookup"><span data-stu-id="9dedf-255">Create the file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="9dedf-256">O arquivo deve ser legível e gravável para a raiz.</span><span class="sxs-lookup"><span data-stu-id="9dedf-256">The file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="9dedf-257">Insira as seguintes linhas no arquivo com a ID e a Chave Compartilhada do Espaço de Trabalho:</span><span class="sxs-lookup"><span data-stu-id="9dedf-257">Insert the following lines in the file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="9dedf-258">Execute o comando a seguir para integrar ao OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="9dedf-258">Run the following command to Onboard to OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="9dedf-259">O arquivo é excluído na integração bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9dedf-259">The file is deleted on successful onboarding.</span></span>

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a><span data-ttu-id="9dedf-260">Habilitar o Agente do OMS para Linux para reportar para o System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9dedf-260">Enable the OMS Agent for Linux to report to System Center Operations Manager</span></span>
<span data-ttu-id="9dedf-261">Execute as seguintes etapas para configurar o Agente do OMS para Linux para reportar para um grupo de gerenciamento do System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="9dedf-261">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="9dedf-262">Edite o arquivo `/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="9dedf-262">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="9dedf-263">Verifique se a linha que começa com **httpsport=** define a porta 1270.</span><span class="sxs-lookup"><span data-stu-id="9dedf-263">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="9dedf-264">Como: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="9dedf-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="9dedf-265">Reinicie o servidor OMI: `sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="9dedf-265">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="9dedf-266">Logs do Agente</span><span class="sxs-lookup"><span data-stu-id="9dedf-266">Agent logs</span></span>
<span data-ttu-id="9dedf-267">Os logs do Agente do OMS para Linux podem ser encontrados em: `/var/opt/microsoft/omsagent/<workspace id>/log/` Os logs do programa omsconfig (configuração do agente) pode ser encontrado em: `/var/opt/microsoft/omsconfig/log/` Os Logs dos componentes OMI e SCX (que fornecem dados de métrica de desempenho) podem ser encontrados em: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span><span class="sxs-lookup"><span data-stu-id="9dedf-267">The logs for the OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` The logs for the omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for the OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="9dedf-268">Configuração de rotação de log##</span><span class="sxs-lookup"><span data-stu-id="9dedf-268">Log rotation configuration##</span></span>
<span data-ttu-id="9dedf-269">A configuração de rotação de log para omsagent pode ser encontrada em: `/etc/logrotate.d/omsagent-<workspace id>`</span><span class="sxs-lookup"><span data-stu-id="9dedf-269">The log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="9dedf-270">As configurações padrão são:</span><span class="sxs-lookup"><span data-stu-id="9dedf-270">The default settings are:</span></span> 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-the-oms-agent-for-linux"></a><span data-ttu-id="9dedf-271">Desinstalar o Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="9dedf-271">Uninstalling the OMS Agent for Linux</span></span>
<span data-ttu-id="9dedf-272">Os pacotes de agente podem ser desinstalados por meio da execução do arquivo bundle.sh com o argumento `--purge`, que remove completamente o agente e a configuração do computador.</span><span class="sxs-lookup"><span data-stu-id="9dedf-272">The agent packages can be uninstalled by running the bundle .sh file with the `--purge` argument, which completely removes the agent and its configuration from the computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="9dedf-273">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9dedf-273">Troubleshooting</span></span>

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a><span data-ttu-id="9dedf-274">Problema: não é possível se conectar por meio do proxy ao OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-274">Issue: Unable to connect through proxy to OMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9dedf-275">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="9dedf-275">Probable causes</span></span>
* <span data-ttu-id="9dedf-276">O proxy especificado durante a integração estava incorreto</span><span class="sxs-lookup"><span data-stu-id="9dedf-276">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="9dedf-277">Os Pontos de Extremidade do Serviço OMS não estão na lista de permissões do seu datacenter</span><span class="sxs-lookup"><span data-stu-id="9dedf-277">The OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="9dedf-278">Resoluções</span><span class="sxs-lookup"><span data-stu-id="9dedf-278">Resolutions</span></span>
1. <span data-ttu-id="9dedf-279">Reintegre ao Serviço OMS com o Agente do OMS para Linux usando o seguinte comando com a opção `-v` habilitada.</span><span class="sxs-lookup"><span data-stu-id="9dedf-279">Reonboard to the OMS Service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="9dedf-280">Isso permite a saída detalhada do agente que está se conectando por meio do proxy ao Serviço OMS.</span><span class="sxs-lookup"><span data-stu-id="9dedf-280">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="9dedf-281">Consulte a seção [Configurando o agente para uso com um servidor proxy HTTP (#configuring the-agent-for-use-with-a-http-proxy-server)] para verificar se você configurou adequadamente o agente para se comunicar pelo servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="9dedf-281">Review the section [Configuring the agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="9dedf-282">Verifique uma segunda vez se os seguintes pontos de extremidade do Serviço OMS estão na lista de permissões:</span><span class="sxs-lookup"><span data-stu-id="9dedf-282">Double check that the following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="9dedf-283">Recurso de agente</span><span class="sxs-lookup"><span data-stu-id="9dedf-283">Agent Resource</span></span>| <span data-ttu-id="9dedf-284">Portas</span><span class="sxs-lookup"><span data-stu-id="9dedf-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="9dedf-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9dedf-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="9dedf-286">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-286">Port 443</span></span>|   
    |<span data-ttu-id="9dedf-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9dedf-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="9dedf-288">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-288">Port 443</span></span>|   
    |<span data-ttu-id="9dedf-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="9dedf-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="9dedf-290">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-290">Port 443</span></span>|   
    |<span data-ttu-id="9dedf-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9dedf-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="9dedf-292">Porta 443</span><span class="sxs-lookup"><span data-stu-id="9dedf-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="9dedf-293">Problema: você recebe um erro 403 quando tentar integrar</span><span class="sxs-lookup"><span data-stu-id="9dedf-293">Issue: You receive a 403 error when trying to onboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9dedf-294">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="9dedf-294">Probable causes</span></span>
* <span data-ttu-id="9dedf-295">A data e a hora estão incorretas no servidor Linux</span><span class="sxs-lookup"><span data-stu-id="9dedf-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="9dedf-296">A ID e a Chave do Espaço de Trabalho usadas estão incorretas</span><span class="sxs-lookup"><span data-stu-id="9dedf-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="9dedf-297">Resolução</span><span class="sxs-lookup"><span data-stu-id="9dedf-297">Resolution</span></span>

1. <span data-ttu-id="9dedf-298">Verifique a hora no servidor Linux com o comando date.</span><span class="sxs-lookup"><span data-stu-id="9dedf-298">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="9dedf-299">Se a hora for +/-15 minutos da hora atual, a integração falhará.</span><span class="sxs-lookup"><span data-stu-id="9dedf-299">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="9dedf-300">Para corrigir esse problema, atualize a data e/ou o fuso horário do servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="9dedf-300">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="9dedf-301">Verifique se você instalou a última versão do Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="9dedf-301">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="9dedf-302">A versão mais recente agora notifica se a distorção de horário está causando a falha de integração.</span><span class="sxs-lookup"><span data-stu-id="9dedf-302">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="9dedf-303">Reintegre usando a ID do Espaço de Trabalho e a Chave do Espaço de Trabalho corretas seguindo as instruções de instalação descritas anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="9dedf-303">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="9dedf-304">Problema: Você vê um erro 404 e 500 no arquivo de log logo após a integração</span><span class="sxs-lookup"><span data-stu-id="9dedf-304">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="9dedf-305">Esse é um problema conhecido que ocorre durante o primeiro upload de dados do Linux em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9dedf-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="9dedf-306">Isso não afeta os dados sendo enviados ou a experiência do serviço.</span><span class="sxs-lookup"><span data-stu-id="9dedf-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a><span data-ttu-id="9dedf-307">Problema: Você não está vendo nenhum dado no portal do OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-307">Issue:  You are not seeing any data in the OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9dedf-308">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="9dedf-308">Probable causes</span></span>

- <span data-ttu-id="9dedf-309">Falha na integração com o Serviço OMS</span><span class="sxs-lookup"><span data-stu-id="9dedf-309">Onboarding to the OMS Service failed</span></span>
- <span data-ttu-id="9dedf-310">A conexão com o Serviço OMS está bloqueada</span><span class="sxs-lookup"><span data-stu-id="9dedf-310">Connection to the OMS Service is blocked</span></span>
- <span data-ttu-id="9dedf-311">Os dados do Agente do OMS para Linux têm o backup realizado</span><span class="sxs-lookup"><span data-stu-id="9dedf-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9dedf-312">Resoluções</span><span class="sxs-lookup"><span data-stu-id="9dedf-312">Resolutions</span></span>
1. <span data-ttu-id="9dedf-313">Verifique se a integração do Serviço OMS foi bem-sucedida verificando se os seguintes arquivos existem: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="9dedf-313">Check if onboarding the OMS Service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="9dedf-314">Reintegração usando as instruções de linha de comando do `omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="9dedf-314">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="9dedf-315">Se estiver usando um proxy, consulte as etapas de resolução de proxy fornecidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-315">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="9dedf-316">Em alguns casos, quando o Agente do OMS para Linux não pode se comunicar com o Serviço OMS, os dados no agente são enfileirados até todo o tamanho do buffer, que é 50 MB.</span><span class="sxs-lookup"><span data-stu-id="9dedf-316">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="9dedf-317">O Agente do OMS para Linux deve ser reiniciado executando o seguinte comando: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span><span class="sxs-lookup"><span data-stu-id="9dedf-317">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="9dedf-318">Esse problema foi corrigido nas versões 1.1.0-28 e posteriores do Agente.</span><span class="sxs-lookup"><span data-stu-id="9dedf-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 