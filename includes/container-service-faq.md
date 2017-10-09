# <a name="container-service-frequently-asked-questions"></a>Perguntas frequentes sobre o Serviço de Contêiner

## <a name="orchestrators"></a>Orquestradores

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Quais orquestradores de contêiner têm suporte no Serviço de Contêiner do Azure? 

Há suporte para o DC/OS de software livre, Docker Swarm e Kubernetes. Para obter mais informações, consulte Olá [visão geral](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Há suporte para o modo Docker Swarm? 

Atualmente não há suporte para o modo por nuvem, mas é no mapa de serviço hello. 

### <a name="does-azure-container-service-support-windows-containers"></a>O Serviço de Contêiner do Azure dá suporte a contêineres do Windows?  

Atualmente há suporte para contêineres do Linux com todos os orquestradores. O suporte para contêineres do Windows com o Kubernetes está em versão prévia.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>É recomendado um orquestrador específico no Serviço de Contêiner do Azure? 
Geralmente, não recomendamos um orquestrador específico. Se você tiver experiência com um orchestrators Olá com suporte, você pode aplicar essa experiência no serviço de contêiner do Azure. No entanto, as tendências de dados sugerem que DC/OS é comprovado em produção para Big Data e cargas de trabalho de IoT, Kubernetes é adequado para cargas de trabalho nativas de nuvem e Docker Swarm é conhecido por sua integração a ferramentas Docker e sua fácil curva de aprendizado.

Dependendo do cenário, você também pode criar e gerenciar soluções de contêiner personalizadas com outros serviços do Azure. Esses serviços incluem [Máquinas Virtuais](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Aplicativos Web](../articles/app-service-web/app-service-web-overview.md) e [Lote](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Qual é a diferença Olá entre o serviço de contêiner do Azure e o mecanismo de ACS? 
Serviço de contêiner do Azure é um serviço do Azure baseado no SLA com recursos do hello portal do Azure, as ferramentas de linha de comando do Azure e APIs do Azure. Olá permite que você tooquickly implementar e gerenciar clusters que executam as ferramentas de orquestração de contêiner padrão com um número relativamente pequeno de opções de configuração do serviço. 

[Mecanismo do ACS](http://github.com/Azure/acs-engine) é um projeto de código-fonte aberto que permite a configuração de cluster de saudação power usuários toocustomize em cada nível. Essa configuração de saudação tooalter capacidade de infraestrutura e o software significa que não oferecemos nenhum SLA para o mecanismo do ACS. O suporte é tratado por meio do projeto de código-fonte aberto Olá no GitHub, em vez de por meio de canais oficiais do Microsoft. 

## <a name="cluster-management"></a>Gerenciamento de clusters

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Como criar chaves SSH para o cluster?

Você pode usar ferramentas padrão em seu sistema operacional de toocreate um par de chamadas chaves público e privado SSH RSA para autenticação em relação a máquinas de virtuais de Linux Olá para seu cluster. Para obter as etapas, consulte Olá [OS X e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) orientação. 

Se você usar [comandos 2.0 do CLI do Azure](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy um contêiner de serviço de cluster, SSH chaves podem ser geradas automaticamente para seu cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Como criar uma entidade de serviço para o cluster Kubernetes?

Uma ID de entidade de serviço do Active Directory do Azure e a senha também são necessário toocreate um cluster Kubernetes no serviço de contêiner do Azure. Para obter mais informações, consulte [sobre a entidade de serviço Olá para um cluster Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Se você usar [comandos 2.0 do CLI do Azure](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy um Kubernetes serviço de cluster, credenciais principais podem ser geradas automaticamente para seu cluster.

### <a name="how-large-a-cluster-can-i-create"></a>Posso criar um cluster de qual tamanho?
Você pode criar um cluster com 1, 3 ou 5 nós mestres. Você pode escolher o too100 nós de agente.

> [!IMPORTANT]
> Para clusters maiores e dependendo Olá escolha para os nós de tamanho da VM, talvez seja necessário tooincrease cota de núcleos de saudação em sua assinatura. toorequest um aumento de cota, abra um [solicitação de suporte do cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) sem custo adicional. Se estiver usando uma [conta gratuita do Azure](https://azure.microsoft.com/free/), você poderá usar apenas um número limitado de núcleos de computação do Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Como aumentar número de saudação de mestres depois de criar um cluster? 
Depois de criar o cluster hello, o número de saudação de mestres é fixo e não pode ser alterado. Durante a criação de saudação do cluster hello, você deve selecionar idealmente vários mestres para alta disponibilidade.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Como aumentar número de saudação de agentes depois de criar um cluster? 
Você pode dimensionar número Olá de agentes no cluster hello usando ferramentas de linha de comando ou Olá portal do Azure. Confira [Dimensionar um cluster do Serviço de Contêiner do Azure](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Quais são as URLs de saudação do meu mestres e agentes? 
Olá URLs de cluster de recursos no serviço de contêiner do Azure se baseiam no hello prefixo fornecer e Olá nome da saudação região do Azure que você escolheu para implantação de nome DNS. Por exemplo, o nome de domínio totalmente qualificado (FQDN) saudação do nó mestre Olá é deste formulário:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Você pode encontrar as URLs usadas para seu cluster em Olá portal do Azure, Olá Gerenciador de recursos do Azure ou outras ferramentas do Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Como saber a qual versão de orquestrador está em execução no meu cluster?

* Controlador de domínio/SO: Consulte Olá [documentação Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: Executar `docker version`
* Kubernetes: Executar `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Como atualizar o orchestrator Olá após a implantação?

No momento, o serviço de contêiner do Azure não fornece versão das ferramentas tooupgrade saudação do orchestrator Olá implantadas no cluster. Se o Serviço de Contêiner oferecer suporte a uma versão posterior, você pode implantar um novo cluster. Outra opção é toouse ferramentas de orchestrator específica se eles estiverem disponível tooupgrade um cluster local. Por exemplo, consulte [Atualização de DC/OS](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Onde encontrar o cluster toomy de cadeia de caracteres de conexão do hello SSH?

Você pode encontrar a cadeia de caracteres de conexão Olá no hello portal do Azure, ou usando as ferramentas de linha de comando do Azure. 

1. No portal de hello, navegue até toohello o grupo de recursos para implantação de cluster de saudação.  

2. Clique em **visão geral** e clique em Vincular Olá para **implantações** em **Essentials**. 

3. Em hello **histórico de implantação** folha, clique em implantação Olá que tem um nome que começa com **microsoft acs** seguido por uma data de implantação. Exemplo: microsoft-acs-201701310000.  

4. Em Olá **resumo** página em **saídas**, vários links de cluster são fornecidos. **SSHMaster0** fornece um SSH conexão cadeia de caracteres toohello primeiro mestre no cluster do serviço de contêiner. 

Como mencionado anteriormente, você também pode usar as ferramentas do Azure toofind Olá FQDN do mestre de saudação. Fazer uma conexão SSH toohello mestre usando Olá FQDN do mestre de saudação e nome de usuário Olá que você especificou ao criar o cluster de saudação. Por exemplo:

```bash
ssh userName@masterFQDN –A –p 22 
```

Para obter mais informações, consulte [cluster de serviço de contêiner do Azure Connect tooan](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Próximas etapas

* [Saiba mais](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) sobre o Serviço de Contêiner do Azure.
* Implantar um cluster de serviço de contêiner usando Olá [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) ou [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
