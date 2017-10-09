---
title: aaaUse Phoenix Apache e esquilo com baseados no Windows Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Phoenix Apache no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Usar Apache Phoenix e SQuirreL com clusters do HBase baseados em Windows no HDInsight
Saiba como toouse [Apache Phoenix](http://phoenix.apache.org/) no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight. Para obter mais informações sobre o Phoenix, consulte [Phoenix em 15 minutos ou menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Para Olá gramática Phoenix, consulte [Phoenix gramática](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Para Olá informações de versão de Phoenix no HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Olá etapas para esse trabalho de documento somente para clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obter informações sobre como usar o Phoenix no HDInsight baseado em Linux, consulte [Usar o Apache Phoenix com clusters HBase baseados em Linux no HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Usar o SQLLine
[SQLLine](http://sqlline.sourceforge.net/) é um utilitário de linha de comando tooexecute SQL.

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar SQLLine, você deve ter o seguinte hello:

* **Um cluster HBase no HDInsight**. Para obter informações sobre como provisionar o cluster HBase, consulte [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started].
* **Conecte toohello HBase cluster por meio do protocolo de área de trabalho remota Olá**. Para obter instruções, consulte [Hadoop gerenciar clusters de HDInsight usando Olá Portal clássico do Azure][hdinsight-manage-portal].

**toofind nome de host Olá**

1. Abra **linha de comando do Hadoop** na área de trabalho de saudação.
2. Execute Olá sufixo DNS do comando tooget Olá a seguir:

        ipconfig

    Execute **Connection-specific DNS Suffix**. Por exemplo, *myhbasecluster.f5.internal.cloudapp.net*. Quando você conectar tooan HBase cluster, você precisará tooone tooconnect de Zookeepers hello usando o FQDN. Cada cluster HDInsight possui 3 Zookeepers. São eles: *zookeeper0*, *zookeeper1* e *zookeeper2*. Olá FQDN será algo como *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Abra **linha de comando do Hadoop** na área de trabalho de saudação.
2. Execute Olá comandos tooopen SQLLine a seguir:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    comandos de saudação usados no exemplo hello:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Para obter mais informações, consulte o [Manual SQLLine](http://sqlline.sourceforge.net/#manual) e [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>Usar o SQuirreL
[Esquilo SQL Client](http://squirrel-sql.sourceforge.net/) é um programa Java gráfico que permitem que você tooview estrutura de saudação do banco de dados compatível com JDBC, procurar Olá dados nas tabelas, emitir comandos SQL etc. Ele pode ser usado tooconnect tooApache Phoenix no HDInsight.

Esta seção mostra como tooinstall e configurar esquilo em sua estação de trabalho tooconnect tooan cluster HBase em HDInsight por meio de VPN.

### <a name="prerequisites"></a>Pré-requisitos
Antes de seguir os procedimentos de hello, você deve ter o seguinte hello:

* Um cluster HBase implantado tooan rede virtual do Azure com uma máquina virtual DNS.  Para obter instruções, consulte [Criar clusters HBase na Rede Virtual do Azure][hdinsight-hbase-provision-vnet].

* Obtém o sufixo DNS específico da Conexão do hello HBase cluster cluster. tooget-lo, RDP em cluster Olá, e, em seguida, executar esse comando.  sufixo DNS Olá é semelhante a:

        myhbase.b7.internal.cloudapp.net
* Baixe e instale o [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) em sua estação de trabalho. Você precisará makecert da saudação pacote toocreate seu certificado.  
* Baixe e instale o [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) em sua estação de trabalho.  O SQuirreL SQL client versão 3.0 e superior requer JRE versão 1.6 ou superior.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Configurar uma conexão de VPN ponto a Site toohello rede virtual do Azure
Há três etapas envolvidas na configuração de uma conexão VPN ponto a site:

1. [Configurar uma rede virtual e um gateway de roteamento dinâmico](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Criar seus certificados](#Create-your-certificates)
3. [Configurar o seu cliente VPN](#Configure-your-VPN-client)

Consulte [configurar uma conexão de VPN ponto a Site tooan rede Virtual do Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obter mais informações.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Configurar uma rede virtual e um gateway de roteamento dinâmico
Garantir que você possua um cluster HBase em uma rede virtual do Azure (consulte Olá pré-requisitos para essa seção). Olá próxima etapa é tooconfigure uma conexão ponto a site.

**conectividade de ponto para site Olá tooconfigure**

1. Entrar toohello [Portal clássico do Azure][azure-portal].
2. Olá esquerda, clique em **redes**.
3. Clique em criar a rede virtual Olá (consulte [HBase provisionar clusters na rede Virtual do Azure][hdinsight-hbase-provision-vnet]).
4. Clique em **configurar** da parte superior da saudação.
5. Em Olá **conectividade ponto a site** seção, selecione **configurar conectividade ponto a site**.
6. Configurar **IP inicial** e **CIDR** endereço de intervalo de endereços toospecify Olá IP do qual os clientes VPN receberão um IP quando conectados. intervalo de saudação não pode sobrepor qualquer Olá intervalos localizados em seus locais de rede e Olá rede virtual do Azure, que você irá se conectar. Por exemplo. Se você selecionou 10.0.0.0/20 para rede virtual hello, você pode selecionar 10.1.0.0/24 para o espaço de endereço de cliente hello. Consulte Olá [conectividadepontoaSite] [ vnet-point-to-site-connectivity] para obter mais informações.
7. Na seção de espaços de endereço de rede virtual hello, clique em **Adicionar sub-rede de gateway**.
8. Clique em **salvar** na parte inferior da saudação da página de saudação.
9. Clique em **Sim** tooconfirm alteração de saudação. Aguarde até que o sistema de saudação terminou tornando Olá alterar antes de prosseguir toohello próximo procedimento.

**toocreate um gateway de roteamento dinâmico**

1. De Olá Portal clássico do Azure, clique em **painel** da parte superior da saudação da página de saudação.
2. Clique em **criar GATEWAY** Olá página de baixo hello.
3. Clique em **Sim** tooconfirm. Aguarde até que o gateway de saudação é criado.
4. Clique em **painel** da parte superior da saudação.  Você verá um diagrama visual de rede virtual hello:

    ![Diagrama virtual de ponto para site de rede virtual do Azure][img-vnet-diagram]

    diagrama de saudação mostra 0 conexões de cliente. Depois de fazer uma rede virtual de toohello de conexão, o número de saudação será atualizado tooone.

#### <a name="create-your-certificates"></a>Criar seus certificados
Toocreate unidirecional é um certificado x. 509 usando Olá ferramenta de criação de certificado (makecert.exe) que vem com [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate um certificado raiz autoassinado**

1. Na estação de trabalho, abra uma janela de prompt de comando.
2. Navegue toohello pasta de ferramentas do Visual Studio.
3. Olá comando no exemplo hello abaixo a seguir criar e instalar um certificado raiz no repositório de certificados pessoal Olá na estação de trabalho e também criar um arquivo. cer correspondente que você posteriormente carregará toohello Portal clássico do Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Altere o diretório de toohello que você deseja Olá toobe do arquivo. cer localizado, onde o HBaseVnetVPNRootCertificate é o nome de saudação que você deseja toouse certificado hello.

    Não feche o prompt de comando hello.  Você precisará no procedimento a seguir hello.

   > [!NOTE]
   > Porque você criou um certificado raiz do qual os certificados de cliente serão gerados, você pode desejar tooexport esse certificado junto com sua chave privada e salvá-lo tooa local seguro onde possa ser recuperado.
   >
   >

**toocreate um certificado de cliente**

* De saudação mesmo prompt de comando (tem toobe em Olá mesmo computador em que você criou o certificado de raiz de saudação. certificado de cliente Olá deve ser gerado do certificado de raiz de saudação), execução hello seguinte comando:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate é o nome do certificado raiz hello.  Ele tem o nome do certificado de raiz toomatch hello.  

    Certificado de raiz hello e certificado de saudação do cliente são armazenadas no repositório de certificados pessoais no computador. Use certmgr.msc tooverify.

    ![Certificado VPN de ponto para site de rede virtual do Azure][img-certificate]

    Um certificado de cliente deve ser instalado em cada computador que deseja que a rede virtual do tooconnect toohello. É recomendável que você crie cliente exclusivo certificados para cada computador que deseja que a rede virtual do tooconnect toohello. certificados de cliente de saudação tooexport, use certmgr.msc.

**toohello do certificado raiz do tooupload Olá Portal clássico do Azure**

1. De Olá Portal clássico do Azure, clique em **rede** Olá esquerda.
2. Clique em rede virtual hello, onde o cluster HBase é implantado.
3. Clique em **certificados** da parte superior da saudação.
4. Clique em **carregar** de saudação baixo e especifique o arquivo do certificado raiz Olá você criou no procedimento Olá antes da última. Aguarde até que o certificado de saudação foi importado.
5. Clique em **painel** na parte superior da saudação.  diagrama de virtual Olá mostra o status de saudação.

#### <a name="configure-your-vpn-client"></a>Configurar o seu cliente VPN
**toodownload e instale o pacote VPN de cliente Olá**

1. Na página de painel Olá da rede virtual hello, na seção de visão rápida hello, clique em **Download Olá pacote de VPN de cliente de 64 bits** ou **Download Olá pacote de VPN de cliente de 32 bits** com base em seu versão do sistema operacional da estação de trabalho.
2. Clique em **executar** tooinstall pacote de saudação.
3. No prompt de segurança hello, clique em **obter mais informações**e, em seguida, clique em **executar assim mesmo**.
4. Clique em **Sim** duas vezes.

**tooconnect tooVPN**

1. Na área de trabalho de saudação de sua estação de trabalho, clique o ícone de redes de saudação na barra de tarefas de saudação. Você deverá ver uma conexão VPN com o seu nome de rede virtual.
2. Clique no nome de conexão de VPN hello.
3. Clique em **Conectar**.

**Olá tootest resolução de nome de domínio e a conexão VPN**

* Na estação de trabalho Olá, abra um prompt de comando e ping de saudação nomes de sufixo DNS do cluster do HBase Olá a seguir é myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Instalar e configurar o SQuirreL em sua estação de trabalho
**tooinstall esquilo**

1. Baixar arquivo do hello esquilo SQL client jar do [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Arquivo jar Olá Abrir/executar. Ele requer Olá [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Clique em **Avançar** duas vezes.
4. Especifique um caminho onde Olá você tem permissão de gravação e, em seguida, clique em **próximo**.

  > [!NOTE]
  > pasta de instalação padrão Hello está na pasta de C:\Program Files\squirrel sql 3.6 de saudação.  No caminho de toothis de toowrite de ordem, instalador Olá deve ter o privilégio de administrador hello. Você pode abrir um prompt de comando como administrador, navegue pasta bin do tooJava e, em seguida, execute:
  >
  >     Java.exe-jar [caminho de saudação do arquivo jar do hello esquilo]
5. Clique em **Okey** tooconfirm criando Olá diretório de destino.
6. configuração padrão de saudação é tooinstall Olá Base e pacotes padrão.  Clique em **Avançar**.
7. Clique em **Próximo** duas vezes e, em seguida, clique em **Pronto**.

**driver de Phoenix Olá tooinstall**

arquivo jar do Hello phoenix driver está localizado em um cluster HBase de saudação. caminho de saudação é semelhante seguinte toohello baseados em versões de saudação:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Você precisa toocopy-tooyour estação de trabalho em Olá [pasta de instalação esquilo] /lib caminho.  Olá, a maneira mais fácil é tooRDP cluster hello e, em seguida, use arquivo copiar/colar (CTRL + C e CTRL + V) toocopy-tooyour estação de trabalho.

**tooadd um tooSQuirreL de driver Phoenix**

1. Abra o SQuirreL SQL Client em sua estação de trabalho.
2. Clique em Olá **Driver** guia Olá esquerda.
3. De saudação **Drivers** menu, clique em **novo Driver**.
4. Digite hello informações a seguir:

   * **Nome**: Phoenix
   * **URL de exemplo**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Nome da classe**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Usuário todas as letras minúsculas Olá exemplo de URL. Você pode usar o quorum zookeeper completo no caso de um deles estar inativo.  saudação de nomes de host são zookeeper0, zookeeper1 e zookeeper2.
     >
     >

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-driver]
5. Clique em **OK**.

**toocreate um cluster do alias toohello HBase**

1. De esquilo, clique em Olá **Aliases** guia Olá esquerda.
2. De saudação **Aliases** menu, clique em **novo Alias**.
3. Digite hello informações a seguir:

   * **Nome**: nome de saudação do cluster HBase de saudação ou qualquer nome que você preferir.
   * **Driver**: Phoenix.  Isso deve corresponder a nome do driver Olá criada no procedimento última hello.
   * **URL**: Olá URL é copiada da configuração do driver. Verifique se toouser todas as letras minúsculas.
   * **Nome de usuário**: pode ser qualquer texto.  Como você usar a conectividade VPN aqui, o nome de usuário de saudação não é usado em todos os.
   * **Senha**: pode ser qualquer texto.

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-alias]
4. Clique em **Testar**.
5. Clique em **Conectar**. Quando faz conexão hello, esquilo é semelhante a:

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun um teste**

1. Clique em Olá **SQL** guia direito próximo toohello **objetos** guia.
2. Copie e cole a saudação de código a seguir:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Clique o botão de execução de saudação.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Alternar back toohello **objetos** guia.
5. Expanda o nome do alias hello e, em seguida, expanda **tabela**.  Você deverá ver a nova tabela de hello listada em.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse Phoenix Apache no HDInsight.  toolearn mais, consulte

* [Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.
* [Provisionar clusters HBase na rede Virtual do Azure][hdinsight-hbase-provision-vnet]: com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que os aplicativos podem se comunicar com o HBase diretamente.
* [Configurar a replicação do HBase em HDInsight](hdinsight-hbase-replication.md): Saiba como tooconfigure HBase replicação entre dois datacenters do Azure.
* [Analisar o sentimento do Twitter com HBase em HDInsight][hbase-twitter-sentiment]: Saiba como toodo em tempo real [análise de sentimento](http://en.wikipedia.org/wiki/Sentiment_analysis) de big data usando HBase em um cluster Hadoop no HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
