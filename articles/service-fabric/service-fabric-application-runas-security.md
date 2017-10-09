---
title: "aaaLearn sobre as políticas de segurança do Azure microservices | Microsoft Docs"
description: "Uma visão geral de como toorun um aplicativo de malha do serviço no sistema e as contas de segurança local, incluindo Olá SetupEntry ponto em que um aplicativo precisa tooperform alguns privilegiado ação antes de começar"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="d8e41-103">Configurar políticas de segurança para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8e41-103">Configure security policies for your application</span></span>
<span data-ttu-id="d8e41-104">Usando o Service Fabric do Azure, você pode proteger os aplicativos em execução no cluster de saudação em diferentes contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="d8e41-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="d8e41-105">Serviço de malha também ajuda a certificados, arquivos, diretórios e recursos de saudação seguro que são usados por aplicativos em tempo de saudação da implantação em contas de usuário hello – por exemplo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="d8e41-106">Isso torna os aplicativos em execução, mesmo em um ambiente hospedado compartilhado, mais protegidos uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="d8e41-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="d8e41-107">Por padrão, os aplicativos do Service Fabric são executados sob conta Olá Olá Fabric.exe processo é executado.</span><span class="sxs-lookup"><span data-stu-id="d8e41-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="d8e41-108">Serviço de malha também fornece a capacidade de saudação toorun aplicativos sob uma conta de usuário local ou a conta sistema local, que é especificada no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="d8e41-109">Os tipos de conta do sistema local com suporte são **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="d8e41-110">Quando você estiver executando do Service Fabric no Windows Server em seu data center usando o instalador autônomo do hello, você pode usar contas de domínio do Active Directory, incluindo contas de serviço gerenciado de grupo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="d8e41-111">Você pode definir e criar grupos de usuários para que um ou mais usuários possam ser adicionados tooeach grupo toobe gerenciado juntos.</span><span class="sxs-lookup"><span data-stu-id="d8e41-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="d8e41-112">Isso é útil quando há vários usuários para os pontos de entrada de serviço diferente e é necessário toohave certos privilégios comuns que estão disponíveis no nível do grupo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="d8e41-113">Configurar política de saudação para um ponto de entrada de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="d8e41-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="d8e41-114">Conforme descrito em Olá [modelo de aplicativo](service-fabric-application-model.md), Olá ponto de entrada de configuração, **SetupEntryPoint**, é um ponto de entrada com privilégios que é executado com hello mesmo credenciais como Service Fabric (normalmente Olá *NetworkService* conta) antes de qualquer outro ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="d8e41-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="d8e41-115">executável de saudação que é especificado pelo **EntryPoint** normalmente é o host de serviço de longa execução hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="d8e41-116">Para ter uma entrada de instalação separado do ponto evita a necessidade de host de serviço Olá toorun executável com altos privilégios por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="d8e41-117">Olá executável que **EntryPoint** especifica é executado após a **SetupEntryPoint** é encerrada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d8e41-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="d8e41-118">Olá processo resultante é monitorado e reiniciado e começa novamente com **SetupEntryPoint** se ele nunca termina ou falha.</span><span class="sxs-lookup"><span data-stu-id="d8e41-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="d8e41-119">a seguir Olá é um exemplo de manifesto de serviço simples que mostra Olá SetupEntryPoint e Olá principal ponto de entrada para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e41-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="d8e41-120">Configurar política de saudação usando uma conta local</span><span class="sxs-lookup"><span data-stu-id="d8e41-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="d8e41-121">Depois de configurar Olá serviço toohave um ponto de entrada de configuração, você pode alterar as permissões de segurança de saudação que ele é executado no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="d8e41-122">saudação de exemplo a seguir mostra como tooconfigure Olá toorun de serviço com privilégios de conta de administrador do usuário.</span><span class="sxs-lookup"><span data-stu-id="d8e41-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="d8e41-123">Primeiro, crie uma seção **Principals** com um nome de usuário SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="d8e41-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="d8e41-124">Isso indica que o usuário Olá é um membro do grupo de sistema de administradores de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e41-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="d8e41-125">Em seguida, em Olá **servicemanifestimport ao** seção, configure uma política tooapply essa entidade muito**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="d8e41-126">Isso informa ao serviço de malha que quando hello **MySetup.bat** arquivo é executado, ele deve ser `RunAs` com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="d8e41-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="d8e41-127">Considerando que você tenha *não* aplicada a um ponto de entrada principal toohello de política, o código de Olá em **MyServiceHost.exe** compatível com o sistema Olá **NetworkService** conta.</span><span class="sxs-lookup"><span data-stu-id="d8e41-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="d8e41-128">Esta é a conta de padrão de saudação que todos os pontos de entrada de serviço são executados como.</span><span class="sxs-lookup"><span data-stu-id="d8e41-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="d8e41-129">Agora, vamos adicionar Olá arquivo MySetup.bat toohello Visual Studio project tootest Olá privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="d8e41-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="d8e41-130">No Visual Studio, clique com botão direito Olá serviço e adicione um novo arquivo chamado MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="d8e41-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="d8e41-131">Em seguida, certifique-se de que arquivo hello MySetup.bat está incluído no pacote de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="d8e41-132">Por padrão, não é.</span><span class="sxs-lookup"><span data-stu-id="d8e41-132">By default, it is not.</span></span> <span data-ttu-id="d8e41-133">Selecione o arquivo hello, tooget Olá contexto menu de atalho e escolha **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="d8e41-134">Na caixa de diálogo de propriedades de saudação, certifique-se de que **copiar tooOutput diretório** está definido muito**copiar se mais recente**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="d8e41-135">Consulte Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8e41-135">See hello following screenshot.</span></span>

