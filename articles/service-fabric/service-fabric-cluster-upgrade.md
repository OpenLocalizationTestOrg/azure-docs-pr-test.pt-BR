---
title: aaaUpgrade um cluster do Azure Service Fabric | Microsoft Docs
description: "Atualizar o código do Service Fabric hello e/ou configuração que é executado de um cluster do Service Fabric, incluindo a definição do modo de atualização de cluster, atualizar certificados, adicionando portas de aplicativo, fazendo patches do sistema operacional, e assim por diante. O que você pode esperar quando são executadas atualizações Olá?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Atualizar um cluster do Azure Service Fabric
> [!div class="op_single_selector"]
> * [Cluster do Azure](service-fabric-cluster-upgrade.md)
> * [Cluster Independente](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Para qualquer sistema moderno, criar o sistema é sucesso a longo prazo tooachieving chave do produto. Um cluster do Azure Service Fabric é um recurso cujo proprietário é você, mas que é parcialmente gerenciado pela Microsoft. Este artigo descreve o que é gerenciado automaticamente e o que você pode configurar por conta própria.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Controle de versão do fabric Olá que é executado em seu Cluster
Você pode definir sua malha automática do cluster tooreceive atualizações conforme elas são lançadas pela Microsoft ou você pode selecionar uma versão com suporte de malha que quiser toobe seu cluster.

Você pode fazer isso definindo hello "upgradeMode" cluster a configuração no portal de saudação ou usando o Gerenciador de recursos em tempo de saudação da criação ou posterior em um cluster ao vivo 

> [!NOTE]
> Verifique se tookeep o cluster executando uma versão com suporte de malha sempre. Como e quando é anunciar o lançamento de saudação de uma nova versão da malha do serviço, versão anterior de saudação está marcado para o fim do suporte após um mínimo de 60 dias a partir dessa data. Olá novas versões de saudação são anunciadas [no blog da equipe Olá service fabric](https://blogs.msdn.microsoft.com/azureservicefabric/). nova versão de Hello é toochoose disponível. 
> 
> 

14 dias anteriores toohello expiração da versão de saudação seu cluster está em execução, será gerado um evento de integridade que coloca o cluster em um estado de integridade de aviso. cluster Olá permanece em um estado de aviso até você atualizar a versão de malha com suporte de tooa.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Definir o modo de atualização de saudação por meio do portal
Quando você estiver criando Olá cluster, você pode definir Olá cluster tooautomatic ou manual.

![Create_Manualmode][Create_Manualmode]

Você pode definir Olá cluster tooautomatic ou manual quando em um cluster de ao vivo, usando o hello gerenciar a experiência. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Atualizando tooa nova versão em um cluster que é definir o modo de tooManual por meio do portal.
tooupgrade tooa nova versão, você só precisa toodo é selecionem versão disponível Olá Olá suspenso e salvar. atualização do Fabric Olá obtém foi iniciada automaticamente. Olá diretivas de integridade do cluster (uma combinação de integridade do nó e a integridade de saudação todos os aplicativos em execução no cluster de saudação de Olá) sejam atendidas tooduring atualização de saudação.

Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. Role para baixo essa tooread de documento mais informações sobre como tooset as políticas de integridade personalizado. 

Depois de corrigir problemas de saudação que resultaram em reversão hello, necessidade atualização de saudação tooinitiate novamente, por seguir Olá mesmo etapas como antes.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Definir o modo de atualização de saudação por meio de um modelo do Gerenciador de recursos
Adicione Olá a definição de recurso "upgradeMode" configuração toohello Microsoft.ServiceFabric/clusters e conjunto hello "clusterCodeVersion" tooone de saudação suporte para versões de malha, conforme mostrado abaixo e, em seguida, implante o modelo de saudação. os valores válidos para "upgradeMode" Hello são "Manual" ou "Automático"

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>Atualizando tooa nova versão em um cluster que é definir o modo de tooManual por meio de um modelo do Gerenciador de recursos.
Quando o cluster hello está em modo Manual, tooupgrade tooa nova versão, alterar a versão com suporte do tooa clusterCodeVersion"hello" e implantá-lo. implantação de saudação do modelo Olá, é ativada de atualização do Fabric Olá obtém foi iniciada automaticamente. Olá diretivas de integridade do cluster (uma combinação de integridade do nó e a integridade de saudação todos os aplicativos em execução no cluster de saudação de Olá) sejam atendidas tooduring atualização de saudação.

Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. Role para baixo essa tooread de documento mais informações sobre como tooset as políticas de integridade personalizado. 

Depois de corrigir problemas de saudação que resultaram em reversão hello, necessidade atualização de saudação tooinitiate novamente, por seguir Olá mesmo etapas como antes.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Obter uma lista de todas as versões disponíveis para todos os ambientes para determinada assinatura
Executar Olá o comando a seguir, e você deve obter um toothis semelhante de saída.

"supportExpiryUtc" informa o quando determinada versão está expirando ou expirou. Olá versão mais recente não tem uma data válida - possui um valor de "9999-12-31T23:59:59.9999999", que significa apenas data de expiração de saudação ainda não está definida.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Comportamento de atualização do Fabric quando o modo de atualização de cluster Olá é automático
A Microsoft mantém o código de malha de saudação e de configuração que é executado em um cluster do Azure. Podemos executar o software de toohello monitorado de atualizações automáticas como necessário. Essas atualizações podem ser feitas no código, na configuração ou em ambos. toomake-se de que seu aplicativo não sofre nenhum impacto ou o mínimo de impacto devido a atualizações toothese, podemos realizar atualizações Olá no hello fases a seguir:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Fase 1: uma atualização é executada usando todas as políticas de integridade do cluster
Durante essa fase, atualizações Olá continuar um domínio de atualização por vez, e os aplicativos de saudação que estavam em execução no cluster Olá continuam toorun sem qualquer tempo de inatividade. Olá diretivas de integridade do cluster (uma combinação de integridade do nó e a integridade de saudação todos os aplicativos em execução no cluster de saudação de Olá) sejam atendidas tooduring atualização de saudação.

Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. Em seguida, um email é enviado toohello proprietário da assinatura de saudação. email Olá contém Olá informações a seguir:

* Notificação de que precisamos fazer tooroll uma atualização de cluster.
* Sugestões de ações corretivas, se houver alguma.
* Olá quantos dias (n) até que executamos fase 2.

Tentamos Olá tooexecute que mesmo atualizar mais algumas vezes, no caso de falha de todas as atualizações por motivos de infraestrutura. Após a saudação n dias do email de Olá Olá data foi enviado, podemos continuar tooPhase 2.

Se as diretivas de integridade do cluster Olá forem atendidas, atualização de saudação é considerada bem-sucedida e marcadas como concluída. Isso pode ocorrer durante a atualização de saudação inicial ou de qualquer execução repetida de atualização de saudação nesta fase. Nenhum email de confirmação será enviado após uma execução bem-sucedida. Isso é tooavoid enviando você muitos emails – receber um email deve ser consideradas toonormal uma exceção. Esperamos que a maioria das Olá toosucceed de atualizações de cluster sem afetar a disponibilidade do seu aplicativo.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Fase 2: uma atualização é executada usando apenas as políticas de integridade padrão
políticas de integridade Olá nesta fase são definidas de forma que o número de saudação de aplicativos que foram Íntegro no início de saudação da atualização Olá permanece Olá mesmo para Olá duração do processo de atualização de saudação. Como na fase 1, atualizações Olá fase 2 continuar um domínio de atualização por vez, e os aplicativos de Olá que estavam em execução no cluster Olá continuam toorun sem qualquer tempo de inatividade. diretivas de integridade do cluster Hello (uma combinação de integridade do nó e a integridade de saudação que todos os aplicativos em execução no cluster de saudação de Olá) são toofor sejam seguidos Olá durante atualização de saudação.

Se as diretivas de integridade do cluster Olá em vigor não forem atendidas, atualização de saudação é revertida. Em seguida, um email é enviado toohello proprietário da assinatura de saudação. email Olá contém Olá informações a seguir:

* Notificação de que precisamos fazer tooroll uma atualização de cluster.
* Sugestões de ações corretivas, se houver alguma.
* Olá quantos dias (n) até que executamos fase 3.

Tentamos Olá tooexecute que mesmo atualizar mais algumas vezes, no caso de falha de todas as atualizações por motivos de infraestrutura. Um lembrete será enviado por email alguns dias antes do término dos n dias. Após a saudação n dias do email de Olá Olá data foi enviado, podemos continuar tooPhase 3. emails Olá que enviaremos na fase 2 devem ser levadas a sério e ações corretivas devem ser executadas.

Se as diretivas de integridade do cluster Olá forem atendidas, atualização de saudação é considerada bem-sucedida e marcadas como concluída. Isso pode ocorrer durante a atualização de saudação inicial ou de qualquer execução repetida de atualização de saudação nesta fase. Nenhum email de confirmação será enviado após uma execução bem-sucedida.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Fase 3: uma atualização é executada usando políticas de integridade agressivas
Essas políticas de integridade nessa fase se destinam a conclusão da atualização de saudação em vez de integridade de saudação de aplicativos de saudação. Pouquíssimas atualizações de cluster chegam a esta fase. Se o cluster obtém toothis fase, há uma boa chance de que seu aplicativo se tornará não íntegro e/ou perda de disponibilidade.

Toohello semelhante outras duas fases, atualizações de fase 3 continuar um domínio de atualização por vez.

Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. Tentamos Olá tooexecute que mesmo atualizar mais algumas vezes, no caso de falha de todas as atualizações por motivos de infraestrutura. Depois disso, o cluster de saudação é fixado, para que ele não receberá mais suporte e/ou atualizações.

Proprietário da assinatura toohello, junto com as ações corretivas Olá é enviado a um email com essas informações. Não esperamos que qualquer tooget clusters em um estado em que a fase 3 falhou.

Se as diretivas de integridade do cluster Olá forem atendidas, atualização de saudação é considerada bem-sucedida e marcadas como concluída. Isso pode ocorrer durante a atualização de saudação inicial ou de qualquer execução repetida de atualização de saudação nesta fase. Nenhum email de confirmação será enviado após uma execução bem-sucedida.

## <a name="cluster-configurations-that-you-control"></a>Configurações do cluster que você controla
Além de modo a atualização do cluster de saudação do toohello capacidade tooset, aqui estão configurações de saudação que podem ser alteradas em um cluster ao vivo.

### <a name="certificates"></a>Certificados
Você pode adicionar novas ou exclua os certificados de cliente por meio do portal hello e cluster Olá facilmente. Consulte também[neste documento para obter instruções detalhadas](service-fabric-cluster-security-update-certs-azure.md)

![Captura de tela que mostra as impressões digitais de certificado no portal do Azure de saudação.][CertificateUpgrade]

### <a name="application-ports"></a>Portas do aplicativo
Você pode alterar as portas de aplicativo alterando propriedades de recurso do hello balanceador de carga que estão associadas com o tipo de nó de saudação. Você pode usar o portal de hello, ou você pode usar o Gerenciador de recursos do PowerShell diretamente.

tooopen uma nova porta em todas as VMs em um tipo de nó, Olá a seguir:

1. Adicione um novo balanceador de carga adequado de toohello de teste.
   
    Se você implantou o cluster usando o portal de hello, balanceadores de carga de saudação são nomeados "LB-nome do grupo de recursos de saudação-NodeTypename", uma para cada tipo de nó. Como os nomes de Balanceador de carga de saudação são exclusivos somente dentro de um grupo de recursos, é melhor se você pesquisar por-los em um grupo de recursos específicos.
   
    ![Captura de tela que mostra a adição de uma investigação tooa balanceador de carga no portal de saudação.][AddingProbes]
2. Adicione um balanceador de carga de toohello regra nova.
   
    Adicione um novo toohello de regra mesmo balanceador de carga usando o teste Olá que você criou na etapa anterior hello.
   
    ![Adicionar um balanceador de carga nova regra tooa no portal de saudação.][AddingLBRules]

### <a name="placement-properties"></a>Propriedades de posicionamento
Para cada um dos tipos de nós hello, você pode adicionar propriedades de posicionamento personalizado que você deseja toouse em seus aplicativos. NodeType é uma propriedade padrão que você pode usar sem adicioná-la explicitamente.

> [!NOTE]
> Para obter detalhes sobre o uso de saudação de restrições de posicionamento, propriedades de nó, e como toodefine-los, consulte toohello seção "Restrições de posicionamento e propriedades de nó" hello documento do Gerenciador de recursos de Cluster do serviço de malha em [descrevendo o Cluster ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Métricas de capacidade
Para cada um dos tipos de nós hello, você pode adicionar métricas de capacidade personalizadas que você deseja toouse em sua carga de tooreport de aplicativos. Para obter detalhes sobre o uso de saudação de carga de tooreport de métricas de capacidade, consulte toohello documentos do Gerenciador de recursos de Cluster do serviço de malha em [descrevendo seu Cluster](service-fabric-cluster-resource-manager-cluster-description.md) e [métricas e carga](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Configurações de atualização do Fabric – Políticas de integridade
Você pode especificar as políticas de integridade personalizadas para atualização do Fabric. Se você tiver configurado o cluster tooAutomatic atualizações de malha, essas políticas obtém aplicado toohello fase 1 de atualizações de malha automática hello.
Se você tiver configurado o cluster para a malha Manual atualizações, em seguida, essas políticas são aplicadas a cada vez que você selecionar uma nova versão de disparo Olá sistema tookick desativar a atualização do fabric Olá no cluster. Se você não substituir políticas hello, Olá padrões são usados.

Você pode especificar políticas de integridade personalizado hello ou revisar configurações atuais de saudação com folha de "atualização do fabric" Olá, selecionando Olá atualização configurações avançada. Examine Olá figura abaixo sobre como. 

![Gerenciar políticas de integridade personalizadas][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Personalizar as configurações do Fabric para seu cluster
Consulte também[configurações de malha de cluster de malha do serviço](service-fabric-cluster-fabric-settings.md) sobre o que e como você pode personalizá-los.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Patches do sistema operacional em Olá máquinas virtuais que compõem o cluster Olá
Consulte também[Patch orquestração de aplicativo](service-fabric-patch-orchestration-application.md) que pode ser implantado em seu patches tooinstall de cluster do Windows Update de uma maneira orquestrada, manter os serviços de saudação disponíveis todo o tempo de saudação. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Atualizações de sistema operacional em Olá máquinas virtuais que compõem o cluster Olá
Se você deve atualizar a imagem do sistema operacional Olá em máquinas virtuais de saudação do cluster hello, você deve fazê-lo uma VM por vez. Você é responsável por esta atualização. Atualmente não há nenhuma automação para isso.

## <a name="next-steps"></a>Próximas etapas
* Saiba como toocustomize alguns Olá [configurações de malha de cluster de malha do serviço](service-fabric-cluster-fabric-settings.md)
* Saiba como muito[dimensionar o cluster e sair](service-fabric-cluster-scale-up-down.md)
* Saiba mais sobre [atualizações de aplicativo](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
