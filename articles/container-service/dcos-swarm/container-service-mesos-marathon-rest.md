---
title: aaaManage Azure DC/OS cluster com a API de REST maratona | Microsoft Docs
description: "Implante o cluster de serviço de contêiner do Azure DC/OS contêineres tooan usando Olá maratona REST API."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Gerenciamento de contêiner de DC/sistema operacional por meio de saudação maratona REST API
Controlador de domínio/sistema operacional fornece um ambiente para Implantando e dimensionando cargas de trabalho clusterizadas, enquanto a abstração de hardware subjacente hello. Sobre o DC/OS, há uma estrutura que gerencia o agendamento e a execução das cargas de trabalho de computação. Embora estruturas estão disponíveis para várias cargas de trabalho populares, este documento apresenta criando e escala de implantações de contêiner usando Olá maratona REST API. 

## <a name="prerequisites"></a>Pré-requisitos

Antes de trabalhar nos exemplos, você precisará de um cluster DC/OS configurado no Serviço de Contêiner do Azure. Você também precisa de cluster de toothis toohave conectividade remota. Para obter mais informações sobre esses itens, consulte Olá artigos a seguir:

* [Como implantar um cluster do Serviço de Contêiner do Azure](container-service-deployment.md)
* [Conectar-se o cluster do serviço de contêiner do Azure tooan](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Olá DC/OS APIs de acesso
Depois de cluster do serviço de contêiner do Azure toohello conectado, você pode acessar hello DC/sistema operacional e as APIs REST relacionadas por meio da porta http://localhost:local. exemplos de saudação neste documento pressupõem que você está encapsulando na porta 80. Por exemplo, os pontos de extremidade do hello maratona podem ser contatados em URIs começando com `http://localhost/marathon/v2/`. 

Para obter mais informações sobre Olá várias APIs, consulte a documentação de Mesosphere Olá para Olá [maratona API](https://mesosphere.github.io/marathon/docs/rest-api.html) e [Chronos API](https://mesos.github.io/chronos/docs/api.html)e a documentação do Apache para Olá [Mesos API do Agendador ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Coletar informações do DC/OS e do Marathon
Antes de implantar o cluster de DC/OS contêineres toohello, colete algumas informações sobre o cluster de DC/OS hello, como nomes de saudação e status de saudação DC/OS agentes. toodo consulta assim, Olá `master/slaves` ponto de extremidade da saudação API REST do controlador de domínio/OS. Se tudo correr bem, consulta Olá retorna uma lista de agentes do controlador de domínio/OS e várias propriedades para cada um.

```bash
curl http://localhost/mesos/master/slaves
```

Agora, use Olá maratona `/apps` toocheck de ponto de extremidade para aplicativo implantações toohello DC/SO o cluster atual. Se esse for um cluster novo, você verá uma matriz vazia para os aplicativos.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Implantar um contêiner formatado pelo Docker
Implantar contêineres do Docker formatado por meio de saudação maratona REST API usando um arquivo JSON que descreve a implantação Olá pretendido. Olá, exemplo a seguir implanta um agente Nginx contêiner tooa privado no cluster hello. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy um contêiner Docker formatado, armazene o arquivo JSON de saudação em um local acessível. Próximo, toodeploy Olá contêiner, execute Olá comando a seguir. Especificar nome de saudação do arquivo JSON de saudação (`marathon.json` neste exemplo).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

saída de Hello é a seguir toohello semelhante:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Agora, se você consultar maratona de aplicativos, esse novo aplicativo aparece na saída de hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Acessar o contêiner de saudação

Você pode verificar que Olá que nginx está em execução em um contêiner em um dos agentes de saudação privada no cluster hello. host de saudação do toofind e a porta onde Olá contêiner estiver sendo executado, consultar maratona Olá tarefas em execução: 

```bash
curl localhost/marathon/v2/tasks
```

Localizar o valor de saudação do `host` na saída da saudação (um endereço IP semelhante muito`10.32.0.x`) e o valor de saudação do `ports`.


Fazer um gerenciamento de toohello de conexão terminal (não uma conexão em túnel) de SSH FQDN de cluster hello. Uma vez conectado, fazem Olá solicitação a seguir, substituindo os valores corretos de saudação do `host` e `ports`:

```bash
curl http://host:ports
```

Olá Nginx saída do servidor é a seguir toohello semelhante:

![Nginx do contêiner](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Dimensionar seus contêineres
Você pode usar o hello maratona API tooscale out ou escala em implantações de aplicativo. No exemplo anterior de saudação, você implantou uma instância de um aplicativo. Vamos dimensionar isso toothree instâncias de um aplicativo. Portanto, toodo criar um arquivo JSON usando Olá texto JSON a seguir e armazená-lo em um local acessível.

```json
{ "instances": 3 }
```

A conexão encapsulada, execute Olá comando tooscale aplicativo hello a seguir.

> [!NOTE]
> Olá URI é http://localhost/marathon/v2/apps/ seguido por ID de saudação do hello tooscale de aplicativo. Se você estiver usando o exemplo de Nginx hello fornecido aqui, Olá URI seria http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Por fim, consulte o ponto de extremidade do hello maratona para aplicativos. Você vê que agora há três contêineres Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Comandos equivalentes do PowerShell
Você pode executar essas mesmas ações usando comandos do PowerShell em um sistema Windows.

informações de toogather sobre cluster de DC/OS hello, como nomes de agente e o status do agente, execute Olá comando a seguir:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Implantar contêineres do Docker formatado por meio da maratona usando um arquivo JSON que descreve a implantação Olá pretendido. Olá, exemplo a seguir implanta contêiner de Nginx hello, porta 80 do hello DC/OS agente tooport 80 do contêiner de saudação de associação.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy um contêiner Docker formatado, armazene o arquivo JSON de saudação em um local acessível. Próximo, toodeploy Olá contêiner, execute Olá comando a seguir. Especifique o arquivo JSON do hello caminho toohello (`marathon.json` neste exemplo).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

Você também pode usar o hello maratona API tooscale out ou escala em implantações de aplicativo. No exemplo anterior de saudação, você implantou uma instância de um aplicativo. Vamos dimensionar isso toothree instâncias de um aplicativo. Portanto, toodo criar um arquivo JSON usando Olá texto JSON a seguir e armazená-lo em um local acessível.

```json
{ "instances": 3 }
```

Execute Olá comando tooscale aplicativo hello a seguir:

> [!NOTE]
> Olá URI é http://localhost/marathon/v2/apps/ seguido por ID de saudação do hello tooscale de aplicativo. Se você estiver usando o exemplo de Nginx Olá fornecido aqui, Olá URI seria http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Próximas etapas
* [Leia mais sobre pontos de extremidade de HTTP Mesos Olá](http://mesos.apache.org/documentation/latest/endpoints/)
* [Leia mais sobre Olá maratona REST API](https://mesosphere.github.io/marathon/docs/rest-api.html)

