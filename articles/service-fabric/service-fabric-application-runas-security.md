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
# <a name="configure-security-policies-for-your-application"></a>Configurar políticas de segurança para seu aplicativo
Usando o Service Fabric do Azure, você pode proteger os aplicativos em execução no cluster de saudação em diferentes contas de usuário. Serviço de malha também ajuda a certificados, arquivos, diretórios e recursos de saudação seguro que são usados por aplicativos em tempo de saudação da implantação em contas de usuário hello – por exemplo. Isso torna os aplicativos em execução, mesmo em um ambiente hospedado compartilhado, mais protegidos uns dos outros.

Por padrão, os aplicativos do Service Fabric são executados sob conta Olá Olá Fabric.exe processo é executado. Serviço de malha também fornece a capacidade de saudação toorun aplicativos sob uma conta de usuário local ou a conta sistema local, que é especificada no manifesto de aplicativo hello. Os tipos de conta do sistema local com suporte são **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.

 Quando você estiver executando do Service Fabric no Windows Server em seu data center usando o instalador autônomo do hello, você pode usar contas de domínio do Active Directory, incluindo contas de serviço gerenciado de grupo.

Você pode definir e criar grupos de usuários para que um ou mais usuários possam ser adicionados tooeach grupo toobe gerenciado juntos. Isso é útil quando há vários usuários para os pontos de entrada de serviço diferente e é necessário toohave certos privilégios comuns que estão disponíveis no nível do grupo hello.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Configurar política de saudação para um ponto de entrada de configuração de serviço
Conforme descrito em Olá [modelo de aplicativo](service-fabric-application-model.md), Olá ponto de entrada de configuração, **SetupEntryPoint**, é um ponto de entrada com privilégios que é executado com hello mesmo credenciais como Service Fabric (normalmente Olá *NetworkService* conta) antes de qualquer outro ponto de entrada. executável de saudação que é especificado pelo **EntryPoint** normalmente é o host de serviço de longa execução hello. Para ter uma entrada de instalação separado do ponto evita a necessidade de host de serviço Olá toorun executável com altos privilégios por longos períodos de tempo. Olá executável que **EntryPoint** especifica é executado após a **SetupEntryPoint** é encerrada com êxito. Olá processo resultante é monitorado e reiniciado e começa novamente com **SetupEntryPoint** se ele nunca termina ou falha.

a seguir Olá é um exemplo de manifesto de serviço simples que mostra Olá SetupEntryPoint e Olá principal ponto de entrada para o serviço de saudação.

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

### <a name="configure-hello-policy-by-using-a-local-account"></a>Configurar política de saudação usando uma conta local
Depois de configurar Olá serviço toohave um ponto de entrada de configuração, você pode alterar as permissões de segurança de saudação que ele é executado no manifesto de aplicativo hello. saudação de exemplo a seguir mostra como tooconfigure Olá toorun de serviço com privilégios de conta de administrador do usuário.

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

Primeiro, crie uma seção **Principals** com um nome de usuário SetupAdminUser. Isso indica que o usuário Olá é um membro do grupo de sistema de administradores de saudação.

Em seguida, em Olá **servicemanifestimport ao** seção, configure uma política tooapply essa entidade muito**SetupEntryPoint**. Isso informa ao serviço de malha que quando hello **MySetup.bat** arquivo é executado, ele deve ser `RunAs` com privilégios de administrador. Considerando que você tenha *não* aplicada a um ponto de entrada principal toohello de política, o código de Olá em **MyServiceHost.exe** compatível com o sistema Olá **NetworkService** conta. Esta é a conta de padrão de saudação que todos os pontos de entrada de serviço são executados como.

Agora, vamos adicionar Olá arquivo MySetup.bat toohello Visual Studio project tootest Olá privilégios de administrador. No Visual Studio, clique com botão direito Olá serviço e adicione um novo arquivo chamado MySetup.bat.

Em seguida, certifique-se de que arquivo hello MySetup.bat está incluído no pacote de serviço hello. Por padrão, não é. Selecione o arquivo hello, tooget Olá contexto menu de atalho e escolha **propriedades**. Na caixa de diálogo de propriedades de saudação, certifique-se de que **copiar tooOutput diretório** está definido muito**copiar se mais recente**. Consulte Olá captura de tela a seguir.

![CopyToOutput do Visual Studio para o arquivo em lotes SetupEntryPoint][image1]

