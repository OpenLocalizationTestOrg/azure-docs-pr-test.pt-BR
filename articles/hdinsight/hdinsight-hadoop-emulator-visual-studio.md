---
title: "ferramentas de aaaData Lake para Visual Studio com a área restrita do Hortonworks - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse Olá ferramentas do Azure Data Lake para Visual Studio com a área restrita de Hortonworks Olá executados em uma VM local. Com essas ferramentas, você pode criar e executar trabalhos de Hive e Pig em área restrita Olá e exibir saída de trabalho e o histórico."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="33420-104">Usar ferramentas do Azure Data Lake Olá para o Visual Studio com Olá Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="33420-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="33420-105">O Azure Data Lake inclui ferramentas para trabalhar com clusters Hadoop genéricos.</span><span class="sxs-lookup"><span data-stu-id="33420-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="33420-106">Este documento fornece as etapas de saudação necessárias ferramentas de Data Lake toouse Olá com hello Hortonworks Sandbox em execução em uma máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="33420-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="33420-107">Olá Hortonworks Sandbox permite que você toowork com Hadoop localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="33420-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="33420-108">Depois de desenvolver uma solução e deseja toodeploy-la em grande escala, em seguida, você pode mover o cluster do HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="33420-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33420-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33420-109">Prerequisites</span></span>

