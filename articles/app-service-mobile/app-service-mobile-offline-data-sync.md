---
title: "aaaOffline sincronização de dados em aplicativos móveis do Azure | Microsoft Docs"
description: "Visão geral do recurso de sincronização de dados offline Olá para aplicativos móveis do Azure e referência conceitual"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Sincronização de dados offline em Aplicativos Móveis do Azure
## <a name="what-is-offline-data-sync"></a>O que é sincronização de dados offline?
Sincronização de dados offline é um cliente e o recurso SDK de aplicativos móveis do Azure que torna mais fácil para os desenvolvedores toocreate aplicativos que são funcionais sem uma conexão de rede do servidor.

Quando o aplicativo estiver no modo offline, você pode criar e modificar dados, que são salvo no repositório local tooa. Quando o aplicativo hello está novamente online, ele possa sincronizar as alterações locais com seu back-end do aplicativo do Azure Mobile. recurso Olá também inclui suporte para a detecção de conflitos quando Olá mesmo registro é alterado em ambos Olá cliente e Olá back-end. Conflitos podem ser tratados no servidor de saudação ou cliente hello.

A sincronização offline proporciona vários benefícios:

* Melhorar a capacidade de resposta do aplicativo armazenando dados localmente no dispositivo de saudação do servidor
* Crie aplicativos robustos que permanecem úteis quando há problemas de rede
* Permitir toocreate de usuários finais e modificar dados, mesmo quando não há nenhum acesso de rede, o suporte a cenários com pouca ou nenhuma conectividade
* Sincronizar dados em vários dispositivos e detectar conflitos quando hello mesmo registro é modificado por dois dispositivos
* Limite o uso de rede em redes de alta latência ou monitoradas

Olá tutoriais a seguir mostra como a sincronização offline tooadd tooyour clientes móveis usando aplicativos móveis do Azure:

