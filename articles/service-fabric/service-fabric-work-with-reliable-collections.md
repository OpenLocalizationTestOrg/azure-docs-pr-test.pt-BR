---
title: "aaaWorking com coleções confiável | Microsoft Docs"
description: "Aprenda as práticas recomendadas de saudação para trabalhar com coleções confiável."
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>Trabalhando com Reliable Collections
Service Fabric oferece uma programação de desenvolvedores do modelo too.NET disponíveis por meio de coleções confiável com monitoração de estado. Especificamente, o Service Fabric fornece as classes de dicionário confiável e fila confiável. Quando você usar essas classes, seu estado é particionado (para escalabilidade), replicado (para disponibilidade) e transacionado dentro de uma partição (para semântica ACID). Vejamos um uso típico de um objeto de dicionário confiável para ver o que ele está fazendo realmente.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

Todas as operações em objetos de dicionário confiável (exceto ClearAsync, que não pode ser desfeito) exigem um objeto ITransaction. Esse objeto associado a ela qualquer e todas as alterações que está tentando toomake tooany confiável dicionário e/ou objetos de fila confiável em uma única partição. Adquirir um ITransaction objeto chamando a partição de saudação do método de CreateTransaction do StateManager.

No código de saudação acima, o objeto de ITransaction do hello é passado método de AddAsync do dicionário tooa confiável. Internamente, métodos de dicionário que aceita uma chave de usar um bloqueio de leitor/gravador associado à chave hello. Se o método hello modifica o valor da chave hello, método hello entra em um bloqueio de gravação na chave de saudação e se o método hello lê apenas do valor da chave Olá, em seguida, um bloqueio de leitura é realizado na chave de saudação. Como AddAsync modifica toohello de valor da chave Olá novo, valor transmitido, o bloqueio de gravação da chave Olá é obtido. Portanto, se threads 2 (ou mais) tentam tooadd valores com hello mesma chave no hello mesmo tempo, um thread irá adquirir o bloqueio de gravação da saudação e hello outros threads serão bloqueada. Por padrão, o bloco de métodos para o bloqueio de saudação do too4 segundos tooacquire; Depois de 4 segundos, métodos de saudação gerar uma TimeoutException. As sobrecargas do método existem permitindo que você toopass um valor de tempo limite explícito, se você preferir.

Normalmente, você gravar sua tooa de tooreact código TimeoutException detectá-lo e repetir a operação de inteiro de saudação (conforme mostrado no código de saudação acima). No meu código simples, estou apenas chamando Task.Delay passando 100 milissegundos de cada vez. Porém, na realidade, é melhor usar algum tipo de atraso de recuo exponencial em vez disso.

Depois de saudação bloqueio é adquirido, AddAsync adiciona a chave de saudação e tooan dicionário temporário interno associado Olá ITransaction objeto faz referência a objeto de valor. Isso é feito tooprovide com semântica de leitura-seu-proprietário-gravações. Ou seja, depois de chamar AddAsync, um tooTryGetValueAsync chamada posterior (usando o mesmo objeto ITransaction do hello) retornará o valor de saudação mesmo se você ainda não confirmada transação hello. Em seguida, AddAsync serializa a chave e valor toobyte matrizes de objetos e anexa o arquivo de log de tooa esses bytes matrizes no nó local hello. Por fim, AddAsync envia Olá bytes matrizes tooall Olá réplicas secundárias para que eles têm Olá a mesma chave/valor informações. Mesmo que as informações de chave/valor Olá gravou o arquivo de log tooa, informações de saudação não são consideradas parte do dicionário de saudação até que a transação de saudação que eles estão associados foi confirmada.

No código de saudação acima, Olá chamada tooCommitAsync confirma todas as operações da transação hello. Especificamente, ele anexa o arquivo de log de toohello de informações de confirmação no nó local hello e também envia Olá réplicas secundárias de confirmação tooall registro hello. Depois que um quorum (maioria) de réplicas Olá respondeu, todos os dados de alterações são consideradas permanente e todos os bloqueios associados às chaves que foram manipuladas por meio do objeto de ITransaction do hello são liberados para outros threads/transações pode manipular Olá mesmas chaves e seus valores.

