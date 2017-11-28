---
title: aaaGet iniciado com o Azure Service Fabric e 2.0 do CLI do Azure
description: "Saiba como toouse hello Azure Service Fabric comandos do módulo em CLI do Azure, versão 2.0. Saiba como tooconnect tooa cluster e como toomanage aplicativos."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="7645d-104">Service Fabric e CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7645d-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="7645d-105">Olá, ferramenta de linha de comando do Azure (Azure CLI) versão 2.0 inclui comandos toohelp gerenciar clusters de malha do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="7645d-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="7645d-106">Saiba como tooget iniciado com a CLI do Azure e do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7645d-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="7645d-107">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7645d-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="7645d-108">Você pode usar o Azure CLI 2.0 comandos toointeract com e gerenciar clusters de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="7645d-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="7645d-109">versão mais recente do hello tooget da CLI do Azure, siga Olá [processo de instalação padrão do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7645d-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="7645d-110">Para obter mais informações, consulte Olá [visão geral do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7645d-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="7645d-111">Sintaxe da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7645d-111">Azure CLI syntax</span></span>

<span data-ttu-id="7645d-112">Na CLI do Azure, todos os comandos do Service Fabric são prefixados com `az sf`.</span><span class="sxs-lookup"><span data-stu-id="7645d-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="7645d-113">Para obter informações gerais sobre os comandos de saudação, você pode usar, use `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="7645d-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="7645d-114">Para obter ajuda com um único comando, use `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="7645d-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="7645d-115">Os comandos do Service Fabric na CLI do Azure seguem este padrão de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="7645d-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="7645d-116">`<object>`é o destino hello para `<action>`.</span><span class="sxs-lookup"><span data-stu-id="7645d-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="7645d-117">Selecionar um cluster</span><span class="sxs-lookup"><span data-stu-id="7645d-117">Select a cluster</span></span>

<span data-ttu-id="7645d-118">Antes de executar qualquer operação, você deve selecionar um tooconnect de cluster para.</span><span class="sxs-lookup"><span data-stu-id="7645d-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="7645d-119">Para obter um exemplo, consulte Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7645d-119">For an example, see hello following code.</span></span> <span data-ttu-id="7645d-120">código de saudação conecta cluster segura tooan.</span><span class="sxs-lookup"><span data-stu-id="7645d-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="7645d-121">Não use clusters do Service Fabric não seguros em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="7645d-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="7645d-122">o ponto de extremidade do Hello cluster deve ser antecedido `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="7645d-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="7645d-123">Ele deve incluir a porta Olá para o gateway HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="7645d-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="7645d-124">endereço e porta de saudação são Olá mesmas Olá URL do Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7645d-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="7645d-125">Para clusters protegidos por um certificado, você pode usar arquivos .pem não criptografados ou arquivos .crt e .key.</span><span class="sxs-lookup"><span data-stu-id="7645d-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="7645d-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7645d-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="7645d-127">Para obter mais informações, consulte [cluster seguro de Azure Service Fabric do Connect tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7645d-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7645d-128">Olá `select` comando não agir em todas as solicitações antes de retornar.</span><span class="sxs-lookup"><span data-stu-id="7645d-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="7645d-129">tooverify que você tenha especificado um cluster corretamente, use um comando como `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="7645d-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="7645d-130">Verifique se que o comando Olá não retorna quaisquer erros.</span><span class="sxs-lookup"><span data-stu-id="7645d-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="7645d-131">Operações básicas</span><span class="sxs-lookup"><span data-stu-id="7645d-131">Basic operations</span></span>

<span data-ttu-id="7645d-132">As informações de conexão do cluster persistem por várias sessões da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7645d-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="7645d-133">Depois de selecionar um cluster do Service Fabric, você pode executar qualquer comando de malha do serviço em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7645d-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="7645d-134">Por exemplo, Olá tooget estado de integridade do cluster do Service Fabric, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7645d-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="7645d-135">comando Olá resulta no seguinte hello (supondo que a saída JSON é especificada na configuração de CLI do Azure de saudação) de saída:</span><span class="sxs-lookup"><span data-stu-id="7645d-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="7645d-136">Dicas e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="7645d-136">Tips and troubleshooting</span></span>

<span data-ttu-id="7645d-137">Você pode achar Olá informações úteis a seguir se você tiver problemas ao usar comandos do Service Fabric no CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7645d-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="7645d-138">Converter um certificado de PFX tooPEM formato</span><span class="sxs-lookup"><span data-stu-id="7645d-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="7645d-139">A CLI do Azure dá suporte a certificados de cliente como arquivos PEM (extensão .pem).</span><span class="sxs-lookup"><span data-stu-id="7645d-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="7645d-140">Se você usar arquivos PFX do Windows, você deve converter o formato de tooPEM esses certificados.</span><span class="sxs-lookup"><span data-stu-id="7645d-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="7645d-141">tooconvert um arquivo PFX arquivo tooa PEM, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7645d-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="7645d-142">Para obter mais informações, consulte Olá [OpenSSL documentação](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="7645d-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="7645d-143">Problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="7645d-143">Connection issues</span></span>

<span data-ttu-id="7645d-144">Algumas operações podem gerar Olá a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="7645d-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="7645d-145">Verifique se que esse Olá especificado de ponto de extremidade do cluster está disponível e está ouvindo.</span><span class="sxs-lookup"><span data-stu-id="7645d-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="7645d-146">Além disso, verifique se esse hello, que interface de usuário do Service Fabric Explorer está disponível no host e porta.</span><span class="sxs-lookup"><span data-stu-id="7645d-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="7645d-147">ponto de extremidade de saudação de tooupdate, use `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="7645d-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="7645d-148">Logs detalhados</span><span class="sxs-lookup"><span data-stu-id="7645d-148">Detailed logs</span></span>

<span data-ttu-id="7645d-149">Os logs detalhados costumam ser úteis para depurar ou relatar um problema.</span><span class="sxs-lookup"><span data-stu-id="7645d-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="7645d-150">CLI do Azure oferece um global `--debug` sinalizador que aumenta o detalhamento de saudação de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="7645d-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="7645d-151">Sintaxe e ajuda de comando</span><span class="sxs-lookup"><span data-stu-id="7645d-151">Command help and syntax</span></span>

<span data-ttu-id="7645d-152">Acompanhamento de comandos do Service Fabric Olá mesmas convenções CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7645d-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="7645d-153">Para obter ajuda com um comando específico ou um grupo de comandos, use Olá `-h` sinalizador:</span><span class="sxs-lookup"><span data-stu-id="7645d-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="7645d-154">Veja outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="7645d-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
