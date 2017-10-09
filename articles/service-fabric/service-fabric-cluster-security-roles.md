---
title: "Segurança de cluster do Service Fabric: funções de cliente | Microsoft Docs"
description: "Este artigo descreve duas funções de cliente hello e permissões de saudação fornecidas toohello funções."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Controle de acesso baseado em função para clientes do Service Fabric
Malha do serviço do Azure oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário. Controle de acesso permite Olá administrador toolimit acesso toocertain cluster as operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura.  

**Os administradores** têm acesso completo toomanagement recursos (incluindo recursos de leitura/gravação). Por padrão, **usuários** só têm acesso de leitura toomanagement recursos (por exemplo, recursos de consulta) e serviços e aplicativos de tooresolve de capacidade de saudação.

Você pode especificar funções de cliente Olá dois (cliente e administrador) em tempo de saudação da criação do cluster fornecendo certificados separados para cada. Confira [Service Fabric cluster security](service-fabric-cluster-security.md) (Segurança de cluster do Service Fabric) para obter detalhes sobre como configurar um cluster do Service Fabric.

## <a name="default-access-control-settings"></a>Configurações padrão de controle de acesso
tipo de controle de acesso de administrador Olá tem Olá tooall de acesso completo FabricClient APIs. Ele pode executar qualquer leituras e gravações no cluster do Service Fabric hello, incluindo Olá seguintes operações:

### <a name="application-and-service-operations"></a>Operações de aplicativos e serviço
* **CreateService**: criação de serviço                             
* **CreateServiceFromTemplate**: criação de serviço de um modelo                             
* **UpdateService**: atualizações de serviço                             
* **DeleteService**: exclusão de serviço                             
* **ProvisionApplicationType**: provisionamento do tipo de aplicativo                             
* **CreateApplication**: criação de aplicativos                               
* **DeleteApplication**: exclusão de aplicativos                             
* **UpgradeApplication**: iniciar ou interromper atualizações de aplicativo                             
* **UnprovisionApplicationType**: desprovisionar o tipo de aplicativo                             
* **MoveNextUpgradeDomain**: retomar as atualizações de aplicativo com um domínio de atualização explícito                             
* **ReportUpgradeHealth**: retomando atualizações de aplicativo com o progresso de atualização atual Olá                             
* **ReportHealth**: relatório de integridade                             
* **PredeployPackageToNode**: API de pré-implantação                            
* **CodePackageControl**: reiniciar pacotes de código                             
* **RecoverPartition**: recuperar uma partição                             
* **RecoverPartitions**: recuperar partições                             
* **RecoverServicePartitions**: recuperar partições de serviço                             
* **RecoverSystemPartitions**: recuperar partições de serviço do sistema                             

### <a name="cluster-operations"></a>Operações de cluster
* **ProvisionFabric**: MSI e/ou provisionamento de manifesto do cluster                             
* **UpgradeFabric**: inicialização de atualizações de cluster                             
* **UnprovisionFabric**: MSI e/ou desprovisionamento de manifesto do cluster                         
* **MoveNextFabricUpgradeDomain**: retomar as atualizações de cluster com um domínio de atualização explícito                             
* **ReportFabricUpgradeHealth**: retomando atualizações de cluster com o progresso de atualização atual Olá                             
* **StartInfrastructureTask**: iniciar tarefas de infraestrutura                             
* **FinishInfrastructureTask**: concluir tarefas de infraestrutura                             
* **InvokeInfrastructureCommand**: comandos de gerenciamento de tarefas de infraestrutura                              
* **ActivateNode**: ativar um nó                             
* **DeactivateNode**: desativar um nó                             
* **DeactivateNodesBatch**: desativar múltiplos nós                             
* **RemoveNodeDeactivations**: desativar reversão em vários nós                             
* **GetNodeDeactivationStatus**: verificar o status de desativação                             
* **NodeStateRemoved**: relatar o estado do nó removido                             
* **ReportFault**: falha de relatórios                             
* **FileContent**: a imagem de transferência de arquivos de cliente de armazenamento (toocluster externo)                             
* **FileDownload**: imagem iniciação do download arquivo do repositório de cliente (toocluster externo)                             
* **InternalList**: operação de lista de arquivos de cliente de repositório de imagens (interno)                             
* **Delete**: operação de exclusão do cliente de repositório de imagens                              
* **Upload**: operação de upload do cliente de repositório de imagens                             
* **NodeControl**: iniciar, interromper e reiniciar nós                             
* **MoveReplicaControl**: Mover réplicas de um nó tooanother                             

### <a name="miscellaneous-operations"></a>Operações diversas
* **Ping**: pings em cliente                             
* **Query**: todas as consultas permitidas
* **NameExists**: verificações de existência do URI de nomenclatura                             

Por padrão, Olá tipo de controle de acesso de usuário é limitada toohello seguintes operações: 

* **EnumerateSubnames**: nomenclatura de enumeração de URI                             
* **EnumerateProperties**: nomenclatura de enumeração de propriedade                             
* **PropertyReadBatch**: nomenclatura de operações de leitura de propriedade                             
* **GetServiceDescription**: notificações de serviço de sondagem longa e descrições do serviço de leitura                             
* **ResolveService**: resolução de serviço baseada em reclamações                             
* **ResolveNameOwner**: resolver o proprietário do URI de nomenclatura                             
* **ResolvePartition**: resolver serviços do sistema                             
* **ServiceNotifications**: notificações de serviço baseadas em evento                             
* **GetUpgradeStatus**: status de atualização do aplicativo de sondagem                             
* **GetFabricUpgradeStatus**: status de atualização do cluster de sondagem                             
* **InvokeInfrastructureQuery**: tarefas da infraestrutura de consulta                             
* **List**: operação de lista de arquivos de cliente de repositório de imagens                             
* **ResetPartitionLoad**: redefinir a carga de uma Unidade de Failover                             
* **ToggleVerboseServicePlacementHealthReporting**: alternar o posicionamento do relatório de integridade do serviço detalhado                             

controle de acesso de administrador Olá também tem acesso toohello operações precedentes.

## <a name="changing-default-settings-for-client-roles"></a>Alterando as configurações padrão para funções do cliente
No arquivo de manifesto de cluster hello, você pode fornecer o cliente de toohello de recursos do administrador se necessário. Você pode alterar os padrões de saudação vai toohello **configurações de malha** opção durante [criação de cluster](service-fabric-cluster-creation-via-portal.md)e fornecendo Olá precedem configurações em Olá **nome**, **admin**, **usuário**, e **valor** campos.

## <a name="next-steps"></a>Próximas etapas
[Segurança do Cluster do Service Fabric](service-fabric-cluster-security.md)

[Criação de cluster do Service Fabric](service-fabric-cluster-creation-via-portal.md)