Se CommitAsync não for chamado (geralmente devido tooan exceção), o objeto de ITransaction do hello é descartado. Ao descartar um objeto ITransaction não confirmado, Service Fabric anexa o arquivo de log do nó local de toohello do informações de anulação e nada precisa toobe enviados tooany de saudação réplicas secundárias. E, em seguida, todos os bloqueios associados às chaves que foram manipuladas por meio de transação de saudação são liberados.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Armadilhas comuns e como tooavoid-los
Agora que você sabe como coleções confiável Olá funcionam internamente, vamos dar uma olhada em alguns uso indevido comum deles. Consulte o código de saudação abaixo:

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

Ao trabalhar com um dicionário regular do .NET, você pode adicionar um dicionário de toohello de chave/valor e, em seguida, altere o valor de saudação de uma propriedade (como LastLogin). No entanto, esse código não funcionará corretamente com um dicionário confiável. Lembre-se de saudação discussão anterior, chamada hello tooAddAsync serializa o valor da chave Olá objetos toobyte matrizes e, em seguida, salva Olá matrizes arquivo local tooa e também envia réplicas secundárias toohello. Se você alterar posteriormente uma propriedade, isso altera o valor da propriedade Olá na memória. ele não afeta o arquivo local hello ou dados de saudação enviados toohello réplicas. Se o processo de saudação falhar, o que está na memória é descartada. Quando um novo processo é iniciado ou se outra réplica se tornar primária, Olá, em seguida, o valor antigo da propriedade é o que está disponível.

Não consigo enfatizar bastante fácil é toomake Olá tipo de erro mostrado acima. E, somente aprenderá sobre o erro Olá se/quando processo Olá fica inoperante. Olá maneira correta toowrite Olá código é simplesmente tooreverse Olá duas linhas:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Veja este outro exemplo que mostra um erro comum:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

Novamente, com dicionários do .NET regulares, Olá código acima funciona bem e é um padrão comum: desenvolvedor Olá usa uma chave toolook um valor. Se houver valor Olá, desenvolvedor Olá altera o valor da propriedade. No entanto, com coleções confiáveis, este código exibe Olá mesmo problema como já foi abordado: **você não deve modificar um objeto quando você tiver concedido coleção confiável tooa.**

Olá correto tooupdate de maneira um valor em uma coleção confiável, é tooget Referência toohello existente e considere objeto Olá chamado tooby essa referência imutável. Em seguida, crie um novo objeto que é uma cópia exata do objeto original hello. Agora, você pode modificar o estado de saudação do novo objeto e insira Olá novo objeto na coleção de saudação para que ele obtém serializado toobyte matrizes, o arquivo local toohello anexado e enviadas toohello réplicas. Depois de confirmar Olá alteração (ões), objetos na memória de hello, arquivo de local de Olá, e todas as réplicas de saudação têm Olá mesmo estado. Parece que está tudo bem.

código de saudação abaixo mostra tooupdate de maneira correta de saudação um valor em uma coleção confiável:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Definir o erro do programador de tooprevent de tipos de dados imutáveis
Idealmente, gostaríamos erros de tooreport do compilador hello quando você gerar o código que muda o estado de um objeto que você deve tooconsider imutável acidentalmente. Mas, compilador c# Olá não tem Olá capacidade toodo isso. Portanto, tooavoid possíveis programador bugs, é altamente recomendável que você defina tipos Olá que você usa com coleções confiável toobe imutável tipos. Especificamente, isso significa que você fique toocore tipos de valor (como números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan e hello como). E, claro, você também pode usar String. É melhor propriedades de coleção tooavoid como a serialização e desserialização pode frequentemente pode prejudicar o desempenho. No entanto, se você quiser toouse propriedades de coleção, é altamente recomendável usar saudação do. Biblioteca de coleções imutáveis do NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Essa biblioteca está disponível para download em http://nuget.org. Também recomendamos lacrar suas classes e tornar os campos somente leitura sempre que possível.