![CopyToOutput do Visual Studio para o arquivo em lotes SetupEntryPoint][image1]

<span data-ttu-id="d8e41-137">Agora, abrir o arquivo de MySetup.bat hello e adicione Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8e41-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="d8e41-138">Em seguida, criar e implantar o cluster de desenvolvimento local Olá solução tooa.</span><span class="sxs-lookup"><span data-stu-id="d8e41-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="d8e41-139">Depois que o serviço Olá foi iniciado, conforme mostrado no Gerenciador do Service Fabric, você pode ver que arquivo hello MySetup.bat foi bem-sucedida de um duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="d8e41-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="d8e41-140">Abra um prompt de comando do PowerShell e digite:</span><span class="sxs-lookup"><span data-stu-id="d8e41-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="d8e41-141">Anote o nome Olá Olá nó onde o serviço Olá foi implantado e iniciado no Gerenciador do Service Fabric – por exemplo, nó 2.</span><span class="sxs-lookup"><span data-stu-id="d8e41-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="d8e41-142">Em seguida, navegue toohello instância trabalho pasta toofind Olá out.txt arquivo do aplicativo que mostra o valor de saudação do **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="d8e41-143">Por exemplo, se esse serviço foi implantado tooNode 2, em seguida, você pode ir toothis caminho Olá **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="d8e41-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="d8e41-144">Configurar política de saudação usando contas locais do sistema</span><span class="sxs-lookup"><span data-stu-id="d8e41-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="d8e41-145">Geralmente, é preferível toorun script de inicialização de saudação usando uma conta sistema local em vez de uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="d8e41-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="d8e41-146">Execução da política de RunAs hello como um membro da saudação grupo administradores geralmente não funciona bem como máquinas têm controle de acesso da usuário (UAC) habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d8e41-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="d8e41-147">Nesses casos, **Olá recomenda Olá toorun SetupEntryPoint como LocalSystem, em vez de como um grupo de usuário local adicionado tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="d8e41-148">Olá exemplo a seguir mostra configuração Olá SetupEntryPoint toorun como LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="d8e41-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="d8e41-149">Iniciar comandos do PowerShell em um ponto de entrada de instalação</span><span class="sxs-lookup"><span data-stu-id="d8e41-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="d8e41-150">toorun PowerShell de saudação **SetupEntryPoint** ponto, você pode executar **PowerShell.exe** um arquivo em lotes que aponta tooa PowerShell de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="d8e41-151">Primeiro, adicione um projeto de serviço do PowerShell arquivo toohello – por exemplo, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="d8e41-152">Lembre-se de saudação tooset *copiar se mais recente* propriedade para esse arquivo hello também está incluído no pacote de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="d8e41-153">Olá, exemplo a seguir mostra um arquivo em lotes de exemplo que inicia um arquivo PowerShell chamado MySetup.ps1, que define uma variável de ambiente do sistema chamada **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="d8e41-154">MySetup.bat toostart um arquivo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d8e41-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="d8e41-155">No arquivo de PowerShell Olá, adicione Olá tooset uma variável de ambiente do sistema a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8e41-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="d8e41-156">Por padrão, quando o arquivo em lotes de saudação é executado, parece em pasta do aplicativo hello chamada **trabalhar** para arquivos.</span><span class="sxs-lookup"><span data-stu-id="d8e41-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="d8e41-157">Nesse caso, quando MySetup.bat é executado, queremos que este Olá toofind MySetup.ps1 arquivo hello mesmo pasta, que é o aplicativo hello **pacote de códigos** pasta.</span><span class="sxs-lookup"><span data-stu-id="d8e41-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="d8e41-158">toochange essa pasta, a pasta de trabalho de saudação do conjunto:</span><span class="sxs-lookup"><span data-stu-id="d8e41-158">toochange this folder, set hello working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="d8e41-159">Use o redirecionamento de console para depuração local</span><span class="sxs-lookup"><span data-stu-id="d8e41-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="d8e41-160">Ocasionalmente, é útil toosee saída do console de saudação da execução de um script para fins de depuração.</span><span class="sxs-lookup"><span data-stu-id="d8e41-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="d8e41-161">toodo isso, você pode definir uma política de redirecionamento de console, que grava o arquivo de tooa Olá saída.</span><span class="sxs-lookup"><span data-stu-id="d8e41-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="d8e41-162">Olá arquivo de saída é chamada de pasta de aplicativo escrita toohello **log** no nó Olá onde o aplicativo hello é implantado e executado.</span><span class="sxs-lookup"><span data-stu-id="d8e41-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="d8e41-163">(Consulte onde toofind isso em Olá anterior exemplo.)</span><span class="sxs-lookup"><span data-stu-id="d8e41-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="d8e41-164">Nunca use a política de redirecionamento do console de saudação em um aplicativo que é implantado na produção, pois isso pode afetar o failover de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="d8e41-165">*Só* use isso para fins de depuração e de desenvolvimento locais.</span><span class="sxs-lookup"><span data-stu-id="d8e41-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="d8e41-166">Olá, exemplo a seguir mostra redirecionamento de console de saudação de configuração com um valor de FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="d8e41-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="d8e41-167">Se você alterar Olá MySetup.ps1 arquivo toowrite um **Echo** de comando, isso gravará toohello o arquivo de saída para fins de depuração:</span><span class="sxs-lookup"><span data-stu-id="d8e41-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="d8e41-168">**Depois de depurar seu script, remova imediatamente a política de redirecionamento de console**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="d8e41-169">Configurar uma política para pacotes de código de serviço</span><span class="sxs-lookup"><span data-stu-id="d8e41-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="d8e41-170">Olá etapas anteriores, você viu como tooapply uma tooSetupEntryPoint de política de RunAs.</span><span class="sxs-lookup"><span data-stu-id="d8e41-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="d8e41-171">Vamos examinar um pouco mais como toocreate entidades diferentes que podem ser aplicadas ao serviço políticas.</span><span class="sxs-lookup"><span data-stu-id="d8e41-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="d8e41-172">Criar grupos de usuários locais</span><span class="sxs-lookup"><span data-stu-id="d8e41-172">Create local user groups</span></span>
<span data-ttu-id="d8e41-173">Você pode definir e criar grupos de usuários que permite que um ou mais toobe de usuários adicionados tooa grupo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="d8e41-174">Isso é útil se houver vários usuários para os pontos de entrada de serviço diferente e precisam toohave certos privilégios comuns que estão disponíveis no nível do grupo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="d8e41-175">Olá, exemplo a seguir mostra um grupo local chamado **LocalAdminGroup** que tenha privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="d8e41-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="d8e41-176">Dois usuários, Customer1 e Customer2, tornam-se membros desse grupo local.</span><span class="sxs-lookup"><span data-stu-id="d8e41-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="d8e41-177">Criar usuários locais</span><span class="sxs-lookup"><span data-stu-id="d8e41-177">Create local users</span></span>
<span data-ttu-id="d8e41-178">Você pode criar um serviço de aplicativo hello para um usuário local que pode ser usado toohelp segura.</span><span class="sxs-lookup"><span data-stu-id="d8e41-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="d8e41-179">Quando um **UsuárioLocal** tipo de conta é especificado na seção de entidades de Olá Olá do manifesto do aplicativo, o Service Fabric cria contas de usuário local em computadores em que o aplicativo hello é implantado.</span><span class="sxs-lookup"><span data-stu-id="d8e41-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="d8e41-180">Por padrão, essas contas não têm Olá mesmos nomes que as especificadas no aplicativo hello manifesto (por exemplo, Customer3 em Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="d8e41-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="d8e41-181">Em vez disso, eles são gerados dinamicamente e têm senhas aleatórias.</span><span class="sxs-lookup"><span data-stu-id="d8e41-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="d8e41-182">Se um aplicativo requer que Olá conta de usuário e senha ser a mesma em todos os computadores (por exemplo, autenticação de NTLM tooenable), o manifesto do cluster Olá deve definir NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="d8e41-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="d8e41-183">Olá manifesto do cluster também deve especificar um NTLMAuthenticationPasswordSecret usado toogenerate Olá a mesma senha em todas as máquinas.</span><span class="sxs-lookup"><span data-stu-id="d8e41-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="d8e41-184">Atribuir políticas toohello pacotes de código de serviço</span><span class="sxs-lookup"><span data-stu-id="d8e41-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="d8e41-185">Olá **RunAsPolicy** seção um **servicemanifestimport ao** Especifica a conta de saudação da seção de entidades de saudação que deve ser usado toorun um pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="d8e41-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="d8e41-186">Ele também associa o código de pacotes de serviço Olá manifesto com contas de usuário na seção de entidades de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e41-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="d8e41-187">Você pode especificar isso para instalação hello ou pontos de entrada principal, ou você pode especificar `All` tooapply-tooboth.</span><span class="sxs-lookup"><span data-stu-id="d8e41-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="d8e41-188">Olá, exemplo a seguir mostra políticas diferentes aplicadas:</span><span class="sxs-lookup"><span data-stu-id="d8e41-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="d8e41-189">Se **EntryPointType** não for especificado, o padrão de saudação será definido tooEntryPointType = "Principal".</span><span class="sxs-lookup"><span data-stu-id="d8e41-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="d8e41-190">Especificando **SetupEntryPoint** é especialmente útil quando você deseja toorun determinadas operações de instalação com alto privilégio em uma conta do sistema.</span><span class="sxs-lookup"><span data-stu-id="d8e41-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="d8e41-191">código de serviço real Olá pode ser executado sob uma conta com privilégios inferiores.</span><span class="sxs-lookup"><span data-stu-id="d8e41-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="d8e41-192">Aplicar um padrão política tooall serviço código pacotes</span><span class="sxs-lookup"><span data-stu-id="d8e41-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="d8e41-193">Use Olá **DefaultRunAsPolicy** seção toospecify uma conta de usuário padrão para todos os pacotes de código que não têm um determinado **RunAsPolicy** definido.</span><span class="sxs-lookup"><span data-stu-id="d8e41-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="d8e41-194">Se a maioria dos pacotes de código Olá especificadas no manifesto do serviço Olá usado por um aplicativo precisar toorun em Olá mesmo usuário, hello aplicativo apenas pode definir uma política de executar como padrão com uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="d8e41-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="d8e41-195">Olá exemplo a seguir especifica que, se um pacote de códigos não tem um **RunAsPolicy** especificado, o pacote de códigos Olá deve ser executados Olá **MyDefaultAccount** especificado na seção de entidades de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e41-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="d8e41-196">Usar um usuário ou um grupo de domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8e41-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="d8e41-197">Para uma instância do Service Fabric foi instalado no Windows Server usando o instalador autônomo do hello, você pode executar o serviço de saudação sob as credenciais de saudação para uma conta de usuário ou grupo do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e41-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="d8e41-198">Esse é o Active Directory local em seu domínio e não é com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8e41-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d8e41-199">Usando um usuário de domínio ou grupo, em seguida, você pode acessar outros recursos no domínio hello (por exemplo, compartilhamentos de arquivos) que foram concedidos permissões.</span><span class="sxs-lookup"><span data-stu-id="d8e41-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="d8e41-200">Olá, exemplo a seguir mostra um usuário do Active Directory chamado *TestUser* domínio senha criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="d8e41-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="d8e41-201">Você pode usar o hello `Invoke-ServiceFabricEncryptText` texto do PowerShell comando toocreate Olá secreta de criptografia.</span><span class="sxs-lookup"><span data-stu-id="d8e41-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="d8e41-202">Consulte [Gerenciamento de segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d8e41-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="d8e41-203">Você deve implantar a chave privada Olá Olá certificado toodecrypt Olá senha toohello computador local usando um método fora de banda (no Azure, isso é por meio do Gerenciador de recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="d8e41-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="d8e41-204">Em seguida, quando o Service Fabric implanta a máquina de toohello de pacote de serviço Olá, é capaz de toodecrypt Olá segredo e (junto com o nome de usuário de saudação) autenticar com toorun do Active Directory com essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="d8e41-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="d8e41-205">Use uma Conta de Serviço Gerenciado de Grupo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="d8e41-206">Para uma instância do Service Fabric foi instalado no Windows Server usando o instalador autônomo do hello, você pode executar o serviço de saudação como um grupo de conta de serviço gerenciada (gMSA).</span><span class="sxs-lookup"><span data-stu-id="d8e41-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="d8e41-207">Observe que esse é o Active Directory local em seu domínio e não é com o Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d8e41-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d8e41-208">Usando uma gMSA não há nenhuma senha ou a senha criptografada armazenada no hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="d8e41-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="d8e41-209">Olá exemplo a seguir mostra como toocreate uma conta gMSA chamado *svc teste$*; como toodeploy gerenciados nós de cluster de toohello de conta de serviço; e como tooconfigure Olá principal do usuário.</span><span class="sxs-lookup"><span data-stu-id="d8e41-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="d8e41-210">Pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="d8e41-210">Prerequisites.</span></span>
- <span data-ttu-id="d8e41-211">domínio Olá precisa de uma chave raiz KDS.</span><span class="sxs-lookup"><span data-stu-id="d8e41-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="d8e41-212">domínio Olá precisa toobe em um Windows Server 2012 ou posterior nível funcional.</span><span class="sxs-lookup"><span data-stu-id="d8e41-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="d8e41-213">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d8e41-213">Example</span></span>
1. <span data-ttu-id="d8e41-214">Ter um administrador de domínio do active directory crie uma conta de serviço gerenciado de grupo usando Olá `New-ADServiceAccount` commandlet e certifique-se de que Olá `PrincipalsAllowedToRetrieveManagedPassword` inclui todos os nós do cluster Olá service fabric.</span><span class="sxs-lookup"><span data-stu-id="d8e41-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="d8e41-215">Observe que `AccountName`, `DnsHostName` e `ServicePrincipalName` devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d8e41-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="d8e41-216">Em cada um de nós de cluster de malha Olá serviço (por exemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instalar e testar Olá gMSA.</span><span class="sxs-lookup"><span data-stu-id="d8e41-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="d8e41-217">Configure o UPN Olá e usuário de Olá Olá RunAsPolicy tooreference.</span><span class="sxs-lookup"><span data-stu-id="d8e41-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="d8e41-218">Atribuir uma política de acesso de segurança a pontos de extremidade HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="d8e41-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="d8e41-219">Se você aplicar um serviço de tooa RunAs política e o manifesto de serviço Olá declara recursos de ponto de extremidade com o protocolo de saudação HTTP, você deve especificar um **SecurityAccessPolicy** tooensure portas alocadas pontos de extremidade toothese estão corretamente controle de acesso listados para Olá conta de usuário RunAs Olá serviço é executado.</span><span class="sxs-lookup"><span data-stu-id="d8e41-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="d8e41-220">Caso contrário, **http.sys** não tem acesso toohello serviço, e falhas de chamadas do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="d8e41-221">Olá, exemplo a seguir aplica Olá Customer1 conta tooan ponto de extremidade chamado **EndpointName**, que concede direitos de acesso completo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="d8e41-222">Ponto de extremidade de HTTPS hello, você também tem tooindicate nome de saudação do cliente do hello certificado tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="d8e41-223">Você pode fazer isso usando **EndpointBindingPolicy**, com certificado Olá definido em uma seção de certificados no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="d8e41-224">Atualizando vários aplicativos com pontos de extremidade https</span><span class="sxs-lookup"><span data-stu-id="d8e41-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="d8e41-225">Você precisa toobe cuidado não toouse Olá **mesma porta** para instâncias diferentes do hello aplicativo mesmo quando usando http**s**.</span><span class="sxs-lookup"><span data-stu-id="d8e41-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="d8e41-226">motivo da saudação é que Service Fabric não será capaz de tooupgrade cert de Olá para uma das instâncias de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="d8e41-227">Por exemplo, se quiser que o aplicativo 1 ou aplicativo 2 ambos os tooupgrade seu toocert cert 1 2.</span><span class="sxs-lookup"><span data-stu-id="d8e41-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="d8e41-228">Quando ocorrer a atualização do hello, Service Fabric podem apagadas registro de certificado 1 Olá com HTTP. sys, embora hello outro aplicativo está ainda usá-lo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="d8e41-229">tooprevent, Service Fabric detecta que já há outra instância do aplicativo registrada na porta Olá com certificado hello (vencimento toohttp.sys) e haverá falha na operação de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e41-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="d8e41-230">Portanto, Service Fabric não suporta atualização a dois serviços diferentes usando **Olá a mesma porta** em instâncias de aplicativo diferente.</span><span class="sxs-lookup"><span data-stu-id="d8e41-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="d8e41-231">Em outras palavras, você não pode usar o mesmo certificado de saudação em diferentes serviços em hello mesma porta.</span><span class="sxs-lookup"><span data-stu-id="d8e41-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="d8e41-232">Se você precisar toohave compartilhado de certificado na Olá mesmo porta, você precisa tooensure que Olá serviços são colocados em máquinas diferentes com restrições de posicionamento.</span><span class="sxs-lookup"><span data-stu-id="d8e41-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="d8e41-233">Ou, considere o uso de portas dinâmicas do Service Fabric, se possível, para cada serviço em cada instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8e41-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="d8e41-234">Se você vir uma atualização falha com https, um aviso de erro dizendo "Olá Windows HTTP Server API não suporta vários certificados para aplicativos que compartilham uma porta."</span><span class="sxs-lookup"><span data-stu-id="d8e41-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="d8e41-235">Um exemplo completo de manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8e41-235">A complete application manifest example</span></span>
<span data-ttu-id="d8e41-236">saudação de manifesto do aplicativo a seguir mostra a muitos dos Olá diferentes configurações:</span><span class="sxs-lookup"><span data-stu-id="d8e41-236">hello following application manifest shows many of hello different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d8e41-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8e41-237">Next steps</span></span>
* [<span data-ttu-id="d8e41-238">Entender o modelo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d8e41-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="d8e41-239">Especificar recursos em um manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="d8e41-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="d8e41-240">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8e41-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
