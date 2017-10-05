---
title: Monitorar e gerenciar o Azure HDInsight usando a uusando a IU da Web do Ambari | Microsoft Docs
description: "Aprenda a usar o Ambari para monitorar e gerenciar clusters HDInsight baseados em Linux. Neste documento, você aprenderá a usar a interface de usuário do Ambari Web com clusters HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="bb8d3-104">Gerenciar clusters HDInsight usando a interface de usuário do Ambari Web</span><span class="sxs-lookup"><span data-stu-id="bb8d3-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="bb8d3-105">O Apache Ambari simplifica o gerenciamento e monitoramento de um cluster Hadoop, fornecendo uma forma fácil de usar a interface do usuário da Web e a API REST.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="bb8d3-106">O Ambari está incluído em clusters HDInsight baseados em Linux e é usado para monitorar o cluster e fazer alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="bb8d3-107">Neste documento, você aprenderá a usar a interface de usuário do Ambari Web com um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="bb8d3-108"><a id="whatis"></a>O que é o Ambari?</span><span class="sxs-lookup"><span data-stu-id="bb8d3-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="bb8d3-109">O [Apache Ambari](http://ambari.apache.org) simplifica o gerenciamento do Hadoop, fornecendo uma interface do usuário da Web fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="bb8d3-110">Você pode usar o Ambari para criar, gerenciar e monitorar clusters do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="bb8d3-111">Os desenvolvedores podem integrar essas funcionalidades em seus aplicativos usando as [APIs REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="bb8d3-112">A IU da Web do Ambari é fornecida por padrão com clusters HDInsight que usam o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb8d3-113">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bb8d3-114">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="bb8d3-115">Conectividade</span><span class="sxs-lookup"><span data-stu-id="bb8d3-115">Connectivity</span></span>

<span data-ttu-id="bb8d3-116">A IU da Web do Ambari está disponível no seu cluster HDInsight em HTTPS://CLUSTERNAME.azurehdidnsight.net, onde **CLUSTERNAME** é o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb8d3-117">Conectar-se ao Ambari no HDInsight requer HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="bb8d3-118">Quando a autenticação for solicitada, use o nome e a senha da conta do administrador que você forneceu quando o cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="bb8d3-119">Túnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="bb8d3-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="bb8d3-120">Enquanto o Ambari para o cluster é acessível diretamente pela Internet, alguns links da interface do usuário da Web do Ambari (como para o JobTracker) não são expostos na Internet.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="bb8d3-121">Para acessar esses serviços, você deve criar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="bb8d3-122">Para obter mais informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="bb8d3-123">Interface do usuário da Ambari Web</span><span class="sxs-lookup"><span data-stu-id="bb8d3-123">Ambari Web UI</span></span>

<span data-ttu-id="bb8d3-124">Ao se conectar à interface do usuário do Ambari Web, você recebe uma solicitação para autenticar a página.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="bb8d3-125">Use a senha e o usuário administrador de cluster (Admin padrão) usados durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="bb8d3-126">Quando a página se abrir, observe a barra na parte superior.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="bb8d3-127">Essa barra contém as seguintes informações e controles:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-127">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="bb8d3-129">**Logotipo do Ambari** : abre o painel, que pode ser usado para monitorar o cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="bb8d3-130">**Nº operações do nome de cluster** : exibe o número de operações do Ambari em andamento.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="bb8d3-131">A seleção do nome do cluster ou **Nº operações** exibe uma lista de operações em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="bb8d3-132">**N°. de alertas**: avisos ou alertas críticos, se houver, para o cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="bb8d3-133">**Painel** : exibe o painel.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="bb8d3-134">**Serviços** : informações e definições de configuração dos serviços do cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="bb8d3-135">**Hosts** : informações e definições de configuração dos nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="bb8d3-136">**Alertas** : um log de informações, avisos e alertas críticos.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="bb8d3-137">**Admin** : pilha/serviços de software que estão instalados no cluster, informações de conta de serviço e segurança Kerberos.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="bb8d3-138">**Botão Admin** : gerenciamento, configurações de usuário e logoff do Ambari.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="bb8d3-139">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="bb8d3-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="bb8d3-140">Alertas</span><span class="sxs-lookup"><span data-stu-id="bb8d3-140">Alerts</span></span>

