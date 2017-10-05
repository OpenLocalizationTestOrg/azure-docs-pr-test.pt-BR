---
title: Gerenciamento de segredos em aplicativos do Service Fabric | Microsoft Docs
description: Este artigo descreve como proteger os valores do segredo em um aplicativo do Service Fabric.
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
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="37adb-103">Gerenciamento de segredos em aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="37adb-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="37adb-104">Este guia explica as etapas do gerenciamento de segredos em um aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="37adb-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="37adb-105">Os segredos podem ser informações confidenciais, como cadeias de conexão de armazenamento, senhas ou outros valores que não devem ser tratados como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="37adb-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="37adb-106">Este guia usa o Cofre de Chaves do Azure para gerenciar chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="37adb-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="37adb-107">No entanto, o *uso* de segredos em um aplicativo é independente de plataforma de nuvem para permitir que os aplicativos sejam implantados em um cluster hospedado em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="37adb-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="37adb-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="37adb-108">Overview</span></span>
<span data-ttu-id="37adb-109">A maneira recomendada de gerenciar as definições de configuração de serviço é por meio de [pacotes de configuração de serviço][config-package].</span><span class="sxs-lookup"><span data-stu-id="37adb-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="37adb-110">Os pacotes de configuração são atualizáveis e têm controle de versão por meio de atualizações sem interrupção gerenciadas com reversão automática e validação de integridade.</span><span class="sxs-lookup"><span data-stu-id="37adb-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="37adb-111">Isso é preferível à configuração global, pois reduz as chances de uma interrupção de serviços globais.</span><span class="sxs-lookup"><span data-stu-id="37adb-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="37adb-112">Segredos criptografados não são exceção.</span><span class="sxs-lookup"><span data-stu-id="37adb-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="37adb-113">O Service Fabric tem recursos internos para criptografar e descriptografar valores em um arquivo Settings.XML do pacote de configuração usando a criptografia de certificado.</span><span class="sxs-lookup"><span data-stu-id="37adb-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="37adb-114">O diagrama a seguir ilustra o fluxo básico para gerenciamento de segredos em um aplicativo do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="37adb-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![visão geral do gerenciamento de segredos][overview]

