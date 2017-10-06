---
title: "aaaContainer solução de monitoramento no Azure Log Analytics | Microsoft Docs"
description: "Olá solução de monitoramento de contêiner na análise de Log ajuda a exibir e gerenciar o Docker e Windows hosts de contêiner em um único local."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Solução de Monitoramento de contêiner no Log Analytics

![Símbolo dos Contêineres](./media/log-analytics-containers/containers-symbol.png)

Este artigo descreve como tooset backup e use Olá solução de monitoramento de contêiner na análise de Log, o que ajuda a exibir e gerenciar o Docker e Windows hosts de contêiner em um único local. O docker é um sistema de virtualização de software usado contêineres toocreate automatizam a implantação de software tootheir IT infraestrutura.

Olá mostra de solução que estiver executando contêineres, qual imagem de contêiner que estejam em execução, e onde contêineres estão em execução. Você pode exibir informações detalhadas de auditoria, mostrando os comandos usados com contêineres. E, você pode solucionar problemas de contêineres exibindo e pesquisando centralizado de logs sem a necessidade de exibição tooremotely Docker ou hosts de Windows. Você pode encontrar contêineres que podem estar com ruídos e consumindo recursos em excesso em um host. E você pode exibir o uso de CPU, memória, armazenamento e rede e informações de desempenho centralizadas para contêineres. Nos computadores que executam o Windows, você pode centralizar e comparar os logs do Windows Server, do Hyper-V e dos contêineres do Docker. solução de saudação dá suporte à saudação orchestrators contêiner a seguir:

- Docker Swarm
- DC/OS
- kubernetes
- Service Fabric
- Red Hat OpenShift


Olá diagrama a seguir mostra as relações de saudação entre vários hosts de contêiner e agentes com o OMS.