* [Android: Habilitar a sincronização offline]
* [Apache Cordova: habilitar sincronização offline](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: Habilitar a sincronização offline]
* [Xamarin iOS: Habilitar a sincronização offline]
* [Xamarin Android: Habilitar a sincronização offline]
* [Xamarin.Forms: habilitar a sincronização offline](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [Plataforma Universal do Windows: habilitar a sincronização offline]

## <a name="what-is-a-sync-table"></a>O que é uma tabela de sincronização?
Olá tooaccess "/ tabelas" ponto de extremidade de cliente do Azure Mobile Olá SDKs fornecem interfaces como `IMobileServiceTable` (SDK de cliente .NET) ou `MSTable` (cliente do iOS). Essas APIs se conectar diretamente de back-end de aplicativo do Azure Mobile toohello e falharem se o dispositivo de saudação do cliente não tem uma conexão de rede.

uso off-line de toosupport, seu aplicativo deve usar Olá *tabela sincronização* APIs, como `IMobileServiceSyncTable` (SDK de cliente .NET) ou `MSSyncTable` (cliente do iOS). Olá todas as mesmas operações CRUD (criar, ler, atualizar, excluir) funcionam em sincronização APIs de tabela, exceto agora eles leiam ou gravar tooa *repositório local*. Antes de quaisquer operações de tabela de sincronização podem ser executadas, armazenamento local Olá deve ser inicializado.

## <a name="what-is-a-local-store"></a>O que é um armazenamento local?
Um repositório local é a camada de persistência de dados Olá no dispositivo de cliente hello. implementação do repositório de cliente de aplicativos do Azure Mobile Olá SDKs fornecem um padrão local. No Windows, Xamarin e Android, ele se baseia em SQLite. No iOS, ele se baseia em Core Data.

toouse Olá SQLite implementação baseada no Windows Phone ou da Windows Store 8.1, você precisa tooinstall uma extensão do SQLite. Para obter mais detalhes, veja [Plataforma Universal do Windows: habilitar a sincronização offline]. Android e iOS fornecidos com uma versão do SQLite no dispositivo Olá sistema operacional em si, portanto, não é necessário tooreference sua própria versão do SQLite.

Os desenvolvedores também podem implementar seu próprio armazenamento local. Por exemplo, se você quiser toostore dados em um formato criptografado no cliente móvel Olá, você pode definir um local de armazenamento usa SQLCipher para criptografia.

## <a name="what-is-a-sync-context"></a>O que é um contexto de sincronização?
Um *contexto de sincronização* é associado a um objeto de cliente móvel (como `IMobileServiceClient` ou `MSClient`) e rastreia as alterações que são feitas com tabelas de sincronização. contexto de sincronização Olá mantém um *fila de operação*, que mantém uma lista ordenada de operações CUD (Create, Update, Delete) que for posteriormente enviado toohello server.

Um repositório local está associado com o contexto de sincronização hello usando um método de inicialização como `IMobileServicesSyncContext.InitializeAsync(localstore)` em Olá [cliente .NET SDK].

## <a name="how-sync-works"></a>Como a sincronização offline funciona
Ao usar tabelas de sincronização, o código do cliente controla quando as alterações locais são sincronizadas com um back-end do aplicativo móvel do Azure. Nenhuma informação será enviada toohello back-end até que haja uma chamada muito*push* alterações locais. Da mesma forma, repositório local Olá é preenchido com os novos dados somente quando há uma chamada muito*pull* dados.

* **Push**: Push é uma operação no contexto de sincronização hello e envia todas as alterações CUD desde push última hello. Observe que ele é toosend não é possível somente alterações de uma tabela individual, pois caso contrário, as operações podem ser enviadas fora de ordem. Push executa uma série de REST chamadas tooyour aplicativo do Azure móvel back-end, que por sua vez modifica seu banco de dados do servidor.
* **Pull**: Pull é executado em uma base por tabela e pode ser personalizado com uma consulta tooretrieve apenas um subconjunto de dados do servidor de saudação. Olá cliente do Azure Mobile SDKs e insira dados resultantes Olá no repositório local hello.
* **Envios implícita**: se uma recepção é executada em uma tabela que tem as atualizações locais pendentes, pull Olá primeiro executa um `push()` no contexto de sincronização de saudação. Essa ação ajuda a minimizar conflitos entre as alterações que já estão na fila e novos dados do servidor de saudação.
* **Sincronização incremental**: operação de recepção de toohello do hello primeiro parâmetro é um *nome da consulta* que é usado somente no cliente de saudação. Se você usar um nome de consulta não nulo, Olá SDK do Azure Mobile executa um *sincronização incremental*. Cada vez que uma operação de recepção retorna um conjunto de resultados, Olá mais recente `updatedAt` carimbo de hora em que conjunto de resultados é armazenado em tabelas de sistema local do SDK de saudação. As operações de pull subsequentes recuperarão somente registros após esse carimbo de data/hora.

  toouse a sincronização incremental, o servidor deve retornar significativo `updatedAt` valores e também deve oferecer suporte a classificação por este campo. No entanto, como Olá SDK adiciona seu próprio classificação no campo de updatedAt hello, você não pode usar uma consulta de pull tem seu próprio `orderBy` cláusula.

  nome da consulta Olá pode ser qualquer cadeia de caracteres que você escolher, mas ele deve ser exclusivo para cada consulta lógica em seu aplicativo.
  Caso contrário, as operações de pull diferentes podem substituir Olá mesmo carimbo de hora de sincronização incremental e as consultas podem retornar resultados incorretos.

  Se a consulta Olá tem um parâmetro, uma maneira toocreate um nome exclusivo de consulta é o valor do parâmetro de Olá de tooincorporate.
  Por exemplo, se você estiver filtrando userid, o nome da consulta pode ser da seguinte maneira (em C#):

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Se você quiser tooopt fora de sincronização incremental, passar `null` como Olá ID da consulta. Nesse caso, todos os registros são recuperados em cada chamada muito`PullAsync`, que é potencialmente ineficiente.
* **Limpando**: você pode limpar o conteúdo de saudação do uso do armazenamento local de saudação `IMobileServiceSyncTable.PurgeAsync`.
  Limpeza pode ser necessário se você tiver dados obsoletos no banco de dados de cliente hello, ou se desejar toodiscard todas as alterações pendentes.

  Uma limpeza desmarca uma tabela de armazenamento local hello. Se não houver operações aguardando a sincronização com o banco de dados de servidor de saudação, Olá limpeza lançará uma exceção, a menos que Olá *forçar limpeza* parâmetro está definido.

  Como um exemplo de dados obsoletos no cliente Olá, vamos supor que no exemplo de "lista de tarefas" Olá, Device1 recebe apenas os itens que não foram concluídos. Um todoitem "Comprar leite" está marcado como concluído no servidor de saudação por outro dispositivo. No entanto, Device1 ainda tem hello "Comprar leite" todoitem no repositório local porque ele está recebendo somente itens que não estão marcadas como concluída. Uma limpeza limpa esse item obsoleto.

## <a name="next-steps"></a>Próximas etapas
* [iOS: Habilitar a sincronização offline]
* [Xamarin iOS: Habilitar a sincronização offline]
* [Xamarin Android: Habilitar a sincronização offline]
* [Plataforma Universal do Windows: habilitar a sincronização offline]

<!-- Links -->
[cliente .NET SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: Habilitar a sincronização offline]: app-service-mobile-android-get-started-offline-data.md
[iOS: Habilitar a sincronização offline]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: Habilitar a sincronização offline]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: Habilitar a sincronização offline]: app-service-mobile-xamarin-android-get-started-offline-data.md
[Plataforma Universal do Windows: habilitar a sincronização offline]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
