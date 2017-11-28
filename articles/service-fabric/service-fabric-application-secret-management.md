---
title: aaaManaging segredos em aplicativos do Service Fabric | Microsoft Docs
description: "Este artigo descreve como o segredo toosecure valores em um aplicativo de malha do serviço."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="affc9-103">Gerenciamento de segredos em aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="affc9-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="affc9-104">Este guia aborda etapas de saudação do gerenciamento de segredos em um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="affc9-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="affc9-105">Os segredos podem ser informações confidenciais, como cadeias de conexão de armazenamento, senhas ou outros valores que não devem ser tratados como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="affc9-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="affc9-106">Este guia usa os segredos e chaves do Azure Key Vault toomanage.</span><span class="sxs-lookup"><span data-stu-id="affc9-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="affc9-107">No entanto, *usando* segredos em um aplicativo é implantado tooa cluster em nuvem independente de plataforma tooallow aplicativos toobe hospedados em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="affc9-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="affc9-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="affc9-108">Overview</span></span>
<span data-ttu-id="affc9-109">Olá definições de configuração do serviço de toomanage de maneira recomendada é por meio de [pacotes de configuração de serviço][config-package].</span><span class="sxs-lookup"><span data-stu-id="affc9-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="affc9-110">Os pacotes de configuração são atualizáveis e têm controle de versão por meio de atualizações sem interrupção gerenciadas com reversão automática e validação de integridade.</span><span class="sxs-lookup"><span data-stu-id="affc9-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="affc9-111">Isso é configuração tooglobal preferencial, pois reduz as chances de saudação de uma interrupção do serviço global.</span><span class="sxs-lookup"><span data-stu-id="affc9-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="affc9-112">Segredos criptografados não são exceção.</span><span class="sxs-lookup"><span data-stu-id="affc9-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="affc9-113">O Service Fabric tem recursos internos para criptografar e descriptografar valores em um arquivo Settings.XML do pacote de configuração usando a criptografia de certificado.</span><span class="sxs-lookup"><span data-stu-id="affc9-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="affc9-114">Olá seguinte diagrama ilustra fluxo básico de saudação para gerenciamento de informações secretas em um aplicativo de malha do serviço:</span><span class="sxs-lookup"><span data-stu-id="affc9-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![visão geral do gerenciamento de segredos][overview]