Agora, abrir o arquivo de MySetup.bat hello e adicione Olá comandos a seguir:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Em seguida, criar e implantar o cluster de desenvolvimento local Olá solução tooa. Depois que o serviço Olá foi iniciado, conforme mostrado no Gerenciador do Service Fabric, você pode ver que arquivo hello MySetup.bat foi bem-sucedida de um duas maneiras. Abra um prompt de comando do PowerShell e digite:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Anote o nome Olá Olá nó onde o serviço Olá foi implantado e iniciado no Gerenciador do Service Fabric – por exemplo, nó 2. Em seguida, navegue toohello instância trabalho pasta toofind Olá out.txt arquivo do aplicativo que mostra o valor de saudação do **TestVariable**. Por exemplo, se esse serviço foi implantado tooNode 2, em seguida, você pode ir toothis caminho Olá **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Configurar política de saudação usando contas locais do sistema
Geralmente, é preferível toorun script de inicialização de saudação usando uma conta sistema local em vez de uma conta de administrador. Execução da política de RunAs hello como um membro da saudação grupo administradores geralmente não funciona bem como máquinas têm controle de acesso da usuário (UAC) habilitado por padrão. Nesses casos, **Olá recomenda Olá toorun SetupEntryPoint como LocalSystem, em vez de como um grupo de usuário local adicionado tooAdministrators**. Olá exemplo a seguir mostra configuração Olá SetupEntryPoint toorun como LocalSystem:

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Iniciar comandos do PowerShell em um ponto de entrada de instalação
toorun PowerShell de saudação **SetupEntryPoint** ponto, você pode executar **PowerShell.exe** um arquivo em lotes que aponta tooa PowerShell de arquivo. Primeiro, adicione um projeto de serviço do PowerShell arquivo toohello – por exemplo, **MySetup.ps1**. Lembre-se de saudação tooset *copiar se mais recente* propriedade para esse arquivo hello também está incluído no pacote de serviço hello. Olá, exemplo a seguir mostra um arquivo em lotes de exemplo que inicia um arquivo PowerShell chamado MySetup.ps1, que define uma variável de ambiente do sistema chamada **TestVariable**.

MySetup.bat toostart um arquivo do PowerShell:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

No arquivo de PowerShell Olá, adicione Olá tooset uma variável de ambiente do sistema a seguir:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Por padrão, quando o arquivo em lotes de saudação é executado, parece em pasta do aplicativo hello chamada **trabalhar** para arquivos. Nesse caso, quando MySetup.bat é executado, queremos que este Olá toofind MySetup.ps1 arquivo hello mesmo pasta, que é o aplicativo hello **pacote de códigos** pasta. toochange essa pasta, a pasta de trabalho de saudação do conjunto:
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

## <a name="use-console-redirection-for-local-debugging"></a>Use o redirecionamento de console para depuração local
Ocasionalmente, é útil toosee saída do console de saudação da execução de um script para fins de depuração. toodo isso, você pode definir uma política de redirecionamento de console, que grava o arquivo de tooa Olá saída. Olá arquivo de saída é chamada de pasta de aplicativo escrita toohello **log** no nó Olá onde o aplicativo hello é implantado e executado. (Consulte onde toofind isso em Olá anterior exemplo.)

> [!WARNING]
> Nunca use a política de redirecionamento do console de saudação em um aplicativo que é implantado na produção, pois isso pode afetar o failover de aplicativo hello. *Só* use isso para fins de depuração e de desenvolvimento locais.  
> 
> 

Olá, exemplo a seguir mostra redirecionamento de console de saudação de configuração com um valor de FileRetentionCount:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Se você alterar Olá MySetup.ps1 arquivo toowrite um **Echo** de comando, isso gravará toohello o arquivo de saída para fins de depuração:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Depois de depurar seu script, remova imediatamente a política de redirecionamento de console**.

## <a name="configure-a-policy-for-service-code-packages"></a>Configurar uma política para pacotes de código de serviço
Olá etapas anteriores, você viu como tooapply uma tooSetupEntryPoint de política de RunAs. Vamos examinar um pouco mais como toocreate entidades diferentes que podem ser aplicadas ao serviço políticas.

