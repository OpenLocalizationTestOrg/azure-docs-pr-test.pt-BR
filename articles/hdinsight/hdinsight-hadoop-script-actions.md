---
title: "aaaScript desenvolvimento de ação com o HDInsight - Azure | Microsoft Docs"
description: "Saiba como toocustomize Hadoop clusters com ação de Script. Ação de script pode ser usado tooinstall software adicionais em execução em um cluster ou toochange Olá configuração Hadoop dos aplicativos instalados em um cluster."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Desenvolver scripts do Script de Ação para clusters baseados no Windows do HDInsight
Saiba como os scripts de toowrite ação de Script do HDInsight. Para obter informações sobre scripts de Ação de Script, consulte [Personalizar clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md). Para Olá mesmo artigo escrito para clusters HDInsight baseados em Linux, consulte [scripts de ação de Script desenvolver para HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Olá etapas para esse trabalho de documento somente para clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obter informações sobre como usar ações de script com clusters baseados no Linux, consulte [Desenvolvimento de ação de script com HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).
>
>



Ação de script pode ser usado tooinstall software adicionais em execução em um cluster ou toochange Olá configuração Hadoop dos aplicativos instalados em um cluster. Ações de script são scripts que são executados em nós de cluster hello quando os clusters de HDInsight são implantados, e eles são executados depois que nós no cluster Olá concluir a configuração do HDInsight. Uma ação de script é executada sob privilégios de conta de administrador do sistema e fornece direitos de acesso completo toohello nós de cluster. Cada cluster pode ser fornecido com uma lista de toobe de ações de script executado em ordem de saudação na qual elas são especificadas.

> [!NOTE]
> Se você enfrentar Olá a seguinte mensagem de erro:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: Olá termo 'Salvar HDIFile' não é reconhecido como nome de saudação de um cmdlet, função, arquivo de script ou programa operável. Verificar a ortografia de saudação do nome hello, ou se um caminho tiver sido incluído, verifique se que esse caminho hello está correto e tente novamente.
> É porque você não incluiu métodos auxiliares de saudação.  Consulte [Métodos auxiliares para scripts personalizados](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Exemplos de scripts
Para criar clusters HDInsight no sistema operacional Windows, Olá ação do Script é o script do PowerShell do Azure. Olá, script a seguir está um exemplo para configurar arquivos de configuração de site hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

script de saudação usa quatro parâmetros, nome do arquivo de configuração de hello, Olá propriedade toomodify, Olá valor tooset e uma descrição. Por exemplo:

    hive-site.xml hive.metastore.client.socket.timeout 90

Esses parâmetros define Olá hive.metastore.client.socket.timeout valor too90 no arquivo de hive-site.XML de saudação.  valor padrão de saudação é 60 segundos.

Este exemplo de script pode ser encontrado em [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight fornece vários scripts tooinstall os componentes adicionais em clusters de HDInsight:

| Nome | Script |
| --- | --- |
| **Instalar Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Consulte [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]. |
| **Instalar R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consulte [Instalar e usar o R em clusters HDInsight][hdinsight-r-scripts]. |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Instalar o Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md). |

Ação de script pode ser implantada de saudação portal do Azure, Azure PowerShell ou usando Olá HDInsight .NET SDK.  Para obter mais informações, consulte [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize].

> [!NOTE]
> scripts de exemplo Hello funcionam somente com a versão do cluster HDInsight 3.1 ou superior. Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Métodos auxiliares para scripts personalizados
Os métodos auxiliares da Ação de Script são recursos que podem ser usados durante a gravação de scripts personalizados. Esses métodos são definidos no [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)e pode ser incluído em seus scripts usando Olá exemplo a seguir:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Aqui estão os métodos auxiliares Olá que são fornecidos por esse script:

| Método auxiliar | Descrição |
| --- | --- |
| **Save-HDIFile** |Identificador de recurso uniforme (URI) tooa local especificado pelo download de um arquivo de saudação no disco local do hello associado ao cluster de toohello atribuído em nós Olá VM do Azure. |
| **Expand-HDIZippedFile** |Descompacte um arquivo compactado por zip. |
| **Invoke-HDICmdScript** |Execute um script por meio de cmd.exe. |
| **Write-HDILog** |Grave a saída do script personalizado hello, usado para uma ação de script. |
| **Get-Services** |Obter uma lista de serviços em execução na máquina de saudação em que executa o script hello. |
| **Get-Service** |Com o nome de serviço específico hello como entrada, obter informações detalhadas para um serviço específico (nome do serviço, o processo da ID, estado, etc.) no computador de saudação em que executa o script hello. |
| **Get-HDIServices** |Obter uma lista de serviços HDInsight em execução no computador de saudação em que executa o script hello. |
| **Get-HDIService** |Com hello HDInsight service nome específico como entrada, obter informações detalhadas para um serviço específico (nome do serviço, o processo da ID, estado, etc.) no computador de saudação em que executa o script hello. |
| **Get-ServicesRunning** |Obter uma lista de serviços em execução no computador de saudação em que executa o script hello. |
| **Get-ServiceRunning** |Verifique se um serviço específico (por nome) está em execução no computador de saudação em que executa o script hello. |
| **Get-HDIServicesRunning** |Obter uma lista de serviços HDInsight em execução no computador de saudação em que executa o script hello. |
| **Get-HDIServiceRunning** |Verifique se um serviço HDInsight específico (por nome) está em execução no computador de saudação em que executa o script hello. |
| **Get-HDIHadoopVersion** |Obter a versão de saudação do Hadoop instalado no computador de saudação em que executa o script hello. |
| **Test-IsHDIHeadNode** |Verifique se o computador Olá em que executa o script hello é um nó de cabeçalho. |
| **Test-IsActiveHDIHeadNode** |Verifique se o computador Olá em que executa o script hello é um nó principal ativo. |
| **Test-IsHDIDataNode** |Verifique se o computador de saudação em que executa o script hello é um nó de dados. |
| **Edit-HDIConfigFile** |Edite saudação config arquivos hive-site.XML, Core-site.XML, HDFS-site.XML, mapred-site.XML ou yarn-site.XML. |

## <a name="best-practices-for-script-development"></a>Práticas recomendadas para o desenvolvimento de scripts
Quando você desenvolve um script personalizado para um cluster HDInsight, há vários tookeep práticas recomendadas em mente:

* Verificação de versão do Hadoop Olá

    HDInsight versão 3.1 (Hadoop 2.4) e acima usando componentes personalizados de tooinstall de ação de Script em um cluster. No seu script personalizado, você deve usar o hello **Get-HDIHadoopVersion** versão do Hadoop auxiliar método toocheck Olá antes de continuar a executar outras tarefas no script hello.
* Fornecer estável links tooscript recursos

    Os usuários assegure-se de que todos os scripts de saudação e outros artefatos usados na personalização de saudação de um cluster permanecem disponíveis ao longo do tempo de vida de saudação do cluster hello e que versões Olá desses arquivos não são alterados durante a saudação. Esses recursos são necessários se Olá refazendo as imagens de nós no cluster de saudação é necessária. prática recomendada Olá é toodownload e arquivar tudo em uma conta de armazenamento que Olá controles de usuário. Isso pode ser a conta de armazenamento saudação padrão ou qualquer uma das contas de armazenamento adicionais Olá especificadas no momento da saudação de implantação para um cluster personalizado.
    No hello Spark e R personalizado exemplos de cluster fornecido na documentação do hello, por exemplo, fizemos uma cópia local dos recursos de saudação nesta conta de armazenamento: https://hdiconfigactions.blob.core.windows.net/.
* Certifique-se de que o script de personalização de cluster Olá é idempotente

    Você deve esperar que nós de saudação de um cluster HDInsight recriar a imagem durante o tempo de vida do hello cluster. script de personalização de cluster Olá é executado sempre que recriar a imagem de um cluster. Esse script deve ser projetado toobe idempotente no sentido de saudação que, após a imagem, script hello deve garantir que cluster Olá é retornado toohello que mesmo personalizado estado que estava apenas após a execução de script hello para Olá primeira vez em que o cluster Olá foi inicialmente criado. Por exemplo, se um script personalizado instalado um aplicativo em D:\AppLocation em sua primeira execução, em cada execução subsequente, após a imagem, script hello deve verificar se o aplicativo hello existe em Olá D:\AppLocation local antes de continuar com os outros etapas no script hello.
* Instalar componentes personalizados em local ideal de saudação

    Quando nós de cluster são imagem refeitos, unidade de recurso Olá C:\ e D:\ unidade do sistema podem ser reformatados, resultando na perda de saudação de dados e aplicativos que estavam instalados nessas unidades. Isso também pode acontecer se um nó de máquina virtual do Azure (VM) que faz parte do cluster Olá cair e é substituído por um novo nó. Você pode instalar componentes Olá unidade D:\ ou no local de c:\Apps. Olá no cluster hello. Todos os outros locais na unidade C:\ de saudação são reservados. Especifique o local de Olá onde bibliotecas ou aplicativos são toobe instalado no script de personalização de cluster hello.
* Garantir a alta disponibilidade da arquitetura de cluster Olá

    HDInsight tem uma arquitetura de ativo-passivo para alta disponibilidade, no qual um nó de cabeçalho está no modo ativo (onde Olá HDInsight serviços estão em execução) e hello outros nó principal está em modo de espera (no qual HDInsight serviços são não em execução). nós Olá alternar modos ativos e passivos se serviços HDInsight são interrompidos. Se uma ação de script é serviços tooinstall usadas em ambos os nós principal de alta disponibilidade, observe que esse mecanismo de failover do HDInsight Olá não é capaz de tooautomatically falha esses serviços instalados pelo usuário. Serviços instalados pelo usuário assim em nós de cabeçalho de HDInsight que são esperado toobe altamente disponível devem ter seu próprio mecanismo de failover no modo ativo-passivo ou estar no modo ativo-ativo.

    Um comando HDInsight ação de Script é executado em ambos os nós principal quando a função de nó de cabeçalho de saudação é especificada como um valor em hello *ClusterRoleCollection* parâmetro. Então, quando você cria um script personalizado, verifique se o script está ciente dessa configuração. Você não deve executar problemas onde hello mesmos serviços são instalados e iniciados nos dois nós de cabeçalho hello e acabam compitam entre si. Além disso, esteja ciente de que dados sejam perdidos durante refazer, portanto software instalado por meio de ação de Script tem toobe toosuch resiliente eventos. Aplicativos devem ser toowork projetado com dados altamente disponíveis que são distribuídos entre vários nós. Observe que até 1/5 nós de saudação em um cluster pode ter sua imagem recriada no hello simultaneamente.
* Configurar o armazenamento de BLOBs do Azure em toouse Olá componentes personalizados

    componentes personalizados de saudação que você instala em nós de cluster Olá podem ter uma configuração de padrão toouse armazenamento de sistema de arquivos distribuído da Hadoop (HDFS). Em vez disso, você deve alterar a saudação configuração toouse armazenamento de BLOBs do Azure. Em uma nova imagem de cluster, sistema de arquivos HDFS Olá obtém formatado e você perderia todos os dados armazenados nelas. Usar o Armazenamento de Blobs do Azure em vez dela assegura que seus dados serão mantidos.

## <a name="common-usage-patterns"></a>Padrões comuns de uso
Esta seção fornece orientação sobre como implementar alguns Olá padrões comuns de uso que você pode encontrar ao gravar seu próprio script personalizado.

### <a name="configure-environment-variables"></a>Configurar variáveis de ambiente
Geralmente no desenvolvimento de ação de script, você se sentir Olá necessário tooset variáveis de ambiente. Por exemplo, um cenário mais provável é quando você baixar um binário de um site externo, instalá-lo no cluster hello e adicionar Olá local de onde é variável de ambiente 'PATH' tooyour instalado. saudação de trecho de código a seguir mostra como variáveis de ambiente tooset Olá script personalizado.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Essa instrução define a variável de ambiente Olá **MDS_RUNNER_CUSTOM_CLUSTER** toohello valor 'true' e também conjuntos Olá escopo essa variável toobe todo o computador. Às vezes é importante que as variáveis de ambiente são definidas no escopo apropriado hello – máquina ou usuário. Consulte [aqui][1] para obter mais informações sobre como configurar variáveis de ambiente.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Acesso toolocations onde são armazenados os scripts personalizados Olá
Scripts usados toocustomize tooeither de necessidades de um cluster ser na conta de armazenamento padrão Olá para cluster hello, ou em um contêiner público somente leitura em qualquer outra conta de armazenamento. Se seu script acessa os recursos localizados em outro lugar necessário toobe em publicamente acessível (pelo menos pública somente leitura). Por exemplo, você pode deseja tooaccess um arquivo e salve-o usando o comando Olá SaveFile HDI.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

Neste exemplo, você deve garantir que esse contêiner de saudação 'somecontainer' em 'somestorageaccount' conta de armazenamento é acessível publicamente. Caso contrário, o script hello lança uma exceção 'Não encontrado' e falhar.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Passar parâmetros toohello adicionar AzureRmHDInsightScriptAction cmdlet
toopass vários cmdlet de toohello AzureRmHDInsightScriptAction adicionar parâmetros, você precisa tooformat toocontain de valor de cadeia de caracteres de saudação todos os parâmetros para o script hello. Por exemplo:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

ou o

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Lançar exceção para implantação de cluster malsucedida
Se você quiser tooget notificado com precisão de fato Olá essa personalização de cluster não foi bem-sucedida, conforme o esperado, é importante toothrow uma exceção e falha de criação do cluster hello. Por exemplo, talvez desejado tooprocess um arquivo se ele existe e lidar com hello erro caso em que o arquivo hello não existe. Isso garantiria que sai do script hello normalmente e estado de saudação do cluster Olá corretamente é conhecido. Olá, trecho a seguir fornece um exemplo de como tooachieve isso:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

Neste trecho, se o arquivo hello não existir, ele resultaria tooa estado onde script hello, na verdade, foi encerrado normalmente após imprimir a mensagem de erro de saudação e cluster Olá atinge o estado de execução, supondo que ele concluir o processo de personalização de cluster "com êxito". Se você quiser toobe notificado com precisão de fato Olá que a personalização cluster essencialmente não teve êxito conforme o esperado, devido à falta de um arquivo, ele é mais apropriado toothrow uma exceção e falha Olá etapa de personalização de cluster. tooachieve isso você deve usar o hello trecho de código de exemplo a seguir em vez disso.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Lista de verificação para implantação de uma ação de script
Aqui estão as etapas Olá que demos ao preparar toodeploy esses scripts:

1. Coloca os arquivos de saudação que contêm scripts personalizados de saudação em um local que seja acessível por nós de cluster Olá durante a implantação. Isso pode ser qualquer um dos padrão hello ou outras contas de armazenamento especificadas no momento da saudação de implantação de cluster ou qualquer outro contêiner de armazenamento acessíveis publicamente.
2. Adicionar verificações em scripts toomake-se de que elas são executadas de forma idempotencial, para que o script hello pode ser executado várias vezes em Olá mesmo nó.
3. Saudação de uso **Write-Output** tooSTDOUT de tooprint de cmdlet do PowerShell do Azure, bem como para STDERR. Não use **Write-Host**.
4. Usar uma pasta de arquivo temporário, como $env: TEMP, tookeep Olá usado pelos scripts de saudação de arquivo baixado e, em seguida, limpá-los depois de scripts foram executadas.
5. Instale o software personalizado apenas em D:\ ou C:\apps. Outros locais na Olá unidade c: não devem ser usados como elas estão reservadas. Observe que instalando arquivos na unidade c: de saudação fora da pasta de c:\Apps. Olá pode resultar em falhas de instalação durante a reimages do nó de saudação.
6. Evento de saudação se as configurações de nível de sistema operacional ou arquivos de configuração do serviço de Hadoop foram alterados, convém toorestart HDInsight serviços para que eles podem acompanhar as configurações de nível de sistema operacional, como variáveis de ambiente Olá set em scripts de saudação.

## <a name="debug-custom-scripts"></a>Depurar scripts personalizados
logs de erros de script Hello são armazenados, junto com outra saída, na conta de armazenamento do saudação padrão que você especificou para o cluster de saudação em sua criação. Olá logs são armazenados em uma tabela com o nome da saudação *u < \cluster-name-fragment >< \time-stamp > setuplog*. Esses são os logs agregados que têm registros de todos os nós de saudação (nó principal e nós de trabalho) no qual Olá o script é executado no cluster hello.
Uma maneira fácil toocheck Olá logs é toouse das ferramentas de HDInsight para Visual Studio. Para instalar as ferramentas de hello, consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**log de saudação toocheck usando o Visual Studio**

1. Abra o Visual Studio.
2. Clique em **Exibição**, e clique em **Gerenciador de Servidores**.
3. Clique com botão direito "Azure", clique em conectar muito**assinatura do Microsoft Azure**e, em seguida, insira suas credenciais.
4. Expanda **armazenamento**, expanda a conta de armazenamento do Azure Olá usada como o sistema de arquivos padrão hello, **tabelas**e, em seguida, clique duas vezes no nome da tabela hello.

Você pode também remoto em toosee de nós de cluster Olá STDOUT e STDERR de scripts personalizados. Olá logs em cada nó são específicos somente toothat nó e estão conectados ao **C:\HDInsightLogs\DeploymentAgent.log**. Esses arquivos de log registram todas as saídas de script personalizado hello. Um exemplo de trecho do log para uma Ação de Script de Spark deve ser assim:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


Esse log, fica claro que ação de script hello Spark foi executada em Olá VM denominada HEADNODE0 e que não há exceções foram iniciadas durante a execução de saudação.

No caso de Olá ocorre uma falha na execução, Olá saída que ele descreve também está contida no arquivo de log. informações de saudação fornecidas nesses logs devem ser útil na depuração de problemas de script que podem surgir.

## <a name="see-also"></a>Consulte também
* [Personalizar os clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]
* [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]
* [Instalar e usar R em clusters do HDInsight][hdinsight-r-scripts]
* [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).
* [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