<span data-ttu-id="affc9-116">Há quatro etapas principais nesse fluxo:</span><span class="sxs-lookup"><span data-stu-id="affc9-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="affc9-117">Obtenha um certificado de codificação de dados.</span><span class="sxs-lookup"><span data-stu-id="affc9-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="affc9-118">Instale o certificado de saudação em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="affc9-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="affc9-119">Criptografar segredos valores ao implantar um aplicativo com o certificado de saudação e colocá-los no arquivo de configuração do serviço Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="affc9-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="affc9-120">Valores de leitura criptografado fora Settings.xml Descriptografando com hello mesmo certificado de codificação.</span><span class="sxs-lookup"><span data-stu-id="affc9-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="affc9-121">[Cofre de chaves do Azure] [ key-vault-get-started] é usado aqui como um local de armazenamento seguro de certificados e como uma maneira tooget certificados instalados em clusters de malha do serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="affc9-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="affc9-122">Se você não está implantando tooAzure, não é necessário segredos de toomanage toouse Cofre de chaves em aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="affc9-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="affc9-123">Certificado de codificação de dados</span><span class="sxs-lookup"><span data-stu-id="affc9-123">Data encipherment certificate</span></span>
<span data-ttu-id="affc9-124">Um certificado de codificação de dados é usado estritamente para criptografia e descriptografia de valores de configuração no arquivo Settings.xml de um serviço e não é usado para autenticação nem assinatura do texto da criptografia.</span><span class="sxs-lookup"><span data-stu-id="affc9-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="affc9-125">certificado Olá deve atender aos Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="affc9-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="affc9-126">certificado de saudação deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="affc9-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="affc9-127">certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).</span><span class="sxs-lookup"><span data-stu-id="affc9-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="affc9-128">uso de chave de certificado Olá deve incluir a codificação de dados (10) e não deve incluir a autenticação de servidor ou autenticação de cliente.</span><span class="sxs-lookup"><span data-stu-id="affc9-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="affc9-129">Por exemplo, ao criar um certificado autoassinado usando o PowerShell, Olá `KeyUsage` sinalizador deve ser definido muito`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="affc9-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="affc9-130">Instalar o certificado de saudação do cluster</span><span class="sxs-lookup"><span data-stu-id="affc9-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="affc9-131">Esse certificado deve ser instalado em cada nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="affc9-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="affc9-132">Ele será usado em tempo de execução toodecrypt valores armazenados em Settings.xml do serviço.</span><span class="sxs-lookup"><span data-stu-id="affc9-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="affc9-133">Consulte [como toocreate um cluster usando o Gerenciador de recursos do Azure] [ service-fabric-cluster-creation-via-arm] para obter instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="affc9-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="affc9-134">Criptografar segredos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="affc9-134">Encrypt application secrets</span></span>
<span data-ttu-id="affc9-135">Olá SDK do Service Fabric tem funções internas de criptografia e descriptografia segredas.</span><span class="sxs-lookup"><span data-stu-id="affc9-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="affc9-136">Os valores secretos podem ser criptografados em tempo de compilação e então descriptografados e lidos programaticamente no código de serviço.</span><span class="sxs-lookup"><span data-stu-id="affc9-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="affc9-137">saudação de comando do PowerShell a seguir é usado tooencrypt um segredo.</span><span class="sxs-lookup"><span data-stu-id="affc9-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="affc9-138">Esse comando criptografa apenas o valor de saudação; ele faz **não** entrar texto cifrado de saudação.</span><span class="sxs-lookup"><span data-stu-id="affc9-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="affc9-139">Você deve usar o hello mesmo certificado de codificação que é instalado em seu texto cifrado tooproduce de cluster para valores de segredo:</span><span class="sxs-lookup"><span data-stu-id="affc9-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="affc9-140">Olá cadeia de caracteres de base 64 resultante contém texto cifrado de segredo Olá bem como informações sobre Olá certificado que foi usado tooencrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="affc9-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="affc9-141">Olá codificado em base 64 de cadeia de caracteres pode ser inserida em um parâmetro no arquivo de configuração do serviço Settings.xml com hello `IsEncrypted` atributo definido muito`true`:</span><span class="sxs-lookup"><span data-stu-id="affc9-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="affc9-142">Inserir segredos do aplicativo em instâncias do aplicativo</span><span class="sxs-lookup"><span data-stu-id="affc9-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="affc9-143">Idealmente, ambientes de implantação de toodifferent devem ser automatizados como possível.</span><span class="sxs-lookup"><span data-stu-id="affc9-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="affc9-144">Isso pode ser feito executando criptografia secreta em um ambiente de compilação e fornecendo segredos Olá criptografado como parâmetros durante a criação de instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="affc9-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="affc9-145">Usar parâmetros substituíveis em Settings.xml</span><span class="sxs-lookup"><span data-stu-id="affc9-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="affc9-146">arquivo de configuração do Hello Settings.xml permite que os parâmetros substituíveis que podem ser fornecidos no momento da criação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="affc9-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="affc9-147">Saudação de uso `MustOverride` atributo em vez de fornecer um valor para um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="affc9-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="affc9-148">valores de toooverride em Settings.xml, declarar um parâmetro de substituição para o serviço de saudação applicationmanifest.XML:</span><span class="sxs-lookup"><span data-stu-id="affc9-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="affc9-149">Agora Olá valor pode ser especificado como um *parâmetro aplicativo* durante a criação de uma instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="affc9-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="affc9-150">A criação de uma instância do aplicativo pode ser controlada por script usando o PowerShell, ou escrita em C#, para fácil integração em um processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="affc9-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="affc9-151">Usando o PowerShell, o parâmetro hello é fornecido toohello `New-ServiceFabricApplication` comando como um [tabela de hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="affc9-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="affc9-152">Usando C#, os parâmetros do aplicativo são especificados em um `ApplicationDescription` como um `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="affc9-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="affc9-153">Descriptografar segredos de código de serviço</span><span class="sxs-lookup"><span data-stu-id="affc9-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="affc9-154">Os serviços do Service Fabric executados sob o serviço de rede por padrão no Windows e não têm acesso toocertificates instalado no nó de saudação sem alguma configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="affc9-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="affc9-155">Ao usar um certificado de codificação de dados, você precisa toomake se o serviço de rede ou qualquer serviço de saudação de conta de usuário está em execução em tem chave privada do certificado de acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="affc9-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="affc9-156">Service Fabric tratará a concessão de acesso para o serviço automaticamente se você configurá-lo toodo assim.</span><span class="sxs-lookup"><span data-stu-id="affc9-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="affc9-157">Essa configuração pode ser feita em ApplicationManifest.xml por meio da definição de políticas de usuários e de segurança para certificados.</span><span class="sxs-lookup"><span data-stu-id="affc9-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="affc9-158">Saudação de exemplo a seguir, Olá conta de serviço de rede recebe acesso de leitura tooa certificado definido por sua impressão digital:</span><span class="sxs-lookup"><span data-stu-id="affc9-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="affc9-159">Ao copiar uma impressão digital do certificado do certificado Olá armazenar snap-in no Windows, um caractere invisível é colocado no início de saudação da cadeia de caracteres de impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="affc9-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="affc9-160">Esse caractere invisível pode causar um erro durante a tentativa de toolocate um certificado pela impressão digital, tão ser toodelete-se de que esse caractere extra.</span><span class="sxs-lookup"><span data-stu-id="affc9-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="affc9-161">Use os segredos do aplicativo no código de serviço</span><span class="sxs-lookup"><span data-stu-id="affc9-161">Use application secrets in service code</span></span>
<span data-ttu-id="affc9-162">Olá API para acessar valores de configuração de Settings. XML em um pacote de configuração permite a fácil descriptografia de valores que têm Olá `IsEncrypted` atributo definido muito`true`.</span><span class="sxs-lookup"><span data-stu-id="affc9-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="affc9-163">Como texto de saudação criptografado contém informações sobre Olá certificado usado para criptografia, certificados de saudação localizar toomanually não é necessário.</span><span class="sxs-lookup"><span data-stu-id="affc9-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="affc9-164">certificado Olá precisa apenas toobe instalado no nó Olá Olá serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="affc9-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="affc9-165">Basta chamar hello `DecryptValue()` método tooretrieve Olá secreta valor original:</span><span class="sxs-lookup"><span data-stu-id="affc9-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="affc9-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="affc9-166">Next Steps</span></span>
<span data-ttu-id="affc9-167">Saiba mais sobre [executar aplicativos com permissões de segurança diferentes](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="affc9-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
