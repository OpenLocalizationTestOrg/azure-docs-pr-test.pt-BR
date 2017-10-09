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
# <a name="working-with-reliable-collections"></a><span data-ttu-id="65066-103">Trabalhando com Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="65066-103">Working with Reliable Collections</span></span>
<span data-ttu-id="65066-104">Service Fabric oferece uma programação de desenvolvedores do modelo too.NET disponíveis por meio de coleções confiável com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="65066-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="65066-105">Especificamente, o Service Fabric fornece as classes de dicionário confiável e fila confiável.</span><span class="sxs-lookup"><span data-stu-id="65066-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="65066-106">Quando você usar essas classes, seu estado é particionado (para escalabilidade), replicado (para disponibilidade) e transacionado dentro de uma partição (para semântica ACID).</span><span class="sxs-lookup"><span data-stu-id="65066-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="65066-107">Vejamos um uso típico de um objeto de dicionário confiável para ver o que ele está fazendo realmente.</span><span class="sxs-lookup"><span data-stu-id="65066-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

<span data-ttu-id="65066-108">Todas as operações em objetos de dicionário confiável (exceto ClearAsync, que não pode ser desfeito) exigem um objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="65066-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="65066-109">Esse objeto associado a ela qualquer e todas as alterações que está tentando toomake tooany confiável dicionário e/ou objetos de fila confiável em uma única partição.</span><span class="sxs-lookup"><span data-stu-id="65066-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="65066-110">Adquirir um ITransaction objeto chamando a partição de saudação do método de CreateTransaction do StateManager.</span><span class="sxs-lookup"><span data-stu-id="65066-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="65066-111">No código de saudação acima, o objeto de ITransaction do hello é passado método de AddAsync do dicionário tooa confiável.</span><span class="sxs-lookup"><span data-stu-id="65066-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="65066-112">Internamente, métodos de dicionário que aceita uma chave de usar um bloqueio de leitor/gravador associado à chave hello.</span><span class="sxs-lookup"><span data-stu-id="65066-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="65066-113">Se o método hello modifica o valor da chave hello, método hello entra em um bloqueio de gravação na chave de saudação e se o método hello lê apenas do valor da chave Olá, em seguida, um bloqueio de leitura é realizado na chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="65066-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="65066-114">Como AddAsync modifica toohello de valor da chave Olá novo, valor transmitido, o bloqueio de gravação da chave Olá é obtido.</span><span class="sxs-lookup"><span data-stu-id="65066-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="65066-115">Portanto, se threads 2 (ou mais) tentam tooadd valores com hello mesma chave no hello mesmo tempo, um thread irá adquirir o bloqueio de gravação da saudação e hello outros threads serão bloqueada.</span><span class="sxs-lookup"><span data-stu-id="65066-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="65066-116">Por padrão, o bloco de métodos para o bloqueio de saudação do too4 segundos tooacquire; Depois de 4 segundos, métodos de saudação gerar uma TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="65066-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="65066-117">As sobrecargas do método existem permitindo que você toopass um valor de tempo limite explícito, se você preferir.</span><span class="sxs-lookup"><span data-stu-id="65066-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="65066-118">Normalmente, você gravar sua tooa de tooreact código TimeoutException detectá-lo e repetir a operação de inteiro de saudação (conforme mostrado no código de saudação acima).</span><span class="sxs-lookup"><span data-stu-id="65066-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="65066-119">No meu código simples, estou apenas chamando Task.Delay passando 100 milissegundos de cada vez.</span><span class="sxs-lookup"><span data-stu-id="65066-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="65066-120">Porém, na realidade, é melhor usar algum tipo de atraso de recuo exponencial em vez disso.</span><span class="sxs-lookup"><span data-stu-id="65066-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="65066-121">Depois de saudação bloqueio é adquirido, AddAsync adiciona a chave de saudação e tooan dicionário temporário interno associado Olá ITransaction objeto faz referência a objeto de valor.</span><span class="sxs-lookup"><span data-stu-id="65066-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="65066-122">Isso é feito tooprovide com semântica de leitura-seu-proprietário-gravações.</span><span class="sxs-lookup"><span data-stu-id="65066-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="65066-123">Ou seja, depois de chamar AddAsync, um tooTryGetValueAsync chamada posterior (usando o mesmo objeto ITransaction do hello) retornará o valor de saudação mesmo se você ainda não confirmada transação hello.</span><span class="sxs-lookup"><span data-stu-id="65066-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="65066-124">Em seguida, AddAsync serializa a chave e valor toobyte matrizes de objetos e anexa o arquivo de log de tooa esses bytes matrizes no nó local hello.</span><span class="sxs-lookup"><span data-stu-id="65066-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="65066-125">Por fim, AddAsync envia Olá bytes matrizes tooall Olá réplicas secundárias para que eles têm Olá a mesma chave/valor informações.</span><span class="sxs-lookup"><span data-stu-id="65066-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="65066-126">Mesmo que as informações de chave/valor Olá gravou o arquivo de log tooa, informações de saudação não são consideradas parte do dicionário de saudação até que a transação de saudação que eles estão associados foi confirmada.</span><span class="sxs-lookup"><span data-stu-id="65066-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="65066-127">No código de saudação acima, Olá chamada tooCommitAsync confirma todas as operações da transação hello.</span><span class="sxs-lookup"><span data-stu-id="65066-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="65066-128">Especificamente, ele anexa o arquivo de log de toohello de informações de confirmação no nó local hello e também envia Olá réplicas secundárias de confirmação tooall registro hello.</span><span class="sxs-lookup"><span data-stu-id="65066-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="65066-129">Depois que um quorum (maioria) de réplicas Olá respondeu, todos os dados de alterações são consideradas permanente e todos os bloqueios associados às chaves que foram manipuladas por meio do objeto de ITransaction do hello são liberados para outros threads/transações pode manipular Olá mesmas chaves e seus valores.</span><span class="sxs-lookup"><span data-stu-id="65066-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="65066-130">Se CommitAsync não for chamado (geralmente devido tooan exceção), o objeto de ITransaction do hello é descartado.</span><span class="sxs-lookup"><span data-stu-id="65066-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="65066-131">Ao descartar um objeto ITransaction não confirmado, Service Fabric anexa o arquivo de log do nó local de toohello do informações de anulação e nada precisa toobe enviados tooany de saudação réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="65066-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="65066-132">E, em seguida, todos os bloqueios associados às chaves que foram manipuladas por meio de transação de saudação são liberados.</span><span class="sxs-lookup"><span data-stu-id="65066-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="65066-133">Armadilhas comuns e como tooavoid-los</span><span class="sxs-lookup"><span data-stu-id="65066-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="65066-134">Agora que você sabe como coleções confiável Olá funcionam internamente, vamos dar uma olhada em alguns uso indevido comum deles.</span><span class="sxs-lookup"><span data-stu-id="65066-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="65066-135">Consulte o código de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="65066-135">See hello code below:</span></span>

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

