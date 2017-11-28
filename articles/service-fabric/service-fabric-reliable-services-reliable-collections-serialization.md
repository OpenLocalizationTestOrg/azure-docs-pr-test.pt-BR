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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="4742b-103">Serialização de objeto de Coleções Confiáveis no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4742b-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="4742b-104">Coleções de confiável replicam e manter seu toomake itens são duráveis em falhas de máquina e quedas de energia.</span><span class="sxs-lookup"><span data-stu-id="4742b-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="4742b-105">Itens de tooreplicate e toopersist, tooserialize da necessidade de coleções confiável-los.</span><span class="sxs-lookup"><span data-stu-id="4742b-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="4742b-106">Coleções de confiável obtém serializador adequado Olá para um determinado tipo de Gerenciador de estado confiável.</span><span class="sxs-lookup"><span data-stu-id="4742b-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="4742b-107">Gerenciador de estado confiável contém serializadores internos e permite toobe serializadores personalizados registrados para um determinado tipo.</span><span class="sxs-lookup"><span data-stu-id="4742b-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="4742b-108">Serializadores internos</span><span class="sxs-lookup"><span data-stu-id="4742b-108">Built-in Serializers</span></span>

<span data-ttu-id="4742b-109">O Gerenciador de Estado Confiável inclui um serializador interno para alguns tipos comuns, de forma que eles possam ser serializados com eficiência por padrão.</span><span class="sxs-lookup"><span data-stu-id="4742b-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="4742b-110">Para outros tipos, o Gerenciador de estado confiável reverterá Olá toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="4742b-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="4742b-111">Serializadores internos são mais eficientes, desde que eles saibam que não é possível alterar os tipos e não precisam tooinclude informações sobre tipo hello como seu nome de tipo.</span><span class="sxs-lookup"><span data-stu-id="4742b-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="4742b-112">O Gerenciador de Estado Confiável tem um serializador interno para os seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="4742b-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="4742b-113">Guid</span><span class="sxs-lookup"><span data-stu-id="4742b-113">Guid</span></span>
- <span data-ttu-id="4742b-114">bool</span><span class="sxs-lookup"><span data-stu-id="4742b-114">bool</span></span>
- <span data-ttu-id="4742b-115">byte</span><span class="sxs-lookup"><span data-stu-id="4742b-115">byte</span></span>
- <span data-ttu-id="4742b-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="4742b-116">sbyte</span></span>
- <span data-ttu-id="4742b-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="4742b-117">byte[]</span></span>
- <span data-ttu-id="4742b-118">char</span><span class="sxs-lookup"><span data-stu-id="4742b-118">char</span></span>
- <span data-ttu-id="4742b-119">string</span><span class="sxs-lookup"><span data-stu-id="4742b-119">string</span></span>
- <span data-ttu-id="4742b-120">decimal</span><span class="sxs-lookup"><span data-stu-id="4742b-120">decimal</span></span>
- <span data-ttu-id="4742b-121">double</span><span class="sxs-lookup"><span data-stu-id="4742b-121">double</span></span>
- <span data-ttu-id="4742b-122">flutuante</span><span class="sxs-lookup"><span data-stu-id="4742b-122">float</span></span>
- <span data-ttu-id="4742b-123">int</span><span class="sxs-lookup"><span data-stu-id="4742b-123">int</span></span>
- <span data-ttu-id="4742b-124">uint</span><span class="sxs-lookup"><span data-stu-id="4742b-124">uint</span></span>
- <span data-ttu-id="4742b-125">longo</span><span class="sxs-lookup"><span data-stu-id="4742b-125">long</span></span>
- <span data-ttu-id="4742b-126">ulong</span><span class="sxs-lookup"><span data-stu-id="4742b-126">ulong</span></span>
- <span data-ttu-id="4742b-127">short</span><span class="sxs-lookup"><span data-stu-id="4742b-127">short</span></span>
- <span data-ttu-id="4742b-128">ushort</span><span class="sxs-lookup"><span data-stu-id="4742b-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="4742b-129">Serialização personalizada</span><span class="sxs-lookup"><span data-stu-id="4742b-129">Custom Serialization</span></span>

