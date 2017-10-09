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
# <a name="azure-service-fabric-command-line"></a>Linha de comando do Azure Service Fabric

Olá CLI de malha de serviço do Azure (sfctl) é um utilitário de linha de comando para interagir e gerenciar entidades do Azure Service Fabric. O sfctl pode ser usado com clusters do Windows ou Linux. O sfctl é executado em qualquer plataforma onde o python é suportado.

## <a name="prerequisites"></a>Pré-requisitos

Tooinstallation anterior, verifique se seu ambiente tiver python e pip instalado. Para obter mais informações, examine Olá [pip documentação quickstart](https://pip.pypa.io/en/latest/quickstart/)e oficial [python instala a documentação](https://wiki.python.org/moin/BeginnersGuide/Download).

Embora haja suporte para ambos os python 2.7 e 3.6, é recomendável toouse python 3.6.

## <a name="install"></a>Instalar

Olá CLI de malha de serviço do Azure (sfctl) está em um pacote de python. versão de mais recente de saudação tooinstall executar:

```bash
pip install sfctl
```

Após a instalação, execute `sfctl -h` tooget informações sobre os comandos disponíveis.

## <a name="cli-syntax"></a>Sintaxe da CLI

Os comandos são prefixados sempre `sfctl`. Para obter informações gerais sobre todos os comandos que você pode usar, use `sfctl -h`. Para obter ajuda com um único comando, use `sfctl <command> -h`.

Comandos seguem uma estrutura repetida, com destino de saudação da saudação de comando anterior verbo hello ou ação:

```azurecli
sfctl <object> <action>
```

Neste exemplo, `<object>` é destino Olá `<action>`.

## <a name="select-a-cluster"></a>Selecionar um cluster

Antes de executar qualquer operação, você deve selecionar um tooconnect de cluster para. Por exemplo, executar Olá tooselect a seguir e conecte-se o cluster toohello com nome hello `testcluster.com`.

> [!WARNING]
> Não use clusters do Service Fabric não seguros em ambientes de produção.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

o ponto de extremidade do Hello cluster deve ser antecedido `http` ou `https`. Ele deve incluir a porta Olá para o gateway HTTP de saudação. endereço e porta de saudação são Olá mesmas Olá URL do Gerenciador do Service Fabric.

Para clusters protegidos com um certificado, você pode especificar um certificado PEM codificado. certificado de saudação pode ser especificado como um único arquivo ou o certificado e o par de chaves.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Para obter mais informações, consulte [cluster seguro de Azure Service Fabric do Connect tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Operações básicas

As informações de conexão do cluster persistem em várias sessões do sfctl. Depois de selecionar um cluster do Service Fabric, você pode executar qualquer comando de malha do serviço em cluster hello.

Por exemplo, Olá tooget estado de integridade do cluster do Service Fabric, use Olá comando a seguir:

```azurecli
sfctl cluster health
```

resultados do comando Olá no hello saída a seguir:

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

Algumas sugestões e dicas para resolver problemas comuns.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Converter um certificado de PFX tooPEM formato

Olá CLI de malha do serviço oferece suporte a certificados de cliente como arquivos do PEM (extensão. PEM). Se você usar arquivos PFX do Windows, você deve converter o formato de tooPEM esses certificados. tooconvert um arquivo PFX arquivo tooa PEM, use o seguinte comando:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Para obter mais informações, consulte Olá [OpenSSL documentação](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemas de conexão

Algumas operações podem gerar Olá a seguinte mensagem:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Verifique se que esse Olá especificado de ponto de extremidade do cluster está disponível e está ouvindo. Além disso, verifique se esse hello, que interface de usuário do Service Fabric Explorer está disponível no host e porta. ponto de extremidade de saudação de tooupdate, use `sfctl cluster select`.

### <a name="detailed-logs"></a>Logs detalhados

Os logs detalhados costumam ser úteis para depurar ou relatar um problema. Existe um global `--debug` sinalizador que aumenta o detalhamento de saudação de arquivos de log.

### <a name="command-help-and-syntax"></a>Sintaxe e ajuda de comando

Para obter ajuda com um comando específico ou um grupo de comandos, use Olá `-h` sinalizador:

```azurecli
sfctl application -h
```

Outro exemplo:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Próximas etapas

* [Implantar um aplicativo com hello CLI de malha do serviço do Azure](service-fabric-application-lifecycle-sfctl.md)
* [Introdução ao Service Fabric no Linux](service-fabric-get-started-linux.md)
