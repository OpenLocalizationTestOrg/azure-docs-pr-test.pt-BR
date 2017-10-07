---
title: "aaaAzure preparação da implantação do serviço de malha autônomo Cluster | Microsoft Docs"
description: "Documentação relacionada toopreparing ambiente de saudação e criar a configuração de cluster hello, toobe considerado toodeploying anterior um cluster voltado para a manipulação de uma carga de trabalho de produção."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planejar e preparar a implantação de cluster autônomo do Service Fabric
Execute Olá etapas a seguir antes de criar o cluster.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Etapa 1: Planejar a infraestrutura de cluster
Você está prestes toocreate um cluster do Service Fabric em máquinas que você possui, para que você pode decidir que tipos de falhas que você deseja Olá toosurvive de cluster. Por exemplo, você precisa de linhas de alimentação distintas ou conexões de Internet fornecido máquinas toothese? Além disso, considere a segurança física Olá desses computadores. Máquinas de saudação localização e que precisa de acesso toothem? Após tomar essas decisões, você pode logicamente mapear Olá máquinas toohello vários domínios de falha (consulte a etapa 4). planejamento para clusters de produção de infraestrutura de saudação é mais envolvida que, para clusters de teste.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Etapa 2: Preparar Olá máquinas toomeet pré-requisitos Olá
Pré-requisitos para cada máquina que você deseja que o cluster de toohello tooadd:

