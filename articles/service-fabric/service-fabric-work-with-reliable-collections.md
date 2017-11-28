---
title: "Trabalhando com Coleções Confiáveis | Microsoft Docs"
description: "Conheça as práticas recomendadas para trabalhar com Reliable Collections."
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
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="3f3d0-103">Trabalhando com Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="3f3d0-103">Working with Reliable Collections</span></span>
<span data-ttu-id="3f3d0-104">O Service Fabric oferece um modelo de programação com estado disponível para desenvolvedores .NET por meio das Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="3f3d0-105">Especificamente, o Service Fabric fornece as classes de dicionário confiável e fila confiável.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="3f3d0-106">Quando você usar essas classes, seu estado é particionado (para escalabilidade), replicado (para disponibilidade) e transacionado dentro de uma partição (para semântica ACID).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="3f3d0-107">Vejamos um uso típico de um objeto de dicionário confiável para ver o que ele está fazendo realmente.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="3f3d0-108">Todas as operações em objetos de dicionário confiável (exceto ClearAsync, que não pode ser desfeito) exigem um objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="3f3d0-109">Esse objeto tem associado a ele toda e qualquer alteração que você está tentando realizar em qualquer dicionário confiável e/ou objetos de fila confiável em uma mesma partição.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="3f3d0-110">Você adquire um objeto ITransaction chamando o método CreateTransaction do StateManager da partição.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="3f3d0-111">No código acima, o objeto ITransaction é passado a um método AddAsync de um dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="3f3d0-112">Internamente, os métodos de dicionário que aceitam uma chave usam um bloqueio de leitor/gravador associado à chave.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="3f3d0-113">Se o método modificar o valor da chave, ele usará um bloqueio de gravação nela e se ele apenas ler o valor da chave, um bloqueio de leitura será obtido na chave.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="3f3d0-114">Como o AddAsync modifica o valor da chave para o valor novo repassado, o bloqueio de gravação da chave será obtido.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="3f3d0-115">Desta maneira, se dois (ou mais) threads tentarem adicionar valores com a mesma chave ao mesmo tempo, um deles adquirirá o bloqueio de gravação e os outros ficarão bloqueados.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="3f3d0-116">Por padrão, os métodos ficam bloqueados por até quatro segundos para adquirir o bloqueio; após quatro segundos, os métodos gerarão uma TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="3f3d0-117">Há sobrecargas de método que permitem passar um valor de tempo limite explícito caso você prefira.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="3f3d0-118">Normalmente você pode escrever seu código para reagir a uma TimeoutException capturando-a e repetindo toda a operação (conforme mostrado no código acima).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="3f3d0-119">No meu código simples, estou apenas chamando Task.Delay passando 100 milissegundos de cada vez.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="3f3d0-120">Porém, na realidade, é melhor usar algum tipo de atraso de recuo exponencial em vez disso.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="3f3d0-121">Depois que o bloqueio é adquirido, AddAsync adiciona as referências de objeto de chave e de valor a um dicionário temporário interno associado ao objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="3f3d0-122">Isso é feito para fornecer a semântica de ler-suas-próprias-gravações.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="3f3d0-123">Ou seja, depois de você chamar AddAsync, uma chamada posterior para TryGetValueAsync (usando o mesmo objeto ITransaction) retornará o valor mesmo se você ainda não tiver confirmado a transação.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="3f3d0-124">Em seguida, AddAsync serializa os objetos de chave e de valor para matrizes de bytes e acrescenta essas matrizes de byte em um arquivo de log no nó local.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="3f3d0-125">Por fim, AddAsync envia as matrizes de bytes para todas as réplicas secundárias para que elas tenham as mesmas informações de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="3f3d0-126">Embora as informações de chave/valor tenham sido gravadas em um arquivo de log, as informações não são consideradas parte do dicionário até que a transação à qual elas estão associadas seja confirmada.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="3f3d0-127">No código acima, a chamada para CommitAsync confirma todas as operações da transação.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="3f3d0-128">Especificamente, ela acrescenta informações de confirmação ao arquivo de log no nó local e também envia o registro de confirmação para todas as réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="3f3d0-129">Depois de o quórum (maioria) das réplicas responder, todas as alterações de dados são consideradas permanentes e os bloqueios associados às chaves que foram manipuladas por meio do objeto ITransaction são liberados para que outras threads/transações possam manipular as mesmas chaves e seus valores.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="3f3d0-130">Se CommitAsync não for chamado (geralmente devido a uma exceção é gerada), o objeto ITransaction será descartado.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="3f3d0-131">Ao descartar um objeto ITransaction não confirmado, o Service Fabric acrescenta informações de anulação ao arquivo de log do nó local e nada mais precisa ser enviado para nenhuma das réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="3f3d0-132">Em seguida, todos os bloqueios associados às chaves que foram manipuladas por meio da transação são liberados.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="3f3d0-133">Armadilhas comuns e como evitá-las</span><span class="sxs-lookup"><span data-stu-id="3f3d0-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="3f3d0-134">Agora que você entende como as coleções confiáveis funcionam internamente, vejamos alguns usos indevidos comuns.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="3f3d0-135">Veja o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f3d0-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="3f3d0-136">Ao trabalhar com um dicionário regular do .NET, você pode adicionar uma chave/valor ao dicionário e, em seguida, alterar o valor de uma propriedade (como LastLogin).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="3f3d0-137">No entanto, esse código não funcionará corretamente com um dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="3f3d0-138">Lembre-se da discussão anterior: a chamada para AddAsync serializa os objetos de chave/valor para matrizes de bytes e, em seguida, salva as matrizes em um arquivo local e também as envia para as réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="3f3d0-139">Se você alterar uma propriedade posteriormente, isso apenas alterará o valor da propriedade na memória; isso não afeta o arquivo local ou os dados enviados para as réplicas.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="3f3d0-140">Se o processo falhar, o que estiver na memória será descartado.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="3f3d0-141">Quando um novo processo é iniciado ou se outra réplica se tornar primária, o valor antigo da propriedade será o que está disponível.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="3f3d0-142">Nunca é demais enfatizar como é fácil cometer o tipo de erro mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="3f3d0-143">E você só descobrirá que o erro ocorreu se/quando o processo falhar.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="3f3d0-144">A maneira correta de escrever o código é simplesmente reverter as duas linhas:</span><span class="sxs-lookup"><span data-stu-id="3f3d0-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="3f3d0-145">Veja este outro exemplo que mostra um erro comum:</span><span class="sxs-lookup"><span data-stu-id="3f3d0-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="3f3d0-146">Novamente, com dicionários regulares do .NET, o código acima funciona bem e é um padrão comum: o desenvolvedor usa uma chave para pesquisar um valor.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="3f3d0-147">Se o valor existir, o desenvolvedor alterará o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="3f3d0-148">No entanto, com coleções confiáveis, esse código exibe o mesmo problema já abordado: **você NÃO DEVE modificar um objeto depois de atribui-lo a uma coleção confiável.**</span><span class="sxs-lookup"><span data-stu-id="3f3d0-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="3f3d0-149">A maneira correta de atualizar um valor em uma coleção confiável é obter uma referência ao valor existente e considerar imutável o objeto referenciado por esta referência.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="3f3d0-150">Em seguida, crie um novo objeto que é uma cópia exata do objeto original.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="3f3d0-151">Agora, você pode modificar o estado deste novo objeto e gravá-lo na coleção para que ele seja serializado em matrizes de bytes, anexado ao arquivo local e enviado para as réplicas.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="3f3d0-152">Depois de confirmar as alterações, os objetos na memória, o arquivo local e todas as réplicas terão o mesmo estado exato.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="3f3d0-153">Parece que está tudo bem.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-153">All is good!</span></span>

