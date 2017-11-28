---
title: "aaaUse SSH túnel tooaccess HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse uma toosecurely de túnel SSH procurar recursos da web hospedados em seus nós HDInsight baseados em Linux."
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
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="861ba-103">Usar a interface da web Ambari tooaccess túnel SSH, JobHistory, NameNode, Oozie e outras interfaces do usuário da web</span><span class="sxs-lookup"><span data-stu-id="861ba-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="861ba-104">Clusters de HDInsight baseados em Linux fornecem acesso tooAmbari interface da web sobre Olá da Internet, mas alguns recursos de saudação da interface do usuário não são.</span><span class="sxs-lookup"><span data-stu-id="861ba-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="861ba-105">Por exemplo, Olá interface da web para outros serviços que são apresentados por meio do Ambari.</span><span class="sxs-lookup"><span data-stu-id="861ba-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="861ba-106">Para a funcionalidade completa do Olá Ambari web da interface do usuário, você deve usar um cabeçalho de cluster de toohello de túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="861ba-107">Por que usar um túnel SSH</span><span class="sxs-lookup"><span data-stu-id="861ba-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="861ba-108">Vários menus de saudação do Ambari só funcionam por meio de um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="861ba-109">Esses menus dependem de sites e serviços em execução em outros tipos de nó, como nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="861ba-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="861ba-110">Geralmente, esses sites não são protegidos, portanto, não é seguro toodirectly expor em Olá internet.</span><span class="sxs-lookup"><span data-stu-id="861ba-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="861ba-111">Olá interfaces do usuário da Web a seguir requerem um túnel SSH:</span><span class="sxs-lookup"><span data-stu-id="861ba-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="861ba-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="861ba-112">JobHistory</span></span>
* <span data-ttu-id="861ba-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="861ba-113">NameNode</span></span>
* <span data-ttu-id="861ba-114">Pilhas de Threads</span><span class="sxs-lookup"><span data-stu-id="861ba-114">Thread Stacks</span></span>
* <span data-ttu-id="861ba-115">Interface do usuário da Web do Oozie</span><span class="sxs-lookup"><span data-stu-id="861ba-115">Oozie web UI</span></span>
* <span data-ttu-id="861ba-116">Interface do usuário mestre e de logs do HBase</span><span class="sxs-lookup"><span data-stu-id="861ba-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="861ba-117">Se você usar ações de Script toocustomize seu cluster, todos os serviços ou utilitários que você instalar que expõem uma interface do usuário da web exigem um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="861ba-118">Por exemplo, se você instalar o matiz usando uma ação de Script, você deve usar um SSH túnel tooaccess Olá matiz interface da web.</span><span class="sxs-lookup"><span data-stu-id="861ba-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="861ba-119">Se você tiver acesso direto tooHDInsight por meio de uma rede virtual, não é necessário toouse SSH túneis.</span><span class="sxs-lookup"><span data-stu-id="861ba-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="861ba-120">Para obter um exemplo de como acessar diretamente o HDInsight por meio de uma rede virtual, consulte Olá [HDInsight conectar rede de local de tooyour](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="861ba-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="861ba-121">O que é um túnel SSH</span><span class="sxs-lookup"><span data-stu-id="861ba-121">What is an SSH tunnel</span></span>

<span data-ttu-id="861ba-122">[Secure Shell (SSH) túnel](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) roteia o tráfego enviado porta tooa na sua estação de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="861ba-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="861ba-123">Olá tráfego é roteado por meio de um nó principal SSH conexão tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="861ba-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="861ba-124">solicitação de saudação é resolvida como se ele foi originado no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="861ba-125">resposta de saudação é encaminhada através de estação de trabalho do hello túnel tooyour.</span><span class="sxs-lookup"><span data-stu-id="861ba-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="861ba-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="861ba-126">Prerequisites</span></span>

