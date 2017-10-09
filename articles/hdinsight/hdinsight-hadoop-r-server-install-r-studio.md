---
title: aaaInstall RStudio ao servidor do R no HDInsight - Azure | Microsoft Docs
description: Como tooinstall RStudio com o servidor do R no HDInsight.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="38c21-103">Instalar o RStudio com o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="38c21-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="38c21-104">Este artigo descreve como tooinstall Olá versão (gratuita) da comunidade do [RStudio Server](https://www.rstudio.com/products/rstudio-server/) no nó de borda de saudação de um cluster usando um script personalizado.</span><span class="sxs-lookup"><span data-stu-id="38c21-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="38c21-105">O RStudio Server que fornece um IDE baseado em navegador para uso por clientes remotos e é amplamente usado em Linux.</span><span class="sxs-lookup"><span data-stu-id="38c21-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="38c21-106">Há vários ambientes de desenvolvimento integrado (IDEs) disponíveis para R hoje em dia, incluindo:</span><span class="sxs-lookup"><span data-stu-id="38c21-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="38c21-107">RTVS ([Ferramentas do R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)) da Microsoft</span><span class="sxs-lookup"><span data-stu-id="38c21-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="38c21-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="38c21-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="38c21-109">[StatET](http://www.walware.de/goto/statet) baseado no Eclipse da Walware.</span><span class="sxs-lookup"><span data-stu-id="38c21-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="38c21-110">vantagem de saudação da instalação RStudio Server no nó de borda de saudação de um cluster HDInsight é que ele fornece uma experiência completa do IDE para o desenvolvimento de saudação e execução de scripts de R com R Server no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="38c21-111">Essa configuração pode ser consideravelmente mais produtiva do que o uso do padrão de saudação Console de R.</span><span class="sxs-lookup"><span data-stu-id="38c21-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="38c21-112">procedimento Olá descrito neste artigo só será relevante se você não selecionou tooinstall edição do servidor RStudio community ao provisionar o cluster.</span><span class="sxs-lookup"><span data-stu-id="38c21-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="38c21-113">Se ele foi adicionado durante o provisionamento, então tooaccess-você pode clicar em Olá **R Server painéis** lado a lado no hello entrada de portal do Azure para seu cluster, em seguida, no hello **R Studio Server** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="38c21-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="38c21-114">Se você preferir toouse Olá comercialmente licenciado Pro versão do servidor de RStudio, você deve seguir instruções de instalação de saudação do [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="38c21-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="38c21-115">Se você estiver usando um cluster de HDInsight para o qual R foi instalado usando Olá [ação de Script de instalação do R](hdinsight-hadoop-r-scripts-linux.md), Olá etapas neste documento não funcionarão corretamente precisam de um servidor de R no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="38c21-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38c21-116">Prerequisites</span></span>

* <span data-ttu-id="38c21-117">Um cluster Azure HDInsight com R Server instalado.</span><span class="sxs-lookup"><span data-stu-id="38c21-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="38c21-118">Para obter instruções, confira [Introdução ao Servidor R nos clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="38c21-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="38c21-119">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="38c21-119">An SSH client.</span></span> <span data-ttu-id="38c21-120">Para distribuições do Linux e Unix ou Macintosh OS X, Olá `ssh` comando é fornecido com o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="38c21-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="38c21-121">Para Windows, é recomendável [Cygwin](http://www.redhat.com/services/custom/cygwin/) com hello [opção OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="38c21-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="38c21-122">Instalar o RStudio em cluster hello usando um script personalizado</span><span class="sxs-lookup"><span data-stu-id="38c21-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="38c21-123">Aqui estão as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="38c21-123">Here are hello steps:</span></span>