<span data-ttu-id="37adb-116">Há quatro etapas principais nesse fluxo:</span><span class="sxs-lookup"><span data-stu-id="37adb-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="37adb-117">Obtenha um certificado de codificação de dados.</span><span class="sxs-lookup"><span data-stu-id="37adb-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="37adb-118">Instale o certificado em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="37adb-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="37adb-119">Criptografe valores do segredo ao implantar um aplicativo com o certificado e coloque-os no arquivo de configuração Settings.xml de um serviço.</span><span class="sxs-lookup"><span data-stu-id="37adb-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="37adb-120">Leia os valores criptografados de Settings.xml ao descriptografar com o mesmo certificado de codificação.</span><span class="sxs-lookup"><span data-stu-id="37adb-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="37adb-121">O [Azure Key Vault][key-vault-get-started] é usado aqui como um local de armazenamento seguro para certificados e como uma maneira de obter certificados instalados em clusters do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="37adb-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="37adb-122">Se não estiver implantando no Azure, você não precisará usar o cofre de chaves para gerenciar segredos em aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="37adb-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="37adb-123">Certificado de codificação de dados</span><span class="sxs-lookup"><span data-stu-id="37adb-123">Data encipherment certificate</span></span>
<span data-ttu-id="37adb-124">Um certificado de codificação de dados é usado estritamente para criptografia e descriptografia de valores de configuração no arquivo Settings.xml de um serviço e não é usado para autenticação nem assinatura do texto da criptografia.</span><span class="sxs-lookup"><span data-stu-id="37adb-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="37adb-125">O certificado deve atender aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="37adb-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="37adb-126">O certificado deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="37adb-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="37adb-127">O certificado deve ser criado para troca de chaves, exportável para um arquivo Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="37adb-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="37adb-128">O uso da chave de certificado deve incluir a Codificação de Dados (10) e não deve incluir a Autenticação de Servidor ou de Cliente.</span><span class="sxs-lookup"><span data-stu-id="37adb-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="37adb-129">Por exemplo, ao criar um certificado autoassinado usando o PowerShell, o sinalizador `KeyUsage` deverá ser definido como `DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="37adb-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="37adb-130">Instalar o certificado em seu cluster</span><span class="sxs-lookup"><span data-stu-id="37adb-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="37adb-131">Esse certificado deve ser instalado em cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="37adb-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="37adb-132">Ele será usado em tempo de execução para descriptografar valores armazenados no arquivo Settings.xml de um serviço.</span><span class="sxs-lookup"><span data-stu-id="37adb-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="37adb-133">Veja [como criar um cluster usando o Azure Resource Manager][service-fabric-cluster-creation-via-arm] para obter instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="37adb-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="37adb-134">Criptografar segredos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="37adb-134">Encrypt application secrets</span></span>
<span data-ttu-id="37adb-135">O SDK do Service Fabric tem funções internas de criptografia e descriptografia de segredos.</span><span class="sxs-lookup"><span data-stu-id="37adb-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="37adb-136">Os valores secretos podem ser criptografados em tempo de compilação e então descriptografados e lidos programaticamente no código de serviço.</span><span class="sxs-lookup"><span data-stu-id="37adb-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="37adb-137">O comando do PowerShell a seguir é usado para criptografar um segredo.</span><span class="sxs-lookup"><span data-stu-id="37adb-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="37adb-138">Esse comando só criptografa o valor; ele **não** assina o texto da criptografia.</span><span class="sxs-lookup"><span data-stu-id="37adb-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="37adb-139">Você deve usar o mesmo certificado de codificação instalado no seu cluster para produzir texto cifrado para valores do segredo:</span><span class="sxs-lookup"><span data-stu-id="37adb-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="37adb-140">A cadeia de caracteres de base 64 resultante contém tanto o texto cifrado secreto como informações sobre o certificado usado para criptografá-lo.</span><span class="sxs-lookup"><span data-stu-id="37adb-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="37adb-141">A cadeia de caracteres codificada em base 64 pode ser inserida em um parâmetro no arquivo de configuração Settings.xml do seu serviço com o atributo `IsEncrypted` definido como `true`:</span><span class="sxs-lookup"><span data-stu-id="37adb-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="37adb-142">Inserir segredos do aplicativo em instâncias do aplicativo</span><span class="sxs-lookup"><span data-stu-id="37adb-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="37adb-143">Idealmente, a implantação em ambientes diferentes deve ser mais automatizada possível.</span><span class="sxs-lookup"><span data-stu-id="37adb-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="37adb-144">Isso pode ser feito executando a criptografia secreta em um ambiente de compilação e fornecendo os segredos criptografados como parâmetros durante a criação de instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37adb-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="37adb-145">Usar parâmetros substituíveis em Settings.xml</span><span class="sxs-lookup"><span data-stu-id="37adb-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="37adb-146">O arquivo de configuração de Settings.xml permite a existência de parâmetros substituíveis que podem ser fornecidos no momento da criação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="37adb-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="37adb-147">Use o atributo `MustOverride` em vez de fornecer um valor para um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="37adb-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="37adb-148">Para substituir valores em Settings.xml, declare um parâmetro de substituição para o serviço em ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="37adb-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="37adb-149">Agora, o valor pode ser especificado como um *parâmetro de aplicativo* ao criar uma instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37adb-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="37adb-150">A criação de uma instância do aplicativo pode ser controlada por script usando o PowerShell, ou escrita em C#, para fácil integração em um processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="37adb-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="37adb-151">Usando o PowerShell, o parâmetro é fornecido para o comando `New-ServiceFabricApplication` como uma [tabela de hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="37adb-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="37adb-152">Usando C#, os parâmetros do aplicativo são especificados em um `ApplicationDescription` como um `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="37adb-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="37adb-153">Descriptografar segredos de código de serviço</span><span class="sxs-lookup"><span data-stu-id="37adb-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="37adb-154">Os serviços do Service Fabric são executados em NETWORK SERVICE por padrão no Windows e não têm acesso a certificados instalados no nó sem alguma configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="37adb-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="37adb-155">Ao usar um certificado de codificação de dados, você precisa certificar-se de que NETWORK SERVICE ou qualquer conta sob a qual o serviço esteja sendo executado terá acesso à chave privada do certificado.</span><span class="sxs-lookup"><span data-stu-id="37adb-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="37adb-156">O Service Fabric tratará da concessão de acesso para seu serviço de forma automática caso você o configure para isso.</span><span class="sxs-lookup"><span data-stu-id="37adb-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="37adb-157">Essa configuração pode ser feita em ApplicationManifest.xml por meio da definição de políticas de usuários e de segurança para certificados.</span><span class="sxs-lookup"><span data-stu-id="37adb-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="37adb-158">No exemplo a seguir, a conta NETWORK SERVICE obtém acesso de leitura para um certificado definido por sua impressão digital:</span><span class="sxs-lookup"><span data-stu-id="37adb-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="37adb-159">Ao copiar uma impressão digital do certificado do snap-in de armazenamento de certificado no Windows, um caractere invisível é colocado no início da cadeia de caracteres de impressão digital.</span><span class="sxs-lookup"><span data-stu-id="37adb-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="37adb-160">Esse caractere invisível pode causar um erro ao tentar localizar um certificado por impressão digital, portanto exclua esse caractere extra.</span><span class="sxs-lookup"><span data-stu-id="37adb-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="37adb-161">Use os segredos do aplicativo no código de serviço</span><span class="sxs-lookup"><span data-stu-id="37adb-161">Use application secrets in service code</span></span>
<span data-ttu-id="37adb-162">A API para acessar valores de configuração de Settings.xml em um pacote de configuração permite fácil descriptografia de valores que têm o `IsEncrypted` atributo definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="37adb-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="37adb-163">Como o texto criptografado contém informações sobre o certificado usado para criptografia, você não precisa encontrar o certificado manualmente.</span><span class="sxs-lookup"><span data-stu-id="37adb-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="37adb-164">Apenas o certificado deve ser instalado no nó que o serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="37adb-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="37adb-165">Basta chamar o `DecryptValue()` método para recuperar o valor do segredo original:</span><span class="sxs-lookup"><span data-stu-id="37adb-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="37adb-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37adb-166">Next Steps</span></span>
<span data-ttu-id="37adb-167">Saiba mais sobre [executar aplicativos com permissões de segurança diferentes](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="37adb-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
