---
title: "Monitorar e gerenciar o Hadoop com a API REST do Ambari – Azure HDInsight | Microsoft Docs"
description: "Aprenda a usar o Ambari para monitorar e gerenciar clusters Hadoop no Azure HDInsight. Neste documento, você aprenderá a usar a API REST do Ambari incluída com clusters HDInsight."
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
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="e1339-104">Gerenciar clusters HDInsight usando a API REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="e1339-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="e1339-105">Aprenda a usar a API REST do Ambari para gerenciar e monitorar clusters Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1339-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="e1339-106">O Apache Ambari simplifica o gerenciamento e monitoramento de um cluster Hadoop, fornecendo uma forma fácil de usar a interface do usuário da Web e a API REST.</span><span class="sxs-lookup"><span data-stu-id="e1339-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="e1339-107">O Ambari é incluído em clusters HDInsight que usam o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="e1339-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="e1339-108">Você pode usar o Ambari para monitorar o cluster e fazer alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="e1339-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="e1339-109"><a id="whatis"></a>O que é o Ambari</span><span class="sxs-lookup"><span data-stu-id="e1339-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="e1339-110">O [Apache Ambari](http://ambari.apache.org) fornece uma interface do usuário da Web que pode ser usada para provisionar, gerenciar e monitorar clusters Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e1339-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="e1339-111">Os desenvolvedores podem integrar essas funcionalidades em seus aplicativos usando as [APIs REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e1339-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="e1339-112">Ambari é fornecido por padrão com os clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="e1339-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="e1339-113">Como usar a API REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="e1339-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1339-114">As informações e exemplos deste documento exigem um cluster HDInsight que usa o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="e1339-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="e1339-115">Para saber mais, confira [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e1339-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="e1339-116">Os exemplos neste documento são fornecidos para o shell Bourne (bash) e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1339-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="e1339-117">O bash exemplos foram testados com GNU bash 4.3.11, mas devem funcionar com outros shells do Unix.</span><span class="sxs-lookup"><span data-stu-id="e1339-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="e1339-118">Os exemplos do PowerShell foram testados com o PowerShell 5.0, mas devem funcionar com o PowerShell 3.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e1339-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="e1339-119">Se usar o __shell Bourne__ (Bash), você deve ter o seguinte instalado:</span><span class="sxs-lookup"><span data-stu-id="e1339-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="e1339-120">[cURL](http://curl.haxx.se/): o cURL é um utilitário que pode ser usado para trabalhar com APIs REST na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e1339-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="e1339-121">Neste documento, ele é usado para se comunicar com a API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="e1339-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="e1339-122">Se usar Bash ou o PowerShell, você também deverá ter o [jq](https://stedolan.github.io/jq/) instalado.</span><span class="sxs-lookup"><span data-stu-id="e1339-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="e1339-123">Jq é um utilitário para trabalhar com documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="e1339-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="e1339-124">Ele é usado em **todos os** exemplos Bash, e **um** dos exemplos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1339-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="e1339-125">Base de URI para a API de Rest do Ambari</span><span class="sxs-lookup"><span data-stu-id="e1339-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="e1339-126">A URI de base para a API REST em clusters HDInsight é https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, em que **CLUSTERNAME** é o nome do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1339-127">Embora o nome do cluster na parte do nome de domínio totalmente qualificado (FQDN) do URI (CLUSTERNAME.azurehdinsight.net) diferencie maiúsculas de minúsculas, outras ocorrências no URI diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e1339-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="e1339-128">Por exemplo, se seu cluster se chamar `MyCluster`, os seguintes URIs serão válidos:</span><span class="sxs-lookup"><span data-stu-id="e1339-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="e1339-129">Os URIs a seguir retornam um erro, pois a segunda ocorrência do nome não apresenta o uso correto de maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e1339-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="e1339-130">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e1339-130">Authentication</span></span>

<span data-ttu-id="e1339-131">Conectar-se ao Ambari no HDInsight requer HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e1339-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="e1339-132">Use o nome da conta do administrador (o padrão é **admin**) e a senha fornecidos durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="e1339-133">Exemplos: Autenticação e analisando o JSON</span><span class="sxs-lookup"><span data-stu-id="e1339-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="e1339-134">Os exemplos a seguir demonstram como fazer uma solicitação GET em relação a API REST do Ambari base:</span><span class="sxs-lookup"><span data-stu-id="e1339-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="e1339-135">Os exemplos neste documento Bash fazem as seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="e1339-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="e1339-136">O nome de logon para o cluster é o valor padrão de `admin`.</span><span class="sxs-lookup"><span data-stu-id="e1339-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="e1339-137">`$PASSWORD`contém a senha para o comando de logon do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1339-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="e1339-138">Você pode definir esse valor usando `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="e1339-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="e1339-139">`$CLUSTERNAME` contém o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="e1339-140">Você pode definir esse valor usando `set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="e1339-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="e1339-141">Os exemplos do PowerShell neste documento fazem as seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="e1339-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="e1339-142">`$creds`é um objeto de credencial que contém o logon de administrador e a senha do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="e1339-143">Você pode definir esse valor usando `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` e fornecer as credenciais quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="e1339-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="e1339-144">`$clusterName` é uma cadeia de caracteres que contém o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="e1339-145">Você pode definir esse valor usando `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="e1339-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="e1339-146">Ambos os exemplos retornam um documento JSON que começa com informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1339-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="e1339-147">Analisar dados JSON</span><span class="sxs-lookup"><span data-stu-id="e1339-147">Parsing JSON data</span></span>

<span data-ttu-id="e1339-148">O exemplo a seguir usa `jq` para analisar o documento de resposta JSON e exibir apenas o `health_report` informações dos resultados.</span><span class="sxs-lookup"><span data-stu-id="e1339-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="e1339-149">O PowerShell 3.0 e superior fornece o cmdlet `ConvertFrom-Json`, que converte o documento JSON em um objeto com que é mais fácil de trabalhar desde o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1339-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="e1339-150">O exemplo a seguir usa `ConvertFrom-Json` para exibir somente as informações de `health_report` dos resultados.</span><span class="sxs-lookup"><span data-stu-id="e1339-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="e1339-151">Enquanto a maioria dos exemplos deste documento usa `ConvertFrom-Json` para exibir elementos do documento de resposta, o exemplo [Atualizar configuração do Ambari](#example-update-ambari-configuration) usa jq.</span><span class="sxs-lookup"><span data-stu-id="e1339-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="e1339-152">Jq é usado neste exemplo, para criar um novo modelo do documento de resposta JSON.</span><span class="sxs-lookup"><span data-stu-id="e1339-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="e1339-153">Para obter uma referência completa da API REST, consulte [Referência de API do Ambari, V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e1339-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="e1339-154">Exemplo: obter o FQDN de nós do cluster</span><span class="sxs-lookup"><span data-stu-id="e1339-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="e1339-155">Ao trabalhar com o HDInsight, você precisará saber o nome de domínio totalmente qualificado (FQDN) de um nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="e1339-156">Você pode recuperar facilmente o FQDN para vários nós no cluster usando os seguintes exemplos:</span><span class="sxs-lookup"><span data-stu-id="e1339-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="e1339-157">**Todos os nós**</span><span class="sxs-lookup"><span data-stu-id="e1339-157">**All nodes**</span></span>

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

* <span data-ttu-id="e1339-158">**Nós de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="e1339-158">**Head nodes**</span></span>

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

* <span data-ttu-id="e1339-159">**Nós de trabalho**</span><span class="sxs-lookup"><span data-stu-id="e1339-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="e1339-160">**Nós do Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="e1339-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="e1339-161">Exemplo: Obter o endereço IP interno de nós de cluster</span><span class="sxs-lookup"><span data-stu-id="e1339-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1339-162">Os endereços IP retornados pelos exemplos nesta seção não estão diretamente acessíveis pela internet.</span><span class="sxs-lookup"><span data-stu-id="e1339-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="e1339-163">Eles só são acessíveis na rede Virtual do Azure que contém o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1339-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="e1339-164">Para saber mais sobre como trabalhar com o HDInsight e com as redes virtuais, veja [Estender os recursos do HDInsight usando a Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="e1339-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="e1339-165">Para localizar o endereço IP, você deve saber o FQDN (nome de domínio totalmente qualificado) interno dos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="e1339-166">Uma vez que o FQDN, em seguida, você pode obter o endereço IP do host.</span><span class="sxs-lookup"><span data-stu-id="e1339-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="e1339-167">Os exemplos a seguir primeiro consultar o Ambari para o FQDN de todos os nós de host e consultar o Ambari para o endereço IP de cada host.</span><span class="sxs-lookup"><span data-stu-id="e1339-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

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

## <a name="example-get-the-default-storage"></a><span data-ttu-id="e1339-168">Exemplo: Obtenha o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="e1339-168">Example: Get the default storage</span></span>

<span data-ttu-id="e1339-169">Quando você criar um cluster HDInsight, será necessário usar uma conta do Armazenamento do Azure ou o Data Lake Store como o armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="e1339-170">Você pode usar o Ambari para recuperar essas informações após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="e1339-171">Por exemplo, se você quiser ler/gravar dados no contêiner fora do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1339-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="e1339-172">Os exemplos a seguir recuperar a configuração de armazenamento padrão do cluster:</span><span class="sxs-lookup"><span data-stu-id="e1339-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

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
> <span data-ttu-id="e1339-173">Estes exemplos retornam a primeira configuração aplicada ao servidor (`service_config_version=1`) que contém essas informações.</span><span class="sxs-lookup"><span data-stu-id="e1339-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="e1339-174">Se você recuperar um valor que foi modificado após a criação do cluster, talvez seja necessário listar as versões de configuração e recuperar a mais recente.</span><span class="sxs-lookup"><span data-stu-id="e1339-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="e1339-175">O valor de retorno é semelhante a um dos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1339-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="e1339-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Este valor indica que o cluster está usando uma conta de armazenamento do Azure para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="e1339-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="e1339-177">O valor `ACCOUNTNAME` é o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1339-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="e1339-178">O `CONTAINER` parte é o nome do contêiner de blob na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1339-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="e1339-179">O contêiner é a raiz de armazenamento compatível com HDFS para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="e1339-180">`adl://home`-Este valor indica que o cluster está usando um Azure Data Lake Store para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="e1339-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="e1339-181">Para localizar o nome da conta Data Lake Store, use os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1339-181">To find the Data Lake Store account name, use the following examples:</span></span>

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

    <span data-ttu-id="e1339-182">O valor de retorno é semelhante ao `ACCOUNTNAME.azuredatalakestore.net`, onde `ACCOUNTNAME` é o nome da conta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e1339-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="e1339-183">Para localizar o diretório no Data Lake Store que contém o armazenamento do cluster, use os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1339-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

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

    <span data-ttu-id="e1339-184">O valor de retorno é semelhante ao `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="e1339-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="e1339-185">Esse valor é um caminho dentro da conta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e1339-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="e1339-186">Esse caminho é a raiz do sistema de arquivos compatível com HDFS para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="e1339-187">O cmdlet `Get-AzureRmHDInsightCluster` fornecido pelo [Azure PowerShell](/powershell/azure/overview) também retorna as informações de armazenamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="e1339-188">Exemplo: obter configuração</span><span class="sxs-lookup"><span data-stu-id="e1339-188">Example: Get configuration</span></span>

1. <span data-ttu-id="e1339-189">Obtenha as configurações que estão disponíveis para o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="e1339-190">Esse exemplo retorna um documento JSON contendo a configuração atual (identificada pelo valor *tag* ) para os componentes instalados no cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="e1339-191">O exemplo a seguir é um trecho dos dados retornados de um tipo de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e1339-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="e1339-192">Obtenha a configuração para o componente em que você tem interesse.</span><span class="sxs-lookup"><span data-stu-id="e1339-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="e1339-193">No exemplo a seguir, substitua `INITIAL` pelo valor retornado da solicitação anterior.</span><span class="sxs-lookup"><span data-stu-id="e1339-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="e1339-194">Este exemplo retorna um documento JSON que contém a configuração atual do componente `core-site`.</span><span class="sxs-lookup"><span data-stu-id="e1339-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="e1339-195">Exemplo: Atualizar a configuração</span><span class="sxs-lookup"><span data-stu-id="e1339-195">Example: Update configuration</span></span>

1. <span data-ttu-id="e1339-196">Obtenha a configuração atual, que o Ambari armazena como a "configuração desejada":</span><span class="sxs-lookup"><span data-stu-id="e1339-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="e1339-197">Esse exemplo retorna um documento JSON contendo a configuração atual (identificada pelo valor *tag* ) para os componentes instalados no cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="e1339-198">O exemplo a seguir é um trecho dos dados retornados de um tipo de cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e1339-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="e1339-199">Nesta lista, você precisa copiar o nome do componente (por exemplo, **spark\_thrift\_sparkconf** e o valor **tag**.</span><span class="sxs-lookup"><span data-stu-id="e1339-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="e1339-200">Recupere a configuração do componente e da marca usando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1339-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
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
    > <span data-ttu-id="e1339-201">Substitua **spark-thrift-sparkconf** e **INITIAL** pelo componente e pela marcação cuja configuração você deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="e1339-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="e1339-202">O jq é usado para transformar os dados recuperados do HDInsight em um novo modelo de configuração.</span><span class="sxs-lookup"><span data-stu-id="e1339-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="e1339-203">Especificamente, esses exemplos executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="e1339-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="e1339-204">Cria um valor exclusivo que contém a cadeia de caracteres "version" e a data, que é armazenada em `newtag`.</span><span class="sxs-lookup"><span data-stu-id="e1339-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="e1339-205">Cria um documento raiz para a nova configuração desejada.</span><span class="sxs-lookup"><span data-stu-id="e1339-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="e1339-206">Obtém o conteúdo da matriz `.items[]` e o adiciona sob o elemento **desired_config**.</span><span class="sxs-lookup"><span data-stu-id="e1339-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="e1339-207">Exclui os elementos `href`, `version` e `Config`, pois eles não são necessários para enviar uma nova configuração.</span><span class="sxs-lookup"><span data-stu-id="e1339-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="e1339-208">Adiciona um elemento `tag` com um valor de `version#################`.</span><span class="sxs-lookup"><span data-stu-id="e1339-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="e1339-209">A parte numérica tem base na data atual.</span><span class="sxs-lookup"><span data-stu-id="e1339-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="e1339-210">Cada configuração deve ter uma marca exclusiva.</span><span class="sxs-lookup"><span data-stu-id="e1339-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="e1339-211">Por fim, os dados são salvos no documento `newconfig.json`.</span><span class="sxs-lookup"><span data-stu-id="e1339-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="e1339-212">A estrutura do documento deve ser semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1339-212">The document structure should appear similar to the following example:</span></span>
     
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

3. <span data-ttu-id="e1339-213">Abra o documento `newconfig.json` e modifique/adicione valores no objeto `properties`.</span><span class="sxs-lookup"><span data-stu-id="e1339-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="e1339-214">O exemplo a seguir altera o valor de `"spark.yarn.am.memory"` desde `"1g"` até `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="e1339-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="e1339-215">Ele também adiciona `"spark.kryoserializer.buffer.max"` com um valor de `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="e1339-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="e1339-216">Quando terminar de fazer modificações, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1339-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="e1339-217">Use os seguintes comandos para enviar a configuração atualizada ao Ambari.</span><span class="sxs-lookup"><span data-stu-id="e1339-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
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
   
    <span data-ttu-id="e1339-218">Esses comandos enviam o conteúdo do arquivo **newconfig.json** para o cluster como a nova configuração desejada.</span><span class="sxs-lookup"><span data-stu-id="e1339-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="e1339-219">A solicitação retorna um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="e1339-219">The request returns a JSON document.</span></span> <span data-ttu-id="e1339-220">O elemento **versionTag** nesse documento deverá corresponder à versão enviada e o objeto **configs** conterá as alterações de configuração solicitadas.</span><span class="sxs-lookup"><span data-stu-id="e1339-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="e1339-221">Exemplo: reiniciar um componente de serviço</span><span class="sxs-lookup"><span data-stu-id="e1339-221">Example: Restart a service component</span></span>

<span data-ttu-id="e1339-222">Neste ponto, se você examinar a interface do usuário da Web do Ambari, o serviço do Spark indicará que ele precisa ser reiniciado para que a nova configuração entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="e1339-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="e1339-223">Use as etapas a seguir para reiniciar o serviço.</span><span class="sxs-lookup"><span data-stu-id="e1339-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="e1339-224">Use o seguinte para habilitar o modo de manutenção para o serviço do Spark:</span><span class="sxs-lookup"><span data-stu-id="e1339-224">Use the following to enable maintenance mode for the Spark service:</span></span>

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
   
    <span data-ttu-id="e1339-225">Estes comandos enviam um documento JSON para o servidor que ativa o modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="e1339-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="e1339-226">Você pode verificar se o serviço está em modo de manutenção usando a seguinte solicitação:</span><span class="sxs-lookup"><span data-stu-id="e1339-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
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
   
    <span data-ttu-id="e1339-227">O valor de retorno é `ON`.</span><span class="sxs-lookup"><span data-stu-id="e1339-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="e1339-228">Em seguida, use o seguinte para desativar o serviço:</span><span class="sxs-lookup"><span data-stu-id="e1339-228">Next, use the following to turn off the service:</span></span>

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
    
    <span data-ttu-id="e1339-229">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1339-229">The response is similar to the following example:</span></span>
   
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
    > <span data-ttu-id="e1339-230">O valor `href` retornado por esse URI usa o endereço IP interno do nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="e1339-231">Para usá-lo de fora do cluster, substitua a parte '10.0.0.18:8080' pelo FQDN do cluster.</span><span class="sxs-lookup"><span data-stu-id="e1339-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="e1339-232">Os comandos a seguir recuperam o status da solicitação:</span><span class="sxs-lookup"><span data-stu-id="e1339-232">The following commands retrieve the status of the request:</span></span>

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

    <span data-ttu-id="e1339-233">Uma resposta de `COMPLETED` indica que a solicitação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="e1339-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="e1339-234">Quando a solicitação anterior for concluída, use o seguinte para iniciar o serviço:</span><span class="sxs-lookup"><span data-stu-id="e1339-234">Once the previous request completes, use the following to start the service.</span></span>
   
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
    <span data-ttu-id="e1339-235">O serviço agora está usando a nova configuração.</span><span class="sxs-lookup"><span data-stu-id="e1339-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="e1339-236">Por fim, use o seguinte para desativar o modo de manutenção:</span><span class="sxs-lookup"><span data-stu-id="e1339-236">Finally, use the following to turn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="e1339-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1339-237">Next steps</span></span>

<span data-ttu-id="e1339-238">Para obter uma referência completa da API REST, consulte [Referência de API do Ambari, V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="e1339-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

