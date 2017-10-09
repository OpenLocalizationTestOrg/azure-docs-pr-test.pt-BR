---
title: "eventos de ciclo de vida do serviço de nuvem aaaHandle | Microsoft Docs"
description: "Saiba como métodos de ciclo de vida de saudação de uma função de serviço de nuvem podem ser usados no .NET"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Personalizar a saudação do ciclo de vida de uma função Web ou de trabalho no .NET
Quando você cria uma função de trabalho, você estende Olá [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe que fornece métodos para você toooverride que permitem a você responder a eventos de toolifecycle. Para funções web essa classe é opcional, portanto, você deve usar toorespond toolifecycle eventos.

## <a name="extend-hello-roleentrypoint-class"></a>Estender a classe RoleEntryPoint de saudação
Olá [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe inclui métodos que são chamados pelo Azure quando ele **inicia**, **executa**, ou **interrompe** uma função web ou de trabalho. Opcionalmente, você pode substituir esses métodos toomanage função inicialização, as sequências de desligamento de função ou thread de execução de saudação da função hello. 

Ao estender **RoleEntryPoint**, você deve estar atento a saudação comportamentos dos métodos Olá a seguir:

* Olá [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) e [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) métodos retornam um valor booliano, portanto, é possível tooreturn **false** entre esses métodos.
  
   Se seu código retorna **false**, o processo de saudação da função será finalizado abruptamente, sem executar nenhuma sequência de desligamento, você pode ter em vigor. Em geral, evite retornar **false** de saudação **OnStart** método.
* Qualquer exceção não capturada em uma sobrecarga de um método **RoleEntryPoint** será tratada como uma exceção sem tratamento.
  
   Se uma exceção ocorrer dentro de um dos métodos de ciclo de vida de saudação, o Azure aumentará Olá [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) evento, e, em seguida, o processo de saudação é encerrado. Depois que sua função ficar offline, ela será reiniciada pelo Azure. Quando uma exceção não tratada ocorre, hello [parando](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) evento não será gerado e Olá **OnStop** método não for chamado.

Se sua função não for iniciado ou estiver Reciclando entre hello inicializando, ocupados e parando estados, seu código poderá estar lançando uma exceção sem tratamento dentro de um dos eventos de ciclo de vida Olá que reinicia cada função de saudação do tempo. Nesse caso, use Olá [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) evento toodetermine Olá causa da exceção hello e manipulá-lo adequadamente. Sua função também pode estar retornando do hello [executar](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, o que faz com que o hello função toorestart. Para obter mais informações sobre estados de implantação, consulte [tooRecycle problemas que causa funções comuns](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Se você estiver usando Olá **ferramentas do Azure para Microsoft Visual Studio** toodevelop seu aplicativo, modelos de projeto de função hello estendem automaticamente Olá **RoleEntryPoint** classe para você, no hello *WebRole.cs* e *WorkerRole.cs* arquivos.
> 
> 

## <a name="onstart-method"></a>Método OnStart
Olá **OnStart** método é chamado quando sua instância de função é trazida online pelo Azure. Durante a execução de saudação código OnStart, instância de função hello está marcada como **ocupado** e nenhum tráfego externo será direcionado tooit pelo Balanceador de carga de saudação. Você pode substituir o trabalho de inicialização de tooperform esse método, como implementar manipuladores de eventos e iniciar [diagnóstico do Azure](cloud-services-how-to-monitor.md).

Se **OnStart** retorna **true**, instância de saudação é inicializada com êxito e o Azure chamará Olá **RoleEntryPoint** método. Se **OnStart** retorna **false**, função hello encerra imediatamente, sem executar quaisquer sequências de desligamento planejado.

Olá mostra exemplo de código a seguir como Olá toooverride **OnStart** método. Este método configura e inicia um monitor de diagnóstico quando a instância de função hello inicia e define uma transferência de conta de armazenamento tooa dados de log:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>Método OnStop
Olá **OnStop** método é chamado depois que uma instância de função foi colocada offline pelo Azure e antes de sair do processo de saudação. Você pode substituir esse código de toocall método necessário para sua toocleanly de instância de função desligar.

> [!IMPORTANT]
> Código em execução no hello **OnStop** método tem um tempo limitado toofinish quando ele é chamado para razões diferentes de um desligamento iniciado pelo usuário. Depois que essa hora decorre, processo Olá é finalizado e, portanto você deve garantir que o código no hello **OnStop** método pode ser executado rapidamente ou tolerar toocompletion não está em execução. Olá **OnStop** método é chamado após Olá **parando** é gerado.
> 
> 

## <a name="run-method"></a>Método Run
Você pode substituir Olá **executar** método tooimplement um thread de execução longa para sua instância de função.

Substituindo Olá **executar** método não é necessário; a implementação do padrão de saudação inicia um thread que está sempre em suspensão. Se você substituir Olá **executar** método, seu código deve ser bloqueado indefinidamente. Se hello **executar** método retorna, Olá função será reciclada automaticamente normalmente; em outras palavras, o Azure gera Olá **parando** Olá eventos e chamadas **OnStop** método para que as sequências de desligamento podem ser executadas antes da função hello é colocada offline.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Implementação de métodos de ciclo de vida do ASP.NET Olá para uma função web
Você pode usar métodos de ciclo de vida do ASP.NET hello, além disso toothose fornecido pelo Olá **RoleEntryPoint** classe toomanage sequências de inicialização e desligamento para uma função web. Isso pode ser útil para fins de compatibilidade se você estiver portando um tooAzure de aplicativo ASP.NET existente. métodos de ciclo de vida do ASP.NET Olá são chamados de dentro de saudação **RoleEntryPoint** métodos. Olá **aplicativo\_iniciar** método é chamado após Olá **RoleEntryPoint** conclusão do método. Olá **aplicativo\_final** método é chamado antes de saudação **RoleEntryPoint** método é chamado.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[criar um pacote de serviço de nuvem](cloud-services-model-and-package.md).

