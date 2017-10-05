---
title: "Saiba mais sobre as políticas de segurança dos microsserviços do Azure | Microsoft Docs"
description: "Uma visão geral de como executar um aplicativo Service Fabric em contas de segurança do sistema e locais, incluindo o SetupEntryPoint no qual o aplicativo precisa executar alguma ação privilegiada antes de iniciar"
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
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="c2001-103">Configurar políticas de segurança para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2001-103">Configure security policies for your application</span></span>
<span data-ttu-id="c2001-104">Usando o Azure Service Fabric, é possível proteger aplicativos em execução no cluster em contas de usuário diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2001-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="c2001-105">O Service Fabric também protege os recursos usados pelos aplicativos no momento da implantação nas contas de usuário, por exemplo, arquivos, diretórios e certificados.</span><span class="sxs-lookup"><span data-stu-id="c2001-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="c2001-106">Isso torna os aplicativos em execução, mesmo em um ambiente hospedado compartilhado, mais protegidos uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="c2001-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="c2001-107">Por padrão, os aplicativos de Service Fabric são executados na conta sob a qual o processo Fabric.exe está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="c2001-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="c2001-108">O Service Fabric também fornece a capacidade de executar aplicativos em uma conta de usuário local ou em uma conta de sistema local, especificada no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="c2001-109">Os tipos de conta do sistema local com suporte são **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="c2001-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="c2001-110">Durante a execução do Service Fabric no Windows Server em seu datacenter usando o instalador autônomo, é possível usar contas de domínio do Active Directory, incluindo contas de serviço gerenciado de grupo.</span><span class="sxs-lookup"><span data-stu-id="c2001-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="c2001-111">É possível definir e criar grupos de usuários para que um ou mais usuários possam ser adicionados a cada grupo para serem gerenciados em conjunto.</span><span class="sxs-lookup"><span data-stu-id="c2001-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="c2001-112">Isso será útil quando houver vários usuários para pontos de entrada de serviço diferentes e eles precisarem de privilégios comuns disponíveis no nível do grupo.</span><span class="sxs-lookup"><span data-stu-id="c2001-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="c2001-113">Configurar a política para um ponto de entrada de instalação do serviço</span><span class="sxs-lookup"><span data-stu-id="c2001-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="c2001-114">Conforme descrito no [modelo de aplicativo](service-fabric-application-model.md) , o ponto de entrada de instalação, **SetupEntryPoint**, é um ponto de entrada privilegiado executado com as mesmas credenciais que o Service Fabric (normalmente, a conta *NetworkService*) antes de qualquer outro ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="c2001-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="c2001-115">O executável especificado pelo **EntryPoint** normalmente é o host de serviço de execução longa.</span><span class="sxs-lookup"><span data-stu-id="c2001-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="c2001-116">Portanto, ter um ponto de entrada de instalação separado evita a necessidade de executar o executável do host de serviço com altos privilégios por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="c2001-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="c2001-117">O executável especificado pelo **EntryPoint** é executado depois que o **SetupEntryPoint** é encerrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="c2001-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="c2001-118">O processo resultante é monitorado e reiniciado, começando novamente com **SetupEntryPoint**, caso ele termine ou falhe.</span><span class="sxs-lookup"><span data-stu-id="c2001-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="c2001-119">O item a seguir é um exemplo simples de manifesto do serviço mostrando o SetupEntryPoint e o EntryPoint principal para o serviço.</span><span class="sxs-lookup"><span data-stu-id="c2001-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

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

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="c2001-120">Configurar a política usando uma conta local</span><span class="sxs-lookup"><span data-stu-id="c2001-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="c2001-121">Após ter configurado do serviço para ter um SetupEntryPoint, é possível alterar as permissões de segurança sob as quais ele é executado no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="c2001-122">O item a seguir mostra como configurar o serviço para ser executado com privilégios de conta de administrador de usuário.</span><span class="sxs-lookup"><span data-stu-id="c2001-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

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

