---
title: "aaaManage Azure DC/OS de cluster com interface de usuário maratona | Microsoft Docs"
description: "Implante o serviço de cluster do serviço de contêiner do Azure de tooan de contêineres usando a interface da web maratona hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Gerenciar um cluster de serviço de contêiner do Azure DC/OS por meio da interface da web maratona Olá
Controlador de domínio/sistema operacional fornece um ambiente para Implantando e dimensionando cargas de trabalho clusterizadas, enquanto a abstração de hardware subjacente hello. Sobre o DC/OS, há uma estrutura que gerencia o agendamento e a execução das cargas de trabalho de computação.

Enquanto as estruturas estão disponíveis para várias cargas de trabalho populares, este documento descreve como tooget iniciada implantar contêineres com maratona. 


## <a name="prerequisites"></a>Pré-requisitos
Antes de trabalhar nos exemplos, você precisará de um cluster DC/OS configurado no Serviço de Contêiner do Azure. Você também precisa de cluster de toothis toohave conectividade remota. Para obter mais informações sobre esses itens, consulte Olá artigos a seguir:

* [Implantar um cluster do Serviço de Contêiner do Azure](container-service-deployment.md)
* [Conecte-se o cluster do serviço de contêiner do Azure tooan](../container-service-connect.md)

> [!NOTE]
> Este artigo pressupõe que você está encapsulando toohello cluster de DC/OS pela sua porta local 80.
>

## <a name="explore-hello-dcos-ui"></a>Explorar Olá DC/sistema operacional da interface do usuário
Com um túnel de Secure Shell (SSH) [estabelecida](../container-service-connect.md), procurar toohttp://localhost/. Isso carrega a interface da web hello DC/sistema operacional e mostra informações sobre o cluster hello, como os recursos usados, os agentes active e serviços em execução.

![Interface do usuário do DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Explorar Olá maratona da interface do usuário
Olá toosee maratona da interface do usuário, procure toohttp://localhost/marathon. Nessa tela, você pode iniciar um novo contêiner ou outro aplicativo no cluster do serviço de contêiner do Azure DC/OS hello. Você também pode ver informações sobre a execução de aplicativos e de contêineres.  

![Interface do usuário do Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Implantar um contêiner formatado pelo Docker
toodeploy um novo contêiner usando maratona, clique em **criar aplicativo**e digite Olá segue as informações nas guias de formulário hello:

| Campo | Valor |
| --- | --- |
| ID |nginx |
| Memória | 32 |
| Imagem |nginx |
| Rede |Com ponte |
| Porta de host |80 |
| Protocolo |TCP |

![Interface do usuário do novo aplicativo – geral](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interface do usuário do novo aplicativo – contêiner do Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interface do usuário do novo aplicativo - descoberta de serviço e portas](./media/container-service-mesos-marathon-ui/dcos6.png)

Se você quiser toostatically mapa Olá contêiner tooa porta no agente Olá, é necessário toouse modo JSON. toodo então, alternar Assistente do novo aplicativo hello muito**JSON modo** usando a alternância de saudação. Digite hello após a configuração em Olá `portMappings` seção Olá da definição do aplicativo. Este exemplo associa a porta 80 do tooport 80 do contêiner saudação do agente de controlador de domínio/OS hello. Depois de fazer essa alteração, você pode remover o assistente do Modo JSON.

```none
"hostPort": 80,
```

![Interface do usuário do novo aplicativo – exemplo de porta 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Se você quiser tooenable verificações de integridade, definir um caminho em Olá **verificações de integridade** guia.

![Verificações de integridade da interface do usuário do novo aplicativo](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

cluster de DC/OS de saudação é implantado com o conjunto de agentes públicos e privados. Para aplicativos do hello cluster toobe tooaccess capaz de saudação à Internet, você precisa de agente público do toodeploy Olá aplicativos tooa. toodo assim, marque Olá **opcional** guia do Assistente do novo aplicativo hello e digite **slave_public** para Olá **funções de recurso aceitos**.

Em seguida, clique em **Criar Aplicativo**.

![Interface do usuário do novo aplicativo - configuração do agente público](./media/container-service-mesos-marathon-ui/dcos14.png)

Novamente na página principal do maratona Olá, você pode ver o status de implantação de saudação do contêiner de saudação. Inicialmente, você vê um status de **Implantando**. Depois de uma implantação bem-sucedida, Olá alterações de status muito**executando**.

![Interface do usuário da página principal do Marathon – status da implantação do contêiner](./media/container-service-mesos-marathon-ui/dcos7.png)

Quando você alternar toohello back DC/OS IU da web (http://localhost/), você verá que uma tarefa (nesse caso, um contêiner Docker formatado) está em execução no cluster de DC/OS de saudação.

![Controlador de domínio/OS interface da web – tarefas em execução no cluster Olá](./media/container-service-mesos-marathon-ui/dcos8.png)

nó de cluster de saudação toosee que Olá tarefa está em execução no, clique em Olá **nós** guia.

![Interface do usuário Web DC/OS - nó do cluster de tarefa](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Acessar o contêiner de saudação

Neste exemplo, o aplicativo hello está em execução em um nó de agente pública. Acessar o aplicativo hello da saudação internet navegando toohello agente FQDN do cluster Olá: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, onde:

* **DNSPREFIX** é Olá prefixo DNS que você forneceu quando você implantou o cluster hello.
* **REGIÃO** é Olá região na qual o grupo de recursos está localizado.

    ![Nginx da Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Próximas etapas
* [Trabalhar com o controlador de domínio/OS e Olá maratona API](container-service-mesos-marathon-rest.md)

* Mergulho profundo na hello Azure serviço de contêiner com Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
