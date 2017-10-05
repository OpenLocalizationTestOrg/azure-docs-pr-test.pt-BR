---
title: "Usar o túnel SSH para acessar o Azure HDInsight | Microsoft Docs"
description: "Saiba como usar um túnel SSH para navegar com segurança em recursos da Web hospedados em seus nós HDInsight baseados em Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="1367f-103">Usar o Túnel SSH para acessar a interface do usuário do Ambari na Web, JobHistory, NameNode, Oozie, entre outras</span><span class="sxs-lookup"><span data-stu-id="1367f-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="1367f-104">Os clusters do HDInsight baseados em Linux oferecem acesso à interface do usuário do Ambari Web pela Internet, mas alguns recursos da interface do usuário não são acessados.</span><span class="sxs-lookup"><span data-stu-id="1367f-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="1367f-105">Por exemplo, a interface do usuário da Web para outros serviços exibidos por meio do Ambari.</span><span class="sxs-lookup"><span data-stu-id="1367f-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="1367f-106">Para obter a funcionalidade completa da interface do usuário do Ambari Web, você deverá usar um túnel SSH para o início do cluster.</span><span class="sxs-lookup"><span data-stu-id="1367f-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="1367f-107">Por que usar um túnel SSH</span><span class="sxs-lookup"><span data-stu-id="1367f-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="1367f-108">Vários menus no Ambari só funcionam por meio de um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="1367f-109">Esses menus dependem de sites e serviços em execução em outros tipos de nó, como nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1367f-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="1367f-110">Geralmente, esses sites não são protegidos e, portanto, não é seguro expô-los diretamente na Internet.</span><span class="sxs-lookup"><span data-stu-id="1367f-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="1367f-111">As seguintes interfaces do usuário da Web exigem um túnel SSH:</span><span class="sxs-lookup"><span data-stu-id="1367f-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="1367f-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="1367f-112">JobHistory</span></span>
* <span data-ttu-id="1367f-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="1367f-113">NameNode</span></span>
* <span data-ttu-id="1367f-114">Pilhas de Threads</span><span class="sxs-lookup"><span data-stu-id="1367f-114">Thread Stacks</span></span>
* <span data-ttu-id="1367f-115">Interface do usuário da Web do Oozie</span><span class="sxs-lookup"><span data-stu-id="1367f-115">Oozie web UI</span></span>
* <span data-ttu-id="1367f-116">Interface do usuário mestre e de logs do HBase</span><span class="sxs-lookup"><span data-stu-id="1367f-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="1367f-117">Se você usar as Ações de Script para personalizar seu cluster, todos os serviços ou utilitários que forem instalados e que expuserem a interface do usuário da Web exigirão um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="1367f-118">Por exemplo, se você instalar o Hue usando uma Ação de Script, deverá usar um túnel SSH para acessar a interface do usuário da Web do Hue.</span><span class="sxs-lookup"><span data-stu-id="1367f-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1367f-119">Se tiver acesso direto ao HDInsight por meio de uma rede virtual, você não precisará usar túneis SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="1367f-120">Para obter um exemplo de acesso direto ao HDInsight por meio de uma rede virtual, consulte o documento [Conectar HDInsight em sua rede local](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="1367f-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="1367f-121">O que é um túnel SSH</span><span class="sxs-lookup"><span data-stu-id="1367f-121">What is an SSH tunnel</span></span>

<span data-ttu-id="1367f-122">O [túnel de Secure Shell (SSH)](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) roteia o tráfego enviado para uma porta em sua estação de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="1367f-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="1367f-123">O tráfego é roteado por meio de uma conexão SSH para o nó principal do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1367f-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="1367f-124">A solicitação é resolvida como se ela tivesse sido originada no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1367f-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="1367f-125">A resposta é então roteada de volta pelo túnel até a sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1367f-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1367f-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1367f-126">Prerequisites</span></span>