<span data-ttu-id="65066-136">Ao trabalhar com um dicionário regular do .NET, você pode adicionar um dicionário de toohello de chave/valor e, em seguida, altere o valor de saudação de uma propriedade (como LastLogin).</span><span class="sxs-lookup"><span data-stu-id="65066-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="65066-137">No entanto, esse código não funcionará corretamente com um dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="65066-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="65066-138">Lembre-se de saudação discussão anterior, chamada hello tooAddAsync serializa o valor da chave Olá objetos toobyte matrizes e, em seguida, salva Olá matrizes arquivo local tooa e também envia réplicas secundárias toohello.</span><span class="sxs-lookup"><span data-stu-id="65066-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="65066-139">Se você alterar posteriormente uma propriedade, isso altera o valor da propriedade Olá na memória. ele não afeta o arquivo local hello ou dados de saudação enviados toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="65066-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="65066-140">Se o processo de saudação falhar, o que está na memória é descartada.</span><span class="sxs-lookup"><span data-stu-id="65066-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="65066-141">Quando um novo processo é iniciado ou se outra réplica se tornar primária, Olá, em seguida, o valor antigo da propriedade é o que está disponível.</span><span class="sxs-lookup"><span data-stu-id="65066-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="65066-142">Não consigo enfatizar bastante fácil é toomake Olá tipo de erro mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="65066-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="65066-143">E, somente aprenderá sobre o erro Olá se/quando processo Olá fica inoperante.</span><span class="sxs-lookup"><span data-stu-id="65066-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="65066-144">Olá maneira correta toowrite Olá código é simplesmente tooreverse Olá duas linhas:</span><span class="sxs-lookup"><span data-stu-id="65066-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="65066-145">Veja este outro exemplo que mostra um erro comum:</span><span class="sxs-lookup"><span data-stu-id="65066-145">Here is another example showing a common mistake:</span></span>

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