<span data-ttu-id="bb8d3-141">A lista a seguir contém os status de alerta comuns usados pelo Ambari:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="bb8d3-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="bb8d3-142">**OK**</span></span>
* <span data-ttu-id="bb8d3-143">**Aviso**</span><span class="sxs-lookup"><span data-stu-id="bb8d3-143">**Warning**</span></span>
* <span data-ttu-id="bb8d3-144">**CRÍTICO**</span><span class="sxs-lookup"><span data-stu-id="bb8d3-144">**CRITICAL**</span></span>
* <span data-ttu-id="bb8d3-145">**DESCONHECIDO**</span><span class="sxs-lookup"><span data-stu-id="bb8d3-145">**UNKNOWN**</span></span>

<span data-ttu-id="bb8d3-146">Os alertas diferentes de **OK** fazem com que a entrada **nº alertas** na parte superior da página exiba o número de alertas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="bb8d3-147">A seleção dessa entrada exibe os alertas e seus status.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="bb8d3-148">Os alertas estão organizados em vários grupos padrão, que podem ser exibidos na página **Alertas** .</span><span class="sxs-lookup"><span data-stu-id="bb8d3-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![página alertas](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="bb8d3-150">Você pode gerenciar os grupos usando o menu **Ações** e selecionando **Gerenciar Grupos de Alerta**.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![diálogo gerenciar grupos de alerta](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="bb8d3-152">Você também pode gerenciar os métodos de alerta e criar notificações de alerta no menu **Ações** selecionando __Gerenciar Notificações de Alerta__.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="bb8d3-153">Quaisquer notificações atuais são exibidas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-153">Any current notifications are displayed.</span></span> <span data-ttu-id="bb8d3-154">Você também pode criar notificações daqui.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-154">You can also create notifications from here.</span></span> <span data-ttu-id="bb8d3-155">As notificações podem ser enviadas por **EMAIL** ou **SNMP** quando ocorrerem combinações específicas de alerta/gravidade.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="bb8d3-156">Por exemplo, você pode enviar uma mensagem de email quando qualquer um dos alertas no grupo **YARN Padrão** está definido para **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![Diálogo Criar alerta](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="bb8d3-158">Por fim, selecionar __Gerenciar Definições de Alerta__ do menu __Ações__ permite que você defina o número de vezes que um alerta deve ocorrer antes do envio de uma notificação.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="bb8d3-159">Essa configuração pode ser usada para evitar notificações de erros transitórios.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="bb8d3-160">HDInsight</span><span class="sxs-lookup"><span data-stu-id="bb8d3-160">Cluster</span></span>