<span data-ttu-id="c2001-123">Primeiro, crie uma seção **Principals** com um nome de usuário SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="c2001-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="c2001-124">Isso indica que o usuário é membro do grupo do sistema Administradores.</span><span class="sxs-lookup"><span data-stu-id="c2001-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="c2001-125">Em seguida, na seção **ServiceManifestImport**, configure uma política para aplicar essa entidade de segurança ao **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="c2001-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="c2001-126">Isso informa ao Service Fabric que quando o arquivo **MySetup.bat** for executado ele deve ser `RunAs` com privilégios de Administrador.</span><span class="sxs-lookup"><span data-stu-id="c2001-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="c2001-127">Considerando que você *não* aplicou uma política ao ponto de entrada principal, o código em **MyServiceHost.exe** será executado na conta do sistema **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="c2001-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="c2001-128">Essa é a conta padrão que todos os pontos de entrada de serviço são executados como.</span><span class="sxs-lookup"><span data-stu-id="c2001-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="c2001-129">Agora, vamos adicionar o arquivo MySetup.bat ao projeto do Visual Studio para testar os privilégios de Administrador.</span><span class="sxs-lookup"><span data-stu-id="c2001-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="c2001-130">No Visual Studio, clique com o botão direito do mouse no projeto de serviço e adicione um novo arquivo chamado MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="c2001-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="c2001-131">Em seguida, certifique-se de que o arquivo MySetup.bat é incluído no service pack.</span><span class="sxs-lookup"><span data-stu-id="c2001-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="c2001-132">Por padrão, não é.</span><span class="sxs-lookup"><span data-stu-id="c2001-132">By default, it is not.</span></span> <span data-ttu-id="c2001-133">Selecione o arquivo, clique com o botão direito do mouse para exibir o menu de contexto e escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c2001-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="c2001-134">Na caixa de diálogo Propriedades, verifique se **Copiar para Diretório de Saída** está definido como **Copiar se mais recente**.</span><span class="sxs-lookup"><span data-stu-id="c2001-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="c2001-135">Consulte a seguinte captura de tela.</span><span class="sxs-lookup"><span data-stu-id="c2001-135">See the following screenshot.</span></span>

![CopyToOutput do Visual Studio para o arquivo em lotes SetupEntryPoint][image1]

