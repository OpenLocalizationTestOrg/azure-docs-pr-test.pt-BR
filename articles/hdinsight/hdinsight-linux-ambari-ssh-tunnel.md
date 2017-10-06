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
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Usar a interface da web Ambari tooaccess túnel SSH, JobHistory, NameNode, Oozie e outras interfaces do usuário da web

Clusters de HDInsight baseados em Linux fornecem acesso tooAmbari interface da web sobre Olá da Internet, mas alguns recursos de saudação da interface do usuário não são. Por exemplo, Olá interface da web para outros serviços que são apresentados por meio do Ambari. Para a funcionalidade completa do Olá Ambari web da interface do usuário, você deve usar um cabeçalho de cluster de toohello de túnel SSH.

## <a name="why-use-an-ssh-tunnel"></a>Por que usar um túnel SSH

Vários menus de saudação do Ambari só funcionam por meio de um túnel SSH. Esses menus dependem de sites e serviços em execução em outros tipos de nó, como nós de trabalho. Geralmente, esses sites não são protegidos, portanto, não é seguro toodirectly expor em Olá internet.

Olá interfaces do usuário da Web a seguir requerem um túnel SSH:

* JobHistory
* NameNode
* Pilhas de Threads
* Interface do usuário da Web do Oozie
* Interface do usuário mestre e de logs do HBase

Se você usar ações de Script toocustomize seu cluster, todos os serviços ou utilitários que você instalar que expõem uma interface do usuário da web exigem um túnel SSH. Por exemplo, se você instalar o matiz usando uma ação de Script, você deve usar um SSH túnel tooaccess Olá matiz interface da web.

> [!IMPORTANT]
> Se você tiver acesso direto tooHDInsight por meio de uma rede virtual, não é necessário toouse SSH túneis. Para obter um exemplo de como acessar diretamente o HDInsight por meio de uma rede virtual, consulte Olá [HDInsight conectar rede de local de tooyour](connect-on-premises-network.md) documento.

## <a name="what-is-an-ssh-tunnel"></a>O que é um túnel SSH

[Secure Shell (SSH) túnel](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) roteia o tráfego enviado porta tooa na sua estação de trabalho local. Olá tráfego é roteado por meio de um nó principal SSH conexão tooyour HDInsight cluster. solicitação de saudação é resolvida como se ele foi originado no nó de cabeçalho hello. resposta de saudação é encaminhada através de estação de trabalho do hello túnel tooyour.

## <a name="prerequisites"></a>Pré-requisitos