* <span data-ttu-id="861ba-127">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-127">An SSH client.</span></span> <span data-ttu-id="861ba-128">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="861ba-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="861ba-129">Um navegador da web que pode ser configurado toouse um proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="861ba-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="861ba-130">suporte do proxy meias para Olá integrado do Windows não dá suporte a SOCKS5 e não funciona com etapas Olá neste documento.</span><span class="sxs-lookup"><span data-stu-id="861ba-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="861ba-131">Hello seguintes navegadores dependem de configurações de proxy do Windows e não no momento trabalho com etapas Olá neste documento:</span><span class="sxs-lookup"><span data-stu-id="861ba-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="861ba-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="861ba-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="861ba-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="861ba-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="861ba-134">Google Chrome também se baseia em configurações de proxy do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="861ba-135">No entanto, você pode instalar extensões que dão suporte a SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="861ba-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="861ba-136">Recomendamos o [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="861ba-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="861ba-137"><a name="usessh"></a>Criar um túnel usando o comando SSH Olá</span><span class="sxs-lookup"><span data-stu-id="861ba-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="861ba-138">Comando de uso a seguir de Olá toocreate um túnel SSH usando Olá `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="861ba-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="861ba-139">Substituir **USERNAME** com um usuário SSH para o cluster HDInsight e substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="861ba-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="861ba-140">Este comando cria uma conexão que direciona o cluster do tráfego toolocal porta 9876 toohello via SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="861ba-141">Olá opções são:</span><span class="sxs-lookup"><span data-stu-id="861ba-141">hello options are:</span></span>

* <span data-ttu-id="861ba-142">**D 9876** -Olá porta local que roteia o tráfego por meio de túnel hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="861ba-143">**C** : compactar todos os dados, porque o tráfego da Web é texto, em sua maioria.</span><span class="sxs-lookup"><span data-stu-id="861ba-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="861ba-144">**2** -force SSH tootry protocol versão 2 somente.</span><span class="sxs-lookup"><span data-stu-id="861ba-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="861ba-145">**q** : modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="861ba-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="861ba-146">**T** : desabilitar alocação pseudo-tty, já que estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="861ba-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="861ba-147">**n** – impede a leitura de STDIN, já que estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="861ba-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="861ba-148">**N** : não executar um comando remoto, pois estamos apenas encaminhando uma porta.</span><span class="sxs-lookup"><span data-stu-id="861ba-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="861ba-149">**f** -executar no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="861ba-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="861ba-150">Depois de Olá comando é concluído, o tráfego enviado tooport 9876 no computador local Olá é roteado toohello nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="861ba-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="861ba-151"><a name="useputty"></a>Criar um túnel usando o PuTTY</span><span class="sxs-lookup"><span data-stu-id="861ba-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="861ba-152">O [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) é um cliente SSH gráfico do Windows.</span><span class="sxs-lookup"><span data-stu-id="861ba-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="861ba-153">Use Olá um túnel SSH usando PuTTY toocreate as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="861ba-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="861ba-154">Abra o PuTTY e insira as informações da sua conexão.</span><span class="sxs-lookup"><span data-stu-id="861ba-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="861ba-155">Se você não estiver familiarizado com PuTTY, consulte Olá [PuTTY documentação (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="861ba-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="861ba-156">Em Olá **categoria** toohello seção à esquerda da caixa de diálogo hello, expanda **Conexão**, expanda **SSH**e, em seguida, selecione **túneis**.</span><span class="sxs-lookup"><span data-stu-id="861ba-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="861ba-157">Fornecer Olá seguintes informações sobre Olá **encaminhamento de porta de opções que controlam o SSH** formulário:</span><span class="sxs-lookup"><span data-stu-id="861ba-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="861ba-158">**Porta de origem** -Olá porta em que você deseja tooforward de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="861ba-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="861ba-159">Por exemplo, **9876**.</span><span class="sxs-lookup"><span data-stu-id="861ba-159">For example, **9876**.</span></span>

   * <span data-ttu-id="861ba-160">**Destino** -Olá SSH endereço de cluster do HDInsight baseados em Linux hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="861ba-161">Por exemplo, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="861ba-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="861ba-162">**Dinâmico** : habilita roteamento de proxy SOCKS dinâmico.</span><span class="sxs-lookup"><span data-stu-id="861ba-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![imagem de opções de túnel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="861ba-164">Clique em **adicionar** tooadd Olá configurações e, em seguida, clique em **abrir** tooopen uma conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="861ba-165">Quando solicitado, faça logon no servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="861ba-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="861ba-166">Usar o túnel de saudação do navegador</span><span class="sxs-lookup"><span data-stu-id="861ba-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="861ba-167">Olá etapas em Olá de usar esta seção navegador Mozilla FireFox, pois ela fornece as mesmas configurações de proxy Olá todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="861ba-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="861ba-168">Outros navegadores modernos, como Google Chrome, podem exigir uma extensão como toowork FoxyProxy com encapsulamento hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="861ba-169">Configurar Olá navegador toouse **localhost** e porta Olá usado quando criar túnel hello como um **v5 meias para** proxy.</span><span class="sxs-lookup"><span data-stu-id="861ba-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="861ba-170">Aqui está a aparência de configurações do hello Firefox.</span><span class="sxs-lookup"><span data-stu-id="861ba-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="861ba-171">Se você usou uma porta diferente 9876, altere Olá porta toohello que você usado:</span><span class="sxs-lookup"><span data-stu-id="861ba-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![imagem das configurações do Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="861ba-173">Selecionando **DNS remoto** resolve solicitações de sistema de nome de domínio (DNS) usando o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="861ba-174">Essa configuração de DNS usando o nó principal do cluster Olá Olá é resolvido.</span><span class="sxs-lookup"><span data-stu-id="861ba-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="861ba-175">Verifique se esse túnel Olá funciona visitar um site, como [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="861ba-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="861ba-176">Olá IP retornado deve ser um usada por datacenter do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="861ba-177">Verifique com a interface do usuário do Ambari Web</span><span class="sxs-lookup"><span data-stu-id="861ba-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="861ba-178">Após o estabelecimento de cluster hello, use Olá tooverify etapas que você pode acessar as interfaces do usuário da web do serviço de saudação Ambari Web a seguir:</span><span class="sxs-lookup"><span data-stu-id="861ba-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="861ba-179">Em seu navegador, vá toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="861ba-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="861ba-180">Olá `headnodehost` endereço são enviados por cluster de toohello de túnel hello e resolver o nó principal de toohello Ambari está em execução no.</span><span class="sxs-lookup"><span data-stu-id="861ba-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="861ba-181">Quando solicitado, insira o nome de usuário de administrador hello (administrador) e a senha para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="861ba-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="861ba-182">Você pode ser solicitado novamente pelo Olá Ambari web da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="861ba-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="861ba-183">Nesse caso, inserir novamente as informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="861ba-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="861ba-184">Quando usando Olá http://headnodehost:8080 endereço tooconnect toohello cluster, você está se conectando por meio de túnel hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="861ba-185">A comunicação é protegida usando o túnel SSH Olá em vez de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="861ba-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="861ba-186">tooconnect Olá internet usando HTTPS, para usar https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é Olá nome do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="861ba-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="861ba-187">Olá Ambari Web UI, selecione HDFS Olá na lista de saudação esquerda da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="861ba-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Imagem com o HDFS selecionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="861ba-189">Quando Olá informações de serviço do HDFS for exibida, selecione **Links rápidos**.</span><span class="sxs-lookup"><span data-stu-id="861ba-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="861ba-190">Uma lista de nós de cluster de Olá cabeçalho é exibida.</span><span class="sxs-lookup"><span data-stu-id="861ba-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="861ba-191">Selecione um de nós de cabeçalho hello e, em seguida, selecione **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="861ba-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Imagem com o menu de links rápidos Olá expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="861ba-193">Quando você seleciona __Links rápidos__, pode receber um indicador de espera.</span><span class="sxs-lookup"><span data-stu-id="861ba-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="861ba-194">Essa condição poderá ocorrer se você tiver uma conexão de Internet lenta.</span><span class="sxs-lookup"><span data-stu-id="861ba-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="861ba-195">Aguarde um minuto ou dois para Olá dados toobe recebido do servidor de saudação e tente lista Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="861ba-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="861ba-196">Algumas entradas no hello **Links rápidos** menu pode ser cortado por Olá direita da tela hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="861ba-197">Nesse caso, expanda o menu hello usando o mouse e usar Olá seta para a direita tooscroll chave Olá tela toohello toosee direita Olá restante do menu hello.</span><span class="sxs-lookup"><span data-stu-id="861ba-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="861ba-198">Um toohello semelhante página imagem a seguir é exibida:</span><span class="sxs-lookup"><span data-stu-id="861ba-198">A page similar toohello following image is displayed:</span></span>

    ![Imagem de saudação NameNode de UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="861ba-200">Observe Olá URL da página; ele deve ser semelhante muito**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="861ba-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="861ba-201">Esse URI está usando o nome de domínio totalmente qualificado interno (FQDN) do hello do nó de saudação e é acessível apenas ao usar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="861ba-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="861ba-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="861ba-202">Next steps</span></span>

<span data-ttu-id="861ba-203">Agora que você aprendeu como toocreate e use um túnel SSH, consulte Olá documento para outros modos de toouse Ambari a seguir:</span><span class="sxs-lookup"><span data-stu-id="861ba-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="861ba-204">Gerenciar clusters HDInsight usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="861ba-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="861ba-205">Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="861ba-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