<span data-ttu-id="c2001-137">Agora, abra o arquivo MySetup.bat e adicione os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2001-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="c2001-138">Em seguida, compile e implante a solução em um cluster de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="c2001-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="c2001-139">Após a inicialização do serviço, conforme mostrado no Gerenciador do Service Fabric, é possível ver que o arquivo MySetup.bat foi bem-sucedido de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="c2001-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="c2001-140">Abra um prompt de comando do PowerShell e digite:</span><span class="sxs-lookup"><span data-stu-id="c2001-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="c2001-141">Em seguida, anote o nome do nó no qual o serviço foi implantado e iniciado no Service Fabric Explorer, por exemplo, Nó 2.</span><span class="sxs-lookup"><span data-stu-id="c2001-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="c2001-142">Em seguida, navegue até a pasta de trabalho de instância do aplicativo para localizar o arquivo out.txt que mostra o valor de **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="c2001-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="c2001-143">Por exemplo, se o serviço foi implantado no Nó 2, você pode acessar este caminho até o **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="c2001-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="c2001-144">Configurar a política usando contas do sistema local</span><span class="sxs-lookup"><span data-stu-id="c2001-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="c2001-145">Em geral, é preferível executar o script de inicialização usando uma conta do sistema local em vez de uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="c2001-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="c2001-146">A execução da política RunAs como membro do grupo Administradores geralmente não funciona bem, porque os computadores têm o UAC (Controle de Acesso de Usuário) habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c2001-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="c2001-147">Em tais casos, **a recomendação é executar o SetupEntryPoint como LocalSystem em vez de um usuário local adicionado ao grupo Administradores**.</span><span class="sxs-lookup"><span data-stu-id="c2001-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="c2001-148">O exemplo a seguir mostra a definição de SetupEntryPoint para ser executado como LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="c2001-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="c2001-149">Iniciar comandos do PowerShell em um ponto de entrada de instalação</span><span class="sxs-lookup"><span data-stu-id="c2001-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="c2001-150">Para executar o PowerShell do ponto **SetupEntryPoint**, execute **PowerShell.exe** em um arquivo em lotes que aponte para um arquivo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2001-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="c2001-151">Primeiro, adicione um arquivo do PowerShell ao projeto de serviço, por exemplo, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c2001-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="c2001-152">Não deixe de definir a propriedade *Copiar se for mais recente* para que esse arquivo também seja incluído no pacote de serviço.</span><span class="sxs-lookup"><span data-stu-id="c2001-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="c2001-153">O exemplo a seguir mostra um exemplo de arquivo em lotes que inicia um arquivo do PowerShell chamado MySetup.ps1, que define uma variável de ambiente do sistema chamada **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="c2001-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="c2001-154">MySetup.bat para iniciar o arquivo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2001-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="c2001-155">No arquivo do PowerShell, adicione o seguinte para definir uma variável de ambiente do sistema:</span><span class="sxs-lookup"><span data-stu-id="c2001-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="c2001-156">Por padrão, quando o arquivo em lotes é executado, ele examina a pasta de aplicativo chamada **trabalho** em busca de arquivos.</span><span class="sxs-lookup"><span data-stu-id="c2001-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="c2001-157">Nesse caso, quando MySetup.bat é executado, queremos que o arquivo MySetup.ps1 seja encontrado na mesma pasta, que é a pasta do **pacote de códigos** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="c2001-158">Para alterar essa pasta, defina a pasta de trabalho:</span><span class="sxs-lookup"><span data-stu-id="c2001-158">To change this folder, set the working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="c2001-159">Use o redirecionamento de console para depuração local</span><span class="sxs-lookup"><span data-stu-id="c2001-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="c2001-160">De vez em quando, é útil ver a saída do console da execução de um script para fins de depuração.</span><span class="sxs-lookup"><span data-stu-id="c2001-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="c2001-161">Para fazer isso, você pode definir uma política de redirecionamento de console que grava a saída em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c2001-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="c2001-162">A saída do arquivo é gravada na pasta de aplicativos chamada **log** no nó no qual o aplicativo é implantado e executado.</span><span class="sxs-lookup"><span data-stu-id="c2001-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="c2001-163">(Consulte onde encontrá-lo no exemplo anterior.)</span><span class="sxs-lookup"><span data-stu-id="c2001-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="c2001-164">Nunca use a política de redirecionamento de console em um aplicativo implantado na produção, pois isso pode afetar o failover do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="c2001-165">*Só* use isso para fins de depuração e de desenvolvimento locais.</span><span class="sxs-lookup"><span data-stu-id="c2001-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="c2001-166">O exemplo a seguir mostra a configuração de redirecionamento do console com um valor FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="c2001-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="c2001-167">Se você alterar o arquivo MySetup.ps1 agora para gravar um comando **Echo** , ele gravará o arquivo de saída para fins de depuração:</span><span class="sxs-lookup"><span data-stu-id="c2001-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="c2001-168">**Depois de depurar seu script, remova imediatamente a política de redirecionamento de console**.</span><span class="sxs-lookup"><span data-stu-id="c2001-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="c2001-169">Configurar uma política para pacotes de código de serviço</span><span class="sxs-lookup"><span data-stu-id="c2001-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="c2001-170">Nas etapas anteriores, você viu como aplicar uma política RunAs a um SetupEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="c2001-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="c2001-171">Agora, vamos analisar com mais detalhes como criar entidades diferentes que possam ser aplicadas como políticas de serviço.</span><span class="sxs-lookup"><span data-stu-id="c2001-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="c2001-172">Criar grupos de usuários locais</span><span class="sxs-lookup"><span data-stu-id="c2001-172">Create local user groups</span></span>
<span data-ttu-id="c2001-173">É possível definir e criar grupos de usuários que permitem que um ou mais usuários sejam adicionados a um grupo.</span><span class="sxs-lookup"><span data-stu-id="c2001-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="c2001-174">Isso será útil se houverem vários usuários para pontos de entrada de serviço diferentes e eles precisarem de privilégios comuns disponíveis no nível do grupo.</span><span class="sxs-lookup"><span data-stu-id="c2001-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="c2001-175">O exemplo a seguir mostra um grupo local chamado **LocalAdminGroup** com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="c2001-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="c2001-176">Dois usuários, Customer1 e Customer2, tornam-se membros desse grupo local.</span><span class="sxs-lookup"><span data-stu-id="c2001-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="c2001-177">Criar usuários locais</span><span class="sxs-lookup"><span data-stu-id="c2001-177">Create local users</span></span>
<span data-ttu-id="c2001-178">É possível criar um usuário local que pode ser usado para ajudar a proteger um serviço dentro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="c2001-179">Quando um tipo de conta **LocalUser** é especificado na seção Entidades do manifesto do aplicativo, o Service Fabric cria contas de usuário local em máquinas nas quais o aplicativo foi implantado.</span><span class="sxs-lookup"><span data-stu-id="c2001-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="c2001-180">Por padrão, essas contas não têm os mesmos nomes especificados no manifesto do aplicativo (por exemplo, Customer3 no exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="c2001-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="c2001-181">Em vez disso, eles são gerados dinamicamente e têm senhas aleatórias.</span><span class="sxs-lookup"><span data-stu-id="c2001-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="c2001-182">Se um aplicativo exigir que a conta de usuário e senha sejam iguais em todos os computadores (por exemplo, para habilitar a autenticação NTLM), o manifesto do cluster deve definir NTLMAuthenticationEnabled como true.</span><span class="sxs-lookup"><span data-stu-id="c2001-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="c2001-183">O manifesto do cluster também deve especificar um NTLMAuthenticationPasswordSecret que será usado para gerar a mesma senha em todos os computadores.</span><span class="sxs-lookup"><span data-stu-id="c2001-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="c2001-184">Atribuir políticas aos pacotes de códigos do serviço</span><span class="sxs-lookup"><span data-stu-id="c2001-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="c2001-185">A seção **RunAsPolicy** para uma **ServiceManifestImport** especifica a conta da seção de entidades que deve ser usada para executar um pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="c2001-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="c2001-186">Ela também associa os pacotes de código do manifesto do serviço com contas de usuário na seção entidades.</span><span class="sxs-lookup"><span data-stu-id="c2001-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="c2001-187">Você pode especificar isso para os pontos de entrada de configuração ou principal, ou especificar `All` para aplicar a ambos.</span><span class="sxs-lookup"><span data-stu-id="c2001-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="c2001-188">O exemplo a seguir mostra a aplicação de políticas diferentes:</span><span class="sxs-lookup"><span data-stu-id="c2001-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="c2001-189">Se **EntryPointType** não for especificado, o padrão será definido como EntryPointType ="Main".</span><span class="sxs-lookup"><span data-stu-id="c2001-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="c2001-190">A especificação de um **SetupEntryPoint** é especialmente útil quando você deseja executar determinadas operações de instalação de privilégio elevado em uma conta do sistema.</span><span class="sxs-lookup"><span data-stu-id="c2001-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="c2001-191">O código de serviço real pode ser executado em uma conta de baixo privilégio.</span><span class="sxs-lookup"><span data-stu-id="c2001-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="c2001-192">Aplicar uma política padrão a todos os pacotes de códigos de serviço</span><span class="sxs-lookup"><span data-stu-id="c2001-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="c2001-193">Use a seção **DefaultRunAsPolicy** para especificar uma conta de usuário padrão para todos os pacotes de códigos que não tenham uma **RunAsPolicy** específica definida.</span><span class="sxs-lookup"><span data-stu-id="c2001-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="c2001-194">Quando a maioria dos pacotes de códigos especificados no manifesto do serviço usado por um aplicativo precisar ser executada com o mesmo usuário, o aplicativo poderá definir apenas uma política RunAs padrão nessa conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="c2001-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="c2001-195">O exemplo a seguir especifica que quando um pacote de códigos não tiver uma **RunAsPolicy** especificada, ele deverá ser executado em uma **MyDefaultAccount** especificada na seção Entidades.</span><span class="sxs-lookup"><span data-stu-id="c2001-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="c2001-196">Usar um usuário ou um grupo de domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2001-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="c2001-197">Para uma instância do Service Fabric instalada no Windows Server usando o instalador autônomo, é possível executar o serviço com as credenciais para uma conta de grupo ou de usuário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2001-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="c2001-198">Esse é o Active Directory local em seu domínio e não é com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2001-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c2001-199">Ao usar um usuário de domínio ou grupo, você pode acessar outros recursos do domínio (por exemplo, compartilhamentos de arquivos) que receberam permissões.</span><span class="sxs-lookup"><span data-stu-id="c2001-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="c2001-200">O exemplo a seguir mostra um usuário do Active Directory denominado *TestUser* com a senha de domínio criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="c2001-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="c2001-201">É possível usar o comando `Invoke-ServiceFabricEncryptText` do Powershell para criar o texto cifrado secreto.</span><span class="sxs-lookup"><span data-stu-id="c2001-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="c2001-202">Consulte [Gerenciamento de segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c2001-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="c2001-203">É necessário implantar a chave privada do certificado para descriptografar a senha no computador local usando um método fora de banda (no Azure, isso ocorre por meio do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c2001-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="c2001-204">Em seguida, quando o Service Fabric implanta o pacote de serviço no computador, ele é capaz de descriptografar o segredo e (juntamente com o nome de usuário) autenticar com o Active Directory para execução com essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="c2001-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="c2001-205">Use uma Conta de Serviço Gerenciado de Grupo.</span><span class="sxs-lookup"><span data-stu-id="c2001-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="c2001-206">Para uma instância do Service Fabric instalada no Windows Server usando o instalador autônomo, é possível executar o serviço como uma Conta de Serviço Gerenciado (gMSA).</span><span class="sxs-lookup"><span data-stu-id="c2001-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="c2001-207">Observe que esse é o Active Directory local em seu domínio e não é com o Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c2001-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c2001-208">Ao usar uma gMSA, a senha ou senha criptografada não será armazenada no `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="c2001-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="c2001-209">O exemplo a seguir mostra como criar uma conta gMSA chamada *svc-Test$*; como implantar essa conta de serviço gerenciado nos nós de cluster; e como configurar a entidade de segurança do usuário.</span><span class="sxs-lookup"><span data-stu-id="c2001-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="c2001-210">Pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="c2001-210">Prerequisites.</span></span>
- <span data-ttu-id="c2001-211">O domínio precisa de uma chave raiz KDS.</span><span class="sxs-lookup"><span data-stu-id="c2001-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="c2001-212">O domínio deve ser um Windows Server 2012 ou nível funcional posterior.</span><span class="sxs-lookup"><span data-stu-id="c2001-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="c2001-213">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c2001-213">Example</span></span>
1. <span data-ttu-id="c2001-214">Peça para um administrador de domínio do Active Directory criar uma conta de serviço gerenciado de grupo usando o cmdlet `New-ADServiceAccount` e verifique se o `PrincipalsAllowedToRetrieveManagedPassword` inclui todos os nós de cluster de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="c2001-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="c2001-215">Observe que `AccountName`, `DnsHostName` e `ServicePrincipalName` devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="c2001-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="c2001-216">Em cada um dos nós de cluster do Service Fabric (por exemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instale e teste a gMSA.</span><span class="sxs-lookup"><span data-stu-id="c2001-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="c2001-217">Configure a entidade de usuário e a RunAsPolicy para fazer referência ao usuário.</span><span class="sxs-lookup"><span data-stu-id="c2001-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="c2001-218">Atribuir uma política de acesso de segurança a pontos de extremidade HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="c2001-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="c2001-219">Se você aplicar uma política RunAs a um serviço e o manifesto do serviço declarar recursos de ponto de extremidade com o protocolo HTTP, será necessário especificar uma **SecurityAccessPolicy** para assegurar que as portas alocadas a esses pontos de extremidade sejam corretamente listadas no controle de acesso para a conta de usuário RunAs na qual o serviço é executado.</span><span class="sxs-lookup"><span data-stu-id="c2001-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="c2001-220">Caso contrário, o **http.sys** não terá acesso ao serviço e você receberá uma falha com chamadas do cliente.</span><span class="sxs-lookup"><span data-stu-id="c2001-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="c2001-221">O exemplo a seguir aplica a conta Customer1 a um ponto de extremidade chamado **EndpointName**, concedendo a ele direitos de acesso completo.</span><span class="sxs-lookup"><span data-stu-id="c2001-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="c2001-222">Para o ponto de extremidade HTTPS, você também precisa indicar o nome do certificado para retornar para o cliente.</span><span class="sxs-lookup"><span data-stu-id="c2001-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="c2001-223">Você pode fazer isso usando **EndpointBindingPolicy**, com o certificado definido em uma seção de certificados no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="c2001-224">Atualizando vários aplicativos com pontos de extremidade https</span><span class="sxs-lookup"><span data-stu-id="c2001-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="c2001-225">Você precisa ter cuidado para não usar a **mesma porta** para instâncias diferentes do mesmo aplicativo quando estiver usando http**s**.</span><span class="sxs-lookup"><span data-stu-id="c2001-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="c2001-226">O motivo é que o Service Fabric não será capaz de fazer upgrade do certificado para uma das instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="c2001-227">Por exemplo, se o aplicativo 1 ou o aplicativo 2 deseja fazer upgrade do seu cert 1 cert 2.</span><span class="sxs-lookup"><span data-stu-id="c2001-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="c2001-228">Quando o upgrade é feito, o Service Fabric pode apagar o registro cert 1 com o http.sys, embora o outro aplicativo ainda o está usando.</span><span class="sxs-lookup"><span data-stu-id="c2001-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="c2001-229">Para evitar isso, o Service Fabric detecta se já há em outra instância do aplicativo registrada na porta com o certificado (devido ao http. sys) e faz a operação falhar.</span><span class="sxs-lookup"><span data-stu-id="c2001-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="c2001-230">Portanto, o Service Fabric não suporta a atualização de dois serviços diferentes usando **a mesma porta** em instâncias de aplicativo diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2001-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="c2001-231">Em outras palavras, você não pode usar o mesmo certificado em serviços diferentes na mesma porta.</span><span class="sxs-lookup"><span data-stu-id="c2001-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="c2001-232">Se você precisa ter um certificado compartilhado na mesma porta, precisa garantir que os serviços sejam colocados em computadores diferentes com restrições de posicionamento.</span><span class="sxs-lookup"><span data-stu-id="c2001-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="c2001-233">Ou, considere o uso de portas dinâmicas do Service Fabric, se possível, para cada serviço em cada instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2001-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="c2001-234">Se você vir um upgrade falhar com https, um aviso de erro dizendo "A API de servidor HTTP do Windows não suporta vários certificados para aplicativos que compartilham uma porta".</span><span class="sxs-lookup"><span data-stu-id="c2001-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="c2001-235">Um exemplo completo de manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2001-235">A complete application manifest example</span></span>
<span data-ttu-id="c2001-236">O manifesto do aplicativo a seguir mostra várias configurações diferentes:</span><span class="sxs-lookup"><span data-stu-id="c2001-236">The following application manifest shows many of the different settings:</span></span>

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
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


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="c2001-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2001-237">Next steps</span></span>
* [<span data-ttu-id="c2001-238">Entenda o modelo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2001-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="c2001-239">Especificar recursos em um manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="c2001-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="c2001-240">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2001-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
