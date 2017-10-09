# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Criar um cluster de conexão remota tooa Kubernetes, o controlador de domínio/sistema operacional ou o Docker Swarm
Depois de criar um cluster do serviço de contêiner do Azure, você precisa tooconnect toohello cluster toodeploy e gerenciar cargas de trabalho. Este artigo descreve como tooconnect toohello mestre VM de saudação do cluster de um computador remoto. 

clusters de Kubernetes, o controlador de domínio/sistema operacional e o Docker Swarm Olá fornecem pontos de extremidade HTTP localmente. Para Kubernetes, esse ponto de extremidade é exposto de maneira segura em Olá internet e você pode acessá-lo executando Olá `kubectl` ferramenta de linha de comando de qualquer computador conectado à internet. 

Para o controlador de domínio/OS e Docker Swarm, recomendamos que você cria um túnel SSH (secure shell) de seu sistema de gerenciamento de cluster de toohello do computador local. Depois de saudação túnel é estabelecido, você pode executar comandos que usam pontos de extremidade HTTP hello e interface da web do modo de exibição Olá orchestrator (se disponível) do seu sistema local. 

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster Kubernetes, CD/SO ou Docker Swarm [implantado no Serviço de Contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA arquivo de chave privada correspondente toohello toohello adicional de chave pública cluster durante a implantação. Esses comandos pressupõem a chave privada SSH hello está em `$HOME/.ssh/id_rsa` em seu computador. Veja estas instruções para obter mais informações sobre [MacOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md). Se Olá conexão SSH não estiver funcionando, talvez seja necessário muito [redefinir suas chaves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Conecte-se tooa Kubernetes cluster

Siga estas etapas tooinstall e configurar `kubectl` no seu computador.

> [!NOTE] 
> No Linux ou macOS, talvez seja necessário comandos Olá toorun essa seção usando `sudo`.
> 

### <a name="install-kubectl"></a>Instalar kubectl
Uma maneira tooinstall essa ferramenta é Olá toouse `az acs kubernetes install-cli` comando 2.0 do CLI do Azure. toorun esse comando, verifique se você [instalado](/cli/azure/install-az-cli2) Olá 2.0 mais recentes de CLI do Azure e registrado no tooan conta do Azure (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Como alternativa, você pode baixar hello mais recente `kubectl` cliente diretamente do hello [Kubernetes libera página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Para obter mais informações, consulte [Instalando e configurando o kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).

### <a name="download-cluster-credentials"></a>Baixar credenciais de cluster
Uma vez que `kubectl` instalada, você precisará de máquina de tooyour toocopy Olá cluster credenciais. Credenciais de saudação get toodo unidirecional é com hello `az acs kubernetes get-credentials` comando. Passe o nome de Olá Olá do grupo de recursos e nome de saudação do recurso de serviço de contêiner hello:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Esse comando baixa credenciais de cluster Olá muito`$HOME/.kube/config`, onde `kubectl` espera toobe localizado.

Como alternativa, você pode usar `scp` toosecurely copie o arquivo hello de `$HOME/.kube/config` Olá mestre VM tooyour do computador local. Por exemplo:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Se você estiver usando o Windows, você pode usar Bash no Ubuntu no Windows, o cliente de cópia de arquivos seguro PuTTy hello ou uma ferramenta semelhante.

### <a name="use-kubectl"></a>Usar kubectl

Uma vez que `kubectl` configurado, testar conexão Olá lista Olá nós no cluster:

```bash
kubectl get nodes
```

Você pode tentar outros comandos `kubectl`. Por exemplo, você pode exibir hello Kubernetes painel. Primeiro, execute um proxy do servidor de API Kubernetes toohello:

```bash
kubectl proxy
```

Olá Kubernetes UI agora está disponível em: `http://localhost:8001/ui`.

Para obter mais informações, consulte Olá [início rápido Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Conecte-se o cluster de DC/sistema operacional ou por nuvem tooa

Olá toouse DC/OS e clusters de Docker Swarm implantados pelo serviço de contêiner do Azure, siga toocreate essas instruções um túnel SSH do seu sistema Linux, macOS ou Windows local. 

> [!NOTE]
> Essas instruções se concentram no tráfego TCP de túnel via SSH. Você também pode iniciar uma sessão interativa do SSH com um dos sistemas de gerenciamento de cluster interno hello, mas não recomendamos isso. Trabalhar diretamente em um sistema interno acarreta o risco de alterações de configuração acidentais  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Criar um túnel SSH no Linux ou no macOS
Olá primeira coisa que você faz quando você criar um túnel SSH no Linux ou macOS é toolocate Olá nome DNS público de mestres de balanceamento de carga de saudação. Siga estas etapas:


1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello grupo de recursos que contém o cluster do serviço de contêiner. Expanda o grupo de recursos de saudação para que cada recurso é exibido. 

2. Clique em Olá **serviço de contêiner** recurso e clique em **visão geral**. Olá **FQDN mestre** de saudação cluster aparece sob **Essentials**. Salve o nome para uso posterior. 

    ![Nome DNS público](./media/container-service-connect/pubdns.png)

    Como alternativa, executar Olá `az acs show` comando no seu serviço de contêiner. Procure Olá **mestre perfil: fqdn** propriedade na saída do comando hello.

3. Agora, abra um shell e execute Olá `ssh` comando especificando Olá valores a seguir: 

    **LOCAL_PORT** é a porta TCP no lado do serviço de saudação do hello túnel tooconnect para hello. Para por nuvem, defina este too2375. Para DC/OS, defina este too80. 
    **REMOTE_PORT** é a porta de saudação do ponto de extremidade de saudação que você deseja tooexpose. Para a nuvem, use a porta 2375. Para o DC/OS, use a porta 80.  
    **Nome de usuário** é Olá nome de usuário fornecido quando você implantou o cluster hello.  
    **DNSPREFIX** é Olá prefixo DNS que você forneceu quando você implantou o cluster hello.  
    **REGIÃO** é Olá região na qual o grupo de recursos está localizado.  
    **PATH_TO_PRIVATE_KEY** [opcional] é Olá caminho toohello chave privada correspondente toohello chave pública que você forneceu ao criar cluster hello. Use essa opção com hello `-i` sinalizador.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Olá porta de conexão SSH é 2200 e não Olá 22 de porta padrão. Em um cluster com mais de uma VM mestre, isso é o mestre de primeira toohello VM de porta de conexão hello.
  > 

  comando Olá retorna sem saída.

Consulte exemplos de saudação DC/sistema operacional e por nuvem Olá seções a seguir.    

### <a name="dcos-tunnel"></a>Túnel DC/OS
tooopen um encapsulamento para pontos de extremidade do controlador de domínio/OS, execute um comando como Olá a seguir:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Certifique-se de que você não tem outro processo local que associa a porta 80. Se necessário, você pode especificar uma porta local diferente da porta 80, como a porta 8080. No entanto, alguns links da interface do usuário da Web podem não funcionar quando você usa essa porta.
>

Agora você pode acessar os pontos de extremidade de DC/OS de saudação do seu sistema local por meio de saudação seguintes URLs (supondo que a porta local 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Da mesma forma, você pode acessar as APIs de rest Olá para cada aplicativo por esse túnel.

### <a name="swarm-tunnel"></a>Túnel do Swarm
tooopen um toohello por nuvem ponto de extremidade, execute um comando como Olá a seguir:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Certifique-se de que você não tem outro processo local que associa a porta 2375. Por exemplo, se você estiver executando o daemon do Docker Olá localmente, ele é definido como padrão a porta 2375 toouse. Se necessário, você pode especificar uma porta local diferente da porta 2375.
>

Agora você pode acessar o cluster de Docker Swarm de saudação usando a interface de linha de comando Docker hello (CLI do Docker) em seu sistema local. Para as instruções de instalação, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).

Defina sua toohello de variável de ambiente DOCKER_HOST porta local configurado para túnel hello. 

```bash
export DOCKER_HOST=:2375
```

Execute os comandos cluster túnel toohello Docker Swarm. Por exemplo:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Criar um túnel SSH no Windows
Há várias opções para a criação de túneis SSH no Windows. Se você estiver executando Bash no Ubuntu no Windows ou uma ferramenta semelhante, você pode seguir as instruções de túnel de SSH do hello mostradas anteriormente neste artigo para macOS e Linux. Como alternativa no Windows, esta seção descreve como túnel de saudação do toouse toocreate PuTTY.

1. [Baixar o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.

2. Execute o aplicativo hello.

3. Insira um nome de host que é composto de nome de usuário do administrador de cluster de saudação e o nome DNS público de saudação do mestre de saudação primeiro cluster hello. Olá **nome de Host** parece muito`azureuser@PublicDNSName`. Insira 2200 Olá **porta**.

    ![Configuração do PuTTY 1](./media/container-service-connect/putty1.png)

4. Selecione **SSH > Auth**. Adicione um caminho tooyour arquivo de chave privada (formato *.ppk) para autenticação. Você pode usar uma ferramenta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate esse arquivo hello cluster de saudação toocreate usado chave SSH.

    ![Configuração do PuTTY 2](./media/container-service-connect/putty2.png)

5. Selecione **SSH > túneis** e configure o seguinte Olá encaminhados portas:

    * **Porta de Origem:** use 80 para DC/SO ou 2375 para nuvem.
    * **Destino:** use localhost:80 para o DC/OS ou localhost:2375 para o Swarm.

    saudação de exemplo a seguir está configurada para o controlador de domínio/SO, mas será semelhante para Docker Swarm.

    > [!NOTE]
    > A porta 80 não deve estar em uso quando você criar esse túnel.
    > 

    ![Configuração do PuTTY 3](./media/container-service-connect/putty3.png)

6. Quando tiver terminado, clique em **sessão > Salvar** toosave configuração de conexão de saudação.

7. tooconnect toohello PuTTY sessão, clique em **abrir**. Quando você se conectar, você pode ver a configuração da porta Olá no log de eventos PuTTY Olá.

    ![Log de eventos do PuTTY](./media/container-service-connect/putty4.png)

Depois de configurar o túnel Olá para o controlador de domínio/sistema operacional, você pode acessar Olá relacionadas a pontos de extremidade em:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Depois de configurar o túnel de saudação para Docker Swarm, abra seu tooconfigure de configurações do Windows uma variável de ambiente de sistema chamada `DOCKER_HOST` com um valor de `:2375`. Em seguida, você pode acessar o cluster de por nuvem Olá através de Olá CLI do Docker.

## <a name="next-steps"></a>Próximas etapas
Implantar e gerenciar contêineres no cluster:

* [Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Trabalhar com o Serviço de Contêiner do Azure e o DC/SO](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Trabalhar com hello Azure serviço de contêiner e o Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

