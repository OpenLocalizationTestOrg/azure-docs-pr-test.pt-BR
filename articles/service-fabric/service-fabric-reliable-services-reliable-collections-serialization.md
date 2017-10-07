---
title: "aaaReliable serialização do objeto de coleção no Azure Service Fabric | Microsoft Docs"
description: "Serialização de objeto de Coleções Confiáveis do Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Serialização de objeto de Coleções Confiáveis no Azure Service Fabric
Coleções de confiável replicam e manter seu toomake itens são duráveis em falhas de máquina e quedas de energia.
Itens de tooreplicate e toopersist, tooserialize da necessidade de coleções confiável-los.

Coleções de confiável obtém serializador adequado Olá para um determinado tipo de Gerenciador de estado confiável.
Gerenciador de estado confiável contém serializadores internos e permite toobe serializadores personalizados registrados para um determinado tipo.

## <a name="built-in-serializers"></a>Serializadores internos

O Gerenciador de Estado Confiável inclui um serializador interno para alguns tipos comuns, de forma que eles possam ser serializados com eficiência por padrão. Para outros tipos, o Gerenciador de estado confiável reverterá Olá toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Serializadores internos são mais eficientes, desde que eles saibam que não é possível alterar os tipos e não precisam tooinclude informações sobre tipo hello como seu nome de tipo.

O Gerenciador de Estado Confiável tem um serializador interno para os seguintes tipos: 
- Guid
- bool
- byte
- sbyte
- byte[]
- char
- string
- decimal
- double
- flutuante
- int
- uint
- longo
- ulong
- short
- ushort

## <a name="custom-serialization"></a>Serialização personalizada

Serializadores personalizados são dados de saudação desempenho ou tooencrypt tooincrease usadas pela transmissão hello e no disco. Entre outras razões, serializadores personalizados são geralmente mais eficientes do que o serializador genérico, desde que eles não precisam de informações de tooserialize sobre o tipo de saudação. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) é tooregister usado um serializador personalizado para Olá recebe o tipo T. Esse registro deve ocorrer antes do início da recuperação, todas as coleções confiável que na construção de saudação do hello StatefulServiceBase tooensure acessar toohello serializador relevantes tooread seus dados persistentes.

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> Os serializadores personalizados têm precedência sobre os serializadores internos. Por exemplo, quando um serializador personalizado para int é registrado, é usado tooserialize inteiros em vez de serializador internos de saudação para int.

### <a name="how-tooimplement-a-custom-serializer"></a>Como tooimplement um serializador personalizado

Um serializador personalizado precisa Olá tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.

> [!NOTE]
> IStateSerializer<T> inclui uma sobrecarga de Gravação e Leitura que usa um valor base chamado T adicional. Essa API destina-se à serialização diferencial. Atualmente, o recurso de serialização diferencial não está exposto. Portanto, essas duas sobrecargas só são chamadas quando a serialização diferencial é exposta e habilitada.

Veja a seguir um tipo personalizado de exemplo chamado OrderKey que contém quatro propriedades

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

Veja a seguir uma implementação de exemplo de IStateSerializer<OrderKey>.
Observe que as sobrecargas de Leitura e Gravação que usam o baseValue chamam sua respectiva sobrecarga para compatibilidade com versões posteriores.

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a>Possibilidade de atualização
Em um [atualização de aplicativo móvel](service-fabric-application-upgrade.md), atualização de saudação é aplicado tooa subconjunto de nós, um domínio de atualização por vez. Durante esse processo, alguns domínios de atualização estará na versão mais recente de saudação do seu aplicativo, e alguns domínios de atualização estará na versão mais antiga de saudação do seu aplicativo. Durante a distribuição de Olá Olá nova versão do seu aplicativo deve ser capaz de tooread Olá antigo dos seus dados e versão antiga de saudação do seu aplicativo deve ser capaz de tooread Olá nova versão dos dados. Se o formato de dados Olá não for frente e para trás atualização Olá compatível, podem falhar, ou pior, dados pode ser perdido ou corrompido.

Se você estiver usando o serializador interno, você não tem tooworry sobre a compatibilidade.
No entanto, se você estiver usando um serializador personalizado ou hello DataContractSerializer, dados saudação tem toobe infinitamente com versões anteriores e encaminham compatíveis.
Em outras palavras, cada versão do serializador precisa tooserialize capaz de toobe e desserializar em qualquer versão do tipo hello.

Os usuários de contrato de dados devem seguir as regras de versão bem definido de saudação para adicionar, remover e alterar os campos. Contrato de dados também tem suporte para lidar com campos desconhecidos, conectando-se ao processo de serialização e desserialização hello e lidar com herança de classe. Para saber mais, confira [Usando o contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).

Os usuários do serializador personalizado devem aderir toohello diretrizes de serializador Olá usarem toomake se ele está com versões anteriores e encaminha compatível.
Uma maneira comum de oferecer suporte a todas as versões é adicionar informações de tamanho no início de saudação e somente adicionar propriedades opcionais.
Dessa forma cada versão pode ler tanta possa e saltar a parte restante de saudação do fluxo de saudação.

## <a name="next-steps"></a>Próximas etapas
  * [Serialização e atualização](service-fabric-application-upgrade-data-serialization.md)
  * [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.
  * [Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.
  * Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).
  * Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).
  * Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).