* <span data-ttu-id="1367f-127">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-127">An SSH client.</span></span> <span data-ttu-id="1367f-128">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1367f-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="1367f-129">Um navegador da Web que pode ser configurado para usar um proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="1367f-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1367f-130">O suporte a proxy SOCKS integrado do Windows não dá suporte a SOCKS5 e não funciona com as etapas neste documento.</span><span class="sxs-lookup"><span data-stu-id="1367f-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="1367f-131">Os navegadores a seguir contam com as configurações de proxy do Windows e não funcionam com as etapas neste documento:</span><span class="sxs-lookup"><span data-stu-id="1367f-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="1367f-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="1367f-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="1367f-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1367f-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="1367f-134">O Google Chrome também conta com as configurações de proxy do Windows.</span><span class="sxs-lookup"><span data-stu-id="1367f-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="1367f-135">No entanto, você pode instalar extensões que dão suporte a SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="1367f-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="1367f-136">Recomendamos o [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="1367f-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="1367f-137"><a name="usessh"></a>Criar um túnel usando o comando SSH</span><span class="sxs-lookup"><span data-stu-id="1367f-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="1367f-138">Use o comando a seguir para criar um túnel SSH usando o comando `ssh` .</span><span class="sxs-lookup"><span data-stu-id="1367f-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="1367f-139">Substitua **USERNAME** por um usuário SSH para seu cluster HDInsight e substitua **CLUSTERNAME** pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1367f-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="1367f-140">Esse comando cria uma conexão que encaminha o tráfego para a porta local 9876 do cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="1367f-141">As opções são:</span><span class="sxs-lookup"><span data-stu-id="1367f-141">The options are:</span></span>

* <span data-ttu-id="1367f-142">**D 9876**: a porta local que roteará o tráfego pelo túnel.</span><span class="sxs-lookup"><span data-stu-id="1367f-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="1367f-143">**C** : compactar todos os dados, porque o tráfego da Web é texto, em sua maioria.</span><span class="sxs-lookup"><span data-stu-id="1367f-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="1367f-144">**2** : forçar o SSH para tentar somente a versão 2 do protocolo.</span><span class="sxs-lookup"><span data-stu-id="1367f-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="1367f-145">**q** : modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="1367f-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="1367f-146">**T** : desabilitar alocação pseudo-tty, já que estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="1367f-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="1367f-147">**n** – impede a leitura de STDIN, já que estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="1367f-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="1367f-148">**N** : não executar um comando remoto, pois estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="1367f-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="1367f-149">**f** : executar em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="1367f-149">**f** - Run in the background.</span></span>

<span data-ttu-id="1367f-150">Quando o comando terminar, o tráfego enviado para a porta 9876 no computador local será roteado para o nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="1367f-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="1367f-151"><a name="useputty"></a>Criar um túnel usando o PuTTY</span><span class="sxs-lookup"><span data-stu-id="1367f-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="1367f-152">O [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) é um cliente SSH gráfico do Windows.</span><span class="sxs-lookup"><span data-stu-id="1367f-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="1367f-153">Use as etapas a seguir para criar um túnel SSH usando o PuTTY:</span><span class="sxs-lookup"><span data-stu-id="1367f-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="1367f-154">Abra o PuTTY e insira as informações da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="1367f-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="1367f-155">Se não estiver familiarizado com o PuTTY, confira a [documentação do PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="1367f-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="1367f-156">Na seção **Categoria** à esquerda da caixa de diálogo, expanda **Conexão**, expanda **SSH** e selecione **Túneis**.</span><span class="sxs-lookup"><span data-stu-id="1367f-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="1367f-157">Forneça as seguintes informações no formulário **Opções de controle do encaminhamento de porta SSH** :</span><span class="sxs-lookup"><span data-stu-id="1367f-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="1367f-158">**Porta de Origem** : a porta no cliente que você deseja encaminhar.</span><span class="sxs-lookup"><span data-stu-id="1367f-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="1367f-159">Por exemplo, **9876**.</span><span class="sxs-lookup"><span data-stu-id="1367f-159">For example, **9876**.</span></span>

   * <span data-ttu-id="1367f-160">**Destino** : o endereço SSH para o cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="1367f-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1367f-161">Por exemplo, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="1367f-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="1367f-162">**Dinâmico** : habilita roteamento de proxy SOCKS dinâmico.</span><span class="sxs-lookup"><span data-stu-id="1367f-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![imagem de opções de túnel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="1367f-164">Clique em **Adicionar** para adicionar as configurações e clique em **Abrir** para abrir uma conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="1367f-165">Quando solicitado, faça logon no servidor.</span><span class="sxs-lookup"><span data-stu-id="1367f-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="1367f-166">Usar o túnel de seu navegador</span><span class="sxs-lookup"><span data-stu-id="1367f-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1367f-167">As etapas nesta seção usam o navegador Mozilla FireFox, pois ele fornece as mesmas configurações de proxy em todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="1367f-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="1367f-168">Outros navegadores modernos como Google Chrome podem exigir uma extensão como o FoxyProxy para trabalhar com o túnel.</span><span class="sxs-lookup"><span data-stu-id="1367f-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="1367f-169">Configure o navegador para usar **localhost** e a porta usada ao criar o túnel como um proxy **SOCKS v5**.</span><span class="sxs-lookup"><span data-stu-id="1367f-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="1367f-170">Aqui está a aparência das configurações do Firefox.</span><span class="sxs-lookup"><span data-stu-id="1367f-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="1367f-171">Se você tiver usado uma porta diferente da 9876, altere a porta que usou:</span><span class="sxs-lookup"><span data-stu-id="1367f-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![imagem das configurações do Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="1367f-173">Selecionar **DNS Remoto** resolve as solicitações de DNS (Sistema de Nomes de Domínio) usando o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1367f-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="1367f-174">Essa configuração resolve o DNS usando o nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="1367f-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="1367f-175">Verifique se o túnel funciona visitando um site, como [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="1367f-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="1367f-176">O IP retornado deve ser um IP usado pelo data center do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1367f-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="1367f-177">Verifique com a interface do usuário do Ambari Web</span><span class="sxs-lookup"><span data-stu-id="1367f-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="1367f-178">Assim que o cluster tiver sido estabelecido, use as etapas a seguir para verificar se você pode acessar as interfaces do usuário da Web do serviço Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="1367f-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="1367f-179">Em seu navegador, vá para http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="1367f-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="1367f-180">O endereço `headnodehost` é enviado pelo túnel para o cluster e resolverá o nó principal Ambari em execução.</span><span class="sxs-lookup"><span data-stu-id="1367f-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="1367f-181">Quando solicitado, insira o nome de usuário do administrador (admin) e a senha do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1367f-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="1367f-182">Talvez a interface do usuário do Ambari Web seja solicitada uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="1367f-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="1367f-183">Nesse caso, insira novamente as informações.</span><span class="sxs-lookup"><span data-stu-id="1367f-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1367f-184">Ao usar o endereço http://headnodehost:8080 para se conectar ao cluster, você estará se conectando através do túnel.</span><span class="sxs-lookup"><span data-stu-id="1367f-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="1367f-185">A comunicação é protegida usando o túnel SSH em vez de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1367f-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="1367f-186">Para se conectar pela Internet usando o HTTPS, use https://CLUSTERNAME.azurehdinsight.net, em que **CLUSTERNAME** é o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="1367f-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="1367f-187">Na interface do usuário do Ambari na Web, selecione HDFS na lista à esquerda da página.</span><span class="sxs-lookup"><span data-stu-id="1367f-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Imagem com o HDFS selecionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="1367f-189">Quando as informações do serviço HDFS forem exibidas, selecione **Links Rápidos**.</span><span class="sxs-lookup"><span data-stu-id="1367f-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="1367f-190">Uma lista de nós de cabeçalho do cluster é exibida.</span><span class="sxs-lookup"><span data-stu-id="1367f-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="1367f-191">Escolha um dos nós de cabeça e **Interface de Usuário do NameNode**.</span><span class="sxs-lookup"><span data-stu-id="1367f-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Imagem do menu Links Rápidos expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="1367f-193">Quando você seleciona __Links rápidos__, pode receber um indicador de espera.</span><span class="sxs-lookup"><span data-stu-id="1367f-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="1367f-194">Essa condição poderá ocorrer se você tiver uma conexão de Internet lenta.</span><span class="sxs-lookup"><span data-stu-id="1367f-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="1367f-195">Aguarde um minuto ou dois pelos dados a serem recebidos do servidor e experimente a lista novamente.</span><span class="sxs-lookup"><span data-stu-id="1367f-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="1367f-196">Algumas entradas no menu **Links rápidos** podem ser cortadas pelo lado direito da tela.</span><span class="sxs-lookup"><span data-stu-id="1367f-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="1367f-197">Nesse caso, expanda o menu usando o mouse e a tecla de seta para a direita para rolar a tela para a direita e ver o restante do menu.</span><span class="sxs-lookup"><span data-stu-id="1367f-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="1367f-198">Uma página semelhante à seguinte imagem será exibida:</span><span class="sxs-lookup"><span data-stu-id="1367f-198">A page similar to the following image is displayed:</span></span>

    ![Imagem da interface do usuário do NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="1367f-200">Observe a URL da página; ela deve ser semelhante a **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="1367f-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="1367f-201">Essa URI está usando o nome de domínio totalmente qualificado (FQDN) interno do nó e é acessada apenas ao utilizar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="1367f-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1367f-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1367f-202">Next steps</span></span>

<span data-ttu-id="1367f-203">Agora que você aprendeu a criar e usar um túnel SSH, veja o documento a seguir para outras maneiras de usar o Ambari:</span><span class="sxs-lookup"><span data-stu-id="1367f-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="1367f-204">Gerenciar clusters HDInsight usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="1367f-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="1367f-205">Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1367f-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

