---
title: "Introdução ao Azure Service Fabric e à CLI do Azure 2.0"
description: "Saiba como usar o módulo de comandos do Azure Service Fabric na CLI do Azure, versão 2.0. Saiba como se conectar a um cluster e como gerenciar aplicativos."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="6b6a9-104">Service Fabric e CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6b6a9-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="6b6a9-105">A Azure CLI (ferramenta de linha de comando) versão 2.0 inclui comandos para ajudá-lo a gerenciar clusters do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="6b6a9-106">Aprenda a usar a CLI do Azure e o Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="6b6a9-107">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b6a9-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="6b6a9-108">Você pode usar comandos da CLI do Azure 2.0 para gerenciar e interagir com clusters do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="6b6a9-109">Para obter a versão mais recente da CLI do Azure, siga o [processo de instalação padrão da CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b6a9-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6b6a9-110">Para saber mais, confira a [Visão geral da CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6b6a9-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="6b6a9-111">Sintaxe da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6b6a9-111">Azure CLI syntax</span></span>

<span data-ttu-id="6b6a9-112">Na CLI do Azure, todos os comandos do Service Fabric são prefixados com `az sf`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="6b6a9-113">Para obter informações gerais sobre os comandos que você pode usar, use `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="6b6a9-114">Para obter ajuda com um único comando, use `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="6b6a9-115">Os comandos do Service Fabric na CLI do Azure seguem este padrão de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="6b6a9-116">Aqui, `<object>` é o destino de `<action>`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="6b6a9-117">Selecionar um cluster</span><span class="sxs-lookup"><span data-stu-id="6b6a9-117">Select a cluster</span></span>

<span data-ttu-id="6b6a9-118">Antes de executar qualquer operação, você deve selecionar um cluster para se conectar.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="6b6a9-119">Para obter um exemplo, veja o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-119">For an example, see the following code.</span></span> <span data-ttu-id="6b6a9-120">O código se conecta a um cluster não seguro.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="6b6a9-121">Não use clusters do Service Fabric não seguros em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="6b6a9-122">O ponto de extremidade do cluster deve ser antecedido por `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="6b6a9-123">Ele deve incluir a porta para o gateway HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="6b6a9-124">Essa porta e o endereço são os mesmos da URL do Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="6b6a9-125">Para clusters protegidos por um certificado, você pode usar arquivos .pem não criptografados ou arquivos .crt e .key.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="6b6a9-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="6b6a9-127">Para saber mais, confira [Conectar-se a um cluster seguro do Azure Service Fabric](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6b6a9-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6b6a9-128">O comando `select` não agir em nenhuma solicitação antes de retornar.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="6b6a9-129">Para verificar se você especificou um cluster corretamente, use um comando como `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="6b6a9-130">Verifique se o comando não retorna erros.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="6b6a9-131">Operações básicas</span><span class="sxs-lookup"><span data-stu-id="6b6a9-131">Basic operations</span></span>

<span data-ttu-id="6b6a9-132">As informações de conexão do cluster persistem por várias sessões da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="6b6a9-133">Depois de selecionar um cluster do Service Fabric, você poderá executar todos os comandos do Service Fabric no cluster.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="6b6a9-134">Por exemplo, para obter o estado de integridade do cluster do Service Fabric, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="6b6a9-135">O comando resulta na saída abaixo (supondo que a saída JSON foi especificada na configuração da CLI do Azure):</span><span class="sxs-lookup"><span data-stu-id="6b6a9-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="6b6a9-136">Dicas e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="6b6a9-136">Tips and troubleshooting</span></span>

<span data-ttu-id="6b6a9-137">As informações a seguir poderão ser úteis se você tiver problemas ao usar comandos do Service Fabric na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="6b6a9-138">Converter um certificado de PFX para PEM</span><span class="sxs-lookup"><span data-stu-id="6b6a9-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="6b6a9-139">A CLI do Azure dá suporte a certificados de cliente como arquivos PEM (extensão .pem).</span><span class="sxs-lookup"><span data-stu-id="6b6a9-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="6b6a9-140">Se você usa arquivos PFX do Windows, deve converter esses certificados em formato PEM.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="6b6a9-141">Para converter um arquivo PFX em PEM, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="6b6a9-142">Para saber mais, confira a [documentação OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="6b6a9-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="6b6a9-143">Problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="6b6a9-143">Connection issues</span></span>

<span data-ttu-id="6b6a9-144">Algumas operações podem gerar a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="6b6a9-145">Verifique se o ponto de extremidade do cluster especificado está disponível e está ouvindo.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="6b6a9-146">Verifique também se a interface do usuário do Service Fabric Explorer está acessível no host e na porta.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="6b6a9-147">Para atualizar o ponto de extremidade, use `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="6b6a9-148">Logs detalhados</span><span class="sxs-lookup"><span data-stu-id="6b6a9-148">Detailed logs</span></span>

<span data-ttu-id="6b6a9-149">Os logs detalhados costumam ser úteis para depurar ou relatar um problema.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="6b6a9-150">A CLI do Azure oferece um sinalizador global `--debug` que aumenta o nível de detalhes dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="6b6a9-151">Sintaxe e ajuda de comando</span><span class="sxs-lookup"><span data-stu-id="6b6a9-151">Command help and syntax</span></span>

<span data-ttu-id="6b6a9-152">Os comandos do Service Fabric seguem a mesma convenção da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b6a9-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="6b6a9-153">Para obter ajuda com um comando ou um grupo de comandos específico, use o sinalizador `-h`:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="6b6a9-154">Veja outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="6b6a9-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
