---
title: "aaaLoad equilibrar Kubernetes contêineres no Azure | Microsoft Docs"
description: "Conecte-se externamente e balanceie a carga em vários contêineres em um cluster Kubernetes no Serviço de Contêiner do Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Microsserviços, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Balancear a carga de contêineres em um cluster Kubernetes no Serviço de Contêiner do Azure 
Este artigo apresenta o balanceamento de carga em um cluster Kubernetes no Serviço de Contêiner do Azure. Balanceamento de carga fornece um endereço IP acessível externamente para serviço de saudação e distribui o tráfego de rede entre os compartimentos de saudação em execução no agente de VMs.

Você pode configurar um toouse de serviço Kubernetes [balanceador de carga do Azure](../../load-balancer/load-balancer-overview.md) toomanage tráfego de rede (TCP) externo. Com uma configuração adicional, o balanceamento de carga e roteamento de tráfego HTTP ou HTTPS ou cenários mais avançados são possíveis.

## <a name="prerequisites"></a>Pré-requisitos
* [Implantar um cluster Kubernetes](container-service-kubernetes-walkthrough.md) no Serviço de Contêiner do Azure
* [Conecte o cliente](../container-service-connect.md) tooyour cluster

## <a name="azure-load-balancer"></a>Azure Load Balancer

Por padrão, um cluster Kubernetes implantado no serviço de contêiner do Azure inclui um balanceador de carga do Azure voltado para a Internet para agente Olá VMs. (Um recurso de Balanceador de carga separado é configurado para mestre Olá VMs.) O Azure Load Balancer é um balanceador de carga de Camada 4. No momento, o balanceador de carga de saudação suporta apenas o tráfego TCP em Kubernetes.

Ao criar um serviço Kubernetes, pode configurar automaticamente o serviço de toohello acesso do tooallow de Balanceador de carga do Azure hello. Balanceador de carga tooconfigure hello, serviço de saudação do conjunto `type` muito`LoadBalancer`. Balanceador de carga Olá cria uma regra toomap um endereço IP público e o número da porta de entrada serviço tráfego toohello endereços IP privados e números de porta de compartimentos de saudação no agente de VMs (e vice-versa para o tráfego de resposta). 

 Estes são dois exemplos que mostram como tooset Olá Kubernetes serviço `type` muito`LoadBalancer`. (Depois de tentar exemplos de hello, excluir Olá implantações se você não precisar mais deles.)

### <a name="example-use-hello-kubectl-expose-command"></a>Exemplo: Saudação de uso `kubectl expose` comando 
Olá [Kubernetes passo a passo](container-service-kubernetes-walkthrough.md) inclui um exemplo de como tooexpose um serviço com hello `kubectl expose` comando e sua `--type=LoadBalancer` sinalizador. Aqui estão as etapas de saudação:

