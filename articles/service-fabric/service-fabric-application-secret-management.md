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
# <a name="managing-secrets-in-service-fabric-applications"></a>Gerenciamento de segredos em aplicativos do Service Fabric
Este guia aborda etapas de saudação do gerenciamento de segredos em um aplicativo de malha do serviço. Os segredos podem ser informações confidenciais, como cadeias de conexão de armazenamento, senhas ou outros valores que não devem ser tratados como texto sem formatação.

Este guia usa os segredos e chaves do Azure Key Vault toomanage. No entanto, *usando* segredos em um aplicativo é implantado tooa cluster em nuvem independente de plataforma tooallow aplicativos toobe hospedados em qualquer lugar. 

## <a name="overview"></a>Visão geral
Olá definições de configuração do serviço de toomanage de maneira recomendada é por meio de [pacotes de configuração de serviço][config-package]. Os pacotes de configuração são atualizáveis e têm controle de versão por meio de atualizações sem interrupção gerenciadas com reversão automática e validação de integridade. Isso é configuração tooglobal preferencial, pois reduz as chances de saudação de uma interrupção do serviço global. Segredos criptografados não são exceção. O Service Fabric tem recursos internos para criptografar e descriptografar valores em um arquivo Settings.XML do pacote de configuração usando a criptografia de certificado.

Olá seguinte diagrama ilustra fluxo básico de saudação para gerenciamento de informações secretas em um aplicativo de malha do serviço:

![visão geral do gerenciamento de segredos][overview]

Há quatro etapas principais nesse fluxo:

1. Obtenha um certificado de codificação de dados.
2. Instale o certificado de saudação em seu cluster.
3. Criptografar segredos valores ao implantar um aplicativo com o certificado de saudação e colocá-los no arquivo de configuração do serviço Settings.xml.
4. Valores de leitura criptografado fora Settings.xml Descriptografando com hello mesmo certificado de codificação. 

[Cofre de chaves do Azure] [ key-vault-get-started] é usado aqui como um local de armazenamento seguro de certificados e como uma maneira tooget certificados instalados em clusters de malha do serviço no Azure. Se você não está implantando tooAzure, não é necessário segredos de toomanage toouse Cofre de chaves em aplicativos do Service Fabric.

## <a name="data-encipherment-certificate"></a>Certificado de codificação de dados
Um certificado de codificação de dados é usado estritamente para criptografia e descriptografia de valores de configuração no arquivo Settings.xml de um serviço e não é usado para autenticação nem assinatura do texto da criptografia. certificado Olá deve atender aos Olá requisitos a seguir:

* certificado de saudação deve conter uma chave privada.
* certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).
* uso de chave de certificado Olá deve incluir a codificação de dados (10) e não deve incluir a autenticação de servidor ou autenticação de cliente. 
  
  Por exemplo, ao criar um certificado autoassinado usando o PowerShell, Olá `KeyUsage` sinalizador deve ser definido muito`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Instalar o certificado de saudação do cluster
Esse certificado deve ser instalado em cada nó no cluster hello. Ele será usado em tempo de execução toodecrypt valores armazenados em Settings.xml do serviço. Consulte [como toocreate um cluster usando o Gerenciador de recursos do Azure] [ service-fabric-cluster-creation-via-arm] para obter instruções de instalação. 

## <a name="encrypt-application-secrets"></a>Criptografar segredos do aplicativo
Olá SDK do Service Fabric tem funções internas de criptografia e descriptografia segredas. Os valores secretos podem ser criptografados em tempo de compilação e então descriptografados e lidos programaticamente no código de serviço. 

saudação de comando do PowerShell a seguir é usado tooencrypt um segredo. Esse comando criptografa apenas o valor de saudação; ele faz **não** entrar texto cifrado de saudação. Você deve usar o hello mesmo certificado de codificação que é instalado em seu texto cifrado tooproduce de cluster para valores de segredo:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Olá cadeia de caracteres de base 64 resultante contém texto cifrado de segredo Olá bem como informações sobre Olá certificado que foi usado tooencrypt-lo.  Olá codificado em base 64 de cadeia de caracteres pode ser inserida em um parâmetro no arquivo de configuração do serviço Settings.xml com hello `IsEncrypted` atributo definido muito`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Inserir segredos do aplicativo em instâncias do aplicativo
Idealmente, ambientes de implantação de toodifferent devem ser automatizados como possível. Isso pode ser feito executando criptografia secreta em um ambiente de compilação e fornecendo segredos Olá criptografado como parâmetros durante a criação de instâncias do aplicativo.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Usar parâmetros substituíveis em Settings.xml
arquivo de configuração do Hello Settings.xml permite que os parâmetros substituíveis que podem ser fornecidos no momento da criação de aplicativos. Saudação de uso `MustOverride` atributo em vez de fornecer um valor para um parâmetro:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

valores de toooverride em Settings.xml, declarar um parâmetro de substituição para o serviço de saudação applicationmanifest.XML:

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

Agora Olá valor pode ser especificado como um *parâmetro aplicativo* durante a criação de uma instância do aplicativo hello. A criação de uma instância do aplicativo pode ser controlada por script usando o PowerShell, ou escrita em C#, para fácil integração em um processo de compilação.

Usando o PowerShell, o parâmetro hello é fornecido toohello `New-ServiceFabricApplication` comando como um [tabela de hash](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Usando C#, os parâmetros do aplicativo são especificados em um `ApplicationDescription` como um `NameValueCollection`:

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

## <a name="decrypt-secrets-from-service-code"></a>Descriptografar segredos de código de serviço
Os serviços do Service Fabric executados sob o serviço de rede por padrão no Windows e não têm acesso toocertificates instalado no nó de saudação sem alguma configuração adicional.

Ao usar um certificado de codificação de dados, você precisa toomake se o serviço de rede ou qualquer serviço de saudação de conta de usuário está em execução em tem chave privada do certificado de acesso toohello. Service Fabric tratará a concessão de acesso para o serviço automaticamente se você configurá-lo toodo assim. Essa configuração pode ser feita em ApplicationManifest.xml por meio da definição de políticas de usuários e de segurança para certificados. Saudação de exemplo a seguir, Olá conta de serviço de rede recebe acesso de leitura tooa certificado definido por sua impressão digital:

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
> Ao copiar uma impressão digital do certificado do certificado Olá armazenar snap-in no Windows, um caractere invisível é colocado no início de saudação da cadeia de caracteres de impressão digital de saudação. Esse caractere invisível pode causar um erro durante a tentativa de toolocate um certificado pela impressão digital, tão ser toodelete-se de que esse caractere extra.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Use os segredos do aplicativo no código de serviço
Olá API para acessar valores de configuração de Settings. XML em um pacote de configuração permite a fácil descriptografia de valores que têm Olá `IsEncrypted` atributo definido muito`true`. Como texto de saudação criptografado contém informações sobre Olá certificado usado para criptografia, certificados de saudação localizar toomanually não é necessário. certificado Olá precisa apenas toobe instalado no nó Olá Olá serviço está em execução. Basta chamar hello `DecryptValue()` método tooretrieve Olá secreta valor original:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [executar aplicativos com permissões de segurança diferentes](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
