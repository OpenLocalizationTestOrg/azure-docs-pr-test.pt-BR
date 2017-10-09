Soluções de nuvem do Azure são criadas em máquinas virtuais (emulação de hardware de computador físico), que permitem empacotamento ágil de implantações de software e melhor consolidação de recursos de hardware físico. [Docker](https://www.docker.com) contêineres e hello ecossistema do docker tem formas de saudação drasticamente expandido desenvolver, enviar e gerenciar software distribuído. Código do aplicativo em um contêiner é isolado da VM do host hello e outros contêineres em Olá mesma VM. Esse isolamento proporciona mais desenvolvimento e agilidade de implantação.

O Azure oferece Olá valores Docker a seguir:

* [Muitos](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [diferentes](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) maneiras toocreate Docker hospeda para contêineres toosuit sua situação
* Olá [serviço de contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/) cria clusters de hosts de contêiner usando orchestrators como **maratona** e **swarm**.
* [Gerenciador de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md) e [modelos de grupo de recursos](../articles/resource-group-authoring-templates.md) toosimplify Implantando e atualizando a complexos aplicativos distribuídos
* Integração com uma ampla variedade de ferramentas de gerenciamento de configuração patenteadas e de código aberto

E como você pode criar programaticamente VMs e Linux contêineres no Azure, você também pode usar VM e contêiner *orquestração* ferramentas toocreate grupos de máquinas virtuais (VMs) e aplicativos de toodeploy em ambos os Linux contêineres e agora [contêineres do Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

Este artigo descreve não apenas esses conceitos em um nível alto, ele também contém milhares de informações de toomore links, tutoriais, e produtos relacionados ao uso de toocontainer e cluster no Azure. Se você sabe que tudo isso e quiser apenas links hello, eles estão bem aqui no [ferramentas para trabalhar com contêineres](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>diferença de saudação entre máquinas virtuais e contêineres
Máquinas virtuais são executadas em um ambiente de virtualização de hardware isolado fornecido por um [hipervisor](http://en.wikipedia.org/wiki/Hypervisor). No Azure, Olá [máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/) identificadores do serviço tudo o que você: criar máquinas virtuais, escolha o sistema operacional de saudação e configurando &mdash;ou carregando uma imagem VM personalizada. Máquinas virtuais são uma tecnologia testada, "batalha protegido", e há muitas ferramentas disponíveis toomanage Olá SO e aplicativos que eles contêm.  Aplicativos em uma VM estão ocultos do sistema operacional do host de saudação. De saudação ponto de vista de um aplicativo ou usuário em uma máquina virtual, Olá VM aparece toobe um computador físico autônomo.

[Contêineres do Linux](http://en.wikipedia.org/wiki/LXC) e os criados e hospedados usando as ferramentas do docker, não use uma isolamento de tooprovide do hipervisor. Com contêineres, o host do contêiner Olá usa, de processo e recursos de isolamento de sistema de arquivo do contêiner do hello Linux kernel tooexpose toohello seus aplicativos, alguns recursos do kernel e seu próprio sistema de arquivos isolado. De saudação ponto de vista de um aplicativo em execução dentro de um contêiner, o contêiner de saudação aparece toobe uma instância exclusiva do sistema operacional. Um aplicativo independente não pode ver processos ou quaisquer outros recursos fora de seu contêiner.

Muito menos recursos são usados em um contêiner de encaixe que são usados em uma VM. Contêineres do docker empregam um isolamento e a execução do modelo de aplicativo, que não compartilha o kernel de saudação do host do Docker hello. Olá, contêiner tem muito mais baixa superfície do disco que não inclui Olá todo o sistema operacional. Tempo de inicialização e espaço em disco necessário são significativamente menores do que em uma VM.
Contêineres do Windows fornecem Olá mesmas vantagens que contêineres do Linux para aplicativos que são executados no Windows. Contêineres do Windows oferecem suporte a API de Docker e formato de imagem do Docker hello, mas eles também podem ser gerenciados usando o PowerShell. Dois tempos de execução do contêiner estão disponíveis com contêineres do Windows, contêineres do Windows Server e contêineres do Hyper-V. Os Contêineres de Hyper-V fornecem uma camada adicional de isolamento, hospedando cada contêiner em uma VM superotimizada. toolearn mais sobre contêineres do Windows, consulte [sobre contêineres do Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget iniciado com contêineres do Windows no Azure, saiba como muito[implantar um cluster do serviço de contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Para que os contêineres são eficazes?

Contêineres podem melhorar:

* código do aplicativo Hello velocidade pode ser desenvolvido e compartilhado amplamente
* velocidade de saudação e testar um aplicativo de confiança
* velocidade de saudação e pode ser implantado um aplicativo de confiança

Os contêineres são executados em um host do contêiner &mdash; um sistema operacional e no Azure isso significa uma Máquina Virtual do Azure. Mesmo se você já adorar ideia Olá de contêineres, você ainda vai tooneed uma infraestrutura VM hospedando Olá contêineres, mas Olá vantagens que contêineres não faz na máquina virtual do qual eles estão executando (embora se o contêiner de saudação quer um Linux ou Windows ambiente de execução será importante, por exemplo).


## <a name="what-are-containers-good-for"></a>Para que os contêineres são eficazes?
Eles são ótimos para muitas coisas, mas eles incentivamos&mdash;como [serviços de nuvem do Azure](https://azure.microsoft.com/services/cloud-services/) e [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;Olá criação de serviço único, orientados por microsserviço aplicativos distribuídos, no qual aplicativo de design é baseado em partes pequenas, combináveis mais e não em componentes maiores e mais fortemente acopladas.

Isso vale ainda mais em ambientes de nuvem pública como o Azure, nos quais você aluga as VMs onde e quando precisa delas. Você obtém não só ferramentas de orquestração com implantação rápida e isolamento, mas pode tomar decisões mais eficientes de infraestrutura de aplicativo.

Por exemplo, você pode ter atualmente uma implantação que consiste em 9 VMs do Azure de tamanho grande para um aplicativo distribuído de alta disponibilidade. Se os componentes de saudação do aplicativo podem ser implantados em contêineres, pode ser capaz de toouse apenas 4 VMs e implantar os componentes do aplicativo dentro de contêineres de 20 para redundância e balanceamento de carga.

Este é um exemplo, claro, mas se você pode fazer isso em seu cenário, você pode ajustar picos toousage com mais contêineres em vez de VMs do Azure mais e usar Olá restantes carga geral da CPU de modo muito mais eficiente do que antes.

Além disso, há muitos cenários que não se prestam tooa microservices abordagem; Você saberá que melhor se microservices e contêineres irá ajudá-lo.

### <a name="container-benefits-for-developers"></a>Benefícios do contêiner para desenvolvedores
Em geral, é fácil toosee que a tecnologia de contêiner é um passo à frente, mas há também benefícios mais específicos. Vejamos o exemplo hello de contêineres do Docker. Este tópico não descreverá profundamente em Docker no momento (ler [novidades Docker?](https://www.docker.com/whatisdocker/) para esse história, ou [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), mas o Docker e seu ecossistema oferecem benefícios significativos aos desenvolvedores de tooboth e IT profissionais.

Os desenvolvedores tenham recipientes de tooDocker rapidamente, porque acima de todos os torna fácil o uso de contêineres do Linux e Windows:

* Eles podem usar comandos simples, incremental toocreate uma fixa da imagem que é fácil toodeploy e podem automatizar a criação dessas imagens usando um dockerfile
* Eles podem compartilhar essas imagens facilmente usando simples, [git](https://git-scm.com/)-estilo push e pull comandos muito[pública](https://registry.hub.docker.com/) ou [registros docker privada](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Pense em componentes de aplicativo isolados em vez de computadores
* Eles podem usar um grande número de ferramentas que compreendem contêineres docker e diferentes imagens de base

### <a name="container-benefits-for-operations-and-it-professionals"></a>Benefícios do contêiner para profissionais de TI e operações
IT e profissionais de operações também se beneficiar da combinação de saudação de contêineres e máquinas virtuais.

* Serviços independentes ficam isolados do ambiente de execução do host da VM
* Códigos independentes são comprovadamente idênticos
* Serviços independentes podem ser iniciados, interrompidos e movidos rapidamente entre ambientes de produção, teste e desenvolvimento

Recursos como esses&mdash;e há mais&mdash;excite empresas estabelecidas, onde das empresas de tecnologia de informação professional tem trabalho Olá dos recursos de ajuste&mdash;incluindo a capacidade de processamento puro&mdash; somente toohello tarefas necessárias toonot permanecer nos negócios, mas aumentar a satisfação do cliente e acessar. Pequenas empresas, ISVs e inicializações têm exatamente Olá mesmo requisito, mas eles podem descrevem ele diferente.

## <a name="what-are-virtual-machines-good-for"></a>Para que as máquinas virtuais são eficazes?
Máquinas virtuais fornecem o backbone de saudação da computação em nuvem e que não é alterado. Se máquinas virtuais iniciar mais lentamente, têm um maior volume de disco e não mapeiam diretamente tooa microservices arquitetura, eles têm muito importantes benefícios:

1. Por padrão, elas têm proteções de segurança padrão muito mais robustas para o computador host
2. Elas dão suporte a qualquer uma das principais configurações de aplicativos e sistemas operacionais
3. Elas têm ecossistemas de ferramentas permanentes para comando e controle
4. Eles fornecem a execução de saudação contêineres de toohost do ambiente

Olá último item é importante, como um aplicativo independente ainda requer um tipo de CPU e sistema operacional específico, dependendo das chamadas Olá Olá aplicativo fizer. É importante tooremember instalar contêineres em máquinas virtuais, porque eles contêm Olá aplicativos toodeploy; contêineres não são substituições de VMs ou sistemas operacionais.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Comparação geral de recursos de VMs e contêineres
Olá tabela a seguir descreve um alto diferenças de tipo de nível de saudação do recurso que&mdash;sem muito trabalho extra&mdash;existe entre VMs e Linux contêineres. Observe que pode ser mais ou menos desejável dependendo de seu aplicativo precisa de alguns recursos e que, assim como acontece com todos os softwares, trabalho extra fornece maior suporte ao recurso, especialmente na área de saudação de segurança.

| Recurso | VMs | Contêineres |
|:--- | --- | --- |
| Suporte de segurança "padrão" |tooa maior grau |tooa grau ligeiramente menor |
| Requisição de memória em disco |SO completo, mais aplicativos |Somente os requisitos dos aplicativos |
| Tempo gasto toostart |Muito mais longo: inicialização do sistema operacional e carregamento do aplicativo |Substancialmente mais curto: somente os aplicativos precisam toostart porque kernel já está em execução |
| Portabilidade |Portátil com a preparação adequada |Portátil em dentro do formato de imagem; normalmente menor |
| Automação de imagem |Varia muito de acordo com o SO e os aplicativos |[Registro Docker](https://registry.hub.docker.com/); outros |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Criando e gerenciando grupos de VMs e contêineres
Neste ponto, qualquer arquiteto, desenvolvedor ou especialista de operações de TI pode estar pensando, "Eu posso automatizar TUDO isso. Esse realmente É um banco de dados como serviço! ".

Você está certo, pode ser e qualquer número de sistemas, muitos dos quais você talvez já use, que pode gerenciar grupos de máquinas virtuais do Azure e injetar código personalizado usando scripts, geralmente com hello [CustomScriptingExtension para Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) ou Olá [CustomScriptingExtension para Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Você pode automatizar as implantações do Azure &mdash; e talvez já tenha feito isso &mdash; usando scripts do PowerShell ou a CLI do Azure.

Essas capacidades são muitas vezes e, como o tootools migrados [Puppet](https://puppetlabs.com/) e [Chef](https://www.chef.io/) tooautomate Olá criação do e configuração de máquinas virtuais em escala. (Estes são alguns links muito[usando essas ferramentas com o Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Modelos do grupo de recursos do Azure
Mais recentemente, o Azure lançou Olá [gerenciamento de recursos do Azure](../articles/resource-manager-deployment-model.md) API REST e atualizada toouse de ferramentas do PowerShell e a CLI do Azure-lo facilmente. Você pode implantar, modificar ou reimplantar topologias de todo o aplicativo usando [modelos do Azure Resource Manager](../articles/resource-group-authoring-templates.md) com o uso de API de gerenciamento de recursos do Azure hello:

* Olá [portal do Azure usando modelos](https://github.com/Azure/azure-quickstart-templates)&mdash;dica, use o botão de "DeployToAzure" hello
* Olá [CLI do Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Implantação e gerenciamento de grupos inteiros de VMs do Azure e contêineres
Há vários sistemas populares que podem implantar grupos inteiros de VMs e instalar o Docker (ou outros sistemas de host de contêineres do Linux) nelas como um grupo automatizável. Para obter links diretos, consulte Olá [contêineres e ferramentas](#containers-and-vm-technologies) seção abaixo. Há vários sistemas que fazer extensão tooa maior ou menor, e essa lista não é exaustiva. Dependendo das suas habilidades e do contexto, eles podem ou não ser úteis.

O Docker tem seu próprio conjunto de ferramentas de criação de VMs ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) e uma ferramenta de balanceamento de carga e gerenciamento de cluster de contêineres do Docker ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Além disso, Olá [extensão da VM do Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) vem com suporte de padrão para [ `docker-compose` ](https://docs.docker.com/compose/), que pode implantar configurado os contêineres de aplicativos em vários contêineres.

Além disso, você pode experimentar o [DCOS (Sistema Operacional de Data 
Center) do Mesosphere](http://docs.mesosphere.com). DCOS baseia-se a saudação código-fonte aberto [mesos](http://mesos.apache.org/) "kernel de sistemas distribuídos" que permite que você tootreat seu data center como um serviço endereçável. O DCOS tem pacotes internos para vários sistemas importantes, como [Spark](http://spark.apache.org/) e [Kafka](http://kafka.apache.org/) (e outros), bem como serviços internos como [Marathon](https://mesosphere.github.io/marathon/) (um sistema de controle de contêineres) e [Chronos](https://mesos.github.io/chronos/) (um agendador distribuído). O Mesos foi derivado de lições aprendidas com o Twitter, AirBnb e outras empresas de escala da Web. Você também pode usar **swarm** como mecanismo de orquestração de saudação.

Além disso, o [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) é um sistema de software livre para gerenciamento de grupos de VMs e contêineres, derivado de lições aprendidas no Google. Você pode até usar [kubernetes com Elabore suporte de rede tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) esteja aberto fonte "Plataforma-como-um-serviço" (PaaS) que torna mais fácil toodeploy e gerenciar aplicativos em seus próprios servidores. Deis criado com base em Docker e CoreOS tooprovide um PaaS leve um fluxo de trabalho inspirado Heroku.

O [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), uma distribuição do Linux com superfície otimizada, suporte ao Docker e seu próprio sistema de contêineres chamado [rkt](https://github.com/coreos/rkt), também tem uma ferramenta de gerenciamento de grupos de contêineres chamada [fleet](https://coreos.com/fleet/docs/latest/).

O Ubuntu, outra distribuição muito popular do Linux, dá um suporte muito bom ao Docker, mas dá suporte também a [clusters Linux (estilo LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Ferramentas para trabalhar com máquinas virtuais do Azure e contêineres
Trabalhar com contêineres e VMs do Azure usa ferramentas. Esta seção fornece uma lista de apenas alguns dos conceitos de mais útil ou importantes de saudação e ferramentas de contêineres, grupos e configuração maior hello e orquestração usado com eles.

> [!NOTE]
> Essa área está mudando surpreendentemente rapidamente e enquanto faremos nosso melhor tookeep neste tópico e seus links backup toodate, também pode ser uma tarefa impossível. Certifique-se de que pesquisar em interessantes tookeep assuntos backup toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Tecnologias de contêineres e VMs
Algumas tecnologias de contêineres do Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS e rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Links para contêineres do Windows:

* [Contêineres do Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Links do Visual Studio Docker:

* [Ferramentas do Visual Studio para Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Ferramentas do Docker:

* [Docker daemon](https://docs.docker.com/installation/#installation)
* Clientes Docker
  * [Cliente Docker do Windows no Chocolatey](https://chocolatey.org/packages/docker)
  * [Instruções de instalação do Docker](https://docs.docker.com/installation/#installation)

Docker no Microsoft Azure:

* [Extensão VM Docker para Linux no Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Guia de Usuário da Extensão de VM Docker do Azure](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Usando a extensão da VM Docker de saudação do hello Azure Interface de linha de comando (CLI do Azure)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Usando Olá extensão da VM Docker do hello portal do Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Como toouse docker-máquina no Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Como docker toouse com por nuvem no Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Introdução ao Docker e Redija no Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usando um toocreate de modelo de grupo de recursos do Azure um host Docker no Azure rapidamente](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Olá suporte interno para `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) para aplicativos contidos
* [Implementar um Registro privado do Docker no Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Distribuições do Linux e exemplos do Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configuração, gerenciamento de clusters e coordenação de contêineres:

* [Fleet no CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Concluir a implantação de cluster do guia tooautomated Kubernetes com CoreOS e Trança](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Visualizador do Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [DCOS (Sistema operacional de centro de dados) Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) e [Hudson](http://hudson-ci.org/)

  * [Plug-in do Agente de VM Jenkins para Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [Repositório GitHub: plug-in de armazenamento Jenkins do Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Terceiros: plug-in de subordinado Hudson do Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Terceiros: plug-in de armazenamento Hudson do Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Automação do Azure](https://azure.microsoft.com/services/automation/)

  * [Vídeo: Como tooUse automação do Azure com VMs do Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* PowerShell DSC para Linux

  * [Blog: Como toodo Powershell DSC para Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Cliente Docker DSC](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Próximas etapas
Confira o [Docker](https://www.docker.com) e os [Contêineres do Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
