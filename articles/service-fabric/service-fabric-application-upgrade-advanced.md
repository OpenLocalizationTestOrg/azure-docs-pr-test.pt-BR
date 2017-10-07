---
title: "aaaAdvanced tópicos de atualização de aplicativo | Microsoft Docs"
description: "Este artigo aborda alguns tópicos avançados pertencente tooupgrading um aplicativo de malha do serviço."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="7ea8d-103">Atualização do aplicativo Service Fabric: tópicos avançados</span><span class="sxs-lookup"><span data-stu-id="7ea8d-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="7ea8d-104">Adicionando ou removendo serviços durante uma atualização de aplicativo</span><span class="sxs-lookup"><span data-stu-id="7ea8d-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="7ea8d-105">Se um novo serviço é adicionado aplicativo tooan que já está implantado e publicado como uma atualização, o novo serviço de saudação é aplicativo adicionado toohello implantado.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="7ea8d-106">Essa atualização não afeta nenhum dos serviços de saudação que já fazem parte do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="7ea8d-107">No entanto, uma instância do serviço de saudação que foi adicionado deve ser iniciada para Olá novo serviço toobe active (usando Olá `New-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="7ea8d-108">Os serviços também podem ser removidos de um aplicativo como parte de uma atualização.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="7ea8d-109">No entanto, todas as instâncias do serviço de ser excluído Olá devem ser interrompidas antes de prosseguir com a atualização da saudação (usando Olá `Remove-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="7ea8d-110">Modo de atualização manual</span><span class="sxs-lookup"><span data-stu-id="7ea8d-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="7ea8d-111">o modo manual não monitorado Olá deve ser considerado somente para uma atualização com falha ou suspensa.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="7ea8d-112">modo monitorado Olá é Olá recomendado o modo de atualização para aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="7ea8d-113">Malha do serviço do Azure fornece vários modos de atualização toosupport clusters de desenvolvimento e produção.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="7ea8d-114">As opções de implantação escolhidas podem ser diferentes para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="7ea8d-115">atualização sem interrupção de aplicativo Hello monitorado é Olá toouse mais comuns de atualização no ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="7ea8d-116">Quando atualizar Olá política for especificada, o Service Fabric garante que o aplicativo hello esteja íntegro antes da atualização Olá continua.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="7ea8d-117">administrador do aplicativo Hello pode usar manual Olá sem interrupção aplicativo modo de atualização toohave total controle sobre o progresso da atualização por meio de Olá Olá vários domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="7ea8d-118">Esse modo é útil quando uma política de avaliação de integridade personalizado ou complexa é necessária, ou um processo de atualização não convencional (por exemplo, aplicativo hello já está em perda de dados).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="7ea8d-119">Por fim, hello automatizada atualização sem interrupção do aplicativo é útil para desenvolvimento ou tooprovide de ambientes de teste durante o desenvolvimento de serviços de ciclo de uma iteração rápida.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="7ea8d-120">Alterar o modo de atualização de toomanual</span><span class="sxs-lookup"><span data-stu-id="7ea8d-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="7ea8d-121">**Manual**-atualização do aplicativo de saudação parada no Olá atual UD e alteração Olá atualizar tooUnmonitored de modo Manual.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="7ea8d-122">Olá administrador precisa de chamada de toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed com hello atualizar ou disparar uma reversão, iniciando uma nova atualização.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="7ea8d-123">Depois que a atualização de saudação entra no modo Manual Olá, ela permanece no modo Manual Olá até que uma nova atualização é iniciada.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="7ea8d-124">Olá **GetApplicationUpgradeProgressAsync** comando retorna a MALHA\_aplicativo\_atualização\_estado\_sem interrupção\_FORWARD\_pendente.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="7ea8d-125">Atualizar usando um pacote diff</span><span class="sxs-lookup"><span data-stu-id="7ea8d-125">Upgrade with a diff package</span></span>
<span data-ttu-id="7ea8d-126">Um aplicativo Malha do Serviço pode ser atualizado pelo provisionamento com um pacote de aplicativo completo e independente.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="7ea8d-127">Um aplicativo também pode ser atualizado usando um pacote de comparação que contém apenas arquivos de aplicativo hello atualizado, Olá atualizada manifesto de aplicativo e arquivos de manifesto de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="7ea8d-128">Um pacote de aplicativo completo contém todos os toostart necessários arquivos de saudação e executa um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="7ea8d-129">Um pacote de comparação contém apenas os arquivos de saudação alterado entre provisionar última hello e atualização atual hello, além de arquivos de manifesto do manifesto de aplicativo completo hello e serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="7ea8d-130">Qualquer referência no manifesto do aplicativo hello ou manifesto de serviço que não pode ser encontrado no layout de compilação Olá é procurada no repositório de imagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="7ea8d-131">Pacotes de aplicativo completo são necessários para a primeira instalação Olá de um cluster de toohello do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="7ea8d-132">Atualizações subsequentes podem ser um pacote de aplicativo completo ou um pacote diff.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="7ea8d-133">Hipóteses em que usar um pacote diff seria uma boa opção:</span><span class="sxs-lookup"><span data-stu-id="7ea8d-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="7ea8d-134">Será melhor usar um pacote diff quando você tiver um pacote de aplicativo grande que faça referência a vários arquivos de manifesto do serviço e/ou a vários pacotes de código, de configuração ou de dados.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="7ea8d-135">Um pacote de comparação é preferível quando você tiver um sistema de implantação que gera o layout de compilação Olá diretamente de seu processo de compilação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="7ea8d-136">Nesse caso, mesmo que o código de saudação não for alterado, assemblies recém-criado obtém uma soma de verificação diferente.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="7ea8d-137">Usar um pacote de aplicativo completo exigiria que você tooupdate Olá versão de todos os pacotes de código.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="7ea8d-138">Usando um pacote de comparação, você fornece somente arquivos de Olá que foram alteradas e arquivos de manifesto Olá em que a versão de saudação foi alterada.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="7ea8d-139">Quando um aplicativo é atualizado usando o Visual Studio, o pacote de comparação de saudação é publicado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="7ea8d-140">toocreate um pacote de comparação Olá manualmente, o manifesto de aplicativo e Olá manifestos do serviço devem ser atualizados, mas Olá alterado apenas os pacotes devem ser incluídos no pacote de aplicativo final hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="7ea8d-141">Por exemplo, vamos começar com hello (números de versão fornecidos para facilitar a compreensão) do aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ea8d-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="7ea8d-142">Agora, vamos supor que você desejava tooupdate somente Olá pacote de códigos de service1 usando um pacote de comparação usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="7ea8d-143">Agora, seu aplicativo atualizado tem Olá estrutura de pasta a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ea8d-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="7ea8d-144">Nesse caso, você atualizar too2.0.0 de manifesto de aplicativo hello e Olá manifesto de serviço para atualização de pacote de código do service1 tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="7ea8d-145">pasta de saudação para seu pacote de aplicativo teria Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ea8d-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="7ea8d-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ea8d-146">Next steps</span></span>
<span data-ttu-id="7ea8d-147">[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="7ea8d-148">[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ea8d-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="7ea8d-149">Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="7ea8d-150">Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="7ea8d-151">Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7ea8d-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
