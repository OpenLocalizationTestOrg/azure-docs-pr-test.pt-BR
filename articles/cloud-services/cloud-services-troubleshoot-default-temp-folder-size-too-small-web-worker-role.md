---
title: "O tamanho da pasta TEMP padrão é muito pequeno para uma função | Microsoft Docs"
description: "Uma função de serviço de nuvem tem uma quantidade limitada de espaço para a pasta TEMP. Este artigo fornece algumas sugestões sobre como evitar ficar sem espaço."
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
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="ebcd5-104">O tamanho da pasta TEMP padrão é muito pequeno em uma função de serviço de nuvem Web/trabalho</span><span class="sxs-lookup"><span data-stu-id="ebcd5-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="ebcd5-105">O diretório temporário padrão de uma função de serviço de nuvem Web ou trabalho tem um tamanho máximo de 100 MB, o que pode ficar completo em algum momento.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="ebcd5-106">Este artigo descreve como evitar a falta de espaço para o diretório temporário.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="ebcd5-107">Por que eu fiquei sem espaço?</span><span class="sxs-lookup"><span data-stu-id="ebcd5-107">Why do I run out of space?</span></span>
<span data-ttu-id="ebcd5-108">As variáveis de ambiente TEMP e TMP padrão do Windows estão disponíveis no código em execução em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="ebcd5-109">TEMP e TMP apontam para um único diretório com um tamanho máximo de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="ebcd5-110">Todos os dados armazenados nesse diretório não são persistidos durante o ciclo de vida do serviço de nuvem; se as instâncias de função em um serviço de nuvem forem recicladas, o diretório será limpo.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="ebcd5-111">Sugestão para corrigir o problema</span><span class="sxs-lookup"><span data-stu-id="ebcd5-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="ebcd5-112">Implemente uma das alternativas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebcd5-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="ebcd5-113">Configure um recurso de armazenamento local e acesse-o diretamente, em vez de usar TEMP ou TMP.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="ebcd5-114">Para acessar um recurso de armazenamento local no código em execução dentro de seu aplicativo, chame o método [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ebcd5-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="ebcd5-115">Configure um recurso de armazenamento local e aponte os diretórios TEMP e TMP para apontar para o caminho do recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="ebcd5-116">Essa modificação deve ser executada dentro do método [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ebcd5-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="ebcd5-117">O exemplo de código a seguir mostra como modificar os diretórios de destino para TEMP e TMP de dentro do método OnStart:</span><span class="sxs-lookup"><span data-stu-id="ebcd5-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
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

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ebcd5-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebcd5-118">Next steps</span></span>
<span data-ttu-id="ebcd5-119">Leia um blog que descreve [Como aumentar o tamanho da Pasta Temporária do ASP.NET da Função Web do Azure](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebcd5-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="ebcd5-120">Confira mais [artigos sobre solução de problemas](/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ebcd5-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="ebcd5-121">Para saber como solucionar os problemas das funções do serviço de nuvem usando os dados de diagnóstico do computador Azure PaaS, veja a [série de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebcd5-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
