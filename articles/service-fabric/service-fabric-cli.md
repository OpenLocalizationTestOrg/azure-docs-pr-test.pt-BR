---
title: aaaGet iniciado com o Azure Service Fabric CLI (sfctl)
description: "Saiba como toouse Olá CLI de malha do serviço do Azure. Saiba como tooconnect tooa cluster e como toomanage aplicativos."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="a6397-104">Linha de comando do Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a6397-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="a6397-105">Olá CLI de malha de serviço do Azure (sfctl) é um utilitário de linha de comando para interagir e gerenciar entidades do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6397-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="a6397-106">O sfctl pode ser usado com clusters do Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="a6397-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="a6397-107">O sfctl é executado em qualquer plataforma onde o python é suportado.</span><span class="sxs-lookup"><span data-stu-id="a6397-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6397-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6397-108">Prerequisites</span></span>

<span data-ttu-id="a6397-109">Tooinstallation anterior, verifique se seu ambiente tiver python e pip instalado.</span><span class="sxs-lookup"><span data-stu-id="a6397-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="a6397-110">Para obter mais informações, examine Olá [pip documentação quickstart](https://pip.pypa.io/en/latest/quickstart/)e oficial [python instala a documentação](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="a6397-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="a6397-111">Embora haja suporte para ambos os python 2.7 e 3.6, é recomendável toouse python 3.6.</span><span class="sxs-lookup"><span data-stu-id="a6397-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="a6397-112">Instalar</span><span class="sxs-lookup"><span data-stu-id="a6397-112">Install</span></span>

<span data-ttu-id="a6397-113">Olá CLI de malha de serviço do Azure (sfctl) está em um pacote de python.</span><span class="sxs-lookup"><span data-stu-id="a6397-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="a6397-114">versão de mais recente de saudação tooinstall executar:</span><span class="sxs-lookup"><span data-stu-id="a6397-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="a6397-115">Após a instalação, execute `sfctl -h` tooget informações sobre os comandos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a6397-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="a6397-116">Sintaxe da CLI</span><span class="sxs-lookup"><span data-stu-id="a6397-116">CLI syntax</span></span>

<span data-ttu-id="a6397-117">Os comandos são prefixados sempre `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="a6397-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="a6397-118">Para obter informações gerais sobre todos os comandos que você pode usar, use `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="a6397-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="a6397-119">Para obter ajuda com um único comando, use `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="a6397-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="a6397-120">Comandos seguem uma estrutura repetida, com destino de saudação da saudação de comando anterior verbo hello ou ação:</span><span class="sxs-lookup"><span data-stu-id="a6397-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="a6397-121">Neste exemplo, `<object>` é destino Olá `<action>`.</span><span class="sxs-lookup"><span data-stu-id="a6397-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="a6397-122">Selecionar um cluster</span><span class="sxs-lookup"><span data-stu-id="a6397-122">Select a cluster</span></span>

<span data-ttu-id="a6397-123">Antes de executar qualquer operação, você deve selecionar um tooconnect de cluster para.</span><span class="sxs-lookup"><span data-stu-id="a6397-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="a6397-124">Por exemplo, executar Olá tooselect a seguir e conecte-se o cluster toohello com nome hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="a6397-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="a6397-125">Não use clusters do Service Fabric não seguros em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="a6397-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="a6397-126">o ponto de extremidade do Hello cluster deve ser antecedido `http` ou `https`.</span><span class="sxs-lookup"><span data-stu-id="a6397-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="a6397-127">Ele deve incluir a porta Olá para o gateway HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6397-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="a6397-128">endereço e porta de saudação são Olá mesmas Olá URL do Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6397-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="a6397-129">Para clusters protegidos com um certificado, você pode especificar um certificado PEM codificado.</span><span class="sxs-lookup"><span data-stu-id="a6397-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="a6397-130">certificado de saudação pode ser especificado como um único arquivo ou o certificado e o par de chaves.</span><span class="sxs-lookup"><span data-stu-id="a6397-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="a6397-131">Para obter mais informações, consulte [cluster seguro de Azure Service Fabric do Connect tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a6397-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="a6397-132">Operações básicas</span><span class="sxs-lookup"><span data-stu-id="a6397-132">Basic operations</span></span>

<span data-ttu-id="a6397-133">As informações de conexão do cluster persistem em várias sessões do sfctl.</span><span class="sxs-lookup"><span data-stu-id="a6397-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="a6397-134">Depois de selecionar um cluster do Service Fabric, você pode executar qualquer comando de malha do serviço em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a6397-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="a6397-135">Por exemplo, Olá tooget estado de integridade do cluster do Service Fabric, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6397-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="a6397-136">resultados do comando Olá no hello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6397-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="a6397-137">Dicas e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="a6397-137">Tips and troubleshooting</span></span>

<span data-ttu-id="a6397-138">Algumas sugestões e dicas para resolver problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="a6397-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="a6397-139">Converter um certificado de PFX tooPEM formato</span><span class="sxs-lookup"><span data-stu-id="a6397-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="a6397-140">Olá CLI de malha do serviço oferece suporte a certificados de cliente como arquivos do PEM (extensão. PEM).</span><span class="sxs-lookup"><span data-stu-id="a6397-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="a6397-141">Se você usar arquivos PFX do Windows, você deve converter o formato de tooPEM esses certificados.</span><span class="sxs-lookup"><span data-stu-id="a6397-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="a6397-142">tooconvert um arquivo PFX arquivo tooa PEM, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a6397-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="a6397-143">Para obter mais informações, consulte Olá [OpenSSL documentação](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="a6397-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="a6397-144">Problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="a6397-144">Connection issues</span></span>

<span data-ttu-id="a6397-145">Algumas operações podem gerar Olá a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="a6397-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="a6397-146">Verifique se que esse Olá especificado de ponto de extremidade do cluster está disponível e está ouvindo.</span><span class="sxs-lookup"><span data-stu-id="a6397-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="a6397-147">Além disso, verifique se esse hello, que interface de usuário do Service Fabric Explorer está disponível no host e porta.</span><span class="sxs-lookup"><span data-stu-id="a6397-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="a6397-148">ponto de extremidade de saudação de tooupdate, use `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="a6397-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="a6397-149">Logs detalhados</span><span class="sxs-lookup"><span data-stu-id="a6397-149">Detailed logs</span></span>

<span data-ttu-id="a6397-150">Os logs detalhados costumam ser úteis para depurar ou relatar um problema.</span><span class="sxs-lookup"><span data-stu-id="a6397-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="a6397-151">Existe um global `--debug` sinalizador que aumenta o detalhamento de saudação de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="a6397-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="a6397-152">Sintaxe e ajuda de comando</span><span class="sxs-lookup"><span data-stu-id="a6397-152">Command help and syntax</span></span>

<span data-ttu-id="a6397-153">Para obter ajuda com um comando específico ou um grupo de comandos, use Olá `-h` sinalizador:</span><span class="sxs-lookup"><span data-stu-id="a6397-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="a6397-154">Outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6397-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="a6397-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6397-155">Next steps</span></span>

* [<span data-ttu-id="a6397-156">Implantar um aplicativo com hello CLI de malha do serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="a6397-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="a6397-157">Introdução ao Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="a6397-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