<span data-ttu-id="4742b-130">Serializadores personalizados são dados de saudação desempenho ou tooencrypt tooincrease usadas pela transmissão hello e no disco.</span><span class="sxs-lookup"><span data-stu-id="4742b-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="4742b-131">Entre outras razões, serializadores personalizados são geralmente mais eficientes do que o serializador genérico, desde que eles não precisam de informações de tooserialize sobre o tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4742b-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="4742b-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) é tooregister usado um serializador personalizado para Olá recebe o tipo T. Esse registro deve ocorrer antes do início da recuperação, todas as coleções confiável que na construção de saudação do hello StatefulServiceBase tooensure acessar toohello serializador relevantes tooread seus dados persistentes.</span><span class="sxs-lookup"><span data-stu-id="4742b-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

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
> <span data-ttu-id="4742b-133">Os serializadores personalizados têm precedência sobre os serializadores internos.</span><span class="sxs-lookup"><span data-stu-id="4742b-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="4742b-134">Por exemplo, quando um serializador personalizado para int é registrado, é usado tooserialize inteiros em vez de serializador internos de saudação para int.</span><span class="sxs-lookup"><span data-stu-id="4742b-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="4742b-135">Como tooimplement um serializador personalizado</span><span class="sxs-lookup"><span data-stu-id="4742b-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="4742b-136">Um serializador personalizado precisa Olá tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span><span class="sxs-lookup"><span data-stu-id="4742b-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="4742b-137">IStateSerializer<T> inclui uma sobrecarga de Gravação e Leitura que usa um valor base chamado T adicional.</span><span class="sxs-lookup"><span data-stu-id="4742b-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="4742b-138">Essa API destina-se à serialização diferencial.</span><span class="sxs-lookup"><span data-stu-id="4742b-138">This API is for differential serialization.</span></span> <span data-ttu-id="4742b-139">Atualmente, o recurso de serialização diferencial não está exposto.</span><span class="sxs-lookup"><span data-stu-id="4742b-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="4742b-140">Portanto, essas duas sobrecargas só são chamadas quando a serialização diferencial é exposta e habilitada.</span><span class="sxs-lookup"><span data-stu-id="4742b-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="4742b-141">Veja a seguir um tipo personalizado de exemplo chamado OrderKey que contém quatro propriedades</span><span class="sxs-lookup"><span data-stu-id="4742b-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="4742b-142">Veja a seguir uma implementação de exemplo de IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="4742b-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="4742b-143">Observe que as sobrecargas de Leitura e Gravação que usam o baseValue chamam sua respectiva sobrecarga para compatibilidade com versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="4742b-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="4742b-144">Possibilidade de atualização</span><span class="sxs-lookup"><span data-stu-id="4742b-144">Upgradability</span></span>
<span data-ttu-id="4742b-145">Em um [atualização de aplicativo móvel](service-fabric-application-upgrade.md), atualização de saudação é aplicado tooa subconjunto de nós, um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="4742b-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="4742b-146">Durante esse processo, alguns domínios de atualização estará na versão mais recente de saudação do seu aplicativo, e alguns domínios de atualização estará na versão mais antiga de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4742b-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="4742b-147">Durante a distribuição de Olá Olá nova versão do seu aplicativo deve ser capaz de tooread Olá antigo dos seus dados e versão antiga de saudação do seu aplicativo deve ser capaz de tooread Olá nova versão dos dados.</span><span class="sxs-lookup"><span data-stu-id="4742b-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="4742b-148">Se o formato de dados Olá não for frente e para trás atualização Olá compatível, podem falhar, ou pior, dados pode ser perdido ou corrompido.</span><span class="sxs-lookup"><span data-stu-id="4742b-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="4742b-149">Se você estiver usando o serializador interno, você não tem tooworry sobre a compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="4742b-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="4742b-150">No entanto, se você estiver usando um serializador personalizado ou hello DataContractSerializer, dados saudação tem toobe infinitamente com versões anteriores e encaminham compatíveis.</span><span class="sxs-lookup"><span data-stu-id="4742b-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="4742b-151">Em outras palavras, cada versão do serializador precisa tooserialize capaz de toobe e desserializar em qualquer versão do tipo hello.</span><span class="sxs-lookup"><span data-stu-id="4742b-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="4742b-152">Os usuários de contrato de dados devem seguir as regras de versão bem definido de saudação para adicionar, remover e alterar os campos.</span><span class="sxs-lookup"><span data-stu-id="4742b-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="4742b-153">Contrato de dados também tem suporte para lidar com campos desconhecidos, conectando-se ao processo de serialização e desserialização hello e lidar com herança de classe.</span><span class="sxs-lookup"><span data-stu-id="4742b-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="4742b-154">Para saber mais, confira [Usando o contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="4742b-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="4742b-155">Os usuários do serializador personalizado devem aderir toohello diretrizes de serializador Olá usarem toomake se ele está com versões anteriores e encaminha compatível.</span><span class="sxs-lookup"><span data-stu-id="4742b-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="4742b-156">Uma maneira comum de oferecer suporte a todas as versões é adicionar informações de tamanho no início de saudação e somente adicionar propriedades opcionais.</span><span class="sxs-lookup"><span data-stu-id="4742b-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="4742b-157">Dessa forma cada versão pode ler tanta possa e saltar a parte restante de saudação do fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4742b-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4742b-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4742b-158">Next steps</span></span>
  * [<span data-ttu-id="4742b-159">Serialização e atualização</span><span class="sxs-lookup"><span data-stu-id="4742b-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="4742b-160">Referência do desenvolvedor para Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="4742b-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="4742b-161">[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4742b-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="4742b-162">[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4742b-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="4742b-163">Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="4742b-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="4742b-164">Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="4742b-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="4742b-165">Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4742b-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
