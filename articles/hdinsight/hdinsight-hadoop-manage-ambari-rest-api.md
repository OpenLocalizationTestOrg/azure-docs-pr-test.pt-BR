---
title: aaaMonitor e gerenciar Hadoop com API REST do Ambari - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Ambari toomonitor e gerenciar clusters Hadoop em HDInsight do Azure. Neste documento, você aprenderá como clusters de toouse Olá API REST do Ambari incluídos no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Gerenciar clusters HDInsight usando Olá Ambari REST API

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Saiba como toouse Olá toomanage Ambari REST API e monitorar clusters Hadoop em HDInsight do Azure.

Apache Ambari simplifica o gerenciamento de saudação e monitoramento de um cluster de Hadoop, fornecendo a interface do usuário e REST API toouse fácil da web. Ambari é incluído em clusters de HDInsight que usam o sistema de operacional Linux hello. Você pode usar o cluster de saudação do Ambari toomonitor e fazer alterações de configuração.

## <a id="whatis"></a>O que é o Ambari

[Apache Ambari](http://ambari.apache.org) fornece a interface que pode ser usado tooprovision, gerenciar e monitorar clusters Hadoop da web. Os desenvolvedores podem integrar esses recursos em seus aplicativos usando Olá [APIs de REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari é fornecido por padrão com os clusters HDInsight baseados em Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>Como toouse Olá Ambari REST API

> [!IMPORTANT]
> informações de saudação e exemplos neste documento exigem um cluster HDInsight que usa o sistema operacional Linux. Para saber mais, confira [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

exemplos de saudação neste documento são fornecidos para o shell Bourne de saudação (bash) e o PowerShell. bash Olá exemplos foram testados com GNU bash 4.3.11, mas devem funcionar com outros shells do Unix. exemplos do PowerShell Olá foram testados com o PowerShell 5.0, mas devem funcionar com o PowerShell 3.0 ou superior.

Se usar o hello __shell Bourne__ (Bash), você deve ter o seguinte Olá instalado:

* [cURL](http://curl.haxx.se/): Ondulação é um utilitário que pode ser usado toowork com APIs de REST da linha de comando de saudação. Neste documento, é usado toocommunicate com hello API REST do Ambari.

Se usar Bash ou o PowerShell, você também deverá ter o [jq](https://stedolan.github.io/jq/) instalado. Jq é um utilitário para trabalhar com documentos JSON. Ele é usado em **todos os** Olá Bash exemplos, e **um** de exemplos do PowerShell hello.

### <a name="base-uri-for-ambari-rest-api"></a>Base de URI para a API de Rest do Ambari

Olá, URI de base para Olá API REST do Ambari no HDInsight é https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, onde **CLUSTERNAME** é o nome de saudação do cluster.

> [!IMPORTANT]
> Enquanto o nome do cluster Olá no hello totalmente qualificado parte do nome (FQDN) do domínio de saudação URI (CLUSTERNAME.azurehdinsight.net) diferencia maiusculas de minúsculas, outras ocorrências em Olá URI diferenciam maiusculas de minúsculas. Por exemplo, se o cluster é denominado `MyCluster`, Olá seguem URIs válidos:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> seguir Olá URIs retornará um erro porque Olá segunda ocorrência do nome de saudação não é Olá corrija caso.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Autenticação

Conexão tooAmbari no HDInsight requer HTTPS. Nome de conta de administrador use hello (Olá padrão é **admin**) e a senha fornecidos durante a criação do cluster.

## <a name="examples-authentication-and-parsing-json"></a>Exemplos: Autenticação e analisando o JSON

Olá exemplos a seguir demonstram como toomake uma solicitação GET hello base Ambari REST API:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> exemplos de Bash Olá neste documento fazer Olá seguintes suposições:
>
> * nome de logon de Olá para cluster Olá é o valor padrão de saudação do `admin`.
> * `$PASSWORD`contém a senha Olá Olá comando de login do HDInsight. Você pode definir esse valor usando `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`contém o nome de saudação do cluster hello. Você pode definir esse valor usando `set CLUSTERNAME='clustername'`

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> exemplos do PowerShell Olá neste documento fazer Olá seguintes suposições:
>
> * `$creds`é um objeto de credencial que contém o logon de administrador hello e a senha para o cluster hello. Você pode definir esse valor usando `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` e fornecer credenciais de saudação quando solicitado.
> * `$clusterName`é uma cadeia de caracteres que contém o nome de saudação do cluster de saudação. Você pode definir esse valor usando `$clusterName="clustername"`.

Os dois exemplos retornam um documento JSON que começa com informações toohello semelhante exemplo a seguir:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Analisar dados JSON

Olá exemplo a seguir usa `jq` tooparse Olá documento de resposta JSON e exibir somente Olá `health_report` informações dos resultados de saudação.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 e superior fornece Olá `ConvertFrom-Json` cmdlet, que converte o documento JSON de saudação em um objeto que é mais fácil toowork do PowerShell. Olá exemplo a seguir usa `ConvertFrom-Json` Olá somente toodisplay `health_report` informações dos resultados de saudação.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Embora a maioria dos exemplos deste documento usam `ConvertFrom-Json` toodisplay elementos do documento de resposta hello, Olá [Ambari de atualização de configuração](#example-update-ambari-configuration) exemplo usa jq. Jq é usado em tooconstruct Este exemplo um novo modelo de documento de resposta JSON hello.

Para obter uma referência completa de saudação API REST, consulte [V1 de referência de API do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Exemplo: Obter Olá FQDN de nós de cluster

Ao trabalhar com HDInsight, talvez seja necessário um nome de domínio totalmente qualificado de saudação tooknow (FQDN) de um nó de cluster. Você pode recuperar facilmente hello FQDN para Olá vários nós no cluster hello usando Olá exemplos a seguir:

* **Todos os nós**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **Nós de cabeçalho**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nós de trabalho**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nós do Zookeeper**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Exemplo: Obter o endereço IP interno de saudação de nós de cluster

> [!IMPORTANT]
> endereços IP de saudação retornados por exemplos Olá nesta seção são não diretamente acessível via Olá da internet. Eles são acessíveis apenas dentro de saudação rede Virtual do Azure que contém o cluster do HDInsight hello.
>
> Para saber mais sobre como trabalhar com o HDInsight e com as redes virtuais, veja [Estender os recursos do HDInsight usando a Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).

endereço IP de saudação toofind, você deve saber Olá interno nome totalmente qualificado (FQDN) do hello nós de cluster. Depois que você tiver Olá FQDN, em seguida, você pode obter endereço IP de saudação do host de saudação. Olá exemplos a seguir primeiro consultar Ambari Olá FQDN de todos os nós de host hello e consultar Ambari para o endereço IP de saudação de cada host.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Exemplo: Obter armazenamento padrão da saudação

Quando você cria um cluster HDInsight, você deve usar uma conta de armazenamento do Azure ou um repositório Data Lake como armazenamento de padrão de saudação para cluster hello. Você pode usar essas informações de Ambari tooretrieve depois Olá cluster foi criado. Por exemplo, se você quiser que o contêiner de toohello tooread/gravação dados fora do HDInsight.

Olá exemplos a seguir recuperar configuração de armazenamento padrão de saudação do cluster hello:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Esses exemplos retornam o primeiro servidor de toohello configuração aplicada hello (`service_config_version=1`) que contém essas informações. Se você recuperar um valor que foi modificado após a criação do cluster, você pode precisa toolist Olá configuração versões e recuperar hello mais recente.

valor de retorno de saudação é semelhante tooone de saudação exemplos a seguir:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Este valor indica que o cluster hello está usando uma conta de armazenamento do Azure para armazenamento padrão. Olá `ACCOUNTNAME` valor é o nome de Olá Olá da conta de armazenamento. Olá `CONTAINER` parte é o nome de Olá Olá do contêiner de blob na conta de armazenamento hello. contêiner de saudação é raiz Olá Olá armazenamento compatíveis do HDFS para cluster hello.

* `adl://home`-Este valor indica que o cluster hello está usando um repositório Data Lake do Azure para armazenamento padrão.

    Olá toofind nome de conta do repositório Data Lake, use Olá exemplos a seguir:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Olá valor de retorno é semelhante muito`ACCOUNTNAME.azuredatalakestore.net`, onde `ACCOUNTNAME` é o nome de saudação do hello conta do repositório Data Lake.

    diretório de saudação toofind dentro do repositório Data Lake que contém o armazenamento Olá Olá cluster, use Olá exemplos a seguir:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Olá valor de retorno é semelhante muito`/clusters/CLUSTERNAME/`. Esse valor é um caminho dentro Olá conta do repositório Data Lake. Esse caminho é a raiz de saudação de sistema de arquivos compatíveis do HDFS para o cluster de saudação do hello. 

> [!NOTE]
> Olá `Get-AzureRmHDInsightCluster` cmdlet fornecido pelo [Azure PowerShell](/powershell/azure/overview) também retorna Olá informações de armazenamento de cluster hello.


## <a name="example-get-configuration"></a>Exemplo: obter configuração

1. Obter configurações de saudação que estão disponíveis para seu cluster.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Este exemplo retorna um documento JSON que contém a configuração atual da saudação (identificada pelo Olá *marca* valor) para componentes de saudação instalados no cluster hello. Olá, exemplo a seguir é um trecho da saudação dados retornados de um tipo de cluster do Spark.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Obter a configuração Olá componente Olá que você está interessado. Olá seguinte exemplo, substitua `INITIAL` com valor de marca Olá retornado da solicitação anterior de saudação.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Este exemplo retorna um documento JSON que contém a configuração atual Olá Olá `core-site` componente.

## <a name="example-update-configuration"></a>Exemplo: Atualizar a configuração

1. Obter a configuração atual do hello, que armazena o Ambari como hello "configuração desejada":

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Este exemplo retorna um documento JSON que contém a configuração atual da saudação (identificada pelo Olá *marca* valor) para componentes de saudação instalados no cluster hello. Olá, exemplo a seguir é um trecho da saudação dados retornados de um tipo de cluster do Spark.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    Nesta lista, você precisa toocopy nome de saudação do componente de saudação (por exemplo, **spark\_thrift\_sparkconf** e hello **marca** valor.

2. Recupere a configuração de saudação do componente hello e marca usando Olá comandos a seguir:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Substituir **spark-thrift-sparkconf** e **inicial** com componente hello e marca que você deseja tooretrieve Olá configuração para.
   
    Jq é recuperados do HDInsight em um novo modelo de configuração de dados de saudação tooturn usado. Especificamente, esses exemplos executam Olá ações a seguir:
   
    * Cria um valor exclusivo que contém Olá cadeia de caracteres "versão" e a data de saudação, que é armazenada em `newtag`.

    * Cria um documento de raiz para a nova configuração de desejado hello.

    * Obtém Olá conteúdo da saudação `.items[]` de matriz e adiciona-o em Olá **desired_config** elemento.

    * Olá exclusões `href`, `version`, e `Config` elementos, como esses elementos não são necessário toosubmit uma nova configuração.

    * Adiciona um elemento `tag` com um valor de `version#################`. parte numérica Olá baseia Olá data atual. Cada configuração deve ter uma marca exclusiva.
     
    Por fim, os dados de saudação são salvos toohello `newconfig.json` documento. estrutura do documento Hello deve aparecer semelhante toohello exemplo a seguir:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Olá abrir `newconfig.json` documento e modificar ou adicionar valores em Olá `properties` objeto. exemplo a seguir altera Olá Olá valor `"spark.yarn.am.memory"` de `"1g"` muito`"3g"`. Ele também adiciona `"spark.kryoserializer.buffer.max"` com um valor de `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Salve o arquivo de saudação quando terminar de fazer modificações.

4. Use Olá comandos toosubmit Olá atualizado configuração tooAmbari a seguir.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Esses comandos enviar conteúdo Olá Olá **newconfig.json** arquivo toohello cluster Olá desejado nova configuração. solicitação de saudação retorna um documento JSON. Olá **versionTag** elemento neste documento deve corresponder a versão de saudação enviada e Olá **configurações** objeto contém as alterações de configuração de saudação solicitado.

### <a name="example-restart-a-service-component"></a>Exemplo: reiniciar um componente de serviço

Neste ponto, se você observar Olá Ambari web da interface do usuário, Olá serviço Spark indicando que precisa toobe reiniciado para que a nova configuração de saudação entre em vigor. Use Olá serviço de saudação do toorestart as etapas a seguir.

1. Use Olá tooenable modo de manutenção para Olá serviço Spark a seguir:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Estes comandos enviam um servidor de toohello de documento JSON que ativa o modo de manutenção. Você pode verificar se o serviço de saudação está agora no modo de manutenção usando Olá solicitação a seguir:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Olá valor de retorno é `ON`.

2. Em seguida, use Olá tooturn desativar serviço Olá a seguir:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    resposta de saudação é semelhante toohello exemplo a seguir:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Olá `href` valor retornado por esse URI é usando o endereço IP interno de Olá Olá do nó do cluster. toouse-lo do cluster Olá externa, substituir a parte de saudação '10.0.0.18:8080' com hello FQDN do cluster de saudação. 
    
    Olá comandos a seguir recuperar o status de saudação da solicitação de saudação:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Uma resposta de `COMPLETED` indica que a solicitação Olá foi concluída.

3. Após a conclusão da solicitação anterior hello, use Olá após toostart Olá serviço.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    serviço de saudação agora está usando a nova configuração de saudação.

4. Por fim, use Olá tooturn desativar o modo de manutenção a seguir.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter uma referência completa de saudação API REST, consulte [V1 de referência de API do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