* É recomendável, no mínimo, 16 GB de RAM.
* É recomendável um espaço em disco disponível mínimo de 40 GB.
* É recomendável uma CPU com quatro núcleos ou mais.
* Rede segura de tooa de conectividade ou de rede para todas as máquinas.
* Windows Server 2012 R2 ou Windows Server 2016. 
* [.NET Framework 4.5.1 ou posterior](https://www.microsoft.com/download/details.aspx?id=40773), instalação completa.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Olá [RemoteRegistry serviço](https://technet.microsoft.com/library/cc754820) devem estar em execução em todos os computadores de saudação.

Olá administrador de cluster, implantar e configurar o cluster Olá deve ter [privilégios de administrador](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) em cada uma das máquinas de saudação. Você não pode instalar o Service Fabric em um controlador de domínio.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Etapa 3: Determinar o tamanho de cluster inicial Olá
Cada nó em um cluster do Service Fabric autônomo tem Olá Service Fabric runtime implantado e é membro do cluster de saudação. Em uma implantação típica de produção, há um nó por instância de SO (física ou virtual). tamanho do cluster Olá é determinado por suas necessidades comerciais. No entanto, seu cluster deve ter um tamanho mínimo de três nós (computadores ou máquinas virtuais).
Para fins de desenvolvimento, você pode ter mais de um nó em um determinado computador. Em um ambiente de produção, o Service Fabric dá suporte apenas a um nó por máquina virtual ou física.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Etapa 4: Determinar o número de saudação de domínios de falha e domínios de atualização
Um *domínio de falha* (FD) é uma unidade física de falha e é toohello está diretamente relacionado a infraestrutura física em Olá data centers. Um domínio de falha consiste em componentes de hardware (computadores, comutadores, redes, entre outros) que compartilham um ponto único de falha. Embora não haja um mapeamento individual entre domínios de falha e racks, de maneira geral, cada rack pode ser considerado um domínio de falha. Ao considerar nós Olá no cluster, é altamente recomendável que nós de saudação seja distribuída entre pelo menos três domínios de falha.

Quando você especificar FDs em Clusterconfig, você pode escolher o nome de saudação para cada FD. O Service Fabric dá suporte a FDs hierárquicos, de modo que você pode refletir a topologia da sua infraestrutura neles.  Por exemplo, a saudação FDs a seguir é válida:

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

Um *UD* (Domínio de Atualização) é uma unidade lógica de nós. Durante as atualizações de malha de serviços gerenciados (uma atualização de aplicativo ou uma atualização de cluster), todos os nós em um UD descerão atualização de saudação tooperform enquanto os nós em outros UDs permanecem disponíveis tooserve solicitações. Olá executar em seus computadores de atualizações de firmware não consideram UDs, portanto você deve executá-las um computador por vez.

Olá toothink de maneira mais simples sobre esses conceitos é tooconsider FDs como unidade de saudação de falhas não planejadas e UDs como unidade de saudação de manutenção planejada.

Quando você especificar UDs em Clusterconfig, você pode escolher o nome de saudação para cada UD. Por exemplo, a saudação nomes a seguir é válida:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Para obter informações mais detalhadas sobre os domínios de atualização e de falha, confira [Describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md) (Descrevendo um cluster do Service Fabric).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Etapa 5: Baixar o pacote de autônomo do Service Fabric de saudação para o Windows Server
[Baixe o Link - pacote autônomo do Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) e descompacte o pacote hello, ou implantação tooa do computador que é não faz parte do cluster hello, ou tooone de máquinas de saudação que fará parte do cluster.

### <a name="step-6-modify-cluster-configuration"></a>Etapa 6: modificar a configuração do cluster
toocreate um cluster autônomo que toocreate um cluster configuração Clusterconfig arquivo autônomo, que descreve a especificação de saudação do cluster de saudação. Você pode basear o arquivo de configuração de saudação nos modelos de saudação encontrado em Olá link abaixo. <br>
[Configurações de cluster autônomo](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Para obter detalhes sobre seções Olá nesse arquivo, consulte [definições de configuração para o cluster do Windows autônoma](service-fabric-cluster-manifest.md).

Abra um dos arquivos de Clusterconfig de saudação do pacote de saudação baixado e modificar Olá configurações a seguir:
| **Parâmetro de configuração** | **Descrição** |
| --- | --- |
| **NodeTypes** |Tipos de nós permitem que você tooseparate os nós do cluster em vários grupos. Um cluster precisa ter pelo menos um NodeType. Todos os nós em um grupo têm Olá características comuns a seguir: <br> **Nome** -este é o nome do tipo de nó de saudação. <br>**Portas do Ponto de Extremidade** : são vários pontos de extremidade (portas) nomeados que estão associados a esse tipo de nó. Você pode usar qualquer número de porta que você deseja, desde que eles não entrem em conflito com tudo neste manifesto e já não está em uso por outro aplicativo em execução na VM da máquina hello. <br> **Propriedades de posicionamento** -descreve propriedades para esse tipo de nó que você usa como restrições de posicionamento para serviços do sistema hello ou seus serviços. Essas propriedades são pares de chave/valor definidos pelo usuário que fornecem metadados extras para um determinado nó. Exemplos de propriedades do nó seria se o nó de saudação tem um disco rígido ou a placa gráfica, o número de saudação de eixos em seu disco rígido, núcleos e outras propriedades físicas. <br> **As capacidades** -capacidades de nó definem nome hello e a quantidade de recursos específicos que um determinado nó tem disponível para consumo. Por exemplo, um nó pode definir que tem capacidade para uma métrica chamada "MemoryInMb" e que tem 2048 MB de memória disponível por padrão. Essas capacidades são usadas no tooensure de tempo de execução que os serviços que exigem valores específicos de recursos são colocados em nós Olá que tem os recursos disponíveis no hello necessário quantidades.<br>**IsPrimary** - se você tiver mais de um NodeType definido Verifique se apenas um tooprimary com valor de saudação *true*, que é onde o sistema Olá executar services. Todos os outros tipos de nó devem ser definidos como o valor de toohello *false* |
| **Nós** |Esses são os detalhes de Olá para cada um de nós de saudação que fazem parte do cluster de saudação (tipo de nó, o nome do nó, IP endereço, domínio de falha e domínio de atualização do nó de saudação). máquinas de saudação desejado Olá cluster toobe criado na necessidade toobe listado aqui com seus endereços IP. <br> Se você usar Olá mesmo endereço IP para todos os nós de hello, em seguida, um caixa de um cluster é criado, que pode ser usado para fins de teste. Não use clusters de uma caixa para implantar cargas de trabalho de produção. |

Após a configuração de cluster Olá ambiente de toohello todas as configurações, pode ser testado no ambiente de cluster da saudação (etapa 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Etapa 7. Configuração do ambiente

Quando um administrador de cluster configura um cluster do Service Fabric autônomo, o ambiente de saudação é precisa toobe configurado com hello critérios a seguir: <br>
1. usuário Olá criando Olá cluster deve ter máquinas de tooall de privilégios de segurança em nível de administrador listados como nós no arquivo de configuração de cluster de saudação.
2. Computador do qual Olá cluster é criado, bem como cada máquina do nó de cluster deve:
* Desinstalar o SDK do Service Fabric
* Desinstalar o tempo de execução do Service Fabric 
* Olá serviço de Firewall do Windows (mpssvc) habilitou
* Olá o serviço Registro remoto (remoteregistry) tiver habilitado
* Habilitar o compartilhamento de arquivos (SMB)
* Abrir as portas necessárias, com base nas portas de configuração de cluster
* Abrir as portas necessárias para o Serviço de Registro Remoto e o SMB do Windows: 135, 137, 138, 139 e 445
* Ter tooone de conectividade de rede outro
3. Nenhuma das máquinas de nó de cluster Olá deve ser um controlador de domínio.
4. Se Olá cluster toobe implantado é um cluster seguro, valide pré-requisitos estão em colocar e estão configurados corretamente em relação a configuração de saudação de segurança necessárias do hello.
5. Se as máquinas de cluster Olá não estão acessíveis pela internet, o conjunto seguinte Olá Olá cluster configuração:
* Desabilitar a telemetria: em *Propriedades*, defina *"enableTelemetry": false*
* Desabilitar o download da versão de malha automática & notificações essa versão do cluster atual hello está se aproximando do fim do suporte: em *propriedades* definido *"fabricClusterAutoupgradeEnabled": falso*
* Como alternativa se o acesso à internet de rede é limitados domínios listados toowhite, domínios de saudação abaixo são necessários para a atualização automática: go.microsoft.com download.microsoft.com

6. Defina as exclusões de antivírus do Service Fabric apropriadas:

| **Diretórios de Antivírus excluídos** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (da configuração de cluster) |
| FabricLogRoot (da configuração de cluster) |

| **Processos do antivírus excluídos** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Etapa 8. Validar o ambiente usando o script TestConfiguration
Olá TestConfiguration.ps1 script pode ser encontrado no pacote autônomo de saudação. Ele é usado como um analisador de práticas recomendadas toovalidate alguns dos critérios de saudação acima e deve ser usado como um toovalidate de verificação de integridade se um cluster pode ser implantado em um ambiente específico. Se houver qualquer falha, consulte a lista de toohello em [configuração do ambiente](service-fabric-cluster-standalone-deployment-preparation.md) para solução de problemas. 

Esse script pode ser executado em qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós em um arquivo de configuração de cluster de saudação. máquina de saudação que esse script é executado no não tem toobe parte do cluster de saudação.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

No momento este módulo de teste de configuração não valida a configuração de segurança Olá para que isso tenha toobe feito independentemente.  

> [!NOTE]
> Estamos continuamente fazendo aprimoramentos toomake esse módulo mais robusto, portanto se ocorrer uma falha ou ausente caso que você acredita que atualmente não é detectada pelo TestConfiguration, informe-por meio de nosso [suporte a canais](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Criar um cluster autônomo em execução no Windows Server](service-fabric-cluster-creation-for-windows-server.md)