* <span data-ttu-id="33420-110">Olá Hortonworks área restrita, em execução em uma máquina virtual em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="33420-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="33420-111">Este documento foi gravado e testado com a área restrita de saudação executando em Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="33420-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="33420-112">Para obter informações sobre a configuração de proteção hello, consulte Olá [começar com a área restrita do hello Hortonworks.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="33420-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="33420-113">.</span><span class="sxs-lookup"><span data-stu-id="33420-113">document.</span></span>

* <span data-ttu-id="33420-114">Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (qualquer edição).</span><span class="sxs-lookup"><span data-stu-id="33420-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="33420-115">Olá [SDK do Azure para .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="33420-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="33420-116">Olá [Azure Data Lake ferramentas para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="33420-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="33420-117">Configurar senhas para a área restrita de saudação</span><span class="sxs-lookup"><span data-stu-id="33420-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="33420-118">Certifique-se de que Olá que hortonworks Sandbox está em execução.</span><span class="sxs-lookup"><span data-stu-id="33420-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="33420-119">Siga as etapas de Olá Olá [começar a saudação Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento.</span><span class="sxs-lookup"><span data-stu-id="33420-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="33420-120">Essas etapas configuram senha Olá Olá SSH `root` conta e Olá Ambari `admin` conta.</span><span class="sxs-lookup"><span data-stu-id="33420-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="33420-121">Essas senhas são usadas quando você se conectar toohello sandbox do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33420-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="33420-122">Conecte-se a área restrita do hello ferramentas toohello</span><span class="sxs-lookup"><span data-stu-id="33420-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="33420-123">Abra o Visual Studio e selecione **Exibir**, **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="33420-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="33420-124">De **Server Explorer**, Olá do botão direito do mouse **HDInsight** entrada e, em seguida, selecione **conectar tooHDInsight emulador**.</span><span class="sxs-lookup"><span data-stu-id="33420-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Captura de tela do Gerenciador de servidores, com tooHDInsight conectar emulador realçado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="33420-126">De saudação **conectar tooHDInsight emulador** caixa de diálogo, digite a senha de saudação que você configurou para Ambari.</span><span class="sxs-lookup"><span data-stu-id="33420-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Captura de tela da caixa de diálogo, com a caixa de texto de senha realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="33420-128">Selecione **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="33420-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="33420-129">Saudação de uso **senha** senha de saudação do campo tooenter configurados para hello `root` conta.</span><span class="sxs-lookup"><span data-stu-id="33420-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="33420-130">Deixe Olá outros campos com valor de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-130">Leave hello other fields at hello default value.</span></span>

    ![Captura de tela da caixa de diálogo, com a caixa de texto de senha realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="33420-132">Selecione **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="33420-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="33420-133">Espera para validação de saudação toofinish de serviços.</span><span class="sxs-lookup"><span data-stu-id="33420-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="33420-134">Em alguns casos, a validação pode falhar e solicitará que você tooupdate configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="33420-135">Se a validação falhar, selecione **atualização**e aguarde a configuração hello e verificação de saudação toofinish de serviço.</span><span class="sxs-lookup"><span data-stu-id="33420-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Captura de tela da caixa de diálogo, com o botão Atualizar realçado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="33420-137">o processo de atualização Olá usa Ambari toomodify Olá Hortonworks Sandbox configuração toowhat esperada por ferramentas de Data Lake Olá para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33420-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="33420-138">Depois que a validação foi concluída, selecione **concluir** toocomplete configuração.</span><span class="sxs-lookup"><span data-stu-id="33420-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="33420-139">![Captura de tela da caixa de diálogo, com o botão Concluir realçado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="33420-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="33420-140">Dependendo da velocidade da saudação do seu ambiente de desenvolvimento e Olá quantidade de memória alocada a máquina virtual de toohello, tirar tooconfigure de vários minutos e validar serviços hello.</span><span class="sxs-lookup"><span data-stu-id="33420-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="33420-141">Depois de seguir essas etapas, você agora tem um **cluster local do HDInsight** entrada no Gerenciador de servidores, sob Olá **HDInsight** seção.</span><span class="sxs-lookup"><span data-stu-id="33420-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="33420-142">Escrever uma consulta do Hive</span><span class="sxs-lookup"><span data-stu-id="33420-142">Write a Hive query</span></span>

<span data-ttu-id="33420-143">O Hive fornece uma linguagem de consulta do tipo SQL (HiveQL) para trabalhar com os dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="33420-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="33420-144">As etapas a seguir de saudação do uso toolearn como toorun sob demanda consultas no cluster local hello.</span><span class="sxs-lookup"><span data-stu-id="33420-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="33420-145">Em **Server Explorer**, entrada Olá para o cluster local de saudação que você adicionou anteriormente e, em seguida, selecione **escrever uma consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="33420-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Captura de tela do Gerenciador de Servidores, com a opção Escrever uma Consulta do Hive realçada](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="33420-147">Uma nova janela de consulta é exibida.</span><span class="sxs-lookup"><span data-stu-id="33420-147">A new query window appears.</span></span> <span data-ttu-id="33420-148">Aqui, você pode rapidamente escrever e enviar um cluster local do toohello de consulta.</span><span class="sxs-lookup"><span data-stu-id="33420-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="33420-149">Na nova janela de consulta hello, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="33420-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="33420-150">consulta de saudação toorun, selecione **enviar** na parte superior de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="33420-151">Deixe os outros valores hello (**lote** e o nome do servidor) com valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Captura de tela da janela de consulta, com o botão de envio Olá realçado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="33420-153">Você também pode usar menu suspenso de saudação Avançar muito**enviar** tooselect **avançado**.</span><span class="sxs-lookup"><span data-stu-id="33420-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="33420-154">Opções avançadas permitem opções adicionais de tooprovide ao enviar trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="33420-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Captura de tela da caixa de diálogo Enviar Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="33420-156">Depois que você enviar consulta hello, status do trabalho Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="33420-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="33420-157">status do trabalho Olá exibe informações sobre o trabalho Olá conforme ela é processada pelo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33420-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="33420-158">**Estado do trabalho** fornece o status de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="33420-159">estado de saudação é atualizado periodicamente, ou você pode usar o hello atualizar ícone toorefresh Olá estado manualmente.</span><span class="sxs-lookup"><span data-stu-id="33420-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Captura de tela da caixa de diálogo Exibir Trabalho, com o Estado do Trabalho realçado](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="33420-161">Depois de saudação **estado do trabalho** muda muito**concluído**, um direcionado acíclico Graph (DAG) é exibido.</span><span class="sxs-lookup"><span data-stu-id="33420-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="33420-162">Este diagrama descreve o caminho de execução de saudação foi determinado por Tez durante o processamento de consulta de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="33420-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="33420-163">Tez é o mecanismo de execução de padrão Olá para o Hive no cluster local hello.</span><span class="sxs-lookup"><span data-stu-id="33420-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="33420-164">Tez também é o padrão de hello quando você estiver usando clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="33420-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="33420-165">Não é padrão Olá no HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="33420-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="33420-166">toouse-lo, você deve adicionar a linha hello `set hive.execution.engine = tez;` toohello a partir de sua consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="33420-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="33420-167">Saudação de uso **saída de trabalho** vincular a saída de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="33420-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="33420-168">Nesse caso, é 823, número de saudação de linhas na tabela de sample_08 hello.</span><span class="sxs-lookup"><span data-stu-id="33420-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="33420-169">Você pode exibir informações de diagnóstico sobre o trabalho de saudação usando Olá **Log trabalho** e **baixar YARN Log** links.</span><span class="sxs-lookup"><span data-stu-id="33420-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="33420-170">Você também pode executar trabalhos de Hive interativamente alterando Olá **lote** campo muito**interativo**.</span><span class="sxs-lookup"><span data-stu-id="33420-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="33420-171">Em seguida, selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="33420-171">Then select **Execute**.</span></span>

    ![Captura de tela dos botões Interativo e Executar realçados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="33420-173">Uma consulta interativa fluxos Olá log de saída gerado durante o processamento toohello **HiveServer2 saída** janela.</span><span class="sxs-lookup"><span data-stu-id="33420-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="33420-174">Hello informações é Olá mesmo que está disponível no hello **Log trabalho** link depois que um trabalho foi concluído.</span><span class="sxs-lookup"><span data-stu-id="33420-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Captura de tela do log de saída](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="33420-176">Criar um projeto do Hive</span><span class="sxs-lookup"><span data-stu-id="33420-176">Create a Hive project</span></span>

<span data-ttu-id="33420-177">Você também pode criar um projeto que contém vários scripts do Hive.</span><span class="sxs-lookup"><span data-stu-id="33420-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="33420-178">Use um projeto quando você tiver scripts relacionados ou toostore scripts em um sistema de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="33420-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="33420-179">No Visual Studio, selecione **Arquivo**, **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="33420-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="33420-180">Na lista de saudação de projetos, expanda **modelos**, expanda **Azure Data Lake**e, em seguida, selecione **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="33420-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="33420-181">Saudação de modelos, selecione lista **Hive exemplo**.</span><span class="sxs-lookup"><span data-stu-id="33420-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="33420-182">Insira um nome e um local e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="33420-182">Enter a name and location, and then select **OK**.</span></span>

    ![Captura de tela da janela Novo Projeto com Azure Data Lake, HIVE, Amostra do Hive e OK realçados](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="33420-184">Olá **exemplo Hive** projeto contém dois scripts, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="33420-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="33420-185">Você pode enviar esses scripts usando Olá mesmo **enviar** botão na parte superior de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="33420-186">Criar um projeto Pig</span><span class="sxs-lookup"><span data-stu-id="33420-186">Create a Pig project</span></span>

<span data-ttu-id="33420-187">Enquanto o Hive fornece uma linguagem semelhante ao SQL para trabalhar com os dados estruturados, o Pig funciona executando transformações nos dados.</span><span class="sxs-lookup"><span data-stu-id="33420-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="33420-188">Pig fornece uma linguagem (Pig latino) que permite a você toodevelop um pipeline de transformações.</span><span class="sxs-lookup"><span data-stu-id="33420-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="33420-189">toouse Pig com o cluster local do hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="33420-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="33420-190">Abra o Visual Studio, selecione **Arquivo**, **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="33420-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="33420-191">Na lista de saudação de projetos, expanda **modelos**, expanda **Azure Data Lake**e, em seguida, selecione **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="33420-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="33420-192">Saudação de modelos, selecione lista **Pig aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="33420-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="33420-193">Insira um nome e local e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="33420-193">Enter a name, location, and then select **OK**.</span></span>

    ![Captura de tela da janela Novo Projeto com Azure Data Lake, Pig, Aplicativo Pig e OK realçados](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="33420-195">Digite hello depois do texto como conteúdo de saudação do hello **script.pig** arquivo que foi criado com este projeto.</span><span class="sxs-lookup"><span data-stu-id="33420-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="33420-196">Enquanto Pig usa uma linguagem diferente de Hive, como executar trabalhos de saudação é consistente entre os dois idiomas, por meio de saudação **enviar** botão.</span><span class="sxs-lookup"><span data-stu-id="33420-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="33420-197">Olá selecionando lista suspensa ao lado de **enviar** exibe uma caixa de diálogo de envio avançados de Pig.</span><span class="sxs-lookup"><span data-stu-id="33420-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Captura de tela da caixa de diálogo Enviar Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="33420-199">Olá status do trabalho e de saída também é exibida, Olá mesmo como uma consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="33420-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Captura de tela de um trabalho de Pig concluído](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="33420-201">Exibir trabalhos</span><span class="sxs-lookup"><span data-stu-id="33420-201">View jobs</span></span>

<span data-ttu-id="33420-202">Data Lake ferramentas também permitem que você tooeasily exibir informações sobre os trabalhos que foram executados no Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33420-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="33420-203">Use Olá etapas toosee Olá os trabalhos que foram executados no cluster local Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="33420-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="33420-204">De **Server Explorer**, cluster local hello e, em seguida, selecione **Exibir trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="33420-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="33420-205">Uma lista de trabalhos que foram enviados toohello cluster é exibida.</span><span class="sxs-lookup"><span data-stu-id="33420-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Captura de tela do Gerenciador de Servidores, com a opção Exibir Trabalhos realçada](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="33420-207">Na lista de saudação de trabalhos, selecione um detalhes do trabalho Olá tooview.</span><span class="sxs-lookup"><span data-stu-id="33420-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Captura de tela de trabalho de navegador, com um dos trabalhos de saudação realçados](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="33420-209">informações de saudação exibidas são semelhante toowhat que consulte após executar uma consulta de Hive ou Pig, incluindo links tooview Olá saída e informações de log.</span><span class="sxs-lookup"><span data-stu-id="33420-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="33420-210">Você também pode modificar e envie novamente o trabalho de saudação aqui.</span><span class="sxs-lookup"><span data-stu-id="33420-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="33420-211">Exibir bancos de dados do Hive</span><span class="sxs-lookup"><span data-stu-id="33420-211">View Hive databases</span></span>

1. <span data-ttu-id="33420-212">Em **Server Explorer**, expanda Olá **cluster local do HDInsight** entrada e, em seguida, expanda **bancos de dados de Hive**.</span><span class="sxs-lookup"><span data-stu-id="33420-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="33420-213">Olá **padrão** e **xademo** bancos de dados no cluster local Olá são exibidos.</span><span class="sxs-lookup"><span data-stu-id="33420-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="33420-214">Expandir um banco de dados mostra tabelas Olá no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Captura de tela do Gerenciador de Servidores, com os bancos de dados realçados](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="33420-216">Expandindo uma tabela exibe colunas Olá para aquela tabela.</span><span class="sxs-lookup"><span data-stu-id="33420-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="33420-217">dados de saudação do modo de exibição tooquickly, uma tabela e selecione **exibição Top 100 linhas**.</span><span class="sxs-lookup"><span data-stu-id="33420-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Captura de tela do Gerenciador de Servidores, com a tabela expandida e a opção Exibir as 100 Primeiras Linhas selecionada](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="33420-219">Propriedades do banco de dados e da tabela</span><span class="sxs-lookup"><span data-stu-id="33420-219">Database and table properties</span></span>

<span data-ttu-id="33420-220">Você pode exibir as propriedades de saudação de um banco de dados ou tabela.</span><span class="sxs-lookup"><span data-stu-id="33420-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="33420-221">Selecionando **propriedades** exibe detalhes de item de saudação selecionada na janela de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="33420-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="33420-222">Por exemplo, consulte informações Olá Olá captura de tela a seguir mostradas:</span><span class="sxs-lookup"><span data-stu-id="33420-222">For example, see hello information shown in hello following screenshot:</span></span>

![Captura de tela da janela Propriedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="33420-224">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="33420-224">Create a table</span></span>

<span data-ttu-id="33420-225">toocreate uma tabela, um banco de dados e, em seguida, selecione **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="33420-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Captura de tela do Gerenciador de Servidores, com a opção Criar Tabela realçada](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="33420-227">Você pode criar tabela hello usando um formulário.</span><span class="sxs-lookup"><span data-stu-id="33420-227">You can then create hello table using a form.</span></span> <span data-ttu-id="33420-228">Na parte inferior de saudação do hello captura de tela a seguir, você pode ver Olá HiveQL bruto que é usado toocreate Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="33420-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Captura de tela de formulário Olá usado toocreate uma tabela](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="33420-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33420-230">Next steps</span></span>

* [<span data-ttu-id="33420-231">Aprendizado ropes de saudação do hello Hortonworks seguro</span><span class="sxs-lookup"><span data-stu-id="33420-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="33420-232">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="33420-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