Olá UserInfo tipo abaixo demonstra como toodefine um imutável digite aproveitando as vantagens de recomendações mencionados acima.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

Olá ItemId tipo também é um tipo imutável, conforme mostrado aqui:

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>Controle de versão do esquema (atualizações)
Internamente, as Reliable Collections serializam os objetos usando o DataContractSerializer do .NET. objetos serializado de saudação são disco local da réplica primária toohello persistente e também são transmitido toohello réplicas secundárias. Como seu serviço amadurece, é provável que convém toochange tipo de saudação de dados (esquema) requer que seu serviço. Você deve abordar o controle de versão dos seus dados com muito cuidado. Primeiramente, você sempre deve ser capaz de toodeserialize os dados antigos. Especificamente, isso significa que seu código de desserialização deve ser compatível com versões anteriores infinitamente: 333 de versão do seu código de serviço deve ser capaz de toooperate em dados colocados em uma coleção confiável versão 1 do seu código de serviço cinco anos.

Além disso, o código de serviço é atualizado em um domínio de atualização por vez. Assim, durante uma atualização, você tem duas versões diferentes do seu código de serviço em execução simultaneamente. Você deve evitar a nova versão saudação do seu código de serviço usam Olá novo esquema, como as versões antigas do seu código de serviço podem não ser o novo esquema de toohandle capaz de saudação. Quando possível, você deve projetar cada versão do seu serviço toobe compatível com a 1 versão. Especificamente, isso significa que V1 do seu código de serviço deve ser capaz de toosimply ignorar quaisquer elementos de esquema não tratar explicitamente. No entanto, ele deve ser capaz de toosave quaisquer dados, ela não conhece explicitamente e simplesmente gravá-la de volta ao atualizar um valor ou uma chave de dicionário.

> [!WARNING]
> Enquanto você pode modificar o esquema de saudação de uma chave, você deve garantir que o código de hash da chave e algoritmos de equals são estáveis. Se você alterar como qualquer um desses algoritmos funcionam, não será capaz de toolook chave Olá no dicionário confiável Olá nunca novamente.
>
>

Como alternativa, você pode executar o que é geralmente referidos tooas uma fase de 2 a atualização. Com uma atualização de fase 2, atualize seu serviço de V1 tooV2: V2 contém código Olá que sabe como toodeal com nova alteração de esquema hello, mas esse código não é executado. Quando Olá V2 código lê dados V1, ele opera nele e grava dados V1. Em seguida, após a atualização de saudação for concluída em todos os domínios de atualização, alguma forma você pode sinalizar instâncias em execução de V2 toohello que atualização Olá for concluída. (Uma forma toosignal tooroll fora de uma atualização de configuração; isso é o que torna isso uma atualização da fase 2.) Agora, Olá V2 instâncias podem ler dados V1, convertê-la tooV2 dados, operar nele e grave-os como dados V2. Quando outras instâncias de ler dados V2, eles não precisam de tooconvert, eles apenas operar nele e gravar dados V2.

## <a name="next-steps"></a>Próximas etapas
toolearn sobre a criação de contratos de dados compatível forward, consulte [contratos de dados compatíveis por encaminhamento](https://msdn.microsoft.com/library/ms731083.aspx).

práticas recomendadas do toolearn em contratos de dados de controle de versão, consulte [controle de versão de contrato de dados](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn como contratos de dados do tooimplement versão tolerantes a falhas, consulte [retornos de chamada de serialização tolerantes à versão](https://msdn.microsoft.com/library/ms733734.aspx).

toolearn como tooprovide uma estrutura de dados que pode interoperar em várias versões, consulte [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
