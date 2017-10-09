---
title: "aaaSecure uma malha do Azure serviço de cluster no Windows usando certificados | Microsoft Docs"
description: "Este artigo descreve como toosecure comunicação dentro Olá autônomo ou privada cluster bem como entre clientes e o cluster de saudação."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Proteger um cluster autônomo no Windows usando os certificados X.509
Este artigo descreve como a comunicação entre Olá toosecure Olá vários nós de cluster do Windows autônoma, assim como tooauthenticate os clientes conectados toothis cluster, usando certificados x. 509. Isso garante que somente usuários autorizados possam acessar o cluster de Olá Olá aplicativos implantados e executar tarefas de gerenciamento.  Segurança de certificado deve ser habilitada no cluster hello quando Olá cluster é criado.  

Para obter mais informações sobre segurança de cluster, como nós de segurança, segurança de nó de cliente e controle de acesso baseado em função, confira [Cenários de segurança de cluster](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>De quais certificados você precisará?
toostart, [baixar pacote de cluster autônomo Olá](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nós de saudação do cluster. Em Olá baixado o pacote, você encontrará um **ClusterConfig.X509.MultiMachine.json** arquivo. Abra o arquivo hello e examine a seção Olá para **segurança** em Olá **propriedades** seção:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

Esta seção descreve os certificados de saudação que é necessário para proteger o cluster do Windows autônoma. Se você estiver especificando um certificado de cluster, defina o valor de saudação do **ClusterCredentialType** too_**X509**_. Se você estiver especificando o certificado do servidor para conexões externas, defina Olá **ServerCredentialType** muito_**X509**_. Embora não seja obrigatório, é recomendável toohave ambos esses certificados para um cluster protegido adequadamente. Se você definir esses valores muito*X509* , em seguida, você também deve especificar Olá certificados correspondentes ou do Service Fabric lançará uma exceção. Em alguns cenários, convém apenas Olá toospecify _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Nesses cenários, você não precisa definir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.


> [!NOTE]
> Um [impressão digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) é Olá a identidade primária de um certificado. Leitura [como impressão digital de um certificado do tooretrieve](https://msdn.microsoft.com/library/ms734695.aspx) toofind out impressão digital de saudação de certificados de saudação que você criar.
> 
> 

Olá tabela a seguir lista os certificados de saudação necessários na sua configuração de cluster:

| **Configuração de CertificateInformation** | **Descrição** |
| --- | --- |
| ClusterCertificate |Recomendado para o ambiente de teste. Esse certificado é toosecure necessário Olá comunicação entre os nós de saudação em um cluster. Você pode usar dois certificados diferentes, um principal e um secundário para atualização. Definir a impressão digital de saudação do certificado principal Olá no hello **impressão digital** seção e que Olá secundário no hello **ThumbprintSecondary** variáveis. |
| ClusterCertificateCommonNames |Recomendado para o ambiente de produção. Esse certificado é toosecure necessário Olá comunicação entre os nós de saudação em um cluster. Você pode usar um ou dois nomes comuns de certificado de cluster. |
| ServerCertificate |Recomendado para o ambiente de teste. Esse certificado é apresentado toohello cliente quando ele tenta tooconnect toothis cluster. Para sua conveniência, você pode escolher toouse Olá mesmo certificado para *ClusterCertificate* e *ServerCertificate*. Você pode usar dois certificados de servidor diferentes, um principal e um secundário, para atualização. Definir a impressão digital de saudação do certificado principal Olá no hello **impressão digital** seção e que Olá secundário no hello **ThumbprintSecondary** variáveis. |
| ServerCertificateCommonNames |Recomendado para o ambiente de produção. Esse certificado é apresentado toohello cliente quando ele tenta tooconnect toothis cluster. Para sua conveniência, você pode escolher toouse Olá mesmo certificado para *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*. Você pode usar um ou dois nomes comuns de certificado. |
| ClientCertificateThumbprints |Este é um conjunto de certificados que você deseja tooinstall em clientes Olá autenticado. Você pode ter um número diferente de certificados de cliente instalado nos computadores de saudação que você deseja que o cluster de toohello tooallow acesso. Definir a impressão digital de saudação de cada certificado em Olá **CertificateThumbprint** variável. Se você definir Olá **IsAdmin** muito*true*, e em seguida, cliente Olá com esse certificado instalado pode fazer administrador atividades de gerenciamento de cluster de saudação. Se hello **IsAdmin** é *false*, cliente Olá com esse certificado só pode executar ações de saudação permitidas para direitos de acesso do usuário, normalmente somente leitura. Para obter mais informações sobre funções, leia [RBAC (controle de acesso baseado em função)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Conjunto Olá nome comum do certificado de cliente primeiro Olá Olá **CertificateCommonName**. Olá **CertificateIssuerThumbprint** é a impressão digital de saudação para emissor Olá deste certificado. Leitura [trabalhar com certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow mais sobre nomes comuns e emissor hello. |
| ReverseProxyCertificate |Recomendado para o ambiente de teste. Este é um certificado opcional que pode ser especificado se você quiser toosecure seu [Proxy Inverter](service-fabric-reverseproxy.md). Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado. |
| ReverseProxyCertificateCommonNames |Recomendado para o ambiente de produção. Este é um certificado opcional que pode ser especificado se você quiser toosecure seu [Proxy Inverter](service-fabric-reverseproxy.md). Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado. |

Aqui está o exemplo de configuração de cluster onde os certificados de Cluster de servidor e cliente Olá foram fornecidos. Observe que, para cluster / server / certificados reverseProxy, impressão digital e o nome comum não são permitidas toobe configurados juntos para Olá mesmo tipo de certificado.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Rolagem do certificado
Ao usar o nome comum do certificado em vez de impressão digital, sobreposição de certificado não requer a atualização de configuração do cluster.
Se a sobreposição de certificado envolve emissor sobrepor, mantenha antigo certificado de emissor Olá no repositório de certificados de saudação pelo menos 2 horas depois de instalar o novo certificado de emissor hello.

## <a name="acquire-hello-x509-certificates"></a>Obter certificados x. 509 de saudação
comunicação toosecure em cluster Olá, você primeiro precisará certificados x. 509 de tooobtain para os nós do cluster. Além disso, toolimit conexão toothis tooauthorized máquinas/usuários do cluster, será necessário tooobtain e instalar certificados para computadores cliente do hello.

Para clusters que executam cargas de trabalho de produção, você deve usar um [autoridade de certificação (CA)](https://en.wikipedia.org/wiki/Certificate_authority) assinados do cluster de saudação de toosecure de certificado x. 509. Para obter detalhes sobre como obter esses certificados, acesse muito[como: obter um certificado](http://msdn.microsoft.com/library/aa702761.aspx).

Para clusters que usam para fins de teste, você pode escolher toouse um certificado autoassinado.

## <a name="optional-create-a-self-signed-certificate"></a>Opcional: criar um certificado autoassinado
Uma maneira toocreate um certificado autoassinado que pode ser protegido corretamente é toouse Olá *CertSetup.ps1* script na pasta do SDK do Service Fabric Olá no diretório Olá *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Editar esse nome do arquivo toochange Olá padrão do certificado de saudação (procure o valor de saudação *CN = ServiceFabricDevClusterCert*). Execute esse script como `.\CertSetup.ps1 -Install`.

Exporte arquivo PFX do hello certificado tooa com uma senha protegida. Primeiro obtenha a impressão digital de saudação do certificado de saudação. De saudação *iniciar* menu, executar Olá *gerenciar certificados de computador*. Navegue toohello **Local\Pessoal.** pasta e localize Olá certificado apenas criado. Clique duas vezes em Olá certificado tooopen-lo, selecione Olá *detalhes* guia e role para baixo toohello *impressão digital* campo. Copie o valor de impressão digital Olá comando do PowerShell Olá abaixo, após remover espaços hello.  Saudação de alteração `String` valor tooa adequado senha segura tooprotect-lo e execução hello a seguir no PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

detalhes de saudação toosee de um certificado instalado no hello máquina que você pode executar Olá comando PowerShell a seguir:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Como alternativa, se você tiver uma assinatura do Azure, siga a seção Olá [adicionar certificados tooKey cofre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Instalar certificados de saudação
Uma vez que o certificado, você pode instalá-los em nós de cluster de saudação. Os nós precisam toohave hello mais recente do Windows PowerShell 3. x instalado neles. Você precisará toorepeat essas etapas em cada nó de Cluster e o servidor de certificados e todos os certificados secundários.

1. Copie o nó de toohello hello. pfx (s).
2. Abra uma janela do PowerShell como administrador e digite Olá comandos a seguir. Substituir saudação *$pswd* com senha Olá usado toocreate esse certificado. Substituir saudação *$PfxFilePath* com caminho completo de saudação do nó de toothis copiado do hello. pfx.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Defina agora o controle de acesso de saudação neste certificado para que o processo de Service Fabric hello, que é executado sob Olá conta de serviço de rede, pode usá-lo executando Olá script a seguir. Forneça Olá a impressão digital do certificado hello e "Serviço de rede" hello conta de serviço. Você pode verificar que Olá ACLs no certificado Olá estão corretas abrindo certificado Olá no *iniciar* > *gerenciar certificados de computador* e examinando *todas as tarefas*  >  *Gerenciar chaves particulares*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Repita as etapas de saudação acima para cada certificado de servidor. Você também pode usar essas etapas tooinstall Olá certificados de cliente em computadores de saudação que você deseja que o cluster de toohello tooallow acesso.

## <a name="create-hello-secure-cluster"></a>Criar cluster seguro Olá
Depois de configurar Olá **segurança** seção Olá **ClusterConfig.X509.MultiMachine.json** arquivo, você pode continuar muito[criar seu cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de seção Olá nós e criar um cluster Olá autônomo. Lembre-se de saudação toouse **ClusterConfig.X509.MultiMachine.json** arquivo durante a criação de cluster hello. Por exemplo, o comando pode parecer com hello a seguir:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Depois que você tiver Olá seguro autônomo do Windows cluster com êxito em execução e que a instalação Olá clientes autenticados tooconnect tooit, execute a seção de saudação [conectar tooa cluster seguro usando o PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Por exemplo:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Você pode executar outra toowork de comandos do PowerShell com este cluster. Por exemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow uma lista de nós neste cluster seguro.


cluster de saudação tooremove, conectar toohello nó no cluster Olá onde você baixou o pacote do Service Fabric hello, abra uma linha de comando e navegue toohello pasta do pacote. Agora execute Olá comando a seguir:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Configuração de certificado incorreto pode impedir que o cluster Olá chegando durante a implantação. tooself-diagnosticar problemas de segurança, consulte no grupo de Visualizador de eventos *Applications and Services Logs* > *Microsoft Service Fabric*.
> 
> 

