---
title: aaaUse SSH com Hadoop - HDInsight do Azure | Microsoft Docs
description: "Você pode acessar o HDInsight usando o Secure Shell (SSH). Este documento fornece informações sobre como conectar tooHDInsight usando Olá ssh e comandos de scp de clientes Windows, Linux, Unix ou macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: hadoop comandos no linux, comandos do linux hadoop, hadoop macos, ssh hadoop, ssh cluster hadoop
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Conecte-se tooHDInsight (Hadoop) usando o SSH

Saiba como toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely conectar tooHadoop no Azure HDInsight. 

HDInsight pode usar Linux (Ubuntu) como sistema operacional de saudação para nós de cluster de Hadoop hello. Olá tabela a seguir contém informações de endereço e porta de saudação necessárias ao se conectar com base em tooLinux HDInsight usando um cliente SSH:

| Endereço | Porta | Conecta-se a... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Nó de borda (Servidor R no HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Nó de borda (qualquer outro tipo de cluster, se existir um nó de borda) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Nó de cabeçalho primário |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Nó de cabeçalho secundário |

> [!NOTE]
> Substituir `<edgenodename>` com o nome de saudação do nó de borda hello.
>
> Substituir `<clustername>` com nome de saudação do cluster.
>
> Se o cluster contém um nó de borda, é recomendável que você __sempre se conectam nó de borda toohello__ usando o SSH. nós de cabeçalho Olá hospedar serviços de integridade crítico toohello do Hadoop. nó de borda Olá executa apenas o que é colocado sobre ele.
>
> Para obter mais informações sobre o uso de nós de borda, confira [Usar nós de borda no HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>Clientes SSH

Os sistemas Linux, Unix e macOS fornecem Olá `ssh` e `scp` comandos. Olá `ssh` cliente é comumente usada toocreate uma sessão de linha de comando remoto com um sistema baseado em Unix ou Linux. Olá `scp` cliente é usado toosecurely copiar arquivos entre o sistema remoto de cliente e hello.

Por padrão, o Microsoft Windows não fornece clientes SSH. Olá `ssh` e `scp` clientes estão disponíveis para o Windows por meio de saudação pacotes a seguir:

* [Shell de nuvem do Azure](../cloud-shell/quickstart.md): Olá Shell nuvem fornece um ambiente de Bash no seu navegador e fornece Olá `ssh`, `scp`e outros comandos comuns do Linux.

* [Bash no Ubuntu no Windows 10](https://msdn.microsoft.com/commandline/wsl/about): Olá `ssh` e `scp` comandos estão disponíveis por meio de saudação Bash na linha de comando do Windows.

* [Git (https://git-scm.com/)](https://git-scm.com/): Olá `ssh` e `scp` comandos estão disponíveis por meio da linha de comando GitBash hello.

* [Área de trabalho do GitHub (https://desktop.github.com/)](https://desktop.github.com/) Olá `ssh` e `scp` comandos estão disponíveis por meio de saudação de linha de comando do Shell do GitHub. Área de trabalho do GitHub pode ser configurado toouse Bash, Olá Prompt de comando do Windows ou o PowerShell como saudação de linha de comando para Olá Git Shell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): Olá PowerShell equipe é movimentando OpenSSH tooWindows e fornece versões de teste.

    > [!WARNING]
    > pacote de OpenSSH Olá inclui o componente de servidor SSH Olá, `sshd`. Este componente inicia um servidor SSH no sistema, permitindo que outras pessoas tooconnect tooit. Não configurar esse componente ou abrir a porta 22, a menos que você deseja toohost um servidor SSH no sistema. Não é necessário toocommunicate com HDInsight.

Também há vários clientes SSH gráficos, como [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) e [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Embora esses clientes possam ser usados tooconnect tooHDInsight, processo de saudação de conexão é diferente de usar Olá `ssh` utilitário. Para obter mais informações, consulte a documentação de saudação do cliente gráfica hello, que você está usando.

## <a id="sshkey"></a>Autenticação: chaves SSH

SSH chaves usam [criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessões. As chaves de SSH são mais seguras que senhas e fornecem um cluster de Hadoop maneira fácil toosecure acesso tooyour.

Se sua conta SSH é protegida usando uma chave, o cliente de saudação deve fornecer Olá correspondência de chave privada quando você se conectar:

* A maioria dos clientes pode ser configurado toouse um __chave padrão__. Por exemplo, Olá `ssh` cliente procura uma chave privada no `~/.ssh/id_rsa` em ambientes Linux e Unix.

* Você pode especificar Olá __chave privada do caminho tooa__. Com hello `ssh` client, Olá `-i` parâmetro é a chave de tooprivate toospecify usado Olá caminho. Por exemplo: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Se você tiver __várias chaves privadas__ para uso com servidores diferentes, considere usar um utilitário como [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Olá `ssh-agent` utilitário pode ser usado tooautomatically Olá selecione chave toouse ao estabelecer uma sessão SSH.

> [!IMPORTANT]
>
> Se você proteger sua chave privada com uma senha, você deve inserir Olá senha ao usar a chave de saudação. Utilitários, como `ssh-agent` pode armazenar em cache senha Olá para sua conveniência.

### <a name="create-an-ssh-key-pair"></a>Criar um par de chaves SSH

Saudação de uso `ssh-keygen` arquivos de chave pública e privada toocreate de comando. Olá comando a seguir gera um par de chaves de RSA de 2048 bits que pode ser usado com o HDInsight:

    ssh-keygen -t rsa -b 2048

Você será solicitado para obter informações durante o processo de criação da chave de saudação. Por exemplo, onde chaves de saudação são armazenadas ou se toouse uma frase secreta. Após a conclusão do processo de saudação, dois arquivos são criados; uma chave pública e uma chave privada.

* Olá __chave pública__ é toocreate usado um cluster HDInsight. chave pública Olá tem uma extensão de `.pub`.

* Olá __chave privada__ é tooauthenticate usado ao cluster do HDInsight toohello cliente.

> [!IMPORTANT]
> Você pode proteger as chaves usando uma frase secreta. Uma frase secreta é efetivamente uma senha na chave privada. Mesmo se alguém obtiver sua chave privada, eles devem ter a chave de Olá Olá senha toouse.

### <a name="create-hdinsight-using-hello-public-key"></a>Criar usando a chave pública de saudação do HDInsight

| Método de criação | Como toouse Olá chave pública |
| ------- | ------- |
| **Portal do Azure** | Desmarque __usar a mesma senha de logon de cluster__e, em seguida, selecione __chave pública__ como Olá o tipo de autenticação SSH. Por fim, selecione o arquivo de chave pública hello ou colar conteúdo de texto de saudação do arquivo hello Olá __chave pública SSH__ campo.</br>![Caixa de diálogo de chave pública SSH na criação do cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **PowerShell do Azure** | Saudação de uso `-SshPublicKey` parâmetro hello `New-AzureRmHdinsightCluster` cmdlet e passe conteúdo Olá de chave pública do hello como uma cadeia de caracteres.|
| **CLI 1.0 do Azure** | Saudação de uso `--sshPublicKey` parâmetro hello `azure hdinsight cluster create` de comando e passar o conteúdo de saudação de chave pública hello como uma cadeia de caracteres. |
| **Modelo do Resource Manager** | Para obter um exemplo de como usar chaves SSH com um modelo, confira [Implantar o HDInsight no Linux com uma chave SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/). Olá `publicKeys` elemento Olá [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) arquivo é usado toopass Olá chaves tooAzure ao criar cluster hello. |

## <a id="sshpassword"></a>Autenticação: senha

Contas SSH podem ser protegidas usando uma senha. Quando você conectar tooHDInsight usando SSH, você é solicitadas tooenter Olá por senha.

> [!WARNING]
> Não recomendamos o uso da autenticação de senha para o SSH. As senhas podem ser adivinhadas e são vulneráveis toobrute ataques de força. Em vez disso, é recomendável usar [chaves SSH para autenticação](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Criar o HDInsight usando uma senha

| Método de criação | Como toospecify Olá senha |
| --------------- | ---------------- |
| **Portal do Azure** | Por padrão, a saudação conta de usuário SSH tem Olá mesma senha como a conta de logon de cluster hello. toouse uma senha diferente, desmarque __usar a mesma senha de logon de cluster__e, em seguida, digite a senha de saudação na Olá __senha SSH__ campo.</br>![Caixa de diálogo de senha SSH na criação do cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **PowerShell do Azure** | Saudação de uso `--SshCredential` parâmetro hello `New-AzureRmHdinsightCluster` cmdlet e passar uma `PSCredential` objeto que contém o nome da conta de usuário do hello SSH e uma senha. |
| **CLI 1.0 do Azure** | Saudação de uso `--sshPassword` parâmetro hello `azure hdinsight cluster create` de comando e forneça o valor da senha hello. |
| **Modelo do Resource Manager** | Para obter um exemplo de como usar uma senha com um modelo, confira [Implantar o HDInsight no Linux com uma senha SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). Olá `linuxOperatingSystemProfile` elemento Olá [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) arquivo é usado toopass Olá SSH conta nome e senha tooAzure ao criar cluster hello.|

### <a name="change-hello-ssh-password"></a>Alterar a senha Olá SSH

Para obter informações sobre como alterar a senha de conta de usuário SSH hello, consulte Olá __alterar senhas__ seção Olá [HDInsight gerenciar](hdinsight-administer-use-portal-linux.md#change-passwords) documento.

## <a id="domainjoined"></a>Autenticação: HDInsight associado ao domínio

Se você estiver usando um __domínio cluster do HDInsight__, você deve usar o hello `kinit` comando após a conexão com o SSH. Este comando solicita um usuário de domínio e uma senha e autentica a sessão com o domínio do Active Directory do Azure Olá associado Olá cluster.

Para obter mais informações, confira [Configurar o HDInsight associado ao domínio](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Conecte-se toonodes

Olá nós principal e o nó de borda (se houver) podem ser acessados pela Olá internet nas portas 22 e 23.

* Ao conectar-se toohello __nós de cabeçalho__, usar a porta __22__ tooconnect toohello primário head nó e a porta __23__ toohello tooconnect secundário nó principal. Olá toouse de nome de domínio totalmente qualificado é `clustername-ssh.azurehdinsight.net`, onde `clustername` é o nome de saudação do cluster.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Quando connectiung toohello __nó de borda__, use a porta 22. Olá, nome de domínio totalmente qualificado é `edgenodename.clustername-ssh.azurehdinsight.net`, onde `edgenodename` é um nome que você forneceu ao criar nó de borda de saudação. `clustername`é o nome de saudação do cluster de saudação.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> exemplos anteriores Olá pressupõem que você estiver usando a autenticação de senha ou autenticação de certificado que está ocorrendo automaticamente. Se você usar um par de chaves SSH para autenticação e Olá não será usado automaticamente, use Olá `-i` chave privada do parâmetro toospecify hello. Por exemplo: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Uma vez conectado, prompt Olá altera tooindicate Olá SSH usuário nome e hello nó que você está conectado. Por exemplo, quando conectado toohello nó de cabeçalho principal como `sshuser`, Olá prompt é `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Conecte-se tooworker e nós Zookeeper

Olá nós de trabalho e Olá de Zookeeper nós não são diretamente acessíveis pela internet. Eles podem ser acessados de nós de cabeçalho Olá cluster ou nós de borda. Olá seguem nós de tooother de tooconnect Olá etapas gerais:

1. Use o nó de cabeçalho ou borda de tooa de tooconnect do SSH:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Olá head de toohello conexão SSH ou nó de borda, use Olá `ssh` comando tooconnect tooa trabalho nó Olá cluster:

        ssh sshuser@wn0-myhdi

    tooretrieve uma lista de nomes de domínio Olá de nós de saudação do cluster de hello, consulte Olá [HDInsight gerenciar usando Olá API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) documento.

Se Olá conta SSH é protegida usando um __senha__, digite a senha de saudação ao se conectar.

Se Olá conta SSH é protegida usando __chaves SSH__, certifique-se de que o encaminhamento de SSH está habilitado no cliente de saudação.

> [!NOTE]
> Outra maneira toodirectly acessar todos os nós no cluster de saudação é tooinstall HDInsight em uma rede Virtual do Azure. Em seguida, você pode ingressar em sua máquina remota toohello mesmo virtual de rede e acessar diretamente a todos os nós no cluster de saudação.
>
> Para obter mais informações, confira [Usar uma rede virtual com o HDInsight](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>Configurar o encaminhamento do agente SSH

> [!IMPORTANT]
> Hello etapas a seguir assumem um sistema baseado em UNIX ou Linux e trabalhar com Bash no Windows 10. Se essas etapas não funcionam para o seu sistema, talvez seja necessário tooconsult documentação de saudação de seu cliente SSH.

1. Usando um editor de texto, abra `~/.ssh/config`. Se esse arquivo não existir, você poderá criá-lo digitando `touch ~/.ssh/config` na linha de comando.

2. Adicionar Olá toohello de texto a seguir `config` arquivo.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Substituir saudação __Host__ informações com o endereço de saudação do nó de saudação você conectar toousing SSH. exemplo anterior Hello usa o nó de borda hello. Essa entrada configura agente SSH de encaminhamento para o nó especificado hello.

3. Teste de agente SSH de encaminhamento usando Olá Olá terminal após o comando:

        echo "$SSH_AUTH_SOCK"

    Esse comando retorna informações toohello semelhante texto a seguir:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Se nada for retornado, o `ssh-agent` não estará em execução. Para obter mais informações, consulte informações sobre scripts de inicialização de agente do hello em [usando ssh agente com ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) ou consulte a documentação do cliente SSH.

4. Depois de ter verificado que **ssh agente** está em execução, use Olá após tooadd seu agente de toohello chave privada SSH:

        ssh-add ~/.ssh/id_rsa

    Se a chave privada é armazenada em um arquivo diferente, substitua `~/.ssh/id_rsa` com hello caminho toohello arquivo.

5. Conecte-se de nó de borda toohello cluster ou nós de cabeçalho usando o SSH. Em seguida, use Olá SSH comando tooconnect tooa trabalhador ou um nó de zookeeper. conexão de saudação é estabelecida usando a chave Olá encaminhado.

## <a name="copy-files"></a>Copiar arquivos

Olá `scp` utilitário pode ser usado toocopy arquivos tooand de nós individuais Olá cluster. Por exemplo, Olá Olá de cópias de comando a seguir `test.txt` diretório de saudação sistema local toohello principal nó primário:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Porque nenhum caminho for especificado depois Olá `:`, arquivo de saudação é colocado no hello `sshuser` diretório base.

Olá Olá de cópias de exemplo a seguir `test.txt` arquivo hello `sshuser` diretório base no sistema local do toohello Olá primário nó principal:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`só pode acessar o sistema de arquivos de saudação de nós individuais no cluster hello. Ele não pode ser usado tooaccess dados armazenados Olá HDFS compatível com cluster hello.
>
> Use `scp` quando você precisa de um recurso de tooupload para uso em uma sessão SSH. Por exemplo, carregar um script Python e, em seguida, execute o script de saudação de uma sessão SSH.
>
> Para obter informações sobre como carregar diretamente os dados em Olá armazenamento compatível com o HDFS, consulte Olá documentos a seguir:
>
> * [HDInsight usando o Armazenamento do Azure](hdinsight-hadoop-use-blob-storage.md).
>
> * [HDInsight usando o Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Próximas etapas

* [Usar o túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)
* [Usar uma rede virtual com o HDInsight](hdinsight-extend-hadoop-virtual-network.md)
* [Usar nós de borda no HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node)