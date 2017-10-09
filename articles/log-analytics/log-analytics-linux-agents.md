---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="b9efb-101">Conecte-se a sua tooLog de computadores Linux análise</span><span class="sxs-lookup"><span data-stu-id="b9efb-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="b9efb-102">Usando o Log Analytics, você pode coletar os dados gerados em computadores Linux e tomar ações em relação a eles.</span><span class="sxs-lookup"><span data-stu-id="b9efb-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="b9efb-103">Adicionar dados coletados do Linux tooOMS permite que você toomanage os sistemas Linux e soluções de contêiner como o Docker, independentemente de onde se encontram os computadores – praticamente em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="b9efb-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="b9efb-104">Fontes de dados podem residir em seu datacenter local como servidores físicos, os computadores virtuais em um serviço de nuvem hospedados como serviços AWS (Amazon Web) ou o Microsoft Azure, ou mesmo Olá laptop em sua mesa.</span><span class="sxs-lookup"><span data-stu-id="b9efb-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="b9efb-105">Além disso, o OMS também coleta dados de computadores Windows da mesma forma e, portanto, oferece suporte a um ambiente de TI verdadeiramente híbrido.</span><span class="sxs-lookup"><span data-stu-id="b9efb-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="b9efb-106">Você pode exibir e gerenciar dados de todas essas fontes com o Log Analytics no OMS com um único portal de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b9efb-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="b9efb-107">Isso reduz a necessidade de saudação toomonitor usando vários sistemas diferentes, torna mais fácil tooconsume, e você pode exportar os dados que você deseja toowhatever solução de análise de negócios ou sistema que você já tiver.</span><span class="sxs-lookup"><span data-stu-id="b9efb-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="b9efb-108">Este artigo é um guia de início rápido que ajudarão você a coletar e gerenciar dados de seus computadores Linux usando Olá agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="b9efb-109">Para obter mais detalhes técnicos, como a configuração do servidor proxy, informações sobre as métricas do CollectD e fontes de dados JSON personalizadas, acesse a [Visão geral do Agente OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) e a [Documentação completa do Agente OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b9efb-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="b9efb-110">No momento, você pode coletar Olá seguintes tipos de dados de computadores Linux:</span><span class="sxs-lookup"><span data-stu-id="b9efb-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="b9efb-111">Métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="b9efb-111">Performance metrics</span></span>
* <span data-ttu-id="b9efb-112">Eventos de syslog</span><span class="sxs-lookup"><span data-stu-id="b9efb-112">Syslog events</span></span>
* <span data-ttu-id="b9efb-113">Alertas do Nagios e do Zabbix</span><span class="sxs-lookup"><span data-stu-id="b9efb-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="b9efb-114">Logs, inventário e métricas de desempenho do contêiner Docker</span><span class="sxs-lookup"><span data-stu-id="b9efb-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="b9efb-115">Versões do Linux com suporte</span><span class="sxs-lookup"><span data-stu-id="b9efb-115">Supported Linux versions</span></span>
<span data-ttu-id="b9efb-116">As versões x86 e x64 têm suporte oficial em uma variedade de distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="b9efb-117">No entanto, a saudação do agente do OMS para Linux também pode ser executado em outras distribuições não listadas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="b9efb-118">Amazon Linux 2012.09 a 2015.09</span><span class="sxs-lookup"><span data-stu-id="b9efb-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="b9efb-119">CentOS Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="b9efb-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="b9efb-120">Oracle Linux 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="b9efb-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="b9efb-121">Red Hat Enterprise Linux Server 5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="b9efb-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="b9efb-122">Debian GNU/Linux 6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="b9efb-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="b9efb-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="b9efb-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="b9efb-124">SUSE Linux Enterprise Server 11 e 12</span><span class="sxs-lookup"><span data-stu-id="b9efb-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="b9efb-125">Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-125">OMS Agent for Linux</span></span>
<span data-ttu-id="b9efb-126">Olá agente do Operations Management Suite para Linux consiste em vários pacotes.</span><span class="sxs-lookup"><span data-stu-id="b9efb-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="b9efb-127">versão de arquivo Hello contém Olá pacotes, disponíveis com o pacote de shell Olá em execução com a seguir `--extract`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="b9efb-128">**Pacote**</span><span class="sxs-lookup"><span data-stu-id="b9efb-128">**Package**</span></span> | <span data-ttu-id="b9efb-129">**Versão**</span><span class="sxs-lookup"><span data-stu-id="b9efb-129">**Version**</span></span> | <span data-ttu-id="b9efb-130">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="b9efb-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9efb-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="b9efb-131">omsagent</span></span> |<span data-ttu-id="b9efb-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b9efb-132">1.1.0</span></span> |<span data-ttu-id="b9efb-133">Olá agente do Operations Management Suite para Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="b9efb-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="b9efb-134">omsconfig</span></span> |<span data-ttu-id="b9efb-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b9efb-135">1.1.1</span></span> |<span data-ttu-id="b9efb-136">Agente de configuração para Olá agente do OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="b9efb-137">omi</span><span class="sxs-lookup"><span data-stu-id="b9efb-137">omi</span></span> |<span data-ttu-id="b9efb-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="b9efb-138">1.0.8.3</span></span> |<span data-ttu-id="b9efb-139">OMI (Open Management Infrastructure) – um servidor CIM leve</span><span class="sxs-lookup"><span data-stu-id="b9efb-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="b9efb-140">scx</span><span class="sxs-lookup"><span data-stu-id="b9efb-140">scx</span></span> |<span data-ttu-id="b9efb-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="b9efb-141">1.6.2</span></span> |<span data-ttu-id="b9efb-142">Provedores de CIM OMI para métricas de desempenho do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="b9efb-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="b9efb-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="b9efb-143">apache-cimprov</span></span> |<span data-ttu-id="b9efb-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b9efb-144">1.0.0</span></span> |<span data-ttu-id="b9efb-145">Provedor de monitoramento de desempenho do Servidor HTTP Apache para OMI.</span><span class="sxs-lookup"><span data-stu-id="b9efb-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b9efb-146">Instalado somente se o Servidor HTTP Apache for detectado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="b9efb-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="b9efb-147">mysql-cimprov</span></span> |<span data-ttu-id="b9efb-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b9efb-148">1.0.0</span></span> |<span data-ttu-id="b9efb-149">Provedor de monitoramento de desempenho do Servidor MySQL para OMI.</span><span class="sxs-lookup"><span data-stu-id="b9efb-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b9efb-150">Instalado somente se o servidor MySQL/MariaDB for detectado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="b9efb-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="b9efb-151">docker-cimprov</span></span> |<span data-ttu-id="b9efb-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="b9efb-152">0.1.0</span></span> |<span data-ttu-id="b9efb-153">Provedor do Docker para OMI.</span><span class="sxs-lookup"><span data-stu-id="b9efb-153">Docker provider for OMI.</span></span> <span data-ttu-id="b9efb-154">Instalado somente se o Docker for detectado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="b9efb-155">Artefatos adicionais de instalação</span><span class="sxs-lookup"><span data-stu-id="b9efb-155">Additional installation artifacts</span></span>
<span data-ttu-id="b9efb-156">Depois de instalar o agente do OMS Olá para pacotes Linux, hello seguintes alterações de configuração de todo o sistema adicionais são aplicadas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="b9efb-157">Esses artefatos são removidos quando o pacote do hello omsagent é desinstalado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="b9efb-158">Um usuário sem privilégios chamado: `omsagent` é criado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="b9efb-159">Isso é Olá conta Olá omsagent daemon executa como</span><span class="sxs-lookup"><span data-stu-id="b9efb-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="b9efb-160">Um "inclusão" sudoers é criado em /etc/sudoers.d/omsagent. Isso autoriza o omsagent toorestart Olá syslog e omsagent daemons.</span><span class="sxs-lookup"><span data-stu-id="b9efb-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="b9efb-161">Se as diretivas de "inclusão" do sudo não tiverem suporte na versão Olá instalada do sudo, essas entradas serão gravadas muito/etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="b9efb-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="b9efb-162">configuração de syslog Olá é modificado tooforward um subconjunto do agente de toohello de eventos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="b9efb-163">Para obter mais informações, consulte Olá **configurar coleta de dados** seção abaixo</span><span class="sxs-lookup"><span data-stu-id="b9efb-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="b9efb-164">Detalhes da coleta de dados do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-164">Linux data collection details</span></span>
<span data-ttu-id="b9efb-165">Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="b9efb-166">fonte</span><span class="sxs-lookup"><span data-stu-id="b9efb-166">source</span></span> | <span data-ttu-id="b9efb-167">Agente Direct</span><span class="sxs-lookup"><span data-stu-id="b9efb-167">Direct Agent</span></span> | <span data-ttu-id="b9efb-168">Agente SCOM</span><span class="sxs-lookup"><span data-stu-id="b9efb-168">SCOM agent</span></span> | <span data-ttu-id="b9efb-169">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b9efb-169">Azure Storage</span></span> | <span data-ttu-id="b9efb-170">SCOM necessário?</span><span class="sxs-lookup"><span data-stu-id="b9efb-170">SCOM required?</span></span> | <span data-ttu-id="b9efb-171">Os dados do agente SCOM enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="b9efb-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="b9efb-172">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="b9efb-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b9efb-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="b9efb-173">Zabbix</span></span> |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b9efb-179">1 minuto</span><span class="sxs-lookup"><span data-stu-id="b9efb-179">1 minute</span></span> |
| <span data-ttu-id="b9efb-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="b9efb-180">Nagios</span></span> |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b9efb-186">na chegada</span><span class="sxs-lookup"><span data-stu-id="b9efb-186">on arrival</span></span> |
| <span data-ttu-id="b9efb-187">syslog</span><span class="sxs-lookup"><span data-stu-id="b9efb-187">syslog</span></span> |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b9efb-193">do armazenamento do Azure: 10 minutos; do agente: na chegada</span><span class="sxs-lookup"><span data-stu-id="b9efb-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="b9efb-194">Contadores de desempenho do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-194">Linux performance counters</span></span> |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b9efb-200">Como agendado, mínimo de 10 segundos</span><span class="sxs-lookup"><span data-stu-id="b9efb-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="b9efb-201">controle de alterações</span><span class="sxs-lookup"><span data-stu-id="b9efb-201">change tracking</span></span> |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b9efb-207">por hora</span><span class="sxs-lookup"><span data-stu-id="b9efb-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="b9efb-208">Requisitos de pacote</span><span class="sxs-lookup"><span data-stu-id="b9efb-208">Package Requirements</span></span>
| <span data-ttu-id="b9efb-209">**Pacote necessário**</span><span class="sxs-lookup"><span data-stu-id="b9efb-209">**Required package**</span></span> | <span data-ttu-id="b9efb-210">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="b9efb-210">**Description**</span></span> | <span data-ttu-id="b9efb-211">**Versão mínima**</span><span class="sxs-lookup"><span data-stu-id="b9efb-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9efb-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="b9efb-212">Glibc</span></span> |<span data-ttu-id="b9efb-213">Biblioteca GNU C</span><span class="sxs-lookup"><span data-stu-id="b9efb-213">GNU C library</span></span> |<span data-ttu-id="b9efb-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="b9efb-214">2.5-12</span></span> |
| <span data-ttu-id="b9efb-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="b9efb-215">Openssl</span></span> |<span data-ttu-id="b9efb-216">Bibliotecas OpenSSL</span><span class="sxs-lookup"><span data-stu-id="b9efb-216">OpenSSL libraries</span></span> |<span data-ttu-id="b9efb-217">0.9.8e ou 1.0</span><span class="sxs-lookup"><span data-stu-id="b9efb-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="b9efb-218">Curl</span><span class="sxs-lookup"><span data-stu-id="b9efb-218">Curl</span></span> |<span data-ttu-id="b9efb-219">cliente Web cURL</span><span class="sxs-lookup"><span data-stu-id="b9efb-219">cURL web client</span></span> |<span data-ttu-id="b9efb-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="b9efb-220">7.15.5</span></span> |
| <span data-ttu-id="b9efb-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="b9efb-221">Python-ctypes</span></span> |<span data-ttu-id="b9efb-222">bibliotecas de função</span><span class="sxs-lookup"><span data-stu-id="b9efb-222">function libraries</span></span> |<span data-ttu-id="b9efb-223">n/d</span><span class="sxs-lookup"><span data-stu-id="b9efb-223">n/a</span></span> |
| <span data-ttu-id="b9efb-224">PAM</span><span class="sxs-lookup"><span data-stu-id="b9efb-224">PAM</span></span> |<span data-ttu-id="b9efb-225">Módulos de autenticação conectáveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="b9efb-226">n/d</span><span class="sxs-lookup"><span data-stu-id="b9efb-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="b9efb-227">O rsyslog ou syslog-ng é necessário toocollect mensagens de syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="b9efb-228">Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="b9efb-229">toocollect dados de syslog dessa versão de distribuições, Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="b9efb-230">Instalação rápida</span><span class="sxs-lookup"><span data-stu-id="b9efb-230">Quick install</span></span>
<span data-ttu-id="b9efb-231">Olá comandos toodownload Olá omsagent a seguir é executado, validar a soma de verificação Olá, em seguida, instalar e agente Olá integrado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="b9efb-232">Os comandos são para a versão de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="b9efb-232">Commands are for 64-bit.</span></span> <span data-ttu-id="b9efb-233">Olá ID do espaço de trabalho e chave primária são encontradas no portal do OMS Olá em **configurações** em Olá **fontes conectadas** guia.</span><span class="sxs-lookup"><span data-stu-id="b9efb-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![detalhes do espaço de trabalho](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="b9efb-235">Há uma variedade de outros métodos tooinstall Olá agente e atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="b9efb-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="b9efb-236">Você pode ler mais sobre eles em [Olá tooinstall de etapas do agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="b9efb-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="b9efb-237">Você também pode exibir uma saudação [orientação em vídeo do Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="b9efb-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="b9efb-238">Escolha o método de coleta de dados do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="b9efb-239">A escolha Olá tipos de dados que seria como toocollect depende se você deseja que o portal do OMS Olá toouse ou se quer editar vários arquivos de configuração diretamente nos clientes Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="b9efb-240">Se você escolher o portal de saudação toouse, configuração de saudação é enviada tooall clientes Linux automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9efb-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="b9efb-241">Se você precisar de configurações diferentes para diferentes clientes Linux, será necessário tooedit arquivos de cliente individualmente – ou usar uma alternativa como PowerShell DSC, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="b9efb-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="b9efb-242">Você pode especificar os eventos de syslog hello e contadores de desempenho que você deseja toocollect usando arquivos de configuração em computadores Linux de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="b9efb-243">*Se você escolheu tooconfigure a coleta de dados editando arquivos de configuração do agente, você deve desabilitar a configuração de centralizado de saudação.*</span><span class="sxs-lookup"><span data-stu-id="b9efb-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="b9efb-244">As instruções são fornecidas abaixo de coleta de dados tooconfigure do agente Olá arquivos de configuração, bem como toodisable configuração central para todos os agentes do OMS para Linux ou computadores individuais.</span><span class="sxs-lookup"><span data-stu-id="b9efb-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="b9efb-245">Desabilitar o gerenciamento do OMS para um computador Linux individual</span><span class="sxs-lookup"><span data-stu-id="b9efb-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="b9efb-246">Coleta de dados centralizado para dados de configuração é desabilitada para um computador Linux individual com hello script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="b9efb-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="b9efb-247">Isso poderá ser útil se um subconjunto de computadores tiver uma configuração especializada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="b9efb-248">configuração centralizada de toodisable:</span><span class="sxs-lookup"><span data-stu-id="b9efb-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="b9efb-249">Habilitar toore de configuração centralizada:</span><span class="sxs-lookup"><span data-stu-id="b9efb-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="b9efb-250">Contadores de desempenho do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-250">Linux performance counters</span></span>
<span data-ttu-id="b9efb-251">Contadores de desempenho de Linux são semelhantes contadores de desempenho de tooWindows – ambos operam da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="b9efb-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="b9efb-252">Você pode usar o hello tooadd procedimentos a seguir e configurá-los.</span><span class="sxs-lookup"><span data-stu-id="b9efb-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="b9efb-253">Depois de serem adicionados tooOMS, dados são coletados da cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="b9efb-254">tooadd um contador de desempenho do Linux no OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="b9efb-255">tooconfigure agentes do OMS para Linux usando o portal do OMS hello, você pode adicionar contadores de desempenho do Linux na página de configurações de saudação, clique em **dados**.</span><span class="sxs-lookup"><span data-stu-id="b9efb-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="b9efb-256">Em Olá **configurações** página em **dados** , clique em **contadores de desempenho de Linux** e o nome de hello, em seguida, selecionar ou tipo de contador de saudação que você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9efb-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="b9efb-257">![dados](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="b9efb-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="b9efb-258">Se você não souber o nome completo de saudação do contador Olá, você pode começar por digitar um nome parcial e será exibida uma lista de contadores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b9efb-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="b9efb-259">Quando você encontrar o contador de saudação você deseja tooadd, clique Olá nome na lista de saudação e clique em hello mais saudação do ícone tooadd contador.</span><span class="sxs-lookup"><span data-stu-id="b9efb-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="b9efb-260">Depois de adicionar o contador de hello, ele aparece na lista de saudação de contadores realçado com uma barra colorida.</span><span class="sxs-lookup"><span data-stu-id="b9efb-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="b9efb-261">Por padrão, Olá **aplicar abaixo máquinas de toomy configuração** opção é selecionada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="b9efb-262">Se você quiser toodisable enviar dados de configuração, desmarque a seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="b9efb-263">Quando você terminar de modificar os contadores de desempenho, final Olá Olá página clique **salvar** toofinalize suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b9efb-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="b9efb-264">Olá alterações de configuração feitas são enviadas tooall Olá agentes do OMS para Linux que são registrados com o OMS, normalmente em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="b9efb-265">Configurar contadores de desempenho do Linux no OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="b9efb-266">Para os contadores de desempenho do Windows, você pode escolher uma instância específica para cada contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b9efb-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="b9efb-267">No entanto, para contadores de desempenho do Linux, qualquer instância de um contador que você escolher aplica tooall contadores de filho do contador pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="b9efb-268">Olá tabela a seguir mostra Olá instâncias comuns disponíveis tooboth contadores de desempenho do Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="b9efb-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="b9efb-269">**Nome da instância**</span><span class="sxs-lookup"><span data-stu-id="b9efb-269">**Instance name**</span></span> | <span data-ttu-id="b9efb-270">**Significado**</span><span class="sxs-lookup"><span data-stu-id="b9efb-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="b9efb-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="b9efb-271">\_Total</span></span> |<span data-ttu-id="b9efb-272">Total de todas as instâncias de saudação</span><span class="sxs-lookup"><span data-stu-id="b9efb-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="b9efb-273">Todas as instâncias</span><span class="sxs-lookup"><span data-stu-id="b9efb-273">All instances</span></span> |
| <span data-ttu-id="b9efb-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="b9efb-274">(/&#124;/var)</span></span> |<span data-ttu-id="b9efb-275">Corresponde às instâncias chamadas: / ou /var</span><span class="sxs-lookup"><span data-stu-id="b9efb-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="b9efb-276">Da mesma forma, o intervalo de amostragem de saudação que você escolher para um contador pai aplica tooall seus contadores filho.</span><span class="sxs-lookup"><span data-stu-id="b9efb-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="b9efb-277">Em outras palavras, todos os intervalos de amostra do contador Olá filho e instâncias serão vinculadas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="b9efb-278">Adicionar e configurar métricas de desempenho com o Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="b9efb-279">Toocollect de métricas de desempenho são controlados pela configuração de saudação em/etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="b9efb-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="b9efb-280">Consulte [métricas de desempenho disponíveis](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) para classes e métricas de saudação do agente do OMS para Linux disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b9efb-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="b9efb-281">Cada objeto ou categoria, de toocollect de métricas de desempenho deve ser definido no arquivo de configuração de saudação como um único `<source>` elemento.</span><span class="sxs-lookup"><span data-stu-id="b9efb-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="b9efb-282">sintaxe de saudação segue o padrão de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b9efb-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="b9efb-283">saudação de parâmetros configuráveis desse elemento é:</span><span class="sxs-lookup"><span data-stu-id="b9efb-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="b9efb-284">**Objeto\_nome**: nome do objeto Olá coleção hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="b9efb-285">**Instância\_regex**: um *expressão regular* definindo toocollect quais instâncias.</span><span class="sxs-lookup"><span data-stu-id="b9efb-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="b9efb-286">Olá valor: `.*` especifica todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="b9efb-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="b9efb-287">métricas de processador toocollect para apenas Olá \_instância Total, você poderia especificar `_Total`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="b9efb-288">as métricas do processo toocollect para hello apenas instâncias crond ou sshd, você pode especificar: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="b9efb-289">**Contador\_nome\_regex**: um *expressão regular* definindo toocollect quais contadores (para o objeto de saudação).</span><span class="sxs-lookup"><span data-stu-id="b9efb-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="b9efb-290">Especifique de todos os contadores do objeto hello, toocollect: `.*`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="b9efb-291">toocollect trocas somente contadores de espaço para o objeto de memória hello, você pode especificar:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="b9efb-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="b9efb-292">**Intervalo:**: Olá frequência na qual Olá contadores do objeto são coletados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="b9efb-293">configuração padrão de saudação para métricas de desempenho é:</span><span class="sxs-lookup"><span data-stu-id="b9efb-293">hello default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="b9efb-294">Habilitar os contadores de desempenho do MySQL usando os comandos do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="b9efb-295">Se o servidor MySQL ou MariaDB for detectado no computador de saudação quando o pacote do hello omsagent estiver instalado, um provedor para o MySQL Server de monitoramento de desempenho é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9efb-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="b9efb-296">Esse provedor se conecta toohello local MySQL/MariaDB tooexpose desempenho estatísticas do servidor.</span><span class="sxs-lookup"><span data-stu-id="b9efb-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="b9efb-297">É necessário tooconfigure credenciais de usuário do MySQL para que hello provedor possa acessar saudação do MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="b9efb-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="b9efb-298">toodefine um padrão conta de usuário para o MySQL server de saudação no localhost, use Olá exemplo de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="b9efb-299">o arquivo de credenciais Olá deve ser legível por conta de omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="b9efb-300">É recomendável executar o comando do hello mycimprovauth como omsgent.</span><span class="sxs-lookup"><span data-stu-id="b9efb-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="b9efb-301">Como alternativa, você pode especificar Olá necessárias credenciais do MySQL em um arquivo, Criando arquivo hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Para obter mais informações sobre o gerenciamento de credenciais do MySQL para o monitoramento por meio do arquivo mysql-auth de hello, consulte [monitoramento credenciais no arquivo de autenticação de saudação do MySQL gerenciar](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="b9efb-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="b9efb-302">Consulte [permissões necessárias para contadores de desempenho do MySQL do banco de dados](#database-permissions-required-for-mysql-performance-counters) para obter detalhes sobre as permissões de objeto necessárias Olá MySQL usuário toocollect dados de desempenho do servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="b9efb-303">Habilitar os contadores de desempenho do Servidor HTTP Apache usando os comandos do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="b9efb-304">Se o Apache HTTP Server for detectado no computador de saudação quando o pacote do hello omsagent estiver instalado, um provedor para o Apache HTTP Server de monitoramento de desempenho é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9efb-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="b9efb-305">Esse provedor baseia-se em um "módulo" que deve ser carregado no hello Apache HTTP Server nos dados de desempenho de tooaccess de ordem.</span><span class="sxs-lookup"><span data-stu-id="b9efb-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="b9efb-306">Você pode carregar o módulo de saudação com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="b9efb-307">toounload Olá Apache módulo de monitoramento, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="b9efb-308">dados de desempenho de tooview com análise de Log</span><span class="sxs-lookup"><span data-stu-id="b9efb-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="b9efb-309">No portal do Operations Management Suite hello, clique em bloco de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="b9efb-310">Na barra de pesquisa hello, digite `* (Type=Perf)` tooview todos os contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b9efb-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="b9efb-311">Como o OMS também coleta dados de contador de desempenho do Windows, você deve escopo suspensa Olá dados tooLinux específico de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b9efb-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="b9efb-312">Assim, hello exemplo a seguir mostraria servidor desempenho dados específicos tooan exemplo Linux chamado Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="b9efb-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![servidor de exemplo mostrado nos resultados da pesquisa](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="b9efb-314">Nos resultados de saudação, você pode clicar em **métricas** contadores de saudação tooview que dados foram coletados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="b9efb-315">Os dados em tempo real são mostrados como gráficos para cada contador.</span><span class="sxs-lookup"><span data-stu-id="b9efb-315">Real-time data is shown as graphs for each counter.</span></span>

![Métricas](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="b9efb-317">syslog</span><span class="sxs-lookup"><span data-stu-id="b9efb-317">Syslog</span></span>
<span data-ttu-id="b9efb-318">Syslog é um protocolo semelhante tooWindows logs de eventos de log de eventos – ambos funcionam de forma semelhante ao exibido no OMS.</span><span class="sxs-lookup"><span data-stu-id="b9efb-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="b9efb-319">tooadd um novo recurso de syslog do Linux no OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="b9efb-320">Em Olá **configurações** página em **dados** , clique em **Syslog** e toohello à esquerda do ícone de adição hello, digite Olá nome do recurso de syslog Olá que você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9efb-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="b9efb-321">![Syslog do Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="b9efb-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="b9efb-322">Se você não souber o nome completo de saudação do recurso hello, você pode começar por digitar um nome parcial e será exibida uma lista de instalações de syslog disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b9efb-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="b9efb-323">Quando você encontrar o recurso de syslog Olá deseja tooadd, clique Olá nome na lista de saudação e, em seguida, clique em hello mais saudação do ícone tooadd recurso de syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="b9efb-324">Depois de adicionar instalação hello, ele aparece na lista de saudação do realçado com uma barra colorida.</span><span class="sxs-lookup"><span data-stu-id="b9efb-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="b9efb-325">Em seguida, escolha as gravidades hello (categorias de informações de instalação de syslog) que você deseja toocollect.</span><span class="sxs-lookup"><span data-stu-id="b9efb-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="b9efb-326">Final Olá Olá página clique **salvar** toofinalize suas alterações.</span><span class="sxs-lookup"><span data-stu-id="b9efb-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="b9efb-327">Olá alterações de configuração feitas são enviadas tooall Olá agentes do OMS para Linux que são registrados com o OMS, normalmente em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="b9efb-328">Configurar recursos de syslog do Linux no Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="b9efb-329">Eventos de syslog são enviados do daemon do syslog hello, por exemplo rsyslog ou syslog-ng, porta local tooa que o agente hello está escutando.</span><span class="sxs-lookup"><span data-stu-id="b9efb-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="b9efb-330">Por padrão, a porta 25224.</span><span class="sxs-lookup"><span data-stu-id="b9efb-330">By default, port 25224.</span></span> <span data-ttu-id="b9efb-331">Quando o agente de saudação é instalado, uma configuração de syslog padrão é aplicada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="b9efb-332">Isso é encontrado em:</span><span class="sxs-lookup"><span data-stu-id="b9efb-332">This is found at:</span></span>

<span data-ttu-id="b9efb-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="b9efb-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="b9efb-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="b9efb-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="b9efb-335">configuração de syslog do saudação padrão agente OMS carrega eventos de syslog de todas as instalações com uma severidade de aviso ou superior.</span><span class="sxs-lookup"><span data-stu-id="b9efb-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="b9efb-336">Se você editar configuração de syslog Olá, você deve reiniciar o daemon do syslog Olá Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="b9efb-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="b9efb-337">Olá syslog configuração padrão de saudação do agente do OMS para Linux para OMS é:</span><span class="sxs-lookup"><span data-stu-id="b9efb-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="b9efb-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="b9efb-338">Rsyslog</span></span>
```
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
```

#### <a name="syslog-ng"></a><span data-ttu-id="b9efb-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="b9efb-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="b9efb-340">tooview todos os eventos de Syslog com análise de Log</span><span class="sxs-lookup"><span data-stu-id="b9efb-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="b9efb-341">No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="b9efb-342">Em Olá **gerenciamento de Log** de agrupamento, escolha uma pesquisa de syslog predefinida e, em seguida, selecione um toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="b9efb-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="b9efb-343">Este exemplo mostra todos os eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-343">This example shows all Syslog events.</span></span>

![Eventos de Syslog mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="b9efb-345">Agora você pode analisar os resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b9efb-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="b9efb-346">Alertas do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-346">Linux alerts</span></span>
<span data-ttu-id="b9efb-347">Se você usar Nagios ou Zabbix toomanage suas máquinas Linux, então o OMS pode receber alertas de saudação geradas a partir dessas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="b9efb-348">No entanto, não há atualmente nenhum método tooconfigure alerta dados de entrada usando o portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="b9efb-349">Em vez disso, você precisará tooedit um tooOMS config arquivo toostart enviar alertas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="b9efb-350">Coletar alertas a partir do Nagios</span><span class="sxs-lookup"><span data-stu-id="b9efb-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="b9efb-351">toocollect alertas de um servidor Nagios, você precisa de saudação toomake as seguintes alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b9efb-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="b9efb-352">Usuário de saudação Grant **omsagent** acesso de leitura toohello arquivo de log Nagios (ou seja, /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="b9efb-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="b9efb-353">Supondo que o arquivo nagios.log de saudação pertencem ao grupo Olá **nagios** , você pode adicionar usuário Olá **omsagent** toohello **nagios** grupo.</span><span class="sxs-lookup"><span data-stu-id="b9efb-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="b9efb-354">Modificar o arquivo do hello confconfiguration (/ etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="b9efb-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="b9efb-355">Certifique-se de saudação entradas a seguir está presentes e sem comentários:</span><span class="sxs-lookup"><span data-stu-id="b9efb-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
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
    ```
3. <span data-ttu-id="b9efb-356">Reinicie o daemon omsagent hello:</span><span class="sxs-lookup"><span data-stu-id="b9efb-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="b9efb-357">Coletar alertas do Zabbix</span><span class="sxs-lookup"><span data-stu-id="b9efb-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="b9efb-358">toocollect alertas de um servidor Zabbix, você executará toothose de etapas semelhantes de Nagios acima, exceto que você precisará toospecify um usuário e senha em *limpar texto*.</span><span class="sxs-lookup"><span data-stu-id="b9efb-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="b9efb-359">Isso não é o ideal, mas provavelmente será alterado em breve.</span><span class="sxs-lookup"><span data-stu-id="b9efb-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="b9efb-360">tooaddress esse problema, recomendamos que você cria usuário hello e conceda permissão toomonitor somente.</span><span class="sxs-lookup"><span data-stu-id="b9efb-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="b9efb-361">Uma seção de exemplo do arquivo de configuração omsagent hello (/ etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf) para Zabbix deve ser semelhante à seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b9efb-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="b9efb-362">Exibir alertas na pesquisa do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b9efb-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="b9efb-363">Depois de configurar sua tooOMS de alertas de toosend de computadores Linux, você pode usar alguns log simples pesquisa consultas tooview Olá alertas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="b9efb-364">Olá seguinte exemplo de consulta de pesquisa retorna todos os alertas de saudação registrada que foram gerados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="b9efb-365">Por exemplo, se ocorrer algum tipo de problema em sua infraestrutura de TI, em seguida, resultados para Olá consulta pode indicar onde Olá problemas se originam do exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="b9efb-366">Além disso, você pode facilmente fazer uma busca de alertas toohello por origem sistema toohelp estreita sua investigação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="b9efb-367">Hello vantagem é que você não necessariamente sistemas de gerenciamento de toovarious toogo do início da saudação — desde que os alertas são enviados tooOMS, você pode iniciar de lá.</span><span class="sxs-lookup"><span data-stu-id="b9efb-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="b9efb-368">tooview Nagios todos os alertas com análise de Log</span><span class="sxs-lookup"><span data-stu-id="b9efb-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="b9efb-369">No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="b9efb-370">Na barra de consulta hello, digite o seguinte Olá pesquisa consulta</span><span class="sxs-lookup"><span data-stu-id="b9efb-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertas do Nagios mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="b9efb-372">Depois de ver os resultados da pesquisa hello, você pode analisar detalhes adicionais, como *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="b9efb-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="b9efb-373">tooview todos os alertas de Zabbix com análise de Log</span><span class="sxs-lookup"><span data-stu-id="b9efb-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="b9efb-374">No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="b9efb-375">Na barra de consulta hello, digite o seguinte Olá pesquisa consulta</span><span class="sxs-lookup"><span data-stu-id="b9efb-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertas do Zabbix mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="b9efb-377">Depois de ver os resultados da pesquisa hello, você pode analisar detalhes adicionais, como *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="b9efb-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="b9efb-378">Compatibilidade com o System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b9efb-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="b9efb-379">Olá agente do OMS para Linux compartilha binários de agente com o agente do System Center Operations Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="b9efb-380">Atualizações de instalação Olá agente do OMS para Linux em um sistema gerenciado atualmente pelo Operations Manager Olá pacotes OMI e SCX na versão mais recente do hello computador tooa.</span><span class="sxs-lookup"><span data-stu-id="b9efb-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="b9efb-381">Olá agente do OMS para Linux e do System Center 2012 R2 são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="b9efb-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="b9efb-382">No entanto, **System Center 2012 SP1 e versões anteriores atualmente não são compatíveis ou não tem suporte com hello agente do OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="b9efb-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="b9efb-383">Se Olá agente do OMS para Linux for instalado tooa computador que não é atualmente gerenciado pelo Operations Manager e mais tarde quiser toomanage computador de saudação com o Operations Manager, você deve modificar a configuração do OMI Olá antes de descobrir o computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="b9efb-384">**Essa etapa não é necessária se o agente do Operations Manager de saudação for instalado antes de saudação do agente do OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="b9efb-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="b9efb-385">Olá tooenable agente do OMS para Linux toocommunicate com o Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b9efb-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="b9efb-386">Editar saudação arquivo /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="b9efb-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="b9efb-387">Certifique-se de que Olá linha a partir **httpsport =** define Olá porta 1270.</span><span class="sxs-lookup"><span data-stu-id="b9efb-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="b9efb-388">Como `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="b9efb-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="b9efb-389">Reinicie o servidor OMI de saudação:</span><span class="sxs-lookup"><span data-stu-id="b9efb-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="b9efb-390">Permissões de banco de dados necessárias para contadores de desempenho do MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="b9efb-391">toogrant permissões tooa monitoramento usuário do MySQL, concedendo ao usuário Olá deve ter Olá privilégio 'GRANT option', bem como privilégio Olá sendo concedido.</span><span class="sxs-lookup"><span data-stu-id="b9efb-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="b9efb-392">Para que Olá MySQL usuário tooreturn desempenho dados Olá usuário precisará de acesso toohello consultas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="b9efb-393">Além disso, usuário do MySQL toothese consultas Olá requer acesso SELECT toohello tabelas padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="b9efb-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="b9efb-394">information_schema</span></span>
* <span data-ttu-id="b9efb-395">MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-395">mysql</span></span>

<span data-ttu-id="b9efb-396">Esses privilégios podem ser concedidos, executando Olá comandos de concessão a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="b9efb-397">Gerenciar as credenciais no arquivo de autenticação de saudação de monitoramento do MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="b9efb-398">a seguir Olá seções ajudam você a gerenciar as credenciais do MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="b9efb-399">Configurar Olá provedor de OMI do MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="b9efb-400">Hello provedor de OMI do MySQL requer um usuário do MySQL pré-configurado e bibliotecas de cliente de MySQL instaladas nas informações de integridade do desempenho de saudação ordem tooquery da instância do MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="b9efb-401">Arquivo de autenticação de OMI do MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="b9efb-402">Provedor de OMI do MySQL usa um toodetermine de arquivo de autenticação que instância do MySQL Olá endereço de associação e a porta está escutando e quais credenciais toouse toogather métricas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="b9efb-403">Durante a saudação de instalação de OMI do MySQL provedor verificar arquivos de configuração my.cnf do MySQL (locais padrão) para o endereço de associação e a porta e parcialmente conjunto Olá arquivo de autenticação de OMI do MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="b9efb-404">toocomplete monitoramento de uma instância do servidor MySQL, adicione um arquivo de autenticação de OMI do MySQL pré-gerado diretório correto hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="b9efb-405">Formato do arquivo de autenticação</span><span class="sxs-lookup"><span data-stu-id="b9efb-405">Authentication file format</span></span>
<span data-ttu-id="b9efb-406">Olá arquivo de autenticação de OMI do MySQL é um arquivo de texto que contém informações sobre:</span><span class="sxs-lookup"><span data-stu-id="b9efb-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="b9efb-407">Porta</span><span class="sxs-lookup"><span data-stu-id="b9efb-407">Port</span></span>
* <span data-ttu-id="b9efb-408">Endereço de Ligação</span><span class="sxs-lookup"><span data-stu-id="b9efb-408">Bind-Address</span></span>
* <span data-ttu-id="b9efb-409">Nome de usuário do MySQL</span><span class="sxs-lookup"><span data-stu-id="b9efb-409">MySQL username</span></span>
* <span data-ttu-id="b9efb-410">Senha codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b9efb-410">Base64 encoded password</span></span>

<span data-ttu-id="b9efb-411">Olá arquivo de autenticação de OMI do MySQL concede privilégios de usuário do Linux toohello leitura/gravação que o gerou.</span><span class="sxs-lookup"><span data-stu-id="b9efb-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="b9efb-412">Um padrão de arquivo de autenticação de OMI do MySQL contém uma instância padrão e um número de porta, dependendo de quais informações estão disponíveis e analisadas do hello encontrado o arquivo de configuração do MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="b9efb-413">instância padrão de saudação é um toomake significa gerenciar várias instâncias do MySQL em um host Linux mais fácil e é indicada pela instância de saudação com a porta 0.</span><span class="sxs-lookup"><span data-stu-id="b9efb-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="b9efb-414">Todas as instâncias adicionadas herdarão as propriedades definidas da instância de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="b9efb-415">Por exemplo, se a instância do MySQL escutando na porta '3308' for adicionada, endereço de associação da instância de saudação padrão, nome de usuário e senha codificada em Base64 serão ser tootry usado e monitorar Olá instância escuta na porta 3308.</span><span class="sxs-lookup"><span data-stu-id="b9efb-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="b9efb-416">Se instância Olá em 3308 é o endereço de tooanother associado e usa Olá o mesmo nome de usuário do MySQL e par senha Olá apenas nova especificação de saudação endereço de associação é necessária e hello outras propriedades serão herdadas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="b9efb-417">Exemplos de arquivo de autenticação Olá parecida com a seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="b9efb-418">Instância padrão e instância com porta 3308:</span><span class="sxs-lookup"><span data-stu-id="b9efb-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="b9efb-419">Instância padrão e instância com porta 3308 + senha codificada em Base64 diferente:</span><span class="sxs-lookup"><span data-stu-id="b9efb-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="b9efb-420">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="b9efb-420">**Property**</span></span> | <span data-ttu-id="b9efb-421">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="b9efb-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b9efb-422">Porta</span><span class="sxs-lookup"><span data-stu-id="b9efb-422">Port</span></span> |<span data-ttu-id="b9efb-423">A porta representa Olá Olá atual da porta escuta da instância do MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="b9efb-424">porta de saudação 0 significa que propriedades Olá a seguir são usadas para a instância padrão.</span><span class="sxs-lookup"><span data-stu-id="b9efb-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="b9efb-425">Endereço de Ligação</span><span class="sxs-lookup"><span data-stu-id="b9efb-425">Bind-Address</span></span> |<span data-ttu-id="b9efb-426">Olá endereço de associação é Olá atual MySQL endereço de associação</span><span class="sxs-lookup"><span data-stu-id="b9efb-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="b9efb-427">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="b9efb-427">username</span></span> |<span data-ttu-id="b9efb-428">Esse nome de usuário do usuário MySQL, Olá Olá desejar instância do servidor toouse toomonitor Olá MySQL.</span><span class="sxs-lookup"><span data-stu-id="b9efb-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="b9efb-429">Senha codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b9efb-429">Base64 encoded Password</span></span> |<span data-ttu-id="b9efb-430">Esta é a senha de saudação do usuário monitoramento do MySQL Olá codificada em Base64.</span><span class="sxs-lookup"><span data-stu-id="b9efb-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="b9efb-431">Atualização Automática</span><span class="sxs-lookup"><span data-stu-id="b9efb-431">AutoUpdate</span></span> |<span data-ttu-id="b9efb-432">Quando Olá provedor de OMI do MySQL é atualizado o provedor Olá examinar novamente para que as alterações no arquivo my.cnf de saudação e substituir o arquivo de autenticação de OMI do MySQL Olá.</span><span class="sxs-lookup"><span data-stu-id="b9efb-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="b9efb-433">Defina esse sinalizador tootrue ou false dependendo atualizações necessárias toohello OMI do MySQL arquivo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="b9efb-434">Local do arquivo de autenticação</span><span class="sxs-lookup"><span data-stu-id="b9efb-434">Authentication file location</span></span>
<span data-ttu-id="b9efb-435">Olá arquivo de autenticação de OMI do MySQL deve ser localizado na Olá local a seguir e chamado "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="b9efb-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="b9efb-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="b9efb-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="b9efb-437">arquivo de saudação (e o diretório auth/omsagent) devem ser de propriedade usuário omsagent de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9efb-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="b9efb-438">Logs do Agente</span><span class="sxs-lookup"><span data-stu-id="b9efb-438">Agent logs</span></span>
<span data-ttu-id="b9efb-439">logs de saudação do hello agente do OMS para Linux estão em:</span><span class="sxs-lookup"><span data-stu-id="b9efb-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="b9efb-440">/var/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="b9efb-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="b9efb-441">logs de saudação do hello agente do OMS para Linux para o programa omsconfig (configuração do agente) estão em:</span><span class="sxs-lookup"><span data-stu-id="b9efb-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="b9efb-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="b9efb-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="b9efb-443">Os logs para Olá componentes OMI e SCX (que fornecem dados de métrica de desempenho) estão em:</span><span class="sxs-lookup"><span data-stu-id="b9efb-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="b9efb-444">/var/opt/omi/log/ e /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="b9efb-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="b9efb-445">Saudação de solução de problemas do agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="b9efb-446">Use Olá toodiagnose informações a seguir e solucionar problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="b9efb-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="b9efb-447">Se nenhuma das informações contidas nesta seção de solução de problemas de saudação ajuda a você, você também pode usar Olá seguir recursos toohelp resolver seu problema.</span><span class="sxs-lookup"><span data-stu-id="b9efb-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="b9efb-448">Os clientes com suporte Premier podem registrar um caso de suporte via [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="b9efb-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="b9efb-449">Os clientes com contratos de suporte do Azure podem fazer o logon casos de suporte Olá [portal do Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="b9efb-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="b9efb-450">Arquive um [Problema no GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="b9efb-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="b9efb-451">Fórum de comentários para ideias e um relatório de erros de toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="b9efb-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="b9efb-452">Locais de log importantes</span><span class="sxs-lookup"><span data-stu-id="b9efb-452">Important log locations</span></span>
| <span data-ttu-id="b9efb-453">Arquivo</span><span class="sxs-lookup"><span data-stu-id="b9efb-453">File</span></span> | <span data-ttu-id="b9efb-454">Caminho</span><span class="sxs-lookup"><span data-stu-id="b9efb-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="b9efb-455">Agente do OMS para arquivo de log do Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="b9efb-456">Agente do OMS para arquivo de log de configuração</span><span class="sxs-lookup"><span data-stu-id="b9efb-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="b9efb-457">Arquivos de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="b9efb-457">Important configuration files</span></span>
| <span data-ttu-id="b9efb-458">Categoria</span><span class="sxs-lookup"><span data-stu-id="b9efb-458">Catergory</span></span> | <span data-ttu-id="b9efb-459">Local do arquivo</span><span class="sxs-lookup"><span data-stu-id="b9efb-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="b9efb-460">syslog</span><span class="sxs-lookup"><span data-stu-id="b9efb-460">Syslog</span></span> |<span data-ttu-id="b9efb-461">`/etc/syslog-ng/syslog-ng.conf` ou `/etc/rsyslog.conf` ou `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="b9efb-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="b9efb-462">Desempenho, Nagios, Zabbix, saída do OMS e agente geral</span><span class="sxs-lookup"><span data-stu-id="b9efb-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="b9efb-463">Configurações adicionais</span><span class="sxs-lookup"><span data-stu-id="b9efb-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="b9efb-464">Os arquivos de configuração de edição para contadores de desempenho e syslog serão substituídos se a Configuração do Portal do OMS estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="b9efb-465">Você pode desabilitar a configuração no Portal do OMS da saudação (para todos os nós) ou para nós únicos executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b9efb-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="b9efb-466">Habilitar o log de depuração</span><span class="sxs-lookup"><span data-stu-id="b9efb-466">Enable debug logging</span></span>
<span data-ttu-id="b9efb-467">depuração de tooenable log, você pode usar o plug-in do hello OMS saída e saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="b9efb-468">Plug-in de saída do OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-468">OMS output plugin</span></span>
<span data-ttu-id="b9efb-469">FluentD permite Olá plug-in toospecify níveis de log para os níveis de log diferente para entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="b9efb-470">toospecify um nível de log diferente para a saída do OMS, edita a configuração de agente geral de saudação no hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` arquivo.</span><span class="sxs-lookup"><span data-stu-id="b9efb-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="b9efb-471">Inferior Olá Olá do arquivo de configuração, alterar Olá `log_level` propriedade `info` muito`debug`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="b9efb-472">Log de depuração permite que você toosee em lote carregamentos toohello serviço OMS separado por tipo, o número de itens de dados e o tempo gasto toosend.</span><span class="sxs-lookup"><span data-stu-id="b9efb-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="b9efb-473">*Log habilitado para depuração de exemplo:*</span><span class="sxs-lookup"><span data-stu-id="b9efb-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="b9efb-474">Saída detalhada</span><span class="sxs-lookup"><span data-stu-id="b9efb-474">Verbose output</span></span>
<span data-ttu-id="b9efb-475">Em vez de usar o plug-in de saída OMS hello, você também pode gerar itens de dados diretamente muito`stdout`, que é visível no hello agente do OMS para o arquivo de log do Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="b9efb-476">No arquivo de configuração de agente geral Olá OMS em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, fora de comentário hello OMS saída plug-in adicionando um `#` na frente de cada linha.</span><span class="sxs-lookup"><span data-stu-id="b9efb-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="b9efb-477">Abaixo Olá plug-in de saída, remova o comentário hello em Olá a seção seguinte, removendo Olá `#` símbolo no início de saudação de cada linha.</span><span class="sxs-lookup"><span data-stu-id="b9efb-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="b9efb-478">Mensagens de Syslog encaminhadas não aparecem no log de saudação</span><span class="sxs-lookup"><span data-stu-id="b9efb-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-479">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-479">Probable causes</span></span>
* <span data-ttu-id="b9efb-480">Olá configuração aplicada toohello Linux server não permitir a coleta de instalações de saudação enviada de e/ou níveis de log</span><span class="sxs-lookup"><span data-stu-id="b9efb-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="b9efb-481">Syslog não é está sendo encaminhado corretamente toohello Linux server</span><span class="sxs-lookup"><span data-stu-id="b9efb-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="b9efb-482">número de saudação de mensagens encaminhadas por segundo é muito grande para a configuração de base de saudação de saudação do agente do OMS para Linux toohandle</span><span class="sxs-lookup"><span data-stu-id="b9efb-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-483">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-483">Resolutions</span></span>
* <span data-ttu-id="b9efb-484">Verifique se o essa configuração Olá no Portal do OMS de saudação de Syslog tem todos os recursos de saudação e níveis de log correto Olá</span><span class="sxs-lookup"><span data-stu-id="b9efb-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="b9efb-485">**Portal do OMS > Configurações > Dados > Syslog**</span><span class="sxs-lookup"><span data-stu-id="b9efb-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="b9efb-486">Verifique se que mensagens daemons de syslog nativo (`rsyslog`, `syslog-ng`) é tooreceive capaz de mensagens de saudação encaminhada</span><span class="sxs-lookup"><span data-stu-id="b9efb-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="b9efb-487">Verifique as configurações de firewall no hello Syslog server tooensure mensagens não estão sendo bloqueadas</span><span class="sxs-lookup"><span data-stu-id="b9efb-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="b9efb-488">Simular uma tooOMS de mensagem Syslog usando Olá `logger` comando - por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9efb-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="b9efb-489">Problemas de conexão tooOMS ao usar um proxy</span><span class="sxs-lookup"><span data-stu-id="b9efb-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-490">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-490">Probable causes</span></span>
* <span data-ttu-id="b9efb-491">proxy de saudação especificado quando o agente de saudação instalando e configurando está incorreto</span><span class="sxs-lookup"><span data-stu-id="b9efb-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="b9efb-492">pontos de extremidade de serviço do OMS Olá não são whitelistested em seu data center</span><span class="sxs-lookup"><span data-stu-id="b9efb-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-493">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-493">Resolutions</span></span>
* <span data-ttu-id="b9efb-494">Reinstalar Olá agente do OMS para Linux usando Olá após o comando com a opção de saudação `-v` habilitado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="b9efb-495">Isso permite que a saída detalhada do agente de saudação se conectam por meio do proxy de saudação toohello serviço OMS.</span><span class="sxs-lookup"><span data-stu-id="b9efb-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="b9efb-496">Revisar a documentação Olá para proxy OMS em [Configurando o agente de saudação para uso com um servidor proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="b9efb-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="b9efb-497">Verifique se esse Olá pontos de extremidade de serviço do OMS a seguir estão na lista de permissões</span><span class="sxs-lookup"><span data-stu-id="b9efb-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="b9efb-498">Recurso de agente</span><span class="sxs-lookup"><span data-stu-id="b9efb-498">Agent Resource</span></span> | <span data-ttu-id="b9efb-499">Portas</span><span class="sxs-lookup"><span data-stu-id="b9efb-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="b9efb-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b9efb-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="b9efb-501">Porta 443</span><span class="sxs-lookup"><span data-stu-id="b9efb-501">Port 443</span></span> |
| <span data-ttu-id="b9efb-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="b9efb-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="b9efb-503">Porta 443</span><span class="sxs-lookup"><span data-stu-id="b9efb-503">Port 443</span></span> |
| <span data-ttu-id="b9efb-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="b9efb-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="b9efb-505">Porta 443</span><span class="sxs-lookup"><span data-stu-id="b9efb-505">Port 443</span></span> |
| <span data-ttu-id="b9efb-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="b9efb-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="b9efb-507">Porta 443</span><span class="sxs-lookup"><span data-stu-id="b9efb-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="b9efb-508">É exibido um erro 403 durante a integração</span><span class="sxs-lookup"><span data-stu-id="b9efb-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-509">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-509">Probable causes</span></span>
* <span data-ttu-id="b9efb-510">saudação de data e hora estão incorretas no servidor Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="b9efb-511">Olá ID do espaço de trabalho e a chave do espaço de trabalho usados estão incorretas</span><span class="sxs-lookup"><span data-stu-id="b9efb-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="b9efb-512">Resolução</span><span class="sxs-lookup"><span data-stu-id="b9efb-512">Resolution</span></span>
* <span data-ttu-id="b9efb-513">Verifique se o tempo de saudação em seu servidor Linux com hello `date` comando.</span><span class="sxs-lookup"><span data-stu-id="b9efb-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="b9efb-514">Se Olá dados for maiores ou menor que 15 minutos de hello hora atual, integração falhará.</span><span class="sxs-lookup"><span data-stu-id="b9efb-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="b9efb-515">toocorrect isso, atualize date de hello e/ou fuso horário do servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="b9efb-516">a versão mais recente Olá de saudação do agente do OMS para Linux notifica se uma diferença de hora está causando a falha de integração</span><span class="sxs-lookup"><span data-stu-id="b9efb-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="b9efb-517">Usando re-carregar Olá ID correta do espaço de trabalho e a chave do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b9efb-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="b9efb-518">Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b9efb-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="b9efb-519">Um erro 500 ou erro 404 aparece no arquivo de log Olá após a integração</span><span class="sxs-lookup"><span data-stu-id="b9efb-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="b9efb-520">Esse é um problema conhecido que ocorre durante a saudação primeiro carregamento de dados do Linux em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="b9efb-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="b9efb-521">Ele não afeta os dados que estão sendo enviados ou outros problemas.</span><span class="sxs-lookup"><span data-stu-id="b9efb-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="b9efb-522">Você pode ignorar erros hello quando inicialmente integração.</span><span class="sxs-lookup"><span data-stu-id="b9efb-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="b9efb-523">Dados de Nagios não aparecem no Portal do OMS de saudação</span><span class="sxs-lookup"><span data-stu-id="b9efb-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-524">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-524">Probable causes</span></span>
* <span data-ttu-id="b9efb-525">Olá omsagent o usuário não tem permissões tooread de arquivo de log Nagios Olá</span><span class="sxs-lookup"><span data-stu-id="b9efb-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="b9efb-526">Olá Nagios origem e filtro seções ainda comentários no arquivo de omsagent Olá</span><span class="sxs-lookup"><span data-stu-id="b9efb-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-527">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-527">Resolutions</span></span>
* <span data-ttu-id="b9efb-528">Adicione usuário omsagent de saudação em ordem tooread do arquivo de Nagios hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="b9efb-529">Confira [Alertas do Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b9efb-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="b9efb-530">No hello agente do OMS para o arquivo de configuração geral do Linux no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, certifique-se de que **ambos** Olá Nagios seções de origem e filtro tem comentários removidos, semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="b9efb-531">Dados do Linux não aparecem em Olá Portal do OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-532">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-532">Probable causes</span></span>
* <span data-ttu-id="b9efb-533">Falha de serviço do OMS toohello de integração</span><span class="sxs-lookup"><span data-stu-id="b9efb-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="b9efb-534">Conexão toohello serviço OMS está bloqueado</span><span class="sxs-lookup"><span data-stu-id="b9efb-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="b9efb-535">saudação de agente do OMS para Linux dados é armazenado em backup</span><span class="sxs-lookup"><span data-stu-id="b9efb-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-536">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-536">Resolutions</span></span>
* <span data-ttu-id="b9efb-537">Verifique se que toohello integração serviço OMS foi bem-sucedida verificando que Olá `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="b9efb-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="b9efb-538">Usando re-carregar Olá a linha de comando omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="b9efb-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="b9efb-539">Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b9efb-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="b9efb-540">Se usar um proxy, usar etapas para solução de problemas de proxy de saudação acima</span><span class="sxs-lookup"><span data-stu-id="b9efb-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="b9efb-541">Em alguns casos, quando Olá agente do OMS para Linux não pode se comunicar com hello serviço OMS, dados de saudação Agent estão tamanho de buffer cheio toohello de backup de 50 MB.</span><span class="sxs-lookup"><span data-stu-id="b9efb-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="b9efb-542">Reiniciar Olá agente do OMS para Linux executando Olá `/opt/microsoft/omsagent/bin/service_control restart` comando.</span><span class="sxs-lookup"><span data-stu-id="b9efb-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="b9efb-543">Esse problema foi corrigido nas versões 1.1.0-28 e posteriores do Agente.</span><span class="sxs-lookup"><span data-stu-id="b9efb-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="b9efb-544">Configuração do contador de desempenho de syslog Linux não é aplicada no portal do OMS Olá</span><span class="sxs-lookup"><span data-stu-id="b9efb-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-545">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-545">Probable causes</span></span>
* <span data-ttu-id="b9efb-546">Agente de configuração de saudação de saudação do agente do OMS para Linux não recuperou configuração mais recente de saudação do portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="b9efb-547">Olá revisadas configurações no portal de saudação não foram aplicadas</span><span class="sxs-lookup"><span data-stu-id="b9efb-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-548">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-548">Resolutions</span></span>
<span data-ttu-id="b9efb-549">`omsconfig`é o agente de configuração de saudação de saudação do agente do OMS para Linux que recupera alterações de configuração do portal do OMS a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="b9efb-550">Essa configuração é então aplicado toohello agente do OMS para Linux arquivos de configuração localizado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="b9efb-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="b9efb-551">Em alguns casos, Olá agente do OMS para Linux agente de configuração talvez não seja capaz de toocommunicate com o serviço de configuração do portal Olá resultante na configuração mais recente não está sendo aplicada.</span><span class="sxs-lookup"><span data-stu-id="b9efb-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="b9efb-552">Verifique se esse Olá `omsconfig` agente é instalado com o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b9efb-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="b9efb-553">`dpkg --list omsconfig` ou `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="b9efb-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="b9efb-554">Se não estiver instalado, reinstale a versão mais recente Olá de saudação do agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="b9efb-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="b9efb-555">Verifique se esse Olá `omsconfig` agente possa se comunicar com hello serviço OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="b9efb-556">Executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="b9efb-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="b9efb-557">Olá comando acima retorna Olá configuração que o agente recupera do portal hello, incluindo configurações de Syslog, contadores de desempenho do Linux e logs personalizados</span><span class="sxs-lookup"><span data-stu-id="b9efb-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="b9efb-558">Se Olá comando acima falhar, executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="b9efb-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="b9efb-559">Esse comando força Olá omsconfig agente toocommunicate com a configuração da mais recente de Olá Olá OMS serviço tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="b9efb-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="b9efb-560">Dados de log personalizado do Linux não aparecem na Olá Portal do OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b9efb-561">Causas prováveis</span><span class="sxs-lookup"><span data-stu-id="b9efb-561">Probable causes</span></span>
* <span data-ttu-id="b9efb-562">Falha do serviço de integração tooOMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="b9efb-563">Olá **Olá aplicar configuração toomy servidores Linux a seguir** configuração não tiver sido selecionada</span><span class="sxs-lookup"><span data-stu-id="b9efb-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="b9efb-564">omsconfig não tem escolhidas log personalizado mais recente de saudação do portal de saudação</span><span class="sxs-lookup"><span data-stu-id="b9efb-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="b9efb-565">Olá `omsagent` uso é log personalizado do hello tooaccess não é possível devido a problema de permissões tooa ou `omsagent` não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="b9efb-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="b9efb-566">Nesse caso, você verá Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="b9efb-567">Este é um problema conhecido com hello condição de corrida que foi corrigido hello agente do OMS para Linux versão 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="b9efb-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b9efb-568">Resoluções</span><span class="sxs-lookup"><span data-stu-id="b9efb-568">Resolutions</span></span>
* <span data-ttu-id="b9efb-569">Verifique se que você tenha com êxito incorporados, determinando se hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` arquivo existe.</span><span class="sxs-lookup"><span data-stu-id="b9efb-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="b9efb-570">Se necessário, integrar novamente usando a linha de comando omsadmin.sh hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="b9efb-571">Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b9efb-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="b9efb-572">Em Olá Portal do OMS em **configurações** em Olá **dados** guia, certifique-se de que Olá **Olá aplicar configuração toomy servidores Linux a seguir** configuração é selecionada</span><span class="sxs-lookup"><span data-stu-id="b9efb-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="b9efb-573">![aplicar configuração](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="b9efb-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="b9efb-574">Verifique se esse Olá `omsconfig` agente possa se comunicar com hello serviço OMS</span><span class="sxs-lookup"><span data-stu-id="b9efb-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="b9efb-575">Executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="b9efb-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="b9efb-576">Olá comando acima retorna Olá configuração que o agente recupera do hello Portal, incluindo configurações de Syslog, contadores de desempenho do Linux e Logs personalizados</span><span class="sxs-lookup"><span data-stu-id="b9efb-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="b9efb-577">Se Olá comando acima falhar, executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="b9efb-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="b9efb-578">Esse comando força Olá omsconfig agente toocommunicate com o serviço OMS e recuperar a configuração mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="b9efb-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="b9efb-579">Em vez de saudação do agente do OMS para execução como um usuário com privilégios de usuário do Linux `root`, Olá agente do OMS para Linux como Olá `omsagent` usuário.</span><span class="sxs-lookup"><span data-stu-id="b9efb-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="b9efb-580">Na maioria dos casos, a permissão explícita deve ser concedida usuário toohello em ordem tooread alguns arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9efb-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="b9efb-581">permissão toogrant muito`omsagent` usuário, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="b9efb-582">Adicionar Olá `omsagent` grupo específico do usuário tooa com`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="b9efb-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="b9efb-583">Conceder acesso de leitura universal toohello necessários arquivos com`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="b9efb-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="b9efb-584">Há um problema conhecido com hello condição de corrida que foi corrigido hello agente do OMS para Linux versão 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="b9efb-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="b9efb-585">Depois de atualizar o agente mais recente toohello, execute Olá versão mais recente do comando tooget saudação do plug-in do hello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9efb-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="b9efb-586">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="b9efb-586">Known limitations</span></span>
<span data-ttu-id="b9efb-587">Examine Olá toolearn seções sobre as limitações atuais de saudação do agente do OMS para Linux a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="b9efb-588">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="b9efb-588">Azure Diagnostics</span></span>
<span data-ttu-id="b9efb-589">Para máquinas virtuais do Linux em execução no Azure, etapas adicionais podem ser necessárias tooallow a coleta de dados pelo diagnóstico do Azure e Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="b9efb-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="b9efb-590">**Versão 2.2** da saudação extensão de diagnóstico para Linux é necessária para compatibilidade com hello agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="b9efb-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="b9efb-591">Para obter mais informações sobre como instalar e configurar Olá extensão de diagnóstico para Linux, consulte [usar Olá CLI do Azure comando tooenable extensão de diagnóstico do Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="b9efb-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="b9efb-592">**Atualizando Olá extensão de diagnóstico do Linux do 2.0 too2.2 ASM da CLI do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b9efb-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="b9efb-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="b9efb-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="b9efb-594">Esses exemplos de comando fazem referência a um arquivo chamado PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="b9efb-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="b9efb-595">formato de saudação do arquivo deve ser semelhante a saudação de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9efb-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="b9efb-596">Não há suporte para Sysklog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-596">Sysklog is not supported</span></span>
<span data-ttu-id="b9efb-597">O rsyslog ou syslog-ng é necessário toocollect mensagens de syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="b9efb-598">Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="b9efb-599">toocollect dados de syslog dessa versão de distribuições, Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="b9efb-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="b9efb-600">Para obter mais informações sobre como substituir sysklog por rsyslog, consulte [instalar o RPM de rsyslog Olá recém-criadas](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="b9efb-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9efb-601">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9efb-601">Next Steps</span></span>
* <span data-ttu-id="b9efb-602">[Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="b9efb-603">Familiarize-se com [pesquisas de log](log-analytics-log-searches.md) tooview detalhadas informações coletadas por meio de soluções.</span><span class="sxs-lookup"><span data-stu-id="b9efb-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="b9efb-604">Use [painéis](log-analytics-dashboards.md) toosave e exibição procura próprios e personalizados.</span><span class="sxs-lookup"><span data-stu-id="b9efb-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
