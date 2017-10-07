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
# <a name="azure-service-fabric-and-azure-cli-20"></a>Service Fabric e CLI do Azure 2.0

Olá, ferramenta de linha de comando do Azure (Azure CLI) versão 2.0 inclui comandos toohelp gerenciar clusters de malha do serviço do Azure. Saiba como tooget iniciado com a CLI do Azure e do Service Fabric.

## <a name="install-azure-cli-20"></a>Instalar a CLI 2.0 do Azure

Você pode usar o Azure CLI 2.0 comandos toointeract com e gerenciar clusters de malha do serviço. versão mais recente do hello tooget da CLI do Azure, siga Olá [processo de instalação padrão do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Para obter mais informações, consulte Olá [visão geral do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Sintaxe da CLI do Azure

Na CLI do Azure, todos os comandos do Service Fabric são prefixados com `az sf`. Para obter informações gerais sobre os comandos de saudação, você pode usar, use `az sf -h`. Para obter ajuda com um único comando, use `az sf <command> -h`.

Os comandos do Service Fabric na CLI do Azure seguem este padrão de nomenclatura:

```azurecli
az sf <object> <action>
```

`<object>`é o destino hello para `<action>`.

## <a name="select-a-cluster"></a>Selecionar um cluster

Antes de executar qualquer operação, você deve selecionar um tooconnect de cluster para. Para obter um exemplo, consulte Olá código a seguir. código de saudação conecta cluster segura tooan.

> [!WARNING]
> Não use clusters do Service Fabric não seguros em ambientes de produção.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

o ponto de extremidade do Hello cluster deve ser antecedido `http` ou `https`. Ele deve incluir a porta Olá para o gateway HTTP de saudação. endereço e porta de saudação são Olá mesmas Olá URL do Gerenciador do Service Fabric.

Para clusters protegidos por um certificado, você pode usar arquivos .pem não criptografados ou arquivos .crt e .key. Por exemplo:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Para obter mais informações, consulte [cluster seguro de Azure Service Fabric do Connect tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Olá `select` comando não agir em todas as solicitações antes de retornar. tooverify que você tenha especificado um cluster corretamente, use um comando como `az sf cluster health`. Verifique se que o comando Olá não retorna quaisquer erros.

## <a name="basic-operations"></a>Operações básicas

As informações de conexão do cluster persistem por várias sessões da CLI do Azure. Depois de selecionar um cluster do Service Fabric, você pode executar qualquer comando de malha do serviço em cluster hello.

Por exemplo, Olá tooget estado de integridade do cluster do Service Fabric, use Olá comando a seguir:

```azurecli
az sf cluster health
```

comando Olá resulta no seguinte hello (supondo que a saída JSON é especificada na configuração de CLI do Azure de saudação) de saída:

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

## <a name="tips-and-troubleshooting"></a>Dicas e solução de problemas

Você pode achar Olá informações úteis a seguir se você tiver problemas ao usar comandos do Service Fabric no CLI do Azure.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Converter um certificado de PFX tooPEM formato

A CLI do Azure dá suporte a certificados de cliente como arquivos PEM (extensão .pem). Se você usar arquivos PFX do Windows, você deve converter o formato de tooPEM esses certificados. tooconvert um arquivo PFX arquivo tooa PEM, use Olá comando a seguir:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Para obter mais informações, consulte Olá [OpenSSL documentação](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemas de conexão

Algumas operações podem gerar Olá a seguinte mensagem:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Verifique se que esse Olá especificado de ponto de extremidade do cluster está disponível e está ouvindo. Além disso, verifique se esse hello, que interface de usuário do Service Fabric Explorer está disponível no host e porta. ponto de extremidade de saudação de tooupdate, use `az sf cluster select`.

### <a name="detailed-logs"></a>Logs detalhados

Os logs detalhados costumam ser úteis para depurar ou relatar um problema. CLI do Azure oferece um global `--debug` sinalizador que aumenta o detalhamento de saudação de arquivos de log.

### <a name="command-help-and-syntax"></a>Sintaxe e ajuda de comando

Acompanhamento de comandos do Service Fabric Olá mesmas convenções CLI do Azure. Para obter ajuda com um comando específico ou um grupo de comandos, use Olá `-h` sinalizador:

```azurecli
az sf application -h
```

Veja outro exemplo:

```azurecli
az sf application create -h
```