### <a name="create-local-user-groups"></a>Criar grupos de usuários locais
Você pode definir e criar grupos de usuários que permite que um ou mais toobe de usuários adicionados tooa grupo. Isso é útil se houver vários usuários para os pontos de entrada de serviço diferente e precisam toohave certos privilégios comuns que estão disponíveis no nível do grupo hello. Olá, exemplo a seguir mostra um grupo local chamado **LocalAdminGroup** que tenha privilégios de administrador. Dois usuários, Customer1 e Customer2, tornam-se membros desse grupo local.

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

### <a name="create-local-users"></a>Criar usuários locais
Você pode criar um serviço de aplicativo hello para um usuário local que pode ser usado toohelp segura. Quando um **UsuárioLocal** tipo de conta é especificado na seção de entidades de Olá Olá do manifesto do aplicativo, o Service Fabric cria contas de usuário local em computadores em que o aplicativo hello é implantado. Por padrão, essas contas não têm Olá mesmos nomes que as especificadas no aplicativo hello manifesto (por exemplo, Customer3 em Olá exemplo a seguir). Em vez disso, eles são gerados dinamicamente e têm senhas aleatórias.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Se um aplicativo requer que Olá conta de usuário e senha ser a mesma em todos os computadores (por exemplo, autenticação de NTLM tooenable), o manifesto do cluster Olá deve definir NTLMAuthenticationEnabled tootrue. Olá manifesto do cluster também deve especificar um NTLMAuthenticationPasswordSecret usado toogenerate Olá a mesma senha em todas as máquinas.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Atribuir políticas toohello pacotes de código de serviço
Olá **RunAsPolicy** seção um **servicemanifestimport ao** Especifica a conta de saudação da seção de entidades de saudação que deve ser usado toorun um pacote de códigos. Ele também associa o código de pacotes de serviço Olá manifesto com contas de usuário na seção de entidades de saudação. Você pode especificar isso para instalação hello ou pontos de entrada principal, ou você pode especificar `All` tooapply-tooboth. Olá, exemplo a seguir mostra políticas diferentes aplicadas:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Se **EntryPointType** não for especificado, o padrão de saudação será definido tooEntryPointType = "Principal". Especificando **SetupEntryPoint** é especialmente útil quando você deseja toorun determinadas operações de instalação com alto privilégio em uma conta do sistema. código de serviço real Olá pode ser executado sob uma conta com privilégios inferiores.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Aplicar um padrão política tooall serviço código pacotes
Use Olá **DefaultRunAsPolicy** seção toospecify uma conta de usuário padrão para todos os pacotes de código que não têm um determinado **RunAsPolicy** definido. Se a maioria dos pacotes de código Olá especificadas no manifesto do serviço Olá usado por um aplicativo precisar toorun em Olá mesmo usuário, hello aplicativo apenas pode definir uma política de executar como padrão com uma conta de usuário. Olá exemplo a seguir especifica que, se um pacote de códigos não tem um **RunAsPolicy** especificado, o pacote de códigos Olá deve ser executados Olá **MyDefaultAccount** especificado na seção de entidades de saudação.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Usar um usuário ou um grupo de domínio do Active Directory
Para uma instância do Service Fabric foi instalado no Windows Server usando o instalador autônomo do hello, você pode executar o serviço de saudação sob as credenciais de saudação para uma conta de usuário ou grupo do Active Directory. Esse é o Active Directory local em seu domínio e não é com o Azure Active Directory (Azure AD). Usando um usuário de domínio ou grupo, em seguida, você pode acessar outros recursos no domínio hello (por exemplo, compartilhamentos de arquivos) que foram concedidos permissões.

Olá, exemplo a seguir mostra um usuário do Active Directory chamado *TestUser* domínio senha criptografada usando um certificado chamado *MyCert*. Você pode usar o hello `Invoke-ServiceFabricEncryptText` texto do PowerShell comando toocreate Olá secreta de criptografia. Consulte [Gerenciamento de segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md) para obter detalhes.

Você deve implantar a chave privada Olá Olá certificado toodecrypt Olá senha toohello computador local usando um método fora de banda (no Azure, isso é por meio do Gerenciador de recursos do Azure). Em seguida, quando o Service Fabric implanta a máquina de toohello de pacote de serviço Olá, é capaz de toodecrypt Olá segredo e (junto com o nome de usuário de saudação) autenticar com toorun do Active Directory com essas credenciais.

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
### <a name="use-a-group-managed-service-account"></a>Use uma Conta de Serviço Gerenciado de Grupo.
Para uma instância do Service Fabric foi instalado no Windows Server usando o instalador autônomo do hello, você pode executar o serviço de saudação como um grupo de conta de serviço gerenciada (gMSA). Observe que esse é o Active Directory local em seu domínio e não é com o Azure AD (Active Directory). Usando uma gMSA não há nenhuma senha ou a senha criptografada armazenada no hello `Application Manifest`.

