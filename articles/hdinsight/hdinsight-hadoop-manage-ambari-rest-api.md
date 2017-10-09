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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="b8e6b-104">Gerenciar clusters HDInsight usando Olá Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b8e6b-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="b8e6b-105">Saiba como toouse Olá toomanage Ambari REST API e monitorar clusters Hadoop em HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="b8e6b-106">Apache Ambari simplifica o gerenciamento de saudação e monitoramento de um cluster de Hadoop, fornecendo a interface do usuário e REST API toouse fácil da web.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="b8e6b-107">Ambari é incluído em clusters de HDInsight que usam o sistema de operacional Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="b8e6b-108">Você pode usar o cluster de saudação do Ambari toomonitor e fazer alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="b8e6b-109"><a id="whatis"></a>O que é o Ambari</span><span class="sxs-lookup"><span data-stu-id="b8e6b-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="b8e6b-110">[Apache Ambari](http://ambari.apache.org) fornece a interface que pode ser usado tooprovision, gerenciar e monitorar clusters Hadoop da web.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="b8e6b-111">Os desenvolvedores podem integrar esses recursos em seus aplicativos usando Olá [APIs de REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b8e6b-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="b8e6b-112">Ambari é fornecido por padrão com os clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="b8e6b-113">Como toouse Olá Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b8e6b-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8e6b-114">informações de saudação e exemplos neste documento exigem um cluster HDInsight que usa o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="b8e6b-115">Para saber mais, confira [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b8e6b-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="b8e6b-116">exemplos de saudação neste documento são fornecidos para o shell Bourne de saudação (bash) e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="b8e6b-117">bash Olá exemplos foram testados com GNU bash 4.3.11, mas devem funcionar com outros shells do Unix.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="b8e6b-118">exemplos do PowerShell Olá foram testados com o PowerShell 5.0, mas devem funcionar com o PowerShell 3.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="b8e6b-119">Se usar o hello __shell Bourne__ (Bash), você deve ter o seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="b8e6b-120">[cURL](http://curl.haxx.se/): Ondulação é um utilitário que pode ser usado toowork com APIs de REST da linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="b8e6b-121">Neste documento, é usado toocommunicate com hello API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="b8e6b-122">Se usar Bash ou o PowerShell, você também deverá ter o [jq](https://stedolan.github.io/jq/) instalado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="b8e6b-123">Jq é um utilitário para trabalhar com documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="b8e6b-124">Ele é usado em **todos os** Olá Bash exemplos, e **um** de exemplos do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="b8e6b-125">Base de URI para a API de Rest do Ambari</span><span class="sxs-lookup"><span data-stu-id="b8e6b-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="b8e6b-126">Olá, URI de base para Olá API REST do Ambari no HDInsight é https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, onde **CLUSTERNAME** é o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8e6b-127">Enquanto o nome do cluster Olá no hello totalmente qualificado parte do nome (FQDN) do domínio de saudação URI (CLUSTERNAME.azurehdinsight.net) diferencia maiusculas de minúsculas, outras ocorrências em Olá URI diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="b8e6b-128">Por exemplo, se o cluster é denominado `MyCluster`, Olá seguem URIs válidos:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="b8e6b-129">seguir Olá URIs retornará um erro porque Olá segunda ocorrência do nome de saudação não é Olá corrija caso.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="b8e6b-130">Autenticação</span><span class="sxs-lookup"><span data-stu-id="b8e6b-130">Authentication</span></span>

<span data-ttu-id="b8e6b-131">Conexão tooAmbari no HDInsight requer HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="b8e6b-132">Nome de conta de administrador use hello (Olá padrão é **admin**) e a senha fornecidos durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="b8e6b-133">Exemplos: Autenticação e analisando o JSON</span><span class="sxs-lookup"><span data-stu-id="b8e6b-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="b8e6b-134">Olá exemplos a seguir demonstram como toomake uma solicitação GET hello base Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="b8e6b-135">exemplos de Bash Olá neste documento fazer Olá seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b8e6b-136">nome de logon de Olá para cluster Olá é o valor padrão de saudação do `admin`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="b8e6b-137">`$PASSWORD`contém a senha Olá Olá comando de login do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="b8e6b-138">Você pode definir esse valor usando `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="b8e6b-139">`$CLUSTERNAME`contém o nome de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="b8e6b-140">Você pode definir esse valor usando `set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="b8e6b-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="b8e6b-141">exemplos do PowerShell Olá neste documento fazer Olá seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="b8e6b-142">`$creds`é um objeto de credencial que contém o logon de administrador hello e a senha para o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="b8e6b-143">Você pode definir esse valor usando `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` e fornecer credenciais de saudação quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="b8e6b-144">`$clusterName`é uma cadeia de caracteres que contém o nome de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="b8e6b-145">Você pode definir esse valor usando `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="b8e6b-146">Os dois exemplos retornam um documento JSON que começa com informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="b8e6b-147">Analisar dados JSON</span><span class="sxs-lookup"><span data-stu-id="b8e6b-147">Parsing JSON data</span></span>

<span data-ttu-id="b8e6b-148">Olá exemplo a seguir usa `jq` tooparse Olá documento de resposta JSON e exibir somente Olá `health_report` informações dos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="b8e6b-149">PowerShell 3.0 e superior fornece Olá `ConvertFrom-Json` cmdlet, que converte o documento JSON de saudação em um objeto que é mais fácil toowork do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="b8e6b-150">Olá exemplo a seguir usa `ConvertFrom-Json` Olá somente toodisplay `health_report` informações dos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="b8e6b-151">Embora a maioria dos exemplos deste documento usam `ConvertFrom-Json` toodisplay elementos do documento de resposta hello, Olá [Ambari de atualização de configuração](#example-update-ambari-configuration) exemplo usa jq.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="b8e6b-152">Jq é usado em tooconstruct Este exemplo um novo modelo de documento de resposta JSON hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="b8e6b-153">Para obter uma referência completa de saudação API REST, consulte [V1 de referência de API do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b8e6b-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="b8e6b-154">Exemplo: Obter Olá FQDN de nós de cluster</span><span class="sxs-lookup"><span data-stu-id="b8e6b-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="b8e6b-155">Ao trabalhar com HDInsight, talvez seja necessário um nome de domínio totalmente qualificado de saudação tooknow (FQDN) de um nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="b8e6b-156">Você pode recuperar facilmente hello FQDN para Olá vários nós no cluster hello usando Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="b8e6b-157">**Todos os nós**</span><span class="sxs-lookup"><span data-stu-id="b8e6b-157">**All nodes**</span></span>

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

* <span data-ttu-id="b8e6b-158">**Nós de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="b8e6b-158">**Head nodes**</span></span>

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

* <span data-ttu-id="b8e6b-159">**Nós de trabalho**</span><span class="sxs-lookup"><span data-stu-id="b8e6b-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="b8e6b-160">**Nós do Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="b8e6b-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="b8e6b-161">Exemplo: Obter o endereço IP interno de saudação de nós de cluster</span><span class="sxs-lookup"><span data-stu-id="b8e6b-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8e6b-162">endereços IP de saudação retornados por exemplos Olá nesta seção são não diretamente acessível via Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="b8e6b-163">Eles são acessíveis apenas dentro de saudação rede Virtual do Azure que contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="b8e6b-164">Para saber mais sobre como trabalhar com o HDInsight e com as redes virtuais, veja [Estender os recursos do HDInsight usando a Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="b8e6b-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="b8e6b-165">endereço IP de saudação toofind, você deve saber Olá interno nome totalmente qualificado (FQDN) do hello nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="b8e6b-166">Depois que você tiver Olá FQDN, em seguida, você pode obter endereço IP de saudação do host de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="b8e6b-167">Olá exemplos a seguir primeiro consultar Ambari Olá FQDN de todos os nós de host hello e consultar Ambari para o endereço IP de saudação de cada host.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="b8e6b-168">Exemplo: Obter armazenamento padrão da saudação</span><span class="sxs-lookup"><span data-stu-id="b8e6b-168">Example: Get hello default storage</span></span>

<span data-ttu-id="b8e6b-169">Quando você cria um cluster HDInsight, você deve usar uma conta de armazenamento do Azure ou um repositório Data Lake como armazenamento de padrão de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="b8e6b-170">Você pode usar essas informações de Ambari tooretrieve depois Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="b8e6b-171">Por exemplo, se você quiser que o contêiner de toohello tooread/gravação dados fora do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="b8e6b-172">Olá exemplos a seguir recuperar configuração de armazenamento padrão de saudação do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="b8e6b-173">Esses exemplos retornam o primeiro servidor de toohello configuração aplicada hello (`service_config_version=1`) que contém essas informações.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="b8e6b-174">Se você recuperar um valor que foi modificado após a criação do cluster, você pode precisa toolist Olá configuração versões e recuperar hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="b8e6b-175">valor de retorno de saudação é semelhante tooone de saudação exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="b8e6b-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Este valor indica que o cluster hello está usando uma conta de armazenamento do Azure para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="b8e6b-177">Olá `ACCOUNTNAME` valor é o nome de Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="b8e6b-178">Olá `CONTAINER` parte é o nome de Olá Olá do contêiner de blob na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="b8e6b-179">contêiner de saudação é raiz Olá Olá armazenamento compatíveis do HDFS para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="b8e6b-180">`adl://home`-Este valor indica que o cluster hello está usando um repositório Data Lake do Azure para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="b8e6b-181">Olá toofind nome de conta do repositório Data Lake, use Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="b8e6b-182">Olá valor de retorno é semelhante muito`ACCOUNTNAME.azuredatalakestore.net`, onde `ACCOUNTNAME` é o nome de saudação do hello conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="b8e6b-183">diretório de saudação toofind dentro do repositório Data Lake que contém o armazenamento Olá Olá cluster, use Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="b8e6b-184">Olá valor de retorno é semelhante muito`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="b8e6b-185">Esse valor é um caminho dentro Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="b8e6b-186">Esse caminho é a raiz de saudação de sistema de arquivos compatíveis do HDFS para o cluster de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8e6b-187">Olá `Get-AzureRmHDInsightCluster` cmdlet fornecido pelo [Azure PowerShell](/powershell/azure/overview) também retorna Olá informações de armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="b8e6b-188">Exemplo: obter configuração</span><span class="sxs-lookup"><span data-stu-id="b8e6b-188">Example: Get configuration</span></span>

1. <span data-ttu-id="b8e6b-189">Obter configurações de saudação que estão disponíveis para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="b8e6b-190">Este exemplo retorna um documento JSON que contém a configuração atual da saudação (identificada pelo Olá *marca* valor) para componentes de saudação instalados no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b8e6b-191">Olá, exemplo a seguir é um trecho da saudação dados retornados de um tipo de cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="b8e6b-192">Obter a configuração Olá componente Olá que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="b8e6b-193">Olá seguinte exemplo, substitua `INITIAL` com valor de marca Olá retornado da solicitação anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="b8e6b-194">Este exemplo retorna um documento JSON que contém a configuração atual Olá Olá `core-site` componente.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="b8e6b-195">Exemplo: Atualizar a configuração</span><span class="sxs-lookup"><span data-stu-id="b8e6b-195">Example: Update configuration</span></span>

1. <span data-ttu-id="b8e6b-196">Obter a configuração atual do hello, que armazena o Ambari como hello "configuração desejada":</span><span class="sxs-lookup"><span data-stu-id="b8e6b-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="b8e6b-197">Este exemplo retorna um documento JSON que contém a configuração atual da saudação (identificada pelo Olá *marca* valor) para componentes de saudação instalados no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="b8e6b-198">Olá, exemplo a seguir é um trecho da saudação dados retornados de um tipo de cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="b8e6b-199">Nesta lista, você precisa toocopy nome de saudação do componente de saudação (por exemplo, **spark\_thrift\_sparkconf** e hello **marca** valor.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="b8e6b-200">Recupere a configuração de saudação do componente hello e marca usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="b8e6b-201">Substituir **spark-thrift-sparkconf** e **inicial** com componente hello e marca que você deseja tooretrieve Olá configuração para.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="b8e6b-202">Jq é recuperados do HDInsight em um novo modelo de configuração de dados de saudação tooturn usado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="b8e6b-203">Especificamente, esses exemplos executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="b8e6b-204">Cria um valor exclusivo que contém Olá cadeia de caracteres "versão" e a data de saudação, que é armazenada em `newtag`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="b8e6b-205">Cria um documento de raiz para a nova configuração de desejado hello.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="b8e6b-206">Obtém Olá conteúdo da saudação `.items[]` de matriz e adiciona-o em Olá **desired_config** elemento.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="b8e6b-207">Olá exclusões `href`, `version`, e `Config` elementos, como esses elementos não são necessário toosubmit uma nova configuração.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="b8e6b-208">Adiciona um elemento `tag` com um valor de `version#################`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="b8e6b-209">parte numérica Olá baseia Olá data atual.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="b8e6b-210">Cada configuração deve ter uma marca exclusiva.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="b8e6b-211">Por fim, os dados de saudação são salvos toohello `newconfig.json` documento.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="b8e6b-212">estrutura do documento Hello deve aparecer semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="b8e6b-213">Olá abrir `newconfig.json` documento e modificar ou adicionar valores em Olá `properties` objeto.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="b8e6b-214">exemplo a seguir altera Olá Olá valor `"spark.yarn.am.memory"` de `"1g"` muito`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="b8e6b-215">Ele também adiciona `"spark.kryoserializer.buffer.max"` com um valor de `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="b8e6b-216">Salve o arquivo de saudação quando terminar de fazer modificações.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="b8e6b-217">Use Olá comandos toosubmit Olá atualizado configuração tooAmbari a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="b8e6b-218">Esses comandos enviar conteúdo Olá Olá **newconfig.json** arquivo toohello cluster Olá desejado nova configuração.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="b8e6b-219">solicitação de saudação retorna um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-219">hello request returns a JSON document.</span></span> <span data-ttu-id="b8e6b-220">Olá **versionTag** elemento neste documento deve corresponder a versão de saudação enviada e Olá **configurações** objeto contém as alterações de configuração de saudação solicitado.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="b8e6b-221">Exemplo: reiniciar um componente de serviço</span><span class="sxs-lookup"><span data-stu-id="b8e6b-221">Example: Restart a service component</span></span>

<span data-ttu-id="b8e6b-222">Neste ponto, se você observar Olá Ambari web da interface do usuário, Olá serviço Spark indicando que precisa toobe reiniciado para que a nova configuração de saudação entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="b8e6b-223">Use Olá serviço de saudação do toorestart as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="b8e6b-224">Use Olá tooenable modo de manutenção para Olá serviço Spark a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="b8e6b-225">Estes comandos enviam um servidor de toohello de documento JSON que ativa o modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="b8e6b-226">Você pode verificar se o serviço de saudação está agora no modo de manutenção usando Olá solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="b8e6b-227">Olá valor de retorno é `ON`.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="b8e6b-228">Em seguida, use Olá tooturn desativar serviço Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="b8e6b-229">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="b8e6b-230">Olá `href` valor retornado por esse URI é usando o endereço IP interno de Olá Olá do nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="b8e6b-231">toouse-lo do cluster Olá externa, substituir a parte de saudação '10.0.0.18:8080' com hello FQDN do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="b8e6b-232">Olá comandos a seguir recuperar o status de saudação da solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="b8e6b-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="b8e6b-233">Uma resposta de `COMPLETED` indica que a solicitação Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="b8e6b-234">Após a conclusão da solicitação anterior hello, use Olá após toostart Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="b8e6b-235">serviço de saudação agora está usando a nova configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="b8e6b-236">Por fim, use Olá tooturn desativar o modo de manutenção a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8e6b-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="b8e6b-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8e6b-237">Next steps</span></span>

<span data-ttu-id="b8e6b-238">Para obter uma referência completa de saudação API REST, consulte [V1 de referência de API do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="b8e6b-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