1. Inicie uma nova implantação do contêiner. Olá, por exemplo, após o comando inicia uma nova implantação chamada `mynginx`. Olá implantação consiste em três contêineres com base na imagem do Docker Olá Olá Nginx servidor de web.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Verificar se os contêineres de saudação estão em execução. Por exemplo, se você consultar para contêineres de saudação com `kubectl get pods`, você vê saída semelhante toohello seguinte:

    ![Obter contêineres Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure Olá carga tooaccept tráfego externo toohello implantação de Balanceador, execute `kubectl expose` com `--type=LoadBalancer`. Olá seguinte comando expõe servidor de Nginx Olá na porta 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Tipo `kubectl get svc` estado de saudação do toosee dos serviços de Olá cluster hello. Enquanto o balanceador de carga Olá configura regra hello, Olá `EXTERNAL-IP` de saudação serviço aparece como `<pending>`. Após alguns minutos, o endereço IP externo de saudação é configurado: 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Verifique se que você pode acessar o serviço de saudação no endereço IP externo de saudação. Por exemplo, abra um endereço IP do web navegador toohello mostrado. navegador de saudação mostra o servidor de web Nginx Olá em execução em um dos contêineres de saudação. Ou então, Olá execução `curl` ou `wget` comando. Por exemplo:

    ```
    curl 13.82.93.130
    ```

    Você deve ver uma saída semelhante a:

    ![Acessar o Nginx com curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. configuração de saudação toosee hello Azure do balanceador de carga, vá toohello [portal do Azure](https://portal.azure.com).

7. Procurar o grupo de recursos Olá para o cluster do serviço de contêiner e selecione o balanceador de carga Olá para agente Olá VMs. Seu nome deve ser Olá mesmo que o serviço de contêiner de saudação. (Não escolher Olá balanceador de carga de nós mestres hello, Olá um cujo nome inclui **lb mestre**.) 

    ![Balanceador de carga no grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. toosee Olá detalhes de configuração de Balanceador de carga hello, clique em **regras de balanceamento de carga** e o nome de saudação da regra de saudação que foi configurada.

    ![Regras do balanceador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Exemplo: Especificar `type: LoadBalancer` no arquivo de configuração de serviço Olá

Se você implantar um aplicativo de contêiner Kubernetes de um YAML ou JSON [arquivo de configuração de serviço](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique um balanceador externo adicionando Olá especificação do serviço toohello linha a seguir:

```YAML
 "type": "LoadBalancer"
``` 



Olá, etapas a seguir usam Olá Kubernetes [convidados exemplo](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Este exemplo é um aplicativo Web de várias camadas com base em imagens do Docker PHP e Redis. Você pode especificar no arquivo de configuração de serviço Olá que servidor Olá front-end PHP usa o balanceador de carga do Azure hello.

1. Baixe o arquivo hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Procurar Olá `spec` para Olá `frontend` serviço.
3. Descomente a linha hello `type: LoadBalancer`.

    ![Balanceador de carga na configuração de serviço](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Salvar arquivo hello e implante o aplicativo hello executando Olá comando a seguir:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Tipo `kubectl get svc` estado de saudação do toosee dos serviços de Olá cluster hello. Enquanto o balanceador de carga Olá configura regra hello, Olá `EXTERNAL-IP` de saudação `frontend` serviço aparece como `<pending>`. Após alguns minutos, o endereço IP externo de saudação é configurado: 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Verifique se que você pode acessar o serviço de saudação no endereço IP externo de saudação. Por exemplo, você pode abrir um web navegador toohello endereço IP externo do serviço de saudação.

    ![Acessar a página de recados externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Você pode adicionar entradas da página de recados.

7. configuração de saudação toosee hello Azure do balanceador de carga, navegue para o recurso de Balanceador de carga Olá para cluster Olá Olá [portal do Azure](https://portal.azure.com). Consulte as etapas no exemplo anterior Olá Olá.

### <a name="considerations"></a>Considerações

* Criação de regra de Balanceador de carga Olá ocorre de maneira assíncrona e informações sobre balanceador Olá provisionado são publicadas no serviço de saudação `status.loadBalancer` campo.
* Cada serviço é automaticamente atribuído a seu próprio endereço IP virtual no balanceador de carga de saudação.
* Se você quiser balanceador de carga Olá tooreach por um nome DNS, trabalhe com seu toocreate de provedor de serviços de domínio um nome DNS para o endereço IP da regra de saudação.

## <a name="http-or-https-traffic"></a>Tráfego HTTP ou HTTPS

Saldo de tooload HTTP ou HTTPS tráfego toocontainer aplicativos web e gerenciar certificados de segurança de camada de transporte (TLS), você pode usar o hello Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos. Uma entrada é uma coleção de regras que permitem conexões de entrada de serviços de cluster tooreach hello. Para um toowork de recurso de entrada, o cluster de Kubernetes de saudação deve ter uma [controlador entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) em execução.

O Serviço de Contêiner do Azure não implementa um controlador de Entrada Kubernetes automaticamente. Existem várias implementações de controlador disponíveis. Atualmente, Olá [controlador Nginx entrada](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) é recomendável tooconfigure regras de entrada e balanceamento de carga de tráfego HTTP e HTTPS. 

Para obter mais informações, consulte Olá [documentação do controlador de entrada Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Ao usar o hello controlador Nginx entrada no serviço de contêiner do Azure, você deve expor na implantação do controlador hello como um serviço com `type: LoadBalancer`. Isso configura o controlador de toohello tráfego do tooroute de Balanceador de carga do Azure hello. Para obter mais informações, consulte a seção anterior hello.


## <a name="next-steps"></a>Próximas etapas

* Consulte Olá [Kubernetes LoadBalancer documentação](https://kubernetes.io/docs/user-guide/load-balancer/)
* Saiba mais sobre [controladores de Entrada e Entrada Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)
* Consulte [exemplos do Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)

