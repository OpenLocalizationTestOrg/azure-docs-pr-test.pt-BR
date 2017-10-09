# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Escalar nós de agente em um cluster do Serviço de Contêiner
Depois de [Implantando um cluster do serviço de contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), talvez seja necessário um número de saudação do toochange de nós de agente. Por exemplo, mais agentes podem ser necessários para que você possa executar mais aplicativos ou instâncias de contêiner. 

Você pode alterar o número de saudação de nós de agente em um cluster de DC/OS, o Docker Swarm ou Kubernetes usando Olá portal do Azure ou Olá 2.0 do CLI do Azure. 

## <a name="scale-with-hello-azure-portal"></a>Dimensionar com hello portal do Azure

1. Em Olá [portal do Azure](https://portal.azure.com), procurar **serviços de contêiner**e, em seguida, clique em serviço de contêiner de saudação que você deseja toomodify.
2. Em Olá **serviço de contêiner** folha, clique em **agentes**.
3. Em **contagem de VM**, insira o número desejado de saudação de nós de agentes.

    ![Dimensionar um pool no portal de saudação](./media/container-service-scale/container-service-scale-portal.png)

4. configuração de saudação toosave, clique em **salvar**.

## <a name="scale-with-hello-azure-cli-20"></a>Dimensionar com hello 2.0 do CLI do Azure

Verifique se você [instalado](/cli/azure/install-az-cli2) Olá 2.0 mais recentes de CLI do Azure e registrado no tooan conta do azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Consulte a contagem atual de agente Olá
número de saudação do toosee de agentes no momento em cluster Olá, executar Olá `az acs show` comando. Isso mostra a configuração de cluster de saudação. Por exemplo, Olá mostra Olá a configuração do serviço de contêiner Olá chamado de comando a seguir `containerservice-myACSName` no grupo de recursos de saudação `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

comando Olá retorna o número de saudação de agentes em Olá `Count` valor em `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Use Olá az comando de escala do acs
número de saudação toochange de nós de agente, executar Olá `az acs scale` Olá comando e forneça **grupo de recursos**, **nome do serviço de contêiner**e hello desejado **nova contagem de agente**. Ao usar um número menor ou maior, você pode reduzir e escalar verticalmente, respectivamente.

Por exemplo, número de saudação toochange de agentes na saudação anterior too10 de cluster, digite Olá comando a seguir:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Olá 2.0 do CLI do Azure retorna uma cadeia de caracteres JSON que representa a nova configuração de saudação do serviço de contêiner hello, incluindo a nova contagem de agente hello.

Para obter mais opções de comando, execute `az acs scale --help`.

## <a name="scaling-considerations"></a>Considerações de dimensionamento

* número de saudação de nós de agente deve estar entre 1 e 100, inclusive. 

* Sua cota de núcleos pode limitar o número de saudação de nós de agente em um cluster.

* Operações de dimensionamento de nó do agente são aplicadas tooan conjunto de escala de máquina virtual do Azure que contém o pool de agente hello. Em um cluster de DC/OS, somente nós de agente no pool privada Olá são dimensionados pelas operações de saudação mostradas neste artigo.

* Dependendo orchestrator Olá que implantar em seu cluster, você pode dimensionar separadamente número Olá de instâncias de um contêiner em execução no cluster de saudação. Por exemplo, em um cluster de DC/sistema operacional, use Olá [maratona UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange número de saudação de instâncias de um aplicativo de contêiner.

* Atualmente, não há suporte para o dimensionamento automático dos nós de agente em um cluster do serviço de contêiner.

## <a name="next-steps"></a>Próximas etapas
* Confira [mais exemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) de como usar os comandos da CLI 2.0 do Azure com o Serviço de Contêiner do Azure.
* Saiba mais sobre os [pools de agentes DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) no Serviço de Contêiner do Azure.