<span data-ttu-id="3f3d0-154">O código a seguir mostra a maneira correta de atualizar um valor em uma coleção confiável:</span><span class="sxs-lookup"><span data-stu-id="3f3d0-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="3f3d0-155">Definir tipos de dados imutáveis para evitar erro do programador</span><span class="sxs-lookup"><span data-stu-id="3f3d0-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="3f3d0-156">O ideal seria que o compilador relatasse erros quando você acidentalmente produzisse código que transforma o estado de um objeto que deve ser considerado imutável.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="3f3d0-157">Porém, o compilador C# não consegue fazer isso.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="3f3d0-158">Portanto, para evitar possíveis bugs do programador, é altamente recomendável que você defina os tipos usados com coleções confiáveis como tipos imutáveis.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="3f3d0-159">Especificamente, isso significa usar apenas tipos de valor principais (como números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="3f3d0-160">E, claro, você também pode usar String.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-160">And, of course, you can also use String.</span></span> <span data-ttu-id="3f3d0-161">É melhor evitar propriedades de coleção, pois serializá-las e desserializá-las com frequência pode prejudicar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="3f3d0-162">No entanto, se você quiser usar propriedades de coleção, será altamente recomendável usar a biblioteca de coleções imutáveis do .NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="3f3d0-163">Essa biblioteca está disponível para download em http://nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-163">This library is available for download from http://nuget.org.</span></span> <span data-ttu-id="3f3d0-164">Também recomendamos lacrar suas classes e tornar os campos somente leitura sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-164">We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="3f3d0-165">O tipo de UserInfo abaixo demonstra como definir um tipo imutável tirando proveito das recomendações mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-165">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

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
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="3f3d0-166">O tipo ItemId também é um tipo imutável, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3f3d0-166">The ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="3f3d0-167">Controle de versão do esquema (atualizações)</span><span class="sxs-lookup"><span data-stu-id="3f3d0-167">Schema versioning (upgrades)</span></span>
<span data-ttu-id="3f3d0-168">Internamente, as Reliable Collections serializam os objetos usando o DataContractSerializer do .NET.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-168">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="3f3d0-169">Objetos serializados são persistidos no disco local da réplica primária e também são transmitidos para as réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-169">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="3f3d0-170">À medida que seu serviço amadurece, é provável que você queira alterar o tipo de dados (esquema) que ele requer.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-170">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="3f3d0-171">Você deve abordar o controle de versão dos seus dados com muito cuidado.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-171">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="3f3d0-172">Antes de tudo, você deve sempre ser capaz de desserializar os dados antigos.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-172">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="3f3d0-173">Especificamente, isso significa que seu código de desserialização deve ser infinitamente compatível com versões anteriores: a versão 333 do seu código de serviço deve ser capaz de operar em dados colocados em uma coleção confiável pela versão 1 do seu código de serviço cinco anos atrás.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-173">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="3f3d0-174">Além disso, o código de serviço é atualizado em um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-174">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="3f3d0-175">Assim, durante uma atualização, você tem duas versões diferentes do seu código de serviço em execução simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-175">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="3f3d0-176">Você deve evitar que uma nova versão do seu código de serviço use o novo esquema, pois as versões antigas do seu código de serviço podem não ser capazes de lidar com o novo esquema.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-176">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="3f3d0-177">Quando possível, você deve projetar cada versão do seu serviço para ser compatível com a próxima versão.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-177">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="3f3d0-178">Especificamente, isso significa que a V1 do seu código de serviço deve ser capaz de simplesmente ignorar quaisquer elementos de esquema que não consegue manipular explicitamente.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-178">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="3f3d0-179">No entanto, ela deve ser capaz de salvar todos os dados não conhece explicitamente e simplesmente gravá-los de volta ao atualizar uma chave ou valor do dicionário.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-179">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="3f3d0-180">Embora seja possível modificar o esquema de uma chave, você deve garantir que o código hash da chave e algoritmos igual a sejam estáveis.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-180">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="3f3d0-181">Se você alterar como algum desses algoritmos funciona, não será mais possível pesquisar a chave no dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-181">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="3f3d0-182">Como alternativa, você pode executar o que é normalmente conhecido como uma atualização de fase 2.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-182">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="3f3d0-183">Com uma atualização de fase 2, você atualiza seu serviço de V1 para V2: a V2 contém o código que sabe como lidar com a nova alteração de esquema, mas esse código não é executado.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-183">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="3f3d0-184">Quando o código V2 lê dados V1, ele opera nele e grava dados de V1.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-184">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="3f3d0-185">Em seguida, depois que a atualização for concluída em todos os domínios de atualização, você pode sinalizar de alguma forma para as instâncias V2 em execução que a atualização for concluída.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-185">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="3f3d0-186">(Uma forma de sinalizar isso é distribuir uma atualização de configuração; é isso que faz desta uma atualização de fase 2.) Agora, as instâncias V2 podem ler dados V1, convertê-los em dados V2, operá-los e gravá-los como dados V2.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-186">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="3f3d0-187">Quando outras instâncias lerem dados V2, elas não precisarão convertê-lo, elas simplesmente os operam e gravam dados V2.</span><span class="sxs-lookup"><span data-stu-id="3f3d0-187">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f3d0-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f3d0-188">Next Steps</span></span>
<span data-ttu-id="3f3d0-189">Para saber como criar contratos de dados compatíveis com versões futuras, consulte [Contratos de dados compatíveis com versões futuras](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-189">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="3f3d0-190">Para conhecer as práticas recomendadas de contratos de dados de controle de versão, consulte [Controle de Versão de Contrato de Dados](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-190">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="3f3d0-191">Para saber como implementar contratos de dados tolerantes a versões, consulte [Retornos de Chamada de Serialização Tolerantes a Versões](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-191">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="3f3d0-192">Para saber como fornecer uma estrutura de dados interoperável em várias versões, consulte [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f3d0-192">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
