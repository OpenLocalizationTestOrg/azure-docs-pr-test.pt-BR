---
title: "versão de aaaCanary com Vamp no cluster do Azure DC/sistema operacional | Microsoft Docs"
description: "Como toouse Vamp toocanary versão serviços e aplicar a filtragem em um cluster do serviço de contêiner do Azure DC/OS de tráfego inteligente"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Microsserviços da versão canário com Vamp no cluster de DC/SO do Serviço de Contêiner do Azure

Neste passo a passo, configuramos o Vamp no Serviço de Contêiner do Azure com um cluster de DC/SO. Lançamos canary serviço demonstração de Vamp hello "sava" e, em seguida, resolver uma incompatibilidade de serviço Olá com o Firefox, aplicando a filtragem inteligente. 

> [!TIP] 
> Neste passo a passo Vamp é executado em um cluster de DC/sistema operacional, mas você também pode usar Vamp com Kubernetes como orchestrator hello.
>

## <a name="about-canary-releases-and-vamp"></a>Sobre versões canário e Vamp


A [versão canário](https://martinfowler.com/bliki/CanaryRelease.html) é uma estratégia de implantação inteligente adotada por organizações inovadoras como Netflix, Facebook e Spotify. É uma abordagem que faz sentido, porque reduz problemas, introduz redes de segurança e aumenta a inovação. Então, por que nem todas as empresas estão usando? Estender um tooinclude do pipeline de CI/CD estratégias canary adiciona complexidade e exige experiência e devops extenso conhecimento. É suficiente tooblock pequenas empresas e empresas semelhantes antes de eles mesmo começar. 

[Vamp](http://vamp.io/) é um sistema de código-fonte aberto criado tooease essa transição e coloque canary liberar recursos tooyour preferido contêiner do Agendador. Funcionalidade de canário do Vamp vai além de distribuições baseadas em percentual. Tráfego pode ser filtrado e dividido em uma ampla variedade de condições, por exemplo, usuários específicos tootarget, intervalos de IP ou dispositivos. Vamp monitora e analisa as métricas de desempenho, permitindo a automação baseada em dados reais. Você pode configurar a reversão automática em caso de erros ou dimensionar variantes de serviço individuais com base na carga ou na latência.

## <a name="set-up-azure-container-service-with-dcos"></a>Configurar o Serviço de Contêiner do Azure com o DC/SO



1. [Implantar um cluster de DC/SO](container-service-deployment.md) com um mestre e dois agentes de tamanho padrão. 

2. [Criar um túnel SSH](../container-service-connect.md) cluster do tooconnect toohello DC/OS. Este artigo pressupõe que você criar um túnel de cluster toohello na porta local 80.


## <a name="set-up-vamp"></a>Configurar o Vamp

Agora que você tem um cluster de DC/sistema operacional em execução, você pode instalar Vamp de saudação da interface do usuário do controlador de domínio/OS (http://localhost:80). 

![Interface do usuário do DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

A instalação é feita em duas etapas:

1. **Implantar Elasticsearch**.

2. Em seguida, **implantar Vamp** instalando o pacote de universo Olá Vamp DC/OS.

### <a name="deploy-elasticsearch"></a>Implantar Elasticsearch

O Vamp requer Elasticsearch para coleta e agregação de métricas. Você pode usar o hello [imagens do Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy uma pilha Vamp Elasticsearch compatível.

1. Olá DC/sistema operacional da interface do usuário, vá muito**serviços** e clique em **implantar serviço**.

2. Selecione **modo JSON** de saudação **implantar novo serviço** pop-up.

  ![Selecione o modo JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Cole Olá JSON a seguir. Essa configuração é executado contêiner Olá com 1 GB de RAM e uma verificação básica de integridade na porta de Elasticsearch hello.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Clique em **Implantar**.

  Controlador de domínio/OS implanta contêiner de Elasticsearch hello. Você pode acompanhar o progresso na Olá **serviços** página.  

  ![implantar e?Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Implantar o Vamp

Depois de Elasticsearch informa como **executando**, você pode adicionar Olá Vamp universo de DC/OS pacote. 

1. Vá muito**universo** e procure **vamp**. 
  ![Vamp no DC/SO universal](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Clique em **instalar** toohello próximo vamp pacote e escolha **instalação avançada**.

3. Role para baixo e insira Olá elasticsearch url a seguir: `http://elasticsearch.marathon.mesos:9200`. 

  ![Digitar a URL de Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Clique em **Examine e instale**, em seguida, clique em **instalar** toostart implantação de saudação.  

  O DC/SO implanta todos os componentes necessários do Vamp. Você pode acompanhar o progresso na Olá **serviços** página.
  
  ![Implantar Vamp como um pacote universal](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Depois que a implantação for concluída, você pode acessar Olá Vamp da interface do usuário:

  ![Serviço Vamp no DC/SO](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interface do usuário do Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Implantar seu primeiro serviço

Agora que o Vamp está em execução, implante um serviço de um plano gráfico. 

Em sua forma mais simples, uma [Vamp planta](http://vamp.io/documentation/using-vamp/blueprints/) descreve os pontos de extremidade da saudação (gateways), clusters e toodeploy de serviços. Vamp usa clusters toogroup variantes diferentes Olá mesmo serviço em grupos lógicos para liberar canary ou A / B teste.  

Esse cenário usa um aplicativo monolítico de exemplo chamado [ **sava**](https://github.com/magneticio/sava), que está na versão 1.0. monolito Olá é empacotado em um contêiner do Docker, que está no Hub do Docker em magneticio/sava:1.0.0. Olá aplicativo normalmente é executado na porta 8080, mas você deseja tooexpose na porta 9050 neste caso. Implante o aplicativo de saudação por meio de Vamp usando uma estrutura simple.

1. Vá muito**implantações**.

2. Clique em **Adicionar**.

3. Colar em Olá seguindo plano gráfico YAML. Esse plano gráfico contém um cluster com apenas uma variante de serviço, que podemos alterar em uma etapa posterior:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Clique em **Salvar**. Vamp inicia a implantação de saudação.

implantação Hello está listada no hello **implantações** página. Clique em Olá implantação toomonitor seu status.

![Interface do usuário do Vamp – implantação de sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![serviço sava na interface do usuário do Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

São criados dois gateways, que são listados em Olá **Gateways** página:

* uma saudação de tooaccess estável do ponto de extremidade que está executando o serviço (porta 9050) 
* um gateway interno gerenciado pelo Vamp (mais informações sobre este gateway mais tarde). 

![Interface do usuário do Vamp – gateways de sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

serviço de sava Olá implantou, mas você não pode acessá-lo externamente porque Olá balanceador de carga do Azure não sabe tooforward tráfego tooit ainda. serviço de saudação tooaccess, Olá de atualização de configuração de rede do Azure.


## <a name="update-hello-azure-network-configuration"></a>Atualizar a configuração de rede do Azure Olá

Serviço de sava vamp implantado Olá em nós de agente do DC/OS hello, expor um ponto de extremidade estável na porta 9050. tooaccess serviço de saudação do cluster fora do DC/OS hello, verifique Olá seguinte configuração de rede do Azure toohello alterações em sua implantação de cluster: 

1. **Configurar Olá balanceador de carga do Azure** para agentes hello (Olá recurso denominado **dcos-agente lb xxxx**) com um teste de integridade e o tráfego de tooforward uma regra em instâncias de sava toohello 9050 porta. 

2. **Grupo de segurança de rede atualização Olá** para agentes pública hello (Olá recurso denominado **XXXX-agente-público-nsg-XXXX**) tooallow o tráfego na porta 9050.

Para obter etapas detalhadas toocomplete essas tarefas usando hello Azure portal, consulte [ativar o aplicativo de serviço de contêiner do Azure do acesso público tooan](container-service-enable-public-access.md). Especifique a porta 9050 para todas as configurações de porta.


Quando tudo o que tiver sido criado, acesse toohello **visão geral** folha Olá DC/OS agente de Balanceador de carga (Olá recurso denominado **dcos-agente lb xxxx**). Localize Olá **endereço IP público**e usar o hello endereço tooaccess sava na porta 9050.

![Portal do Azure – obter endereço IP público](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Executar uma versão canário

Suponha que você tenha uma nova versão do aplicativo que você deseja que a versão toocanary em produção. Você tem em contêineres como magneticio/sava:1.1.0 e toogo pronto. Vamp permite adicionar novos toohello de serviços em execução de implantação. Esses serviços "mesclados" são implantados junto com os serviços existentes no cluster Olá Olá e recebe um peso de 0%. Nenhum tráfego é o serviço de tooa roteados recentemente mesclada até que você ajustar a distribuição de tráfego hello. controle deslizante de peso de saudação no hello Vamp da interface do usuário lhe dá controle total sobre a distribuição hello, permitindo ajustes incrementais (versão canary) ou uma reversão de instantâneo.

### <a name="merge-a-new-service-variant"></a>Mesclar uma nova variante do serviço

toomerge Olá novo sava 1.1 serviço com hello executando implantação:

1. No hello Vamp da interface do usuário, clique em **plantas**.

2. Clique em **adicionar** e colar em Olá seguindo plano gráfico YAML: Este diagrama descreve um novo toodeploy de variante (sava: 1.1.0) do serviço em cluster existente da saudação (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Clique em **Salvar**. esquema de saudação é armazenada e listada no hello **plantas** página.

4. Menu de ação Olá aberta no esquema de sava: 1.1 hello e clique em **Mesclar para**.

  ![Interface do usuário do Vamp – planos gráficos](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Selecione Olá **sava** implantação e clique em **mesclar**.

  ![Vamp da interface do usuário - toodeployment plano gráfico de mesclagem](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp implanta Olá nova sava: 1.1.0 serviço variante descrito no esquema Olá junto com sava: 1.0.0 em Olá **sava_cluster** de saudação executando a implantação. 

![Interface do usuário do Vamp – implantação sava atualizada](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Olá **sava_cluster/sava/webport** gateway (ponto de extremidade de cluster Olá) também é atualizada, adicionar uma rota toohello recentemente implantado sava: 1.1.0. Neste momento, nenhum tráfego é roteado aqui (Olá **peso** é definido % too0).

![Interface do usuário do Vamp – gateway do cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Versão canário

Nas versões do sava implantados em Olá mesmo cluster, ajustar a distribuição de saudação do tráfego entre elas, movendo Olá **peso** controle deslizante.

1. Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avançar muito**peso**.

2. Defina Olá peso distribuição too50%/50% e clique em **salvar**.

  ![Interface do usuário do Vamp – controle deslizante de peso de gateway](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Voltar tooyour navegador e atualize a página de sava de saudação mais algumas vezes. aplicativo de sava Hello agora alterna entre uma página sava: 1.0 e uma página de sava: 1.1.

  ![alternando os serviços sava1.0 e sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Essa alternância de página Olá funciona melhor com hello "Incógnita" ou "Anonymous" modo do navegador devido ao caching Olá ativos estático.
  >

### <a name="filter-traffic"></a>Filtrar o tráfego

Suponha que, depois da implantação, você descobriu uma incompatibilidade no sava:1.1.0 que causa problemas de exibição em navegadores Firefox. Você pode definir Vamp toofilter o tráfego de entrada e direcionar a todos os usuários do Firefox fazer toohello conhecido sava: 1.0.0 estável. Esse filtro instantaneamente resolve Olá interrupção para usuários do Firefox, enquanto todos os outros continua tooenjoy benefícios Olá Olá aprimorado sava: 1.1.0.

Vamp usa **condições** toofilter o tráfego entre as rotas de um gateway. O tráfego é filtrado pela primeira vez e direcionadas acordo toohello condições aplicadas tooeach rota. Todo o tráfego restante é distribuído de acordo com a configuração de peso de gateway toohello.

Você pode criar uma condição toofilter todos os usuários do Firefox e encaminhá-los sava: 1.0.0 toohello antigo:

1. Em Olá sava_cluster/sava/webport **Gateways** , clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd um **condição** toohello rota sava/sava_cluster/sava:1.0.0/webport. 

2. Insira a condição de saudação **agente do usuário = = Firefox** e clique em ![Vamp UI - salvar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp adiciona a condição de saudação com um nível padrão de 0%. toostart o tráfego de filtragem, você precisa de intensidade de condição de saudação tooadjust.

3. Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange Olá **força** aplicada toohello condição.
 
4. Saudação de conjunto **força** too100% e clique em ![Vamp UI - salvar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp agora envia todo o tráfego correspondente Olá condição (todos os usuários Firefox) toosava:1.0.0.

  ![Vamp da interface do usuário - aplicar toogateway condição](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Por fim, ajuste todos os demais tráfego (todos os usuários não Firefox) toohello novo sava: 1.1.0 Olá toosend de peso de gateway. Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avançar muito**peso** e definir a distribuição de peso Olá para 100% seja direcionado toohello rota sava/sava_cluster/sava:1.1.0/webport.

  Todo o tráfego não filtrado pela condição Olá agora é direcionado toohello novo sava: 1.1.0.

6. filtro de saudação toosee em ação, abra dois navegadores diferentes (um Firefox e um outro navegador) e acessar o serviço de sava de saudação do. Todas as solicitações de Firefox são enviadas toosava:1.0.0, enquanto todos os outros navegadores estão toosava:1.1.0 direcionado.

  ![Interface do usuário do Vamp – filtrar tráfego](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Resumindo

Este artigo foi tooVamp uma rápida introdução em um cluster de DC/OS. Para começar, você obteve Vamp para cima e em execução em seu contêiner de serviço DC/sistema operacional do Azure cluster, implantado um serviço com um esquema Vamp acessou no ponto de extremidade exposto de saudação (gateway).

Também abordamos na alguns recursos avançados do Vamp: mesclagem de um novo serviço variant toohello executando a implantação e apresentando-lo incrementalmente, filtragem de tráfego tooresolve uma incompatibilidade conhecida.


## <a name="next-steps"></a>Próximas etapas

* Saiba como gerenciar Vamp ações por meio de saudação [Vamp REST API](http://vamp.io/documentation/api/api-reference/).

* Crie scripts de automação do Vamp no Node.js e execute-os como [Fluxos de trabalho do Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Consulte [Tutoriais do VAMP](http://vamp.io/documentation/tutorials/overview/) adicionais.