<span data-ttu-id="65066-146">Novamente, com dicionários do .NET regulares, Olá código acima funciona bem e é um padrão comum: desenvolvedor Olá usa uma chave toolook um valor.</span><span class="sxs-lookup"><span data-stu-id="65066-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="65066-147">Se houver valor Olá, desenvolvedor Olá altera o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="65066-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="65066-148">No entanto, com coleções confiáveis, este código exibe Olá mesmo problema como já foi abordado: **você não deve modificar um objeto quando você tiver concedido coleção confiável tooa.**</span><span class="sxs-lookup"><span data-stu-id="65066-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="65066-149">Olá correto tooupdate de maneira um valor em uma coleção confiável, é tooget Referência toohello existente e considere objeto Olá chamado tooby essa referência imutável.</span><span class="sxs-lookup"><span data-stu-id="65066-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="65066-150">Em seguida, crie um novo objeto que é uma cópia exata do objeto original hello.</span><span class="sxs-lookup"><span data-stu-id="65066-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="65066-151">Agora, você pode modificar o estado de saudação do novo objeto e insira Olá novo objeto na coleção de saudação para que ele obtém serializado toobyte matrizes, o arquivo local toohello anexado e enviadas toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="65066-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="65066-152">Depois de confirmar Olá alteração (ões), objetos na memória de hello, arquivo de local de Olá, e todas as réplicas de saudação têm Olá mesmo estado.</span><span class="sxs-lookup"><span data-stu-id="65066-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="65066-153">Parece que está tudo bem.</span><span class="sxs-lookup"><span data-stu-id="65066-153">All is good!</span></span>

<span data-ttu-id="65066-154">código de saudação abaixo mostra tooupdate de maneira correta de saudação um valor em uma coleção confiável:</span><span class="sxs-lookup"><span data-stu-id="65066-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="65066-155">Definir o erro do programador de tooprevent de tipos de dados imutáveis</span><span class="sxs-lookup"><span data-stu-id="65066-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="65066-156">Idealmente, gostaríamos erros de tooreport do compilador hello quando você gerar o código que muda o estado de um objeto que você deve tooconsider imutável acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="65066-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="65066-157">Mas, compilador c# Olá não tem Olá capacidade toodo isso.</span><span class="sxs-lookup"><span data-stu-id="65066-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="65066-158">Portanto, tooavoid possíveis programador bugs, é altamente recomendável que você defina tipos Olá que você usa com coleções confiável toobe imutável tipos.</span><span class="sxs-lookup"><span data-stu-id="65066-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="65066-159">Especificamente, isso significa que você fique toocore tipos de valor (como números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan e hello como).</span><span class="sxs-lookup"><span data-stu-id="65066-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="65066-160">E, claro, você também pode usar String.</span><span class="sxs-lookup"><span data-stu-id="65066-160">And, of course, you can also use String.</span></span> <span data-ttu-id="65066-161">É melhor propriedades de coleção tooavoid como a serialização e desserialização pode frequentemente pode prejudicar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="65066-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="65066-162">No entanto, se você quiser toouse propriedades de coleção, é altamente recomendável usar saudação do. Biblioteca de coleções imutáveis do NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="65066-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="65066-163">Essa biblioteca está disponível para download em http://nuget.org. Também recomendamos lacrar suas classes e tornar os campos somente leitura sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="65066-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="65066-164">Olá UserInfo tipo abaixo demonstra como toodefine um imutável digite aproveitando as vantagens de recomendações mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="65066-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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

