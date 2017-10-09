---
title: "configurações de KVSActorStateProvider aaaChange no Azure microservices | Microsoft Docs"
description: "Saiba como configurar atores com monitoração de estado do Service Fabric do Azure do tipo KVSActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Configurando Reliable Actors--KVSActorStateProvider
Você pode modificar a configuração padrão de saudação do KVSActorStateProvider alterando Olá settings.xml arquivo gerado na raiz do pacote de saudação Microsoft Visual Studio na pasta de configuração Olá para ator especificado hello.

Hello Azure Service Fabric runtime procura nomes de seção predefinida no arquivo settings.xml de saudação e consome os valores de configuração de saudação ao criar hello subjacente de componentes de tempo de execução.

> [!NOTE]
> Fazer **não** excluir ou modificar os nomes de seção Olá de saudação seguintes configurações no arquivo settings.xml de saudação que é gerado no hello solução do Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Configuração de segurança do replicador
As configurações de segurança do replicador são canal de comunicação do hello toosecure usado é usado durante a replicação. Isso significa que os serviços não consegue ver do outro tráfego de replicação, garantindo que os dados de saudação estará altamente disponíveis também seja seguros.
Por padrão, uma seção de configuração de segurança vazia evita a segurança de replicação.

### <a name="section-name"></a>Nome da seção
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuração do replicador
Configurações de replicador configurar replicador de saudação que é responsável por verificar o estado do provedor de estado de ator Olá altamente confiável.
configuração padrão de saudação é gerada pelo modelo do Visual Studio hello e deve ser suficiente. Esta seção fala sobre as configurações adicionais que são replicador de saudação tootune disponíveis.

### <a name="section-name"></a>Nome da seção
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nomes da configuração
| Nome | Unidade | Valor padrão | Comentários |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0,015 |Período de tempo para o replicador Olá a esperas de saudação secundário após o recebimento de uma operação antes de enviar de volta um reconhecimento toohello primário. Outros toobe de confirmações enviada para operações processadas dentro deste intervalo são enviadas como uma resposta. |
| ReplicatorEndpoint |N/D |Nenhum parâmetro padrão obrigatório |Endereço IP e porta que Olá replicador primário/secundário usará toocommunicate com outros replicadores no conjunto de réplicas de saudação. Isso deve fazer referência a um ponto de extremidade TCP recurso no manifesto do serviço de saudação. Consulte também[recursos de manifesto do serviço](service-fabric-service-manifest-resources.md) tooread mais sobre como definir recursos de ponto de extremidade no manifesto do serviço de saudação. |
| RetryInterval |Segundos |5 |Período de tempo após o qual Olá replicador novamente transmite uma mensagem se não receber uma confirmação de uma operação. |
| MaxReplicationMessageSize |Bytes |50 MB |Tamanho máximo de dados de replicação que podem ser transmitidos em uma única mensagem. |
| MaxPrimaryReplicationQueueSize |Número de operações |1024 |Número máximo de operações em fila primária hello. Uma operação é liberada após replicador primário Olá recebe uma confirmação de todos os replicadores secundário de saudação. Esse valor deve ser maior que 64 e uma potência de 2. |
| MaxSecondaryReplicationQueueSize |Número de operações |2.048 |Número máximo de operações em fila secundária hello. Uma operação é liberada depois de tornar seu estado de altamente disponível por meio de persistência. Esse valor deve ser maior que 64 e uma potência de 2. |

## <a name="store-configuration"></a>Configuração de armazenamento
Configurações de armazenamento são usados tooconfigure Olá local de armazenamento é usada toopersist Olá estado que está sendo replicado.
configuração padrão de saudação é gerada pelo modelo do Visual Studio hello e deve ser suficiente. Esta seção fala sobre as configurações adicionais que são o repositório local de saudação tootune disponíveis.

### <a name="section-name"></a>Nome da seção
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Nomes da configuração
| Nome | Unidade | Valor padrão | Comentários |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Milissegundos |200 |Define o máximo de saudação intervalo para o local de repositório durável confirmações de envio em lote. |
| MaxVerPages |Número de páginas |16384 |número máximo de saudação de páginas de versão no local de saudação armazena o banco de dados. Ele determina o número máximo de saudação de transações pendentes. |

## <a name="sample-configuration-file"></a>Arquivo de exemplo de configuração
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>Comentários
parâmetro de BatchAcknowledgementInterval Hello controla a latência de replicação. Um valor de '0' resulta em Olá menor latência possível, ao custo de saudação de taxa de transferência (conforme mais mensagens de confirmação devem ser enviadas e processadas, cada uma contendo confirmações menos).
Olá maior valor de saudação do BatchAcknowledgementInterval, Olá Olá superior geral produtividade de replicação, ao custo de saudação de maior latência de operação. Isso se traduz diretamente toohello latência de confirmações de transações.

