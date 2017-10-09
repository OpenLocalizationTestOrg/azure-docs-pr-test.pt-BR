---
title: "aaaAzure segurança de contêiner do Service Fabric | Microsoft Docs"
description: "Saiba mais serviços de contêiner toosecure agora."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Segurança do contêiner

Serviço de malha fornece um mecanismo para serviços dentro de um contêiner tooaccess um certificado que é instalado em nós de saudação em um cluster do Windows ou Linux (versão 5.7 ou superior). Além disso, o Service Fabric também dá suporte a gMSA (Contas de Serviço Gerenciado do grupo) para contêineres do Windows. 

## <a name="certificate-management-for-containers"></a>Gerenciamento de certificados para contêineres

Você pode proteger seus serviços de contêiner especificando um certificado. certificado de saudação deve ser instalado em nós de saudação do cluster de saudação. Olá informações do certificado são fornecidas no manifesto de aplicativo hello em Olá `ContainerHostPolicies` marca como Olá trecho a seguir mostra:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Ao iniciar o aplicativo hello, o tempo de execução de saudação lê certificados hello e gera um arquivo PFX e senha para cada certificado. Este arquivo PFX e senha são acessíveis dentro do contêiner hello usando Olá variáveis de ambiente a seguir: 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

Olá contêiner serviço ou processo é responsável para importar o arquivo PFX de saudação para contêiner hello. certificado de saudação tooimport, você pode usar `setupentrypoint.sh` da execução de código personalizado no processo do contêiner de saudação ou scripts. Código de exemplo em c# para importar o arquivo PFX de saudação segue:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Esse certificado PFX pode ser usado para o aplicativo hello de autenticar ou serviço ou commmunication segura com outros serviços.


## <a name="set-up-gmsa-for-windows-containers"></a>Configurar o gMSA para contêineres do Windows

tooset a gMSA (grupo de contas de serviço gerenciado), um arquivo de especificação de credencial (`credspec`) é colocado em todos os nós no cluster de saudação. arquivo Hello pode ser copiado em todos os nós usando uma extensão de VM.  Olá `credspec` arquivo deve conter informações da conta gMSA hello. Para obter mais informações sobre Olá `credspec` de arquivos, consulte [contas de serviço](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). especificação de credencial Hello e hello `Hostname` marca são especificadas no manifesto de aplicativo hello. Olá `Hostname` marca deve corresponder o nome da conta gMSA Olá que Olá é executado de contêiner com.  Olá `Hostname` marca permite Olá tooauthenticate de contêiner em si tooother serviços no domínio hello usando a autenticação Kerberos.  Um exemplo para especificar Olá `Hostname` e hello `credspec` Olá manifesto do aplicativo é mostrado em Olá trecho de código a seguir:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Próximas etapas

* [Implantar um contêiner de Windows tooService malha no Windows Server 2016](service-fabric-get-started-containers.md)
* [Implantar um contêiner de Docker tooService malha no Linux](service-fabric-get-started-containers-linux.md)
