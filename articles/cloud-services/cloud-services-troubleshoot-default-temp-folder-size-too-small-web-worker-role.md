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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="fc068-104">O tamanho da pasta TEMP padrão é muito pequeno em uma função de serviço de nuvem Web/trabalho</span><span class="sxs-lookup"><span data-stu-id="fc068-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="fc068-105">Olá padrão para o diretório temporário de uma função de trabalho ou da web do serviço de nuvem tem um tamanho máximo de 100 MB, o que pode se tornar completo em algum momento.</span><span class="sxs-lookup"><span data-stu-id="fc068-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="fc068-106">Este artigo descreve como tooavoid ficando sem espaço para o diretório temporário hello.</span><span class="sxs-lookup"><span data-stu-id="fc068-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="fc068-107">Por que eu fiquei sem espaço?</span><span class="sxs-lookup"><span data-stu-id="fc068-107">Why do I run out of space?</span></span>
<span data-ttu-id="fc068-108">saudação padrão Windows variáveis de ambiente TEMP e TMP são toocode disponível que está em execução em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc068-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="fc068-109">TEMP e TMP tooa ponto único diretório que tem um tamanho máximo de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="fc068-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="fc068-110">Todos os dados armazenados nesse diretório não são persistidos durante o ciclo de vida Olá Olá do serviço de nuvem; Se as instâncias de função de saudação em um serviço de nuvem forem recicladas, diretório de saudação será limpo.</span><span class="sxs-lookup"><span data-stu-id="fc068-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="fc068-111">Problema de saudação toofix sugestão</span><span class="sxs-lookup"><span data-stu-id="fc068-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="fc068-112">Implemente uma saudação alternativas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc068-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="fc068-113">Configure um recurso de armazenamento local e acesse-o diretamente, em vez de usar TEMP ou TMP.</span><span class="sxs-lookup"><span data-stu-id="fc068-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="fc068-114">um recurso de armazenamento local do código que está sendo executado em seu aplicativo, a saudação da chamada de tooaccess [Getlocalresource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="fc068-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="fc068-115">Configurar um recurso de armazenamento local e, em seguida, aponte hello TEMP e TMP diretórios toopoint toohello caminho Olá local do recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc068-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="fc068-116">Essa modificação deve ser executada no hello [RoleEntryPoint](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="fc068-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="fc068-117">Olá exemplo de código a seguir mostra como toomodify Olá diretórios de destino para TEMP e TMP no método OnStart de saudação:</span><span class="sxs-lookup"><span data-stu-id="fc068-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fc068-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc068-118">Next steps</span></span>
<span data-ttu-id="fc068-119">Leia um blog que descreve [como tooincrease Olá tamanho de saudação pasta temporária do Azure Web função ASP.NET](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc068-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="fc068-120">Confira mais [artigos sobre solução de problemas](/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="fc068-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="fc068-121">toolearn como função de serviço de nuvem tootroubleshoot problemas usando dados de diagnóstico do computador de PaaS do Azure, exibir [série do blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc068-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
