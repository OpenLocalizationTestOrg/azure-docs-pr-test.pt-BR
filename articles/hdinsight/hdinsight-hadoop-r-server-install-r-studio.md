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
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Instalar o RStudio com o Servidor R no HDInsight

Este artigo descreve como tooinstall Olá versão (gratuita) da comunidade do [RStudio Server](https://www.rstudio.com/products/rstudio-server/) no nó de borda de saudação de um cluster usando um script personalizado. O RStudio Server que fornece um IDE baseado em navegador para uso por clientes remotos e é amplamente usado em Linux. Há vários ambientes de desenvolvimento integrado (IDEs) disponíveis para R hoje em dia, incluindo:

- RTVS ([Ferramentas do R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)) da Microsoft 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- [StatET](http://www.walware.de/goto/statet) baseado no Eclipse da Walware.

vantagem de saudação da instalação RStudio Server no nó de borda de saudação de um cluster HDInsight é que ele fornece uma experiência completa do IDE para o desenvolvimento de saudação e execução de scripts de R com R Server no cluster hello. Essa configuração pode ser consideravelmente mais produtiva do que o uso do padrão de saudação Console de R.

> [!NOTE]
> procedimento Olá descrito neste artigo só será relevante se você não selecionou tooinstall edição do servidor RStudio community ao provisionar o cluster. Se ele foi adicionado durante o provisionamento, então tooaccess-você pode clicar em Olá **R Server painéis** lado a lado no hello entrada de portal do Azure para seu cluster, em seguida, no hello **R Studio Server** lado a lado. 

Se você preferir toouse Olá comercialmente licenciado Pro versão do servidor de RStudio, você deve seguir instruções de instalação de saudação do [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Se você estiver usando um cluster de HDInsight para o qual R foi instalado usando Olá [ação de Script de instalação do R](hdinsight-hadoop-r-scripts-linux.md), Olá etapas neste documento não funcionarão corretamente precisam de um servidor de R no cluster do HDInsight hello.
>
> 

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster Azure HDInsight com R Server instalado. Para obter instruções, confira [Introdução ao Servidor R nos clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).
* Um cliente SSH. Para distribuições do Linux e Unix ou Macintosh OS X, Olá `ssh` comando é fornecido com o sistema operacional de saudação. Para Windows, é recomendável [Cygwin](http://www.redhat.com/services/custom/cygwin/) com hello [opção OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Instalar o RStudio em cluster hello usando um script personalizado

Aqui estão as etapas de saudação:

1. Identificar o nó de borda de saudação do cluster de saudação. Para um cluster de HDInsight com R Server, a seguir está a convenção de nomenclatura de Olá para o nó principal e borda.
   * Nó principal `CLUSTERNAME-ssh.azurehdinsight.net`
   * Nó de borda `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH no nó de borda de saudação do cluster de saudação usando o padrão de nomenclatura Olá fornecido na etapa 1. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Quando você estiver conectado, se tornar um usuário raiz no cluster hello. Na sessão SSH hello, use Olá comando a seguir:

        sudo su -

4. Baixe Olá script personalizado tooinstall RStudio. Use Olá comando a seguir:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Alterar permissões de saudação no arquivo de script personalizado hello e executar o script hello. Use Olá comandos a seguir:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Se você usou uma senha SSH durante a criação de um cluster HDInsight com R Server, você pode ignorar esta etapa e continuar toohello lado. Se você usou uma chave SSH em vez disso, cluster de saudação toocreate, você deve definir uma senha para o usuário SSH. Essa senha é necessária ao conectar-se tooRStudio. Execute Olá comandos a seguir:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Quando a **Senha atual do Kerberos** for solicitada, pressione **ENTER**.  Observe que você deve substituir `USERNAME` por um usuário SSH de seu cluster HDInsight. Se sua senha é definida com êxito, você verá a seguinte mensagem de saudação:

        passwd: password updated successfully

    Sair da sessão SSH hello.

8. Criar um cluster de toohello de túnel SSH mapeando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` no hello HDInsight cluster toohello máquina do cliente. Você deve criar um túnel SSH antes de abrir uma nova sessão do navegador.

   * Em um cliente Linux ou um cliente do Windows com [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra uma sessão do terminal e usar Olá comando a seguir:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Substituir **USERNAME** com um usuário SSH para o cluster HDInsight e substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.
       Você também pode usar uma chave SSH em vez de uma senha adicionando `-i id_rsa_key`.        
   * Se estiver usar um cliente do Windows com PuTTY

     1. Abra o PuTTY e insira as informações da sua conexão.
     2. Em Olá **categoria** toohello seção à esquerda da caixa de diálogo hello, expanda **Conexão**, expanda **SSH**e, em seguida, selecione **túneis**.
     3. Fornecer Olá seguintes informações sobre Olá **encaminhamento de porta de opções que controlam o SSH** formulário:

        * **Porta de origem** -Olá porta em que você deseja tooforward de cliente de saudação. Por exemplo, **8787**.
        * **Destino** - Olá destino deve ser mapeado toohello máquina de cliente local. Por exemplo, **localhost:8787**.

            ![Criar um túnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Criar um túnel SSH")

     4. Clique em **adicionar** tooadd Olá configurações e, em seguida, clique em **abrir** tooopen uma conexão SSH.
     5. Quando solicitado, faça logon no toohello servidor tooestablish um túnel de saudação de sessão e enable SSH.

9. Abra um navegador da web e digite Olá com base na porta Olá inserido para o túnel de saudação de URL a seguir:

        http://localhost:8787/ 

10. Você é solicitado tooenter Olá SSH username e password tooconnect toohello cluster. Se você usou uma chave SSH durante a criação de cluster hello, você deverá inserir a senha de saudação criado na etapa 5.

    ![Conecte-se tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "criar um túnel SSH")

11. tootest se Olá RStudio instalação foi bem-sucedida, você pode executar um script de teste que executa trabalhos de MapReduce e Spark R no cluster hello. toodownload Olá teste script toorun em RStudio, volte toohello SSH console e digite Olá comandos a seguir:

    *    Se você criou um cluster Hadoop com R, use este comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Se você criou um cluster Spark com R, use este comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. RStudio, você verá Olá testar o script baixado. Clique duas vezes em Olá tooopen de arquivo, selecione o conteúdo do arquivo hello hello e, em seguida, clique em **executar**. Você deve ver a saída Olá Olá **Console** painel:

   ![Testar a instalação do hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "testar a instalação de saudação")

Outra opção seria tootype `source(testhdi.r)` ou `source(testhdi_spark.r)` tooexecute script de saudação.

## <a name="see-also"></a>Consulte também

* [Opções de contexto de computação para o R Server em clusters HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opções de Armazenamento do Azure para o Servidor R no HDInsight](hdinsight-hadoop-r-server-storage.md)