<span data-ttu-id="65066-165">Olá ItemId tipo também é um tipo imutável, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="65066-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="65066-166">Controle de versão do esquema (atualizações)</span><span class="sxs-lookup"><span data-stu-id="65066-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="65066-167">Internamente, as Reliable Collections serializam os objetos usando o DataContractSerializer do .NET.</span><span class="sxs-lookup"><span data-stu-id="65066-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="65066-168">objetos serializado de saudação são disco local da réplica primária toohello persistente e também são transmitido toohello réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="65066-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="65066-169">Como seu serviço amadurece, é provável que convém toochange tipo de saudação de dados (esquema) requer que seu serviço.</span><span class="sxs-lookup"><span data-stu-id="65066-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="65066-170">Você deve abordar o controle de versão dos seus dados com muito cuidado.</span><span class="sxs-lookup"><span data-stu-id="65066-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="65066-171">Primeiramente, você sempre deve ser capaz de toodeserialize os dados antigos.</span><span class="sxs-lookup"><span data-stu-id="65066-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="65066-172">Especificamente, isso significa que seu código de desserialização deve ser compatível com versões anteriores infinitamente: 333 de versão do seu código de serviço deve ser capaz de toooperate em dados colocados em uma coleção confiável versão 1 do seu código de serviço cinco anos.</span><span class="sxs-lookup"><span data-stu-id="65066-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="65066-173">Além disso, o código de serviço é atualizado em um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="65066-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="65066-174">Assim, durante uma atualização, você tem duas versões diferentes do seu código de serviço em execução simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="65066-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="65066-175">Você deve evitar a nova versão saudação do seu código de serviço usam Olá novo esquema, como as versões antigas do seu código de serviço podem não ser o novo esquema de toohandle capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="65066-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="65066-176">Quando possível, você deve projetar cada versão do seu serviço toobe compatível com a 1 versão.</span><span class="sxs-lookup"><span data-stu-id="65066-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="65066-177">Especificamente, isso significa que V1 do seu código de serviço deve ser capaz de toosimply ignorar quaisquer elementos de esquema não tratar explicitamente.</span><span class="sxs-lookup"><span data-stu-id="65066-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="65066-178">No entanto, ele deve ser capaz de toosave quaisquer dados, ela não conhece explicitamente e simplesmente gravá-la de volta ao atualizar um valor ou uma chave de dicionário.</span><span class="sxs-lookup"><span data-stu-id="65066-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="65066-179">Enquanto você pode modificar o esquema de saudação de uma chave, você deve garantir que o código de hash da chave e algoritmos de equals são estáveis.</span><span class="sxs-lookup"><span data-stu-id="65066-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="65066-180">Se você alterar como qualquer um desses algoritmos funcionam, não será capaz de toolook chave Olá no dicionário confiável Olá nunca novamente.</span><span class="sxs-lookup"><span data-stu-id="65066-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="65066-181">Como alternativa, você pode executar o que é geralmente referidos tooas uma fase de 2 a atualização.</span><span class="sxs-lookup"><span data-stu-id="65066-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="65066-182">Com uma atualização de fase 2, atualize seu serviço de V1 tooV2: V2 contém código Olá que sabe como toodeal com nova alteração de esquema hello, mas esse código não é executado.</span><span class="sxs-lookup"><span data-stu-id="65066-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="65066-183">Quando Olá V2 código lê dados V1, ele opera nele e grava dados V1.</span><span class="sxs-lookup"><span data-stu-id="65066-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="65066-184">Em seguida, após a atualização de saudação for concluída em todos os domínios de atualização, alguma forma você pode sinalizar instâncias em execução de V2 toohello que atualização Olá for concluída.</span><span class="sxs-lookup"><span data-stu-id="65066-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="65066-185">(Uma forma toosignal tooroll fora de uma atualização de configuração; isso é o que torna isso uma atualização da fase 2.) Agora, Olá V2 instâncias podem ler dados V1, convertê-la tooV2 dados, operar nele e grave-os como dados V2.</span><span class="sxs-lookup"><span data-stu-id="65066-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="65066-186">Quando outras instâncias de ler dados V2, eles não precisam de tooconvert, eles apenas operar nele e gravar dados V2.</span><span class="sxs-lookup"><span data-stu-id="65066-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65066-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65066-187">Next Steps</span></span>
<span data-ttu-id="65066-188">toolearn sobre a criação de contratos de dados compatível forward, consulte [contratos de dados compatíveis por encaminhamento](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="65066-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="65066-189">práticas recomendadas do toolearn em contratos de dados de controle de versão, consulte [controle de versão de contrato de dados](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="65066-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="65066-190">toolearn como contratos de dados do tooimplement versão tolerantes a falhas, consulte [retornos de chamada de serialização tolerantes à versão](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="65066-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="65066-191">toolearn como tooprovide uma estrutura de dados que pode interoperar em várias versões, consulte [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="65066-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