<span data-ttu-id="bb8d3-161">A guia **Métricas** do painel contém uma série de widgets que facilitam monitorar o status do cluster em um relance.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="bb8d3-162">Vários widgets, tais como **Uso de CPU**, fornecem informações adicionais quando são clicados.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![painel com metrics](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="bb8d3-164">A guia **Mapa de Dados** exibe as métricas na forma de mapas de dados coloridos, que vão do verde ao vermelho.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![painel com heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="bb8d3-166">Para obter mais informações sobre os nós no cluster, selecione **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="bb8d3-167">Selecione o nó específico em que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-167">Then select the specific node you are interested in.</span></span>

![detalhes do host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="bb8d3-169">Serviços</span><span class="sxs-lookup"><span data-stu-id="bb8d3-169">Services</span></span>

<span data-ttu-id="bb8d3-170">A barra lateral **Serviços** no painel oferece uma visão rápida do status dos serviços em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="bb8d3-171">Ícones diversos são usados para indicar o status ou ações que devem ser realizadas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="bb8d3-172">Por exemplo, um símbolo amarelo de reciclagem será exibido se um serviço precisar ser reciclado.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![barra lateral serviços](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="bb8d3-174">Os serviços exibidos variam de acordo com versões e tipos de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="bb8d3-175">Os serviços exibidos aqui podem ser diferentes dos serviços exibidos para o cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="bb8d3-176">A seleção de um serviço exibirá informações mais detalhadas sobre o serviço.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-176">Selecting a service displays more detailed information on the service.</span></span>

![informações de resumo do serviço](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="bb8d3-178">Links rápidos</span><span class="sxs-lookup"><span data-stu-id="bb8d3-178">Quick links</span></span>

<span data-ttu-id="bb8d3-179">Alguns serviços exibem um link **Links Rápidos** na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="bb8d3-180">Ele pode ser usado para acessar IUs da Web específicas do serviço, como:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="bb8d3-181">**Histórico de Trabalhos** : histórico de trabalhos do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="bb8d3-182">**Gerenciador de Recursos** : IU do gerenciador de recursos YARN RM.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="bb8d3-183">**NameNode** : IU NameNode no HDFS (Sistema de Arquivos Distribuído do Hadoop).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="bb8d3-184">**IU da Web do Oozie** : IU do Oozie.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="bb8d3-185">A seleção de qualquer um desses links abrirá uma nova guia em seu navegador, que exibirá a página selecionada.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="bb8d3-186">Selecionar a entrada **Links Rápidos** para um serviço pode retornar um erro de "servidor não encontrado".</span><span class="sxs-lookup"><span data-stu-id="bb8d3-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="bb8d3-187">Se você encontrar esse erro, você deverá usar um túnel SSH ao usar a entrada **Links rápidos** para esse serviço.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="bb8d3-188">Para obter informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="bb8d3-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="bb8d3-189">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="bb8d3-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="bb8d3-190">Usuários, grupos e permissões do Ambari</span><span class="sxs-lookup"><span data-stu-id="bb8d3-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="bb8d3-191">O trabalho com usuários, grupos e permissões tem suporte ao usar um cluster HDInsight [ingressado no domínio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="bb8d3-192">Para obter informações sobre o uso da IU de Gerenciamento do Ambari em um cluster ingressado no domínio, consulte [Gerenciar clusters HDInsight ingressados no domínio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="bb8d3-193">Não altere a senha do watchdog Ambari (hdinsightwatchdog) no seu cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="bb8d3-194">A alteração da senha interrompe a capacidade de usar as ações de script ou executar operações de dimensionamento com o cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="bb8d3-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="bb8d3-195">Hosts</span></span>

<span data-ttu-id="bb8d3-196">A página **Hosts** lista todos os hosts no cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="bb8d3-197">Para gerenciar hosts, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-197">To manage hosts, follow these steps.</span></span>

![página hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="bb8d3-199">As ações de adicionar, encerrar e reativar um host não devem ser realizadas com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="bb8d3-200">Selecione o host que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="bb8d3-201">Use o menu **Ações** para selecionar a ação que deseja executar:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="bb8d3-202">**Iniciar todos os componentes** : iniciar todos os componentes no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="bb8d3-203">**Parar todos os componentes** : parar todos os componentes no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="bb8d3-204">**Reiniciar todos os componentes** : parar e iniciar todos os componentes no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="bb8d3-205">**Ativar o modo de manutenção** : suprime os alertas sobre o host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="bb8d3-206">Esse modo deverá ser habilitado se você estiver realizando ações que geram alertas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="bb8d3-207">Por exemplo, parar e iniciar um serviço.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="bb8d3-208">**Desativar o modo de manutenção** : retorna o host para o modo de alerta normal.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="bb8d3-209">**Parar** : Para o DataNode ou NodeManagers no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="bb8d3-210">**Iniciar** : Inicia o DataNode ou NodeManagers no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="bb8d3-211">**Reiniciar** : para e inicia o DataNode ou NodeManagers no host.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="bb8d3-212">**Encerramento** : remove um host do cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bb8d3-213">Não use esta ação em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="bb8d3-214">**Reativação** : adiciona ao cluster um host que foi encerrado.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bb8d3-215">Não use esta ação em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="bb8d3-216"><a id="service"></a>Serviços</span><span class="sxs-lookup"><span data-stu-id="bb8d3-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="bb8d3-217">Na página **Painel** ou **Serviços**, use o botão **Ações** na parte inferior da lista de serviços para interromper e iniciar todos os serviços.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![Ações de Serviço](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="bb8d3-219">Enquanto **Adicionar Serviço** estiver listado nesse menu, ele não deverá ser usado para adicionar serviços ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="bb8d3-220">Novos serviços devem ser adicionados usando uma Ação de Script durante o provisionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="bb8d3-221">Para saber mais sobre o uso de ações de script, consulte [Personalizar clusters HDInsight usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="bb8d3-222">Embora o botão **Ações** possa reiniciar todos os serviços, muitas vezes convém iniciar, parar ou reiniciar um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="bb8d3-223">Use as seguintes etapas para executar ações em um serviço individual:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="bb8d3-224">Na página **Painel** ou **Serviços**, selecione um serviço.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="bb8d3-225">Na parte superior da guia **Resumo**, use o botão **Ações de Serviço** e selecione a ação a tomar.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="bb8d3-226">Isso reinicia o serviço em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-226">This restarts the service on all nodes.</span></span>

    ![ação de serviço](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="bb8d3-228">Reiniciar alguns serviços enquanto o cluster estiver em execução pode gerar alertas.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="bb8d3-229">Para evitar alertas, você pode usar o botão **Ações de Serviço** para habilitar o **Modo de manutenção** para o serviço antes de executar a reinicialização.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="bb8d3-230">Depois que uma ação é selecionada, a entrada **Nº operações** na parte superior da página aumenta para mostrar que está ocorrendo uma operação em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="bb8d3-231">Se a exibição estiver configurada, a lista de operações em segundo plano será exibida.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bb8d3-232">Se você habilitou o **modo Manutenção** para o serviço, lembre-se de desabilitá-lo usando o botão **Ações de Serviço** quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="bb8d3-233">Para configurar um serviço, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="bb8d3-234">Na página **Painel** ou **Serviços**, selecione um serviço.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="bb8d3-235">Selecione a guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="bb8d3-235">Select the **Configs** tab.</span></span> <span data-ttu-id="bb8d3-236">A configuração atual é exibida.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-236">The current configuration is displayed.</span></span> <span data-ttu-id="bb8d3-237">Uma lista das configurações anteriores também é exibida.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-237">A list of previous configurations is also displayed.</span></span>

    ![configurações](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="bb8d3-239">Use os campos exibidos para modificar a configuração e selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="bb8d3-240">Ou selecione uma configuração anterior e clique em **Tornar atual** para reverter para as configurações anteriores.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="bb8d3-241">Exibições do Ambari</span><span class="sxs-lookup"><span data-stu-id="bb8d3-241">Ambari views</span></span>

<span data-ttu-id="bb8d3-242">As Exibições do Ambari permitem que os desenvolvedores conectem elementos de interface do usuário à interface do usuário da Web do Ambari usando a [Estrutura de modos de exibição do Ambari](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="bb8d3-243">O HDInsight fornece as seguintes exibições com tipos de cluster do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="bb8d3-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="bb8d3-244">Gerenciador de filas Yarn: o gerenciador de filas fornece uma interface do usuário simples para exibir e modificar filas YARN.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="bb8d3-245">Exibição do Hive: a Exibição do Hive permite executar consultas de Hive diretamente do seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="bb8d3-246">Você pode salvar consultas, exibir os resultados, salvar os resultados no armazenamento de cluster ou baixar os resultados no sistema local.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="bb8d3-247">Para obter mais informações sobre como usar Exibições do Hive, consulte [Usar Exibições do Hive com o HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="bb8d3-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="bb8d3-248">Exibição Tez: a exibição Tez permite que você compreenda melhor e otimize os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="bb8d3-249">Você pode exibir informações sobre como os trabalhos do Tez são executados e quais recursos são usados.</span><span class="sxs-lookup"><span data-stu-id="bb8d3-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