![Diagrama de contêineres](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Requisitos do sistema

Antes de começar, examine Olá tooverify detalhes que você atenda aos pré-requisitos Olá a seguir.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Suporte de solução de monitoramento de contêiner para Docker Orchestrator e plataforma do SO
Olá tabela a seguir descreve Olá orquestração de Docker e o sistema operacional monitoramento suporte de inventário de contêiner, desempenho e logs de análise de Log.   

| | ACS | Linux | Windows | Contêiner<br>Inventário | Imagem<br>Inventário | Nó<br>Inventário | Contêiner<br>Desempenho | Contêiner<br>Evento | Evento<br>Registro | Contêiner<br>Registro |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| O Barramento de<br>Fabric | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>Shift | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(autônomo) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux Server<br>(autônomo) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Versões do Docker com suporte no Linux

- Docker 1.11 too1.13
- Docker CE e EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>As distribuições de Linux x64 têm suporte como hosts de contêiner

- Ubuntu 14.04 LTS e 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 e 7.3
- SLES 12
- RHEL 7.2 e 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Sistema operacional Windows com suporte

- Windows Server 2016
- Edição de aniversário do Windows 10 (Professional ou Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Versões do Docker do Windows com suporte

- Docker 1.12 e 1.13
- Docker 17.03.0 e mais recente

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação.

1. Adicionar Olá monitoramento de contêiner solução tooyour OMS espaço de trabalho de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

2. Instale e use o Docker com um agente do OMS.  Com base no seu sistema operacional, você pode escolher Olá métodos a seguir:

  * Em sistemas operacionais Linux com suporte, instale e execute Docker e, em seguida, instalar e configurar Olá [agente do OMS para Linux](log-analytics-agent-linux.md).  
  * Em CoreOS, você não pode executar Olá agente do OMS para Linux. Em vez disso, você deve executar uma versão em contêineres de saudação do agente do OMS para Linux. Confira [Hosts de contêiner do Linux incluindo CoreOS](#for-all-linux-container-hosts-including-coreos) ou [Hosts de contêiner do Linux do Azure Governamental incluindo CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se você estiver trabalhando com contêineres na nuvem do Azure Governamental.
  * No Windows Server 2016 e Windows 10, instale Olá mecanismo do Docker e o cliente e informações de toogather um agente de conexão e enviá-lo tooLog análise.  

### <a name="container-services"></a>Serviços de Contêiner

- Se você tiver um ambiente do Red Hat OpenShift, confira [Configurar um agente do OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Se você tiver um cluster de Kubernetes usando Olá serviço de contêiner do Azure, examine [monitorar um cluster do serviço de contêiner do Azure com o Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Se você tiver um cluster de DC/SO do Serviço de Contêiner do Azure, saiba mais em [Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Se você tiver um ambiente no modo Docker Swarm, saiba mais em [Configurar um agente do OMS para o Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Se você usa contêineres com o Service Fabric, saiba mais em [Visão geral do Azure Service Fabric](../service-fabric/service-fabric-overview.md).
- Saudação de revisão [mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artigo para obter informações adicionais sobre como tooinstall e configurar os mecanismos de Docker em computadores que executam o Windows.

> [!IMPORTANT]
> Deve estar executando o docker **antes de** instalar Olá [agente do OMS para Linux](log-analytics-agent-linux.md) em seus hosts de contêiner. Se você já tiver instalado o agente de saudação antes de instalar o Docker, será necessário tooreinstall Olá agente do OMS para Linux. Para obter mais informações sobre o Docker, consulte Olá [site Docker](https://www.docker.com).


## <a name="linux-container-hosts"></a>Hosts de contêiner do Linux

Depois de instalar o Docker, use Olá seguindo as configurações para o agente de saudação do contêiner host tooconfigure para uso com o Docker. Primeiro, é necessário a ID do espaço de trabalho do OMS e a chave, o que você pode encontrar no hello portal do Azure. No espaço de trabalho, clique em **início rápido** > **computadores** tooview sua **ID do espaço de trabalho** e **chave primária**.  Copie e cole os dois em seu editor favorito.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Para todos os hosts de contêiner do Linux, exceto CoreOS

- Para obter mais informações e etapas sobre como tooinstall Olá agente do OMS para Linux, consulte [conectar seu tooOperations de computadores Linux Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Para todos os hosts de contêiner do Linux, incluindo o CoreOS

Inicie o contêiner OMS Olá que você deseja toomonitor. Modifique e use Olá exemplo a seguir:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Para todos os hosts de contêiner do Linux no Azure Governamental, incluindo CoreOS

Inicie o contêiner OMS Olá que você deseja toomonitor. Modifique e use Olá exemplo a seguir:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Alternando do usando um tooone de agente Linux instalado em um contêiner
Se você anteriormente usada agente instalado diretamente do hello e deseja tooinstead usar um agente em execução em um contêiner, você deve primeiro remover Olá agente do OMS para Linux. Consulte [Olá de desinstalação do agente do OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand como toosuccessfully desinstalar Olá agente.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Configurar um agente do OMS para o Docker Swarm

Você pode executar Olá agente do OMS como um serviço global em Docker Swarm. Use Olá toocreate informações sobre um serviço de agente do OMS a seguir. É necessário tooinsert sua ID de espaço de trabalho do OMS e a chave primária.

- Execute o seguinte de Olá no nó mestre hello.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Configurar um Agente do OMS para o Red Hat OpenShift
Há três maneiras tooadd Olá agente do OMS tooRed Hat OpenShift toostart coleta contêiner dados de monitoramento.

* [Instalar Olá agente do OMS para Linux](log-analytics-agent-linux.md) diretamente em cada nó de OpenShift  
* [Habilitar a extensão de VM do Log Analytics](log-analytics-azure-vm-extension.md) em cada nó do OpenShift que reside no Azure  
* Instalar Olá agente do OMS como um conjunto de daemon OpenShift  

Nesta seção, abordaremos Olá etapas tooinstall necessário Olá agente do OMS como um conjunto de daemon OpenShift.  

1. Logon toohello OpenShift nó e cópia Olá yaml arquivo mestre [omsagent.yaml ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) do GitHub tooyour mestre nó e modificar o valor de saudação com sua ID de espaço de trabalho do OMS e sua chave primária.
2. Executar um projeto de saudação toocreate comandos a seguir para OMS e definir a conta de usuário de saudação.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Olá toodeploy conjunto de daemon, execute o seguinte de saudação:

    `oc create -f ocp-omsagent.yaml`

5. tooverify está configurado e funcionando corretamente, digite o seguinte hello:

    `oc describe daemonset omsagent`  

    e a saída de hello deve se parecer com:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Se você quiser toouse segredos toosecure sua ID de espaço de trabalho do OMS e a chave primária ao usar arquivo de conjunto daemon yaml de agente do OMS hello, execute Olá etapas a seguir.

1. Logon toohello OpenShift nó e cópia Olá yaml arquivo mestre [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e o segredo Gerando script [secretgen.sh ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) do GitHub.  Esse script vai gerar arquivo de yaml de segredos Olá para ID de espaço de trabalho do OMS e a chave primária toosecure seu secrete informações.  
2. Executar um projeto de saudação toocreate comandos a seguir para OMS e definir a conta de usuário de saudação. segredo de saudação Gerando script solicita sua ID de espaço de trabalho do OMS <WSID> e a chave primária <KEY> e após a conclusão, ele cria o arquivo de ocp-secret.yaml de saudação.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Implante arquivo secreto Olá executando Olá seguinte:

    `oc create -f ocp-secret.yaml`

5. Verifique se a implantação executando Olá seguinte:

    `oc describe secret omsagent-secret`  

    e a saída de hello deve se parecer com:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Implante arquivo de conjunto de daemon yaml agente do OMS Olá executando Olá seguinte:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Verifique se a implantação executando Olá seguinte:

    `oc describe ds oms`

    e a saída de hello deve se parecer com:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Proteger suas informações secretas do Docker Swarm e Kubernetes

Proteja sua ID do Espaço de Trabalho do OMS e as Chaves Primárias secretas para os serviços de contêiner Docker Swarm e Kubernetes.

#### <a name="secure-secrets-for-docker-swarm"></a>Proteger segredos do Docker Swarm

Para Docker Swarm, quando segredo Olá para o ID do espaço de trabalho e a chave primária é criado, você pode executar Olá criar serviço do Docker Olá para OMSagent. Use suas informações de segredo de Olá toocreate informações a seguir.

1. Execute o seguinte de Olá no nó mestre hello.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Verifique se os segredos foram criados corretamente.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Olá execução após o comando toomount Olá segredos toohello em contêineres do agente do OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Proteger segredos do Kubernetes com arquivos yaml

Para Kubernetes, você pode usar um arquivo de yaml script toogenerate Olá segredos para a ID do espaço de trabalho e a chave primária. Em Olá [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) página, os arquivos que você pode usar com ou sem informações de segredo.

- saudação padrão DaemonSet de agente do OMS não tem informações secretas (omsagent.yaml)
- arquivo de yaml Olá DaemonSet de agente do OMS usa informações secretas (omsagent-ds-secrets.yaml) com secreta arquivo geração de scripts toogenerate Olá segredos yaml (omsagentsecret.yaml).

Você pode escolher toocreate omsagent DaemonSets com ou sem segredos.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Arquivo yaml do DaemonSet do OMSagent Padrão sem segredos

- Para o arquivo yaml do saudação padrão DaemonSet de agente do OMS, substitua Olá `<WSID>` e `<KEY>` tooyour WSID e a chave. Copiar nó mestre da saudação arquivo tooyour e seguir Olá execução:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Arquivo yaml do DaemonSet do OMSagent Padrão com segredos

1. toouse DaemonSet de agente do OMS usando informações secretas, criar segredos Olá primeiro.
    1. Copie o script hello e arquivo de modelo de segredo e verifique se estão em uma saudação mesmo diretório.
        - Script de geração de segredo – secret-gen.sh
        - modelo de segredo – secret-template.yaml
    2. Execute script hello, como Olá exemplo a seguir. script Hello solicita Olá ID do espaço de trabalho do OMS e a chave primária e depois que você inseri-los, script hello cria um arquivo de segredo yaml para possam ser executados.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Crie pod de segredos Olá executando Olá seguinte:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, execute Olá seguinte:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        O resultado deve ser semelhante a este:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        O resultado deve ser semelhante a este:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Criar o omsagent daemon-set executando ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Verifique se esse Olá que daemonset de agente do OMS está em execução, toohello semelhante a seguir:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Para Kubernetes, use um arquivo de yaml de segredos do script toogenerate Olá para o ID do espaço de trabalho e chave primária. Saudação de uso a seguir exemplos de informações com hello [omsagent yaml arquivo](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure suas informações secretas.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Hosts de contêiner do Windows

### <a name="preparation-before-installing-windows-agents"></a>Preparação antes de instalar os agentes do Windows

Antes de instalar agentes em computadores que executam o Windows, você precisa de serviço de Docker de saudação tooconfigure. configuração de saudação permite Olá Windows agente ou hello análise de Log máquina virtual extensão toouse hello de soquete TCP de Docker para que os agentes Olá podem acessar o daemon do Docker Olá remotamente e toocapture dados para o monitoramento.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker e verifique se sua configuração

Há etapas necessárias tooset backup TCP pipe nomeado para o Windows Server:

1. No Windows PowerShell, habilite o pipe TCP e o pipe nomeado.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Configurar o Docker com o arquivo de configuração de saudação do pipe TCP e o pipe nomeado. arquivo de configuração de saudação está localizado em C:\ProgramData\docker\config\daemon.json.

    Arquivo daemon JSON hello, você precisará seguir hello:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Para obter mais informações sobre a configuração de daemon do Docker Olá usada com contêineres do Windows, consulte [mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Instalar agentes do Windows

tooenable Windows e contêiner do Hyper-V de monitoramento, instale Olá agente de monitoramento da Microsoft (MMA) em computadores com Windows que são hosts de contêiner. Para computadores que executam o Windows em seu ambiente local, consulte [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md). Para máquinas virtuais em execução no Azure, conecte-os tooLog análise usando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).

Você pode monitorar os contêineres do Windows em execução no Service Fabric. No entanto, apenas [máquinas virtuais em execução no Azure](log-analytics-azure-vm-extension.md) e [computadores executando o Windows no seu ambiente local](log-analytics-windows-agents.md) têm suporte atualmente para o Service Fabric.

Você pode verificar que essa solução de monitoramento de contêiner hello está definida corretamente para o Windows. toocheck se o pacote de gerenciamento de saudação foi download corretamente, procure *ContainerManagement.xxx*. Olá arquivos devem ser na pasta C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de saudação.


## <a name="solution-components"></a>Componentes da solução

Se você estiver usando agentes do Windows, em seguida, hello seguinte pacote de gerenciamento é instalado em cada computador com um agente quando você adicionar essa solução. Nenhuma configuração ou a manutenção é necessária para o pacote de gerenciamento de saudação.

- *ContainerManagement.xxx* instalado em C:\Arquivos de Programas\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs

## <a name="container-data-collection-details"></a>Detalhes da coleta de dados dos contêineres
Olá solução de monitoramento de contêiner coleta vários dados de log e métricas de desempenho de hosts de contêiner e contêineres usando agentes que permitem a você.

Dados são coletados a cada três minutos por Olá seguintes tipos de agente.

- [Agente do OMS para Linux](log-analytics-linux-agents.md)
- [Agente do Windows](log-analytics-windows-agents.md)
- [Extensão de VM do Log Analytics](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Registros de contêiner

Olá tabela a seguir mostra exemplos de registros coletados pela solução de monitoramento de contêiner de saudação e tipos de dados de saudação que aparecem nos resultados da pesquisa de log.

| Tipo de dados | Tipo de dados na Pesquisa de Log | Campos |
| --- | --- | --- |
| Desempenho de hosts e contêineres | `Type=Perf` | Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| Inventário de contêiner | `Type=ContainerInventory` | TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Inventário de imagem de contêiner | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer |
| Log do contêiner | `Type=ContainerLog` | TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Log do serviço de contêiner | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID |
| Inventário de nós do contêiner | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Inventário de Kubernetes | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Processo do contêiner | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Eventos de Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message |

Rótulos anexados muito*PodLabel* tipos de dados são seus próprios rótulos personalizados. Olá acrescentados rótulos PodLabel mostrados na tabela de saudação são exemplos. Portanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` serão diferentes no conjunto de dados de seu ambiente, e genericamente lembram `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Monitorar contêineres
Depois de ter solução Olá habilitada no portal do OMS hello, Olá **contêineres** bloco mostra informações resumidas sobre os hosts de contêiner e os contêineres de saudação em execução em hosts.

![Bloco Contêineres](./media/log-analytics-containers/containers-title.png)

bloco de saudação mostra uma visão geral de contêineres quantos você tem no ambiente hello e se está falha, em execução ou parado.

### <a name="using-hello-containers-dashboard"></a>Usando o painel de contêineres de saudação
Clique em Olá **contêineres** lado a lado. A partir daí, você verá exibições organizadas por:

- **Eventos de Contêiner** - Mostra o status do contêiner, e os computadores com contêineres com falha.
- **Logs do contêiner** -mostra um gráfico dos arquivos de log do contêiner gerado com o tempo e uma lista de computadores com o número mais alto de saudação de arquivos de log.
- **Eventos de Kubernetes** -mostra um gráfico de Kubernetes eventos gerados por hora e uma lista de motivos Olá por compartimentos gerados eventos hello. *Esse conjunto de dados é usado somente em ambientes Linux.*
- **Inventário de Namespace Kubernetes** - mostra o número de saudação de namespaces e compartimentos e mostra sua hierarquia. *Esse conjunto de dados é usado somente em ambientes Linux.*
- **Inventário de nó do contêiner** -mostra o número Olá dos tipos de orquestração usado em nós/hosts de contêiner. Olá computador nós/hosts também são listados pelo número de saudação de contêineres. *Esse conjunto de dados é usado somente em ambientes Linux.*
- **Inventário de imagens de contêiner** -mostra o número total de saudação de imagens de contêiner usado e número de tipos de imagem. número de saudação de imagens também é listado por marca de imagem hello.
- **Status de contêineres** -mostra o número total de saudação do contêiner de computadores de host/nós que têm contêineres em execução. Computadores também estarão listados pelo número de saudação da execução de hosts.
- **Processo do Contêiner** - Mostra um gráfico de linhas dos processos de contêiner em execução ao longo do tempo. Os contêineres também são listados por meio da execução do comando/processo dentro dos contêineres. *Esse conjunto de dados é usado somente em ambientes Linux.*
- **Desempenho de CPU do contêiner** -mostra um gráfico de linha de saudação utilização média da CPU ao longo do tempo para nós/hosts do computador. Também lista Olá computador nós/hosts com base na média de utilização da CPU.
- **Desempenho de Memória de Contêiner** - Mostra um gráfico de linhas do uso da memória ao longo do tempo. Também lista a utilização da memória do computador com base no nome da instância.
- **Desempenho do computador** -mostra os gráficos de linhas de por cento de saudação do desempenho da CPU ao longo do tempo, porcentagem de uso de memória ao longo do tempo e megabytes de espaço livre em disco ao longo do tempo. Você pode passar por qualquer linha em um gráfico tooview obter mais detalhes.


Cada área do painel de saudação é uma representação visual de uma pesquisa que é executada em dados coletados.

![Painel de Contêineres](./media/log-analytics-containers/containers-dash01.png)

![Painel de Contêineres](./media/log-analytics-containers/containers-dash02.png)

Em Olá **Status contêiner** área, clique em área superior do hello, conforme mostrado abaixo.

![Status dos contêineres](./media/log-analytics-containers/containers-status.png)

Pesquisa de log é aberto, exibindo informações sobre o estado de saudação de seus contêineres.

![Pesquisa de Log para contêineres](./media/log-analytics-containers/containers-log-search.png)

A partir daqui, você pode editar Olá toomodify de consulta de pesquisa-informações específicas de saudação toofind você está interessado. Para obter mais informações sobre as Pesquisas de Log, consulte [Pesquisas de log no Log Analytics](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Solucionar problemas localizando um contêiner com falha

O Log Analytics marca um contêiner como **Com Falha** se ele tiver sido encerrado com um código de saída diferente de zero. Você pode ver uma visão geral de erros de saudação e falhas no ambiente Olá Olá **falha contêineres** área.

### <a name="toofind-failed-containers"></a>contêineres de toofind falhou
1. Clique em Olá **Status contêiner** área.  
   ![status dos contêineres](./media/log-analytics-containers/containers-status.png)
2. Pesquisa de log é aberto e exibe o estado de saudação de seus contêineres, toohello semelhante a seguir.  
   ![estado dos contêineres](./media/log-analytics-containers/containers-log-search.png)
3. Em seguida, clique em valor Olá agregado de informações adicionais de tooview contêineres com falha. Expanda **Mostrar mais** ID de imagem tooview hello.  
   ![contêineres com falha](./media/log-analytics-containers/containers-state-failed.png)  
4. Em seguida, digite o seguinte Olá Olá consulta de pesquisa. `Type=ContainerInventory <ImageID>`toosee os detalhes sobre a imagem hello como o tamanho da imagem e o número de imagens parados e com falha.  
   ![contêineres com falha](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Pesquisar nos logs por dados do contêiner
Quando você estiver solucionando um erro específico, isso poderá ajudar toosee onde ele está ocorrendo em seu ambiente. Olá tipos de log a seguir ajudará você a criar consultas de informações de saudação tooreturn desejadas.


- **ContainerImageInventory** – Use este tipo quando você estiver tentando toofind informações organizadas por informações de imagem de imagem e tooview como IDs de imagem ou tamanhos.
- **ContainerInventory** – use este tipo quando desejar obter informações sobre a localização do contêiner, quais são seus nomes e quais imagens eles estão executando.
- **ContainerLog** – Use este tipo quando você deseja informações de log de erro específicas toofind e entradas.
- **ContainerNodeInventory_CL** usar este tipo quando você deseja Olá informações sobre o nó do host onde residem os contêineres. Ele fornece ao Docker informações de versão, tipo de orquestração, armazenamento e rede.
- **ContainerProcess_CL** tooquickly esse tipo de uso consulte processo Olá em execução dentro do contêiner de saudação.
- **ContainerServiceLog** – Use este tipo quando estiver tentando toofind informações sobre a trilha de auditoria para hello daemon do Docker, como iniciar, interromper, excluir ou comandos de pull.
- **KubeEvents_CL** usar esse tipo toosee Olá Kubernetes os eventos.
- **KubePodInventory_CL** usar esse tipo de informações da hierarquia toounderstand Olá cluster.


### <a name="toosearch-logs-for-container-data"></a>logs de toosearch para dados de contêiner
* Escolha uma imagem que você sabe que falhou recentemente e localizar os logs de erros de saudação para ele. Comece localizando um nome de contêiner que está executando a imagem com uma pesquisa **ContainerInventory**. Por exemplo, pesquise por `Type=ContainerInventory ubuntu Failed`  
    ![Pesquisar por contêineres do Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Olá nome do contêiner de saudação Avançar muito**nome**e pesquise esses logs. Neste exemplo, é `Type=ContainerLog cranky_stonebreaker`.

**Exibir informações de desempenho**

Quando você está começando a consultas tooconstruct, ela pode ajudar a toosee que é possível primeiro. Por exemplo, a consulta toosee pesquisar todos os dados de desempenho, tente uma consulta ampla digitando Olá a seguir.

```
Type=Perf
```

![desempenho de contêineres](./media/log-analytics-containers/containers-perf01.png)

Você pode definir o escopo de dados de desempenho de saudação que você esteja vendo contêiner específico tooa digitando o nome hello dele toohello à direita da sua consulta.

```
Type=Perf <containerName>
```

Que mostra a lista de saudação de métricas de desempenho são coletadas para um contêiner individual.

![desempenho de contêineres](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Exemplo de consultas de pesquisa de log
É geralmente útil toobuild consulta começando com um ou dois exemplos e, em seguida, modificá-los toofit seu ambiente. Como ponto de partida, você pode experimentar Olá **exemplos de consultas** toohelp área criar consultas mais avançadas.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contêineres](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Salvando as consultas de pesquisa de log
Salvar consultas é um recurso padrão do Log Analytics. Ao salvá-las, você terá aquelas que considerou úteis acessíveis para uso futuro.

Depois de criar uma consulta que sejam úteis, salvá-lo clicando em **Favoritos** na parte superior de saudação da página de pesquisa de Log de saudação. Em seguida, você pode acessá-lo facilmente mais tarde da saudação **meu painel** página.

## <a name="next-steps"></a>Próximas etapas
* [Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas registros de dados de contêiner.