Olá exemplo a seguir mostra como toocreate uma conta gMSA chamado *svc teste$*; como toodeploy gerenciados nós de cluster de toohello de conta de serviço; e como tooconfigure Olá principal do usuário.

##### <a name="prerequisites"></a>Pré-requisitos.
- domínio Olá precisa de uma chave raiz KDS.
- domínio Olá precisa toobe em um Windows Server 2012 ou posterior nível funcional.

##### <a name="example"></a>Exemplo
1. Ter um administrador de domínio do active directory crie uma conta de serviço gerenciado de grupo usando Olá `New-ADServiceAccount` commandlet e certifique-se de que Olá `PrincipalsAllowedToRetrieveManagedPassword` inclui todos os nós do cluster Olá service fabric. Observe que `AccountName`, `DnsHostName` e `ServicePrincipalName` devem ser exclusivos.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Em cada um de nós de cluster de malha Olá serviço (por exemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instalar e testar Olá gMSA.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Configure o UPN Olá e usuário de Olá Olá RunAsPolicy tooreference.
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Atribuir uma política de acesso de segurança a pontos de extremidade HTTP e HTTPS
Se você aplicar um serviço de tooa RunAs política e o manifesto de serviço Olá declara recursos de ponto de extremidade com o protocolo de saudação HTTP, você deve especificar um **SecurityAccessPolicy** tooensure portas alocadas pontos de extremidade toothese estão corretamente controle de acesso listados para Olá conta de usuário RunAs Olá serviço é executado. Caso contrário, **http.sys** não tem acesso toohello serviço, e falhas de chamadas do cliente hello. Olá, exemplo a seguir aplica Olá Customer1 conta tooan ponto de extremidade chamado **EndpointName**, que concede direitos de acesso completo.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Ponto de extremidade de HTTPS hello, você também tem tooindicate nome de saudação do cliente do hello certificado tooreturn toohello. Você pode fazer isso usando **EndpointBindingPolicy**, com certificado Olá definido em uma seção de certificados no manifesto de aplicativo hello.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Atualizando vários aplicativos com pontos de extremidade https
Você precisa toobe cuidado não toouse Olá **mesma porta** para instâncias diferentes do hello aplicativo mesmo quando usando http**s**. motivo da saudação é que Service Fabric não será capaz de tooupgrade cert de Olá para uma das instâncias de aplicativo hello. Por exemplo, se quiser que o aplicativo 1 ou aplicativo 2 ambos os tooupgrade seu toocert cert 1 2. Quando ocorrer a atualização do hello, Service Fabric podem apagadas registro de certificado 1 Olá com HTTP. sys, embora hello outro aplicativo está ainda usá-lo. tooprevent, Service Fabric detecta que já há outra instância do aplicativo registrada na porta Olá com certificado hello (vencimento toohttp.sys) e haverá falha na operação de hello.

Portanto, Service Fabric não suporta atualização a dois serviços diferentes usando **Olá a mesma porta** em instâncias de aplicativo diferente. Em outras palavras, você não pode usar o mesmo certificado de saudação em diferentes serviços em hello mesma porta. Se você precisar toohave compartilhado de certificado na Olá mesmo porta, você precisa tooensure que Olá serviços são colocados em máquinas diferentes com restrições de posicionamento. Ou, considere o uso de portas dinâmicas do Service Fabric, se possível, para cada serviço em cada instância do aplicativo. 

Se você vir uma atualização falha com https, um aviso de erro dizendo "Olá Windows HTTP Server API não suporta vários certificados para aplicativos que compartilham uma porta."

## <a name="a-complete-application-manifest-example"></a>Um exemplo completo de manifesto do aplicativo
saudação de manifesto do aplicativo a seguir mostra a muitos dos Olá diferentes configurações:

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
## <a name="next-steps"></a>Próximas etapas
* [Entender o modelo de aplicativo hello](service-fabric-application-model.md)
* [Especificar recursos em um manifesto do serviço](service-fabric-service-manifest-resources.md)
* [Implantar um aplicativo](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