1. <span data-ttu-id="38c21-124">Identificar o nó de borda de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="38c21-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="38c21-125">Para um cluster de HDInsight com R Server, a seguir está a convenção de nomenclatura de Olá para o nó principal e borda.</span><span class="sxs-lookup"><span data-stu-id="38c21-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="38c21-126">Nó principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="38c21-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="38c21-127">Nó de borda `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="38c21-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="38c21-128">SSH no nó de borda de saudação do cluster de saudação usando o padrão de nomenclatura Olá fornecido na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="38c21-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="38c21-129">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="38c21-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="38c21-130">Quando você estiver conectado, se tornar um usuário raiz no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="38c21-131">Na sessão SSH hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="38c21-132">Baixe Olá script personalizado tooinstall RStudio.</span><span class="sxs-lookup"><span data-stu-id="38c21-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="38c21-133">Use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="38c21-134">Alterar permissões de saudação no arquivo de script personalizado hello e executar o script hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="38c21-135">Use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="38c21-136">Se você usou uma senha SSH durante a criação de um cluster HDInsight com R Server, você pode ignorar esta etapa e continuar toohello lado.</span><span class="sxs-lookup"><span data-stu-id="38c21-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="38c21-137">Se você usou uma chave SSH em vez disso, cluster de saudação toocreate, você deve definir uma senha para o usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="38c21-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="38c21-138">Essa senha é necessária ao conectar-se tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="38c21-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="38c21-139">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="38c21-140">Quando a **Senha atual do Kerberos** for solicitada, pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="38c21-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="38c21-141">Observe que você deve substituir `USERNAME` por um usuário SSH de seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38c21-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="38c21-142">Se sua senha é definida com êxito, você verá a seguinte mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="38c21-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="38c21-143">Sair da sessão SSH hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="38c21-144">Criar um cluster de toohello de túnel SSH mapeando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` no hello HDInsight cluster toohello máquina do cliente.</span><span class="sxs-lookup"><span data-stu-id="38c21-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="38c21-145">Você deve criar um túnel SSH antes de abrir uma nova sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="38c21-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="38c21-146">Em um cliente Linux ou um cliente do Windows com [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra uma sessão do terminal e usar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="38c21-147">Substituir **USERNAME** com um usuário SSH para o cluster HDInsight e substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38c21-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="38c21-148">Você também pode usar uma chave SSH em vez de uma senha adicionando `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="38c21-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="38c21-149">Se estiver usar um cliente do Windows com PuTTY</span><span class="sxs-lookup"><span data-stu-id="38c21-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="38c21-150">Abra o PuTTY e insira as informações da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="38c21-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="38c21-151">Em Olá **categoria** toohello seção à esquerda da caixa de diálogo hello, expanda **Conexão**, expanda **SSH**e, em seguida, selecione **túneis**.</span><span class="sxs-lookup"><span data-stu-id="38c21-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="38c21-152">Fornecer Olá seguintes informações sobre Olá **encaminhamento de porta de opções que controlam o SSH** formulário:</span><span class="sxs-lookup"><span data-stu-id="38c21-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="38c21-153">**Porta de origem** -Olá porta em que você deseja tooforward de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="38c21-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="38c21-154">Por exemplo, **8787**.</span><span class="sxs-lookup"><span data-stu-id="38c21-154">For example, **8787**.</span></span>
        * <span data-ttu-id="38c21-155">**Destino** - Olá destino deve ser mapeado toohello máquina de cliente local.</span><span class="sxs-lookup"><span data-stu-id="38c21-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="38c21-156">Por exemplo, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="38c21-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="38c21-157">![Criar um túnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Criar um túnel SSH")</span><span class="sxs-lookup"><span data-stu-id="38c21-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="38c21-158">Clique em **adicionar** tooadd Olá configurações e, em seguida, clique em **abrir** tooopen uma conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="38c21-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="38c21-159">Quando solicitado, faça logon no toohello servidor tooestablish um túnel de saudação de sessão e enable SSH.</span><span class="sxs-lookup"><span data-stu-id="38c21-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="38c21-160">Abra um navegador da web e digite Olá com base na porta Olá inserido para o túnel de saudação de URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="38c21-161">Você é solicitado tooenter Olá SSH username e password tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="38c21-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="38c21-162">Se você usou uma chave SSH durante a criação de cluster hello, você deverá inserir a senha de saudação criado na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="38c21-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="38c21-163">![Conecte-se tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "criar um túnel SSH")</span><span class="sxs-lookup"><span data-stu-id="38c21-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="38c21-164">tootest se Olá RStudio instalação foi bem-sucedida, você pode executar um script de teste que executa trabalhos de MapReduce e Spark R no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38c21-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="38c21-165">toodownload Olá teste script toorun em RStudio, volte toohello SSH console e digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="38c21-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="38c21-166">Se você criou um cluster Hadoop com R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="38c21-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="38c21-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="38c21-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="38c21-168">Se você criou um cluster Spark com R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="38c21-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="38c21-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="38c21-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="38c21-170">RStudio, você verá Olá testar o script baixado.</span><span class="sxs-lookup"><span data-stu-id="38c21-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="38c21-171">Clique duas vezes em Olá tooopen de arquivo, selecione o conteúdo do arquivo hello hello e, em seguida, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="38c21-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="38c21-172">Você deve ver a saída Olá Olá **Console** painel:</span><span class="sxs-lookup"><span data-stu-id="38c21-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="38c21-173">![Testar a instalação do hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "testar a instalação de saudação")</span><span class="sxs-lookup"><span data-stu-id="38c21-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="38c21-174">Outra opção seria tootype `source(testhdi.r)` ou `source(testhdi_spark.r)` tooexecute script de saudação.</span><span class="sxs-lookup"><span data-stu-id="38c21-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="38c21-175">Consulte também</span><span class="sxs-lookup"><span data-stu-id="38c21-175">See also</span></span>

* [<span data-ttu-id="38c21-176">Opções de contexto de computação para o R Server em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="38c21-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="38c21-177">Opções de Armazenamento do Azure para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="38c21-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

