---
title: "tamanho da pasta TEMP aaaDefault é muito pequeno para uma função | Microsoft Docs"
description: "Uma função de serviço de nuvem tem uma quantidade limitada de espaço para a pasta TEMP de saudação. Este artigo fornece algumas sugestões sobre como tooavoid ficando sem espaço."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>O tamanho da pasta TEMP padrão é muito pequeno em uma função de serviço de nuvem Web/trabalho
Olá padrão para o diretório temporário de uma função de trabalho ou da web do serviço de nuvem tem um tamanho máximo de 100 MB, o que pode se tornar completo em algum momento. Este artigo descreve como tooavoid ficando sem espaço para o diretório temporário hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Por que eu fiquei sem espaço?
saudação padrão Windows variáveis de ambiente TEMP e TMP são toocode disponível que está em execução em seu aplicativo. TEMP e TMP tooa ponto único diretório que tem um tamanho máximo de 100 MB. Todos os dados armazenados nesse diretório não são persistidos durante o ciclo de vida Olá Olá do serviço de nuvem; Se as instâncias de função de saudação em um serviço de nuvem forem recicladas, diretório de saudação será limpo.

## <a name="suggestion-toofix-hello-problem"></a>Problema de saudação toofix sugestão
Implemente uma saudação alternativas a seguir:

* Configure um recurso de armazenamento local e acesse-o diretamente, em vez de usar TEMP ou TMP. um recurso de armazenamento local do código que está sendo executado em seu aplicativo, a saudação da chamada de tooaccess [Getlocalresource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.
* Configurar um recurso de armazenamento local e, em seguida, aponte hello TEMP e TMP diretórios toopoint toohello caminho Olá local do recurso de armazenamento. Essa modificação deve ser executada no hello [RoleEntryPoint](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.

Olá exemplo de código a seguir mostra como toomodify Olá diretórios de destino para TEMP e TMP no método OnStart de saudação:

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a>Próximas etapas
Leia um blog que descreve [como tooincrease Olá tamanho de saudação pasta temporária do Azure Web função ASP.NET](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Confira mais [artigos sobre solução de problemas](/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.

toolearn como função de serviço de nuvem tootroubleshoot problemas usando dados de diagnóstico do computador de PaaS do Azure, exibir [série do blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
