---
title: "Instalar o RStudio com o R Server no HDInsight – Azure | Microsoft Docs"
description: Como instalar o RStudio com o Servidor R no HDInsight.
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
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="c57a5-103">Instalar o RStudio com o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c57a5-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="c57a5-104">Este artigo descreve como instalar a versão de comunidade (gratuita) do [RStudio Server](https://www.rstudio.com/products/rstudio-server/) no nó de borda de um cluster usando um script personalizado.</span><span class="sxs-lookup"><span data-stu-id="c57a5-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="c57a5-105">O RStudio Server que fornece um IDE baseado em navegador para uso por clientes remotos e é amplamente usado em Linux.</span><span class="sxs-lookup"><span data-stu-id="c57a5-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="c57a5-106">Há vários ambientes de desenvolvimento integrado (IDEs) disponíveis para R hoje em dia, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c57a5-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="c57a5-107">RTVS ([Ferramentas do R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)) da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c57a5-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="c57a5-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="c57a5-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="c57a5-109">[StatET](http://www.walware.de/goto/statet) baseado no Eclipse da Walware.</span><span class="sxs-lookup"><span data-stu-id="c57a5-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="c57a5-110">A vantagem de instalar o RStudio Server no nó de borda de um cluster HDInsight é que ele proporciona uma experiência completa de IDE para o desenvolvimento e a execução de scripts R com o R Server no cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="c57a5-111">Essa configuração pode ser consideravelmente mais produtiva do que o uso padrão do Console R.</span><span class="sxs-lookup"><span data-stu-id="c57a5-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="c57a5-112">O procedimento descrito neste artigo só será relevante se você não tiver selecionado a instalação da edição de comunidade do RStudio Server ao provisionar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="c57a5-113">Se ele tiver sido adicionado durante o provisionamento, acesse-o clicando no bloco **Painéis do R Server** na entrada do Portal do Azure de seu cluster e, em seguida, no bloco **R Studio Server**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="c57a5-114">Se preferir usar a versão Pro licenciada comercialmente do RStudio Server, você deverá seguir as instruções de instalação do [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="c57a5-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="c57a5-115">Se você estiver usando um cluster HDInsight em que o R foi instalado usando [Instalar a Ação de Script R](hdinsight-hadoop-r-scripts-linux.md), as etapas neste documento não funcionarão corretamente, pois elas exigem um R Server no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c57a5-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="c57a5-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c57a5-116">Prerequisites</span></span>

* <span data-ttu-id="c57a5-117">Um cluster Azure HDInsight com R Server instalado.</span><span class="sxs-lookup"><span data-stu-id="c57a5-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="c57a5-118">Para obter instruções, confira [Introdução ao Servidor R nos clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c57a5-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="c57a5-119">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c57a5-119">An SSH client.</span></span> <span data-ttu-id="c57a5-120">Para distribuições Linux e Unix ou o Macintosh OS X, o comando `ssh` é fornecido com o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="c57a5-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="c57a5-121">Para o Windows, recomendamos [Cygwin](http://www.redhat.com/services/custom/cygwin/) com a [opção OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU) ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="c57a5-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="c57a5-122">Instalar o RStudio no cluster usando um script personalizado</span><span class="sxs-lookup"><span data-stu-id="c57a5-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="c57a5-123">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c57a5-123">Here are the steps:</span></span>

1. <span data-ttu-id="c57a5-124">Identifique o nó de borda do cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="c57a5-125">Para um cluster HDInsight com R Server, esta é a convenção de nomenclatura para o nó principal e o nó de borda:</span><span class="sxs-lookup"><span data-stu-id="c57a5-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="c57a5-126">Nó principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="c57a5-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="c57a5-127">Nó de borda `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="c57a5-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="c57a5-128">SSH no nó de borda do cluster usando o padrão de nomenclatura fornecido na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="c57a5-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="c57a5-129">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c57a5-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c57a5-130">Quando você estiver conectado, torne-se um usuário raiz no cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="c57a5-131">Na sessão do SSH, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c57a5-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="c57a5-132">Baixe o script personalizado para instalar o RStudio.</span><span class="sxs-lookup"><span data-stu-id="c57a5-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="c57a5-133">Use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c57a5-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="c57a5-134">Altere as permissões no arquivo de script personalizado e execute o script.</span><span class="sxs-lookup"><span data-stu-id="c57a5-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="c57a5-135">Use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c57a5-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="c57a5-136">Se você usou uma senha do SSH ao criar um cluster HDInsight com o R Server, pode ignorar esta etapa e ir para a próxima.</span><span class="sxs-lookup"><span data-stu-id="c57a5-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="c57a5-137">Se, em vez disso, você usou uma chave do SSH para criar o cluster, você deve definir uma senha para seu usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="c57a5-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="c57a5-138">Você precisa dessa senha ao se conectar ao RStudio.</span><span class="sxs-lookup"><span data-stu-id="c57a5-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="c57a5-139">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c57a5-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="c57a5-140">Quando a **Senha atual do Kerberos** for solicitada, pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="c57a5-141">Observe que você deve substituir `USERNAME` por um usuário SSH de seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c57a5-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="c57a5-142">Se sua senha tiver sido definida com êxito, você deverá ver a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="c57a5-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="c57a5-143">Saia da sessão do SSH.</span><span class="sxs-lookup"><span data-stu-id="c57a5-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="c57a5-144">Crie um túnel SSH para o cluster, mapeando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` no cluster HDInsight para o computador cliente.</span><span class="sxs-lookup"><span data-stu-id="c57a5-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="c57a5-145">Você deve criar um túnel SSH antes de abrir uma nova sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="c57a5-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="c57a5-146">Em um cliente Linux ou um cliente Windows com [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra uma sessão de terminal e use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c57a5-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="c57a5-147">Substitua **USERNAME** por um usuário SSH para seu cluster HDInsight e substitua **CLUSTERNAME** pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c57a5-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="c57a5-148">Você também pode usar uma chave SSH em vez de uma senha adicionando `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="c57a5-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="c57a5-149">Se estiver usar um cliente do Windows com PuTTY</span><span class="sxs-lookup"><span data-stu-id="c57a5-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="c57a5-150">Abra o PuTTY e insira as informações da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="c57a5-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="c57a5-151">Na seção **Categoria** à esquerda da caixa de diálogo, expanda **Conexão**, expanda **SSH** e selecione **Túneis**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="c57a5-152">Forneça as seguintes informações no formulário **Opções de controle do encaminhamento de porta SSH** :</span><span class="sxs-lookup"><span data-stu-id="c57a5-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="c57a5-153">**Porta de Origem** : a porta no cliente que você deseja encaminhar.</span><span class="sxs-lookup"><span data-stu-id="c57a5-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="c57a5-154">Por exemplo, **8787**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-154">For example, **8787**.</span></span>
        * <span data-ttu-id="c57a5-155">**Destino** – o destino que deve ser mapeado para o computador cliente local.</span><span class="sxs-lookup"><span data-stu-id="c57a5-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="c57a5-156">Por exemplo, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="c57a5-157">![Criar um túnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Criar um túnel SSH")</span><span class="sxs-lookup"><span data-stu-id="c57a5-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="c57a5-158">Clique em **Adicionar** para adicionar as configurações e clique em **Abrir** para abrir uma conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="c57a5-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="c57a5-159">Quando solicitado, faça logon no servidor para estabelecer uma sessão SSH e habilitar o túnel.</span><span class="sxs-lookup"><span data-stu-id="c57a5-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="c57a5-160">Abra um navegador da Web e digite a URL a seguir com base na porta que você inseriu para o túnel:</span><span class="sxs-lookup"><span data-stu-id="c57a5-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="c57a5-161">Será solicitado que você insira o nome de usuário e a senha do SSH para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="c57a5-162">Se você usou uma chave SSH ao criar o cluster, deverá inserir a senha criada na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="c57a5-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="c57a5-163">![Conectar-se ao Studio R](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Criar um túnel SSH")</span><span class="sxs-lookup"><span data-stu-id="c57a5-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="c57a5-164">Para testar se a instalação do RStudio foi bem-sucedida, você pode executar um script de teste que execute trabalhos do MapReduce e do Spark baseados em R no cluster.</span><span class="sxs-lookup"><span data-stu-id="c57a5-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="c57a5-165">Para baixar o script de teste a ser executado no RStudio, volte para o console do SSH e insira os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c57a5-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="c57a5-166">Se você criou um cluster Hadoop com R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="c57a5-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="c57a5-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="c57a5-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="c57a5-168">Se você criou um cluster Spark com R, use este comando:</span><span class="sxs-lookup"><span data-stu-id="c57a5-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="c57a5-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="c57a5-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="c57a5-170">No RStudio, você verá o script de teste que você baixou.</span><span class="sxs-lookup"><span data-stu-id="c57a5-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="c57a5-171">Clique duas vezes no arquivo para abri-lo, selecione o conteúdo e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="c57a5-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="c57a5-172">Você deverá ver a saída no painel **Console**:</span><span class="sxs-lookup"><span data-stu-id="c57a5-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="c57a5-173">![Testar a instalação](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Testar a instalação")</span><span class="sxs-lookup"><span data-stu-id="c57a5-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="c57a5-174">Outra opção seria digitar `source(testhdi.r)` ou `source(testhdi_spark.r)` para executar o script.</span><span class="sxs-lookup"><span data-stu-id="c57a5-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="c57a5-175">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c57a5-175">See also</span></span>

* [<span data-ttu-id="c57a5-176">Opções de contexto de computação para o R Server em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="c57a5-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="c57a5-177">Opções de Armazenamento do Azure para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c57a5-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