* Um cliente SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Um navegador da web que pode ser configurado toouse um proxy SOCKS5.

    > [!WARNING]
    > suporte do proxy meias para Olá integrado do Windows não dá suporte a SOCKS5 e não funciona com etapas Olá neste documento. Hello seguintes navegadores dependem de configurações de proxy do Windows e não no momento trabalho com etapas Olá neste documento:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome também se baseia em configurações de proxy do Windows hello. No entanto, você pode instalar extensões que dão suporte a SOCKS5. Recomendamos o [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Criar um túnel usando o comando SSH Olá

Comando de uso a seguir de Olá toocreate um túnel SSH usando Olá `ssh` comando. Substituir **USERNAME** com um usuário SSH para o cluster HDInsight e substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Este comando cria uma conexão que direciona o cluster do tráfego toolocal porta 9876 toohello via SSH. Olá opções são:

* **D 9876** -Olá porta local que roteia o tráfego por meio de túnel hello.
* **C** : compactar todos os dados, porque o tráfego da Web é texto, em sua maioria.
* **2** -force SSH tootry protocol versão 2 somente.
* **q** : modo silencioso.
* **T** : desabilitar alocação pseudo-tty, já que estamos apenas encaminhando uma porta.
* **n** – impede a leitura de STDIN, já que estamos apenas encaminhando uma porta.
* **N** : não executar um comando remoto, pois estamos apenas encaminhando uma porta.
* **f** -executar no plano de fundo de saudação.

Depois de Olá comando é concluído, o tráfego enviado tooport 9876 no computador local Olá é roteado toohello nó principal do cluster.

## <a name="useputty"></a>Criar um túnel usando o PuTTY

O [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) é um cliente SSH gráfico do Windows. Use Olá um túnel SSH usando PuTTY toocreate as etapas a seguir:

1. Abra o PuTTY e insira as informações da sua conexão. Se você não estiver familiarizado com PuTTY, consulte Olá [PuTTY documentação (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. Em Olá **categoria** toohello seção à esquerda da caixa de diálogo hello, expanda **Conexão**, expanda **SSH**e, em seguida, selecione **túneis**.

3. Fornecer Olá seguintes informações sobre Olá **encaminhamento de porta de opções que controlam o SSH** formulário:
   
   * **Porta de origem** -Olá porta em que você deseja tooforward de cliente de saudação. Por exemplo, **9876**.

   * **Destino** -Olá SSH endereço de cluster do HDInsight baseados em Linux hello. Por exemplo, **mycluster-ssh.azurehdinsight.net**.

   * **Dinâmico** : habilita roteamento de proxy SOCKS dinâmico.
     
     ![imagem de opções de túnel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Clique em **adicionar** tooadd Olá configurações e, em seguida, clique em **abrir** tooopen uma conexão SSH.

5. Quando solicitado, faça logon no servidor de toohello.

## <a name="use-hello-tunnel-from-your-browser"></a>Usar o túnel de saudação do navegador

> [!IMPORTANT]
> Olá etapas em Olá de usar esta seção navegador Mozilla FireFox, pois ela fornece as mesmas configurações de proxy Olá todas as plataformas. Outros navegadores modernos, como Google Chrome, podem exigir uma extensão como toowork FoxyProxy com encapsulamento hello.

1. Configurar Olá navegador toouse **localhost** e porta Olá usado quando criar túnel hello como um **v5 meias para** proxy. Aqui está a aparência de configurações do hello Firefox. Se você usou uma porta diferente 9876, altere Olá porta toohello que você usado:
   
    ![imagem das configurações do Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Selecionando **DNS remoto** resolve solicitações de sistema de nome de domínio (DNS) usando o cluster do HDInsight hello. Essa configuração de DNS usando o nó principal do cluster Olá Olá é resolvido.

2. Verifique se esse túnel Olá funciona visitar um site, como [http://www.whatismyip.com/](http://www.whatismyip.com/). Olá IP retornado deve ser um usada por datacenter do Microsoft Azure hello.

## <a name="verify-with-ambari-web-ui"></a>Verifique com a interface do usuário do Ambari Web

Após o estabelecimento de cluster hello, use Olá tooverify etapas que você pode acessar as interfaces do usuário da web do serviço de saudação Ambari Web a seguir:

1. Em seu navegador, vá toohttp://headnodehost:8080. Olá `headnodehost` endereço são enviados por cluster de toohello de túnel hello e resolver o nó principal de toohello Ambari está em execução no. Quando solicitado, insira o nome de usuário de administrador hello (administrador) e a senha para seu cluster. Você pode ser solicitado novamente pelo Olá Ambari web da interface do usuário. Nesse caso, inserir novamente as informações de saudação.

   > [!NOTE]
   > Quando usando Olá http://headnodehost:8080 endereço tooconnect toohello cluster, você está se conectando por meio de túnel hello. A comunicação é protegida usando o túnel SSH Olá em vez de HTTPS. tooconnect Olá internet usando HTTPS, para usar https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é Olá nome do cluster de saudação.

2. Olá Ambari Web UI, selecione HDFS Olá na lista de saudação esquerda da página de saudação.

    ![Imagem com o HDFS selecionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Quando Olá informações de serviço do HDFS for exibida, selecione **Links rápidos**. Uma lista de nós de cluster de Olá cabeçalho é exibida. Selecione um de nós de cabeçalho hello e, em seguida, selecione **NameNode UI**.

    ![Imagem com o menu de links rápidos Olá expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Quando você seleciona __Links rápidos__, pode receber um indicador de espera. Essa condição poderá ocorrer se você tiver uma conexão de Internet lenta. Aguarde um minuto ou dois para Olá dados toobe recebido do servidor de saudação e tente lista Olá novamente.
   >
   > Algumas entradas no hello **Links rápidos** menu pode ser cortado por Olá direita da tela hello. Nesse caso, expanda o menu hello usando o mouse e usar Olá seta para a direita tooscroll chave Olá tela toohello toosee direita Olá restante do menu hello.

4. Um toohello semelhante página imagem a seguir é exibida:

    ![Imagem de saudação NameNode de UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Observe Olá URL da página; ele deve ser semelhante muito**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**. Esse URI está usando o nome de domínio totalmente qualificado interno (FQDN) do hello do nó de saudação e é acessível apenas ao usar um túnel SSH.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toocreate e use um túnel SSH, consulte Olá documento para outros modos de toouse Ambari a seguir:

* [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)

Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

