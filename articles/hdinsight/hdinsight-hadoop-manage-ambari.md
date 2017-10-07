---
title: "aaaMonitor e gerenciar o HDInsight do Azure usando a interface do usuário do Ambari Web | Microsoft Docs"
description: "Saiba como toouse Ambari toomonitor e gerencie clusters HDInsight baseados em Linux. Neste documento, você aprenderá como clusters de saudação toouse Ambari da interface do usuário da Web incluídos no HDInsight."
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
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="da1ac-104">Gerenciar clusters HDInsight usando Olá Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="da1ac-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="da1ac-105">Apache Ambari simplifica o gerenciamento de saudação e monitoramento de um cluster de Hadoop, fornecendo a interface do usuário e REST API toouse fácil da web.</span><span class="sxs-lookup"><span data-stu-id="da1ac-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="da1ac-106">Ambari é incluído em clusters HDInsight baseados em Linux e é Olá toomonitor usado cluster e faça alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="da1ac-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="da1ac-107">Neste documento, você aprenderá como toouse Olá Ambari Web UI com um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da1ac-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="da1ac-108"><a id="whatis"></a>O que é o Ambari?</span><span class="sxs-lookup"><span data-stu-id="da1ac-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="da1ac-109">O [Apache Ambari](http://ambari.apache.org) simplifica o gerenciamento do Hadoop, fornecendo uma interface do usuário da Web fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="da1ac-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="da1ac-110">Você pode usar o Ambari para criar, gerenciar e monitorar clusters do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="da1ac-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="da1ac-111">Os desenvolvedores podem integrar esses recursos em seus aplicativos usando Olá [APIs de REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="da1ac-112">Saudação da interface do usuário do Ambari Web é fornecida por padrão com clusters de HDInsight que usam o sistema de operacional Linux hello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da1ac-113">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="da1ac-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="da1ac-114">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="da1ac-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="da1ac-115">Conectividade</span><span class="sxs-lookup"><span data-stu-id="da1ac-115">Connectivity</span></span>

<span data-ttu-id="da1ac-116">Saudação da interface do usuário do Ambari Web está disponível no seu cluster HDInsight no HTTPS://CLUSTERNAME.azurehdidnsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da1ac-117">Conexão tooAmbari no HDInsight requer HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da1ac-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="da1ac-118">Quando solicitado para autenticação, use o nome de conta de administrador hello e senha que você forneceu quando Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="da1ac-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="da1ac-119">Túnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="da1ac-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="da1ac-120">Enquanto o Ambari para o cluster pode ser acessada diretamente pela Internet de hello, alguns links da saudação Ambari Web UI (como toohello JobTracker) não são expostos no hello da internet.</span><span class="sxs-lookup"><span data-stu-id="da1ac-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="da1ac-121">tooaccess esses serviços, você deve criar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="da1ac-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="da1ac-122">Para obter mais informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="da1ac-123">Interface do usuário da Ambari Web</span><span class="sxs-lookup"><span data-stu-id="da1ac-123">Ambari Web UI</span></span>

<span data-ttu-id="da1ac-124">Ao conectar-se toohello Ambari Web UI, será solicitado tooauthenticate toohello página.</span><span class="sxs-lookup"><span data-stu-id="da1ac-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="da1ac-125">Use o usuário de administrador de cluster saudação (padrão de administrador) e a senha usada durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="da1ac-126">Quando abre a página hello, observe barra Olá na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="da1ac-127">Essa barra contém seguinte Olá informações e controles:</span><span class="sxs-lookup"><span data-stu-id="da1ac-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="da1ac-129">**Logotipo do Ambari** -abre o painel hello, que pode ser usado toomonitor Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="da1ac-130">**Operações de # nome de cluster** -exibe o número de saudação do Ambari as operações em andamento.</span><span class="sxs-lookup"><span data-stu-id="da1ac-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="da1ac-131">Selecionar nome do cluster hello ou **ops #** exibe uma lista de operações em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="da1ac-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="da1ac-132">**alertas de #** -exibe avisos ou alertas críticos, se houver, para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="da1ac-133">**Painel** -painel de saudação exibe.</span><span class="sxs-lookup"><span data-stu-id="da1ac-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="da1ac-134">**Serviços** -configurações de configuração e as informações para os serviços de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="da1ac-135">**Hosts** -configurações de configuração e as informações de nós de saudação no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="da1ac-136">**Alertas** : um log de informações, avisos e alertas críticos.</span><span class="sxs-lookup"><span data-stu-id="da1ac-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="da1ac-137">**Administrador** -pilha/serviços de Software que estão instalados no cluster hello, informações de conta de serviço e segurança Kerberos.</span><span class="sxs-lookup"><span data-stu-id="da1ac-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="da1ac-138">**Botão Admin** : gerenciamento, configurações de usuário e logoff do Ambari.</span><span class="sxs-lookup"><span data-stu-id="da1ac-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="da1ac-139">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="da1ac-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="da1ac-140">Alertas</span><span class="sxs-lookup"><span data-stu-id="da1ac-140">Alerts</span></span>

<span data-ttu-id="da1ac-141">Olá lista a seguir contém Olá comuns status usados pelo Ambari:</span><span class="sxs-lookup"><span data-stu-id="da1ac-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="da1ac-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="da1ac-142">**OK**</span></span>
* <span data-ttu-id="da1ac-143">**Aviso**</span><span class="sxs-lookup"><span data-stu-id="da1ac-143">**Warning**</span></span>
* <span data-ttu-id="da1ac-144">**CRÍTICO**</span><span class="sxs-lookup"><span data-stu-id="da1ac-144">**CRITICAL**</span></span>
* <span data-ttu-id="da1ac-145">**DESCONHECIDO**</span><span class="sxs-lookup"><span data-stu-id="da1ac-145">**UNKNOWN**</span></span>

<span data-ttu-id="da1ac-146">Alertas que **Okey** causar Olá **alertas #** entrada na parte superior de saudação do número da saudação toodisplay Olá página de alertas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="da1ac-147">Selecionar essa entrada exibe alertas hello e seus status.</span><span class="sxs-lookup"><span data-stu-id="da1ac-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="da1ac-148">Alertas são organizados em vários grupos padrão, que podem ser exibidos da saudação **alertas** página.</span><span class="sxs-lookup"><span data-stu-id="da1ac-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![página alertas](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="da1ac-150">Você pode gerenciar grupos de saudação usando Olá **ações** menu e selecionando **gerenciar grupos de alerta**.</span><span class="sxs-lookup"><span data-stu-id="da1ac-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![diálogo gerenciar grupos de alerta](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="da1ac-152">Você também pode gerenciar os métodos de alerta e criar notificações de alerta de saudação **ações** menu selecionando __gerenciar notificações de alerta__.</span><span class="sxs-lookup"><span data-stu-id="da1ac-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="da1ac-153">Quaisquer notificações atuais são exibidas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-153">Any current notifications are displayed.</span></span> <span data-ttu-id="da1ac-154">Você também pode criar notificações daqui.</span><span class="sxs-lookup"><span data-stu-id="da1ac-154">You can also create notifications from here.</span></span> <span data-ttu-id="da1ac-155">As notificações podem ser enviadas por **EMAIL** ou **SNMP** quando ocorrerem combinações específicas de alerta/gravidade.</span><span class="sxs-lookup"><span data-stu-id="da1ac-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="da1ac-156">Por exemplo, você pode enviar uma mensagem de email quando qualquer um dos alertas de saudação em Olá **YARN padrão** grupo está definido muito**crítico**.</span><span class="sxs-lookup"><span data-stu-id="da1ac-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![Diálogo Criar alerta](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="da1ac-158">Por fim, selecionando __gerenciar configurações de alerta__ de saudação __ações__ menu permite tooset número de saudação de vezes que um alerta deve ocorrer antes que uma notificação é enviada.</span><span class="sxs-lookup"><span data-stu-id="da1ac-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="da1ac-159">Essa configuração pode ser usado tooprevent notificações para erros transitórios.</span><span class="sxs-lookup"><span data-stu-id="da1ac-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="da1ac-160">HDInsight</span><span class="sxs-lookup"><span data-stu-id="da1ac-160">Cluster</span></span>

<span data-ttu-id="da1ac-161">Olá **métricas** Olá painel contém uma série de widgets que tornam mais fácil toomonitor status de saudação do cluster em um relance.</span><span class="sxs-lookup"><span data-stu-id="da1ac-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="da1ac-162">Vários widgets, tais como **Uso de CPU**, fornecem informações adicionais quando são clicados.</span><span class="sxs-lookup"><span data-stu-id="da1ac-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![painel com metrics](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="da1ac-164">Olá **Heatmaps** guia exibe as métricas como heatmaps colorida, indo de toored verde.</span><span class="sxs-lookup"><span data-stu-id="da1ac-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![painel com heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="da1ac-166">Para obter mais informações sobre nós Olá em cluster hello, selecione **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="da1ac-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="da1ac-167">Selecione Olá nó específico que lhe interessam.</span><span class="sxs-lookup"><span data-stu-id="da1ac-167">Then select hello specific node you are interested in.</span></span>

![detalhes do host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="da1ac-169">Serviços</span><span class="sxs-lookup"><span data-stu-id="da1ac-169">Services</span></span>

<span data-ttu-id="da1ac-170">Olá **serviços** barra lateral no painel de saudação fornece visão rápida do status de Olá dos serviços de saudação em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="da1ac-171">Vários ícones são usados tooindicate status ou ações que devem ser tomadas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="da1ac-172">Por exemplo, um símbolo de reciclagem amarelo é exibido se um serviço precisa toobe reciclado.</span><span class="sxs-lookup"><span data-stu-id="da1ac-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![barra lateral serviços](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="da1ac-174">serviços Olá exibidos diferem entre as versões e tipos de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da1ac-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="da1ac-175">Serviços de saudação exibidos aqui podem ser diferentes Olá serviços exibidos para o cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="da1ac-176">Selecionar um serviço exibe informações mais detalhadas no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-176">Selecting a service displays more detailed information on hello service.</span></span>

![informações de resumo do serviço](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="da1ac-178">Links rápidos</span><span class="sxs-lookup"><span data-stu-id="da1ac-178">Quick links</span></span>

<span data-ttu-id="da1ac-179">Alguns serviços exibição um **Links rápidos** link na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="da1ac-180">Isso pode ser web específico do serviço de tooaccess usado interfaces do usuário, como:</span><span class="sxs-lookup"><span data-stu-id="da1ac-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="da1ac-181">**Histórico de Trabalhos** : histórico de trabalhos do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="da1ac-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="da1ac-182">**Gerenciador de Recursos** : IU do gerenciador de recursos YARN RM.</span><span class="sxs-lookup"><span data-stu-id="da1ac-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="da1ac-183">**NameNode** : IU NameNode no HDFS (Sistema de Arquivos Distribuído do Hadoop).</span><span class="sxs-lookup"><span data-stu-id="da1ac-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="da1ac-184">**IU da Web do Oozie** : IU do Oozie.</span><span class="sxs-lookup"><span data-stu-id="da1ac-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="da1ac-185">Selecionar qualquer um desses links abre uma nova guia no seu navegador, que exibe a página selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="da1ac-186">Olá selecionando **Links rápidos** entrada para um serviço pode retornar um erro "servidor não encontrado".</span><span class="sxs-lookup"><span data-stu-id="da1ac-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="da1ac-187">Se você encontrar esse erro, você deve usar um túnel SSH ao usar Olá **Links rápidos** entrada para este serviço.</span><span class="sxs-lookup"><span data-stu-id="da1ac-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="da1ac-188">Para obter informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="da1ac-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="da1ac-189">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="da1ac-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="da1ac-190">Usuários, grupos e permissões do Ambari</span><span class="sxs-lookup"><span data-stu-id="da1ac-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="da1ac-191">O trabalho com usuários, grupos e permissões tem suporte ao usar um cluster HDInsight [ingressado no domínio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="da1ac-192">Para obter informações sobre como usar o hello Ambari da interface do usuário de gerenciamento em um cluster de domínio, consulte [gerenciar clusters de HDInsight domínio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="da1ac-193">Não altere a senha de saudação de watchdog de Ambari hello (hdinsightwatchdog) no seu cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="da1ac-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="da1ac-194">Alteração quebras de senha Olá Olá ações de script toouse capacidade ou executam operações de dimensionamento com o cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="da1ac-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="da1ac-195">Hosts</span></span>

<span data-ttu-id="da1ac-196">Olá **Hosts** página lista todos os hosts no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="da1ac-197">hosts de toomanage, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-197">toomanage hosts, follow these steps.</span></span>

![página hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="da1ac-199">As ações de adicionar, encerrar e reativar um host não devem ser realizadas com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da1ac-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="da1ac-200">Selecione host Olá que você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="da1ac-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="da1ac-201">Saudação de uso **ações** ação de saudação do menu tooselect que você deseja tooperform:</span><span class="sxs-lookup"><span data-stu-id="da1ac-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="da1ac-202">**Iniciar todos os componentes** -iniciar todos os componentes no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="da1ac-203">**Parar todos os componentes** -parar todos os componentes no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="da1ac-204">**Reinicie todos os componentes** - parar e iniciar todos os componentes no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="da1ac-205">**Ativar o modo de manutenção** -suprime os alertas para o host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="da1ac-206">Esse modo deverá ser habilitado se você estiver realizando ações que geram alertas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="da1ac-207">Por exemplo, parar e iniciar um serviço.</span><span class="sxs-lookup"><span data-stu-id="da1ac-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="da1ac-208">**Desativar o modo de manutenção** -retorna Olá host toonormal alertas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="da1ac-209">**Parar** -DataNode para ou NodeManagers no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="da1ac-210">**Iniciar** -DataNode inicia ou NodeManagers no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="da1ac-211">**Reiniciar** -interrompe e inicia DataNode ou NodeManagers no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="da1ac-212">**Encerrar** -remove um host de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="da1ac-213">Não use esta ação em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da1ac-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="da1ac-214">**Recommission** -adiciona um cluster de toohello host encerrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da1ac-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="da1ac-215">Não use esta ação em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da1ac-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="da1ac-216"><a id="service"></a>Serviços</span><span class="sxs-lookup"><span data-stu-id="da1ac-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="da1ac-217">De saudação **painel** ou **serviços** página, use Olá **ações** botão final Olá Olá lista de serviços toostop e iniciar todos os serviços.</span><span class="sxs-lookup"><span data-stu-id="da1ac-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Ações de Serviço](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="da1ac-219">Enquanto **Adicionar serviço** está listado no menu, não deve ser cluster do HDInsight usado tooadd serviços toohello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="da1ac-220">Novos serviços devem ser adicionados usando uma Ação de Script durante o provisionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="da1ac-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="da1ac-221">Para saber mais sobre o uso de ações de script, consulte [Personalizar clusters HDInsight usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="da1ac-222">Durante a saudação **ações** botão poderá reiniciar todos os serviços, geralmente você deseja toostart, parar ou reiniciar um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="da1ac-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="da1ac-223">Use Olá ações de tooperform as etapas a seguir em um serviço individual:</span><span class="sxs-lookup"><span data-stu-id="da1ac-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="da1ac-224">De saudação **painel** ou **serviços** , selecione um serviço.</span><span class="sxs-lookup"><span data-stu-id="da1ac-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="da1ac-225">Da parte superior de saudação do hello **resumo** guia, use Olá **ações de serviço** botão e selecione Olá ação tootake.</span><span class="sxs-lookup"><span data-stu-id="da1ac-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="da1ac-226">Isso reinicia o serviço de saudação em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="da1ac-226">This restarts hello service on all nodes.</span></span>

    ![ação de serviço](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="da1ac-228">Reiniciar alguns serviços enquanto Olá cluster está em execução pode gerar alertas.</span><span class="sxs-lookup"><span data-stu-id="da1ac-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="da1ac-229">tooavoid alertas, você pode usar o hello **ações de serviço** botão tooenable **modo de manutenção** para serviço de saudação antes de executar a reinicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="da1ac-230">Quando uma ação tiver sido selecionada, Olá **op #** entrada na parte superior de saudação do hello tooshow de incrementos de página que está ocorrendo uma operação em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="da1ac-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="da1ac-231">Se configurado toodisplay, lista de saudação de operações em segundo plano é exibida.</span><span class="sxs-lookup"><span data-stu-id="da1ac-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="da1ac-232">Se você habilitou o **modo de manutenção** para serviço hello, lembre-se de toodisable usando Olá **ações de serviço** botão quando tiver terminado de operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="da1ac-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="da1ac-233">tooconfigure um serviço, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="da1ac-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="da1ac-234">De saudação **painel** ou **serviços** , selecione um serviço.</span><span class="sxs-lookup"><span data-stu-id="da1ac-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="da1ac-235">Selecione Olá **configurações** configuração atual de saudação de guia é exibida.</span><span class="sxs-lookup"><span data-stu-id="da1ac-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="da1ac-236">Uma lista das configurações anteriores também é exibida.</span><span class="sxs-lookup"><span data-stu-id="da1ac-236">A list of previous configurations is also displayed.</span></span>

    ![configurações](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="da1ac-238">Usar configuração de Olá Olá campos exibidos toomodify e, em seguida, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="da1ac-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="da1ac-239">Ou selecione uma configuração anterior e, em seguida, selecione **tornar atual** tooroll fazer configurações anteriores toohello.</span><span class="sxs-lookup"><span data-stu-id="da1ac-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="da1ac-240">Exibições do Ambari</span><span class="sxs-lookup"><span data-stu-id="da1ac-240">Ambari views</span></span>

<span data-ttu-id="da1ac-241">Modos de exibição do Ambari permitem que os desenvolvedores tooplug elementos de interface do usuário em Olá Ambari Web UI usando Olá [Ambari exibições Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="da1ac-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="da1ac-242">HDInsight fornece Olá exibições com tipos de cluster de Hadoop a seguir:</span><span class="sxs-lookup"><span data-stu-id="da1ac-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="da1ac-243">Gerenciador de filas de yarn: Gerenciador de filas de saudação fornece uma interface do usuário simple para exibir e modificar as filas do YARN.</span><span class="sxs-lookup"><span data-stu-id="da1ac-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="da1ac-244">Exibição de hive: Olá Hive exibição permite consultas de Hive toorun diretamente do seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="da1ac-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="da1ac-245">Salvar consultas, exibir os resultados, salvar os resultados do armazenamento de cluster toohello ou baixar o sistema local do tooyour de resultados.</span><span class="sxs-lookup"><span data-stu-id="da1ac-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="da1ac-246">Para obter mais informações sobre como usar Exibições do Hive, consulte [Usar Exibições do Hive com o HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="da1ac-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="da1ac-247">Exibição Tez: Olá Tez exibição permite que você toobetter entender e otimizar os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="da1ac-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="da1ac-248">Você pode exibir informações sobre como os trabalhos do Tez são executados e quais recursos são usados.</span><span class="sxs-lookup"><span data-stu-id="da1ac-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
