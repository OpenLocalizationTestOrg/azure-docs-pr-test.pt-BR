---
title: "aaaSecure um cluster em execução no Windows usando a segurança do Windows | Microsoft Docs"
description: "Saiba como tooconfigure segurança de nó para nó e o nó do cliente em um autônomo cluster em execução no Windows usando a segurança do Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Proteger um cluster autônomo no Windows usando a Segurança do Windows
tooprevent de cluster de malha do serviço de tooa de acesso não autorizado, você deve proteger o cluster de saudação. Segurança é especialmente importante quando o cluster Olá executa cargas de trabalho de produção. Este artigo descreve como segurança tooconfigure de nó do cliente e de nó para nó usando a segurança do Windows no hello *Clusterconfig* arquivo.  processo de saudação corresponde toohello configurar segurança de [criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md). Para saber mais sobre como o Service Fabric usa a Segurança do Windows, veja [Cenários de segurança de cluster](service-fabric-cluster-security.md).

> [!NOTE]
> Você deve considerar seleção Olá de nó para nó segurança com cuidado porque não há nenhuma atualização de cluster de um tooanother de opção de segurança. seleção de segurança do toochange hello, você tem toorebuild Olá completo do cluster.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Configurar a segurança do Windows usando gMSA  
exemplo Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* baixar um arquivo de configuração com hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) autônomo pacote de cluster contém um modelo de configuração de segurança do Windows usando [conta de serviço gerenciado de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Parâmetro de configuração** | **Descrição** |  
| --- | --- |  
| WindowsIdentities |Contém as identidades de cliente e o cluster de saudação. |  
| ClustergMSAIdentity |Configura a segurança de nó para nó. Uma conta de serviço gerenciado de grupo. |  
| ClusterSPN |SPN de domínio totalmente qualificado para a conta gMSA|  
| ClientIdentities |Configura a segurança de cliente para nó. Uma matriz de contas de usuário do cliente. |  
| Identidade |identidade do cliente Hello, um usuário de domínio. |  
| IsAdmin |O valor True Especifica que esse usuário de domínio Olá tenha acesso de cliente de administrador, false para acesso de cliente do usuário. |  
  
[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada definindo **ClustergMSAIdentity** quando do service fabric precisa toorun em gMSA. Em relações de confiança de toobuild ordem entre os nós, eles devem ser informados uns dos outros. Isso pode ser feito de duas maneiras diferentes: especifique Olá grupo de conta de serviço gerenciado que inclui todos os nós no cluster de saudação ou grupo de computadores do domínio Olá que inclui todos os nós no cluster de saudação. É altamente recomendável usar Olá [conta de serviço gerenciado de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) abordagem, particularmente para clusters maiores (mais de 10 nós) ou para clusters que são provavelmente toogrow ou reduzidas.  
Essa abordagem não exige a saudação de criação de um grupo de domínio para o qual os administradores de cluster foram concedidos tooadd de direitos de acesso e remover membros. Essas contas também são úteis para gerenciamento automático de senha. Para obter mais informações, confira [Introdução a contas de serviços gerenciados de grupo](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Segurança do cliente toonode](service-fabric-cluster-security.md#client-to-node-security) é configurado usando **ClientIdentities**. Em ordem tooestablish relação de confiança entre um cluster de cliente e hello, configure Olá cluster tooknow quais identidades de cliente que pode confiar. Isso pode ser feito de duas maneiras diferentes: especificar usuários Olá de grupo de domínio que podem se conectar ou especifique Olá usuários de nó do domínio que podem se conectar. Malha do serviço oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário. Controle de acesso permite Olá Olá tipos cluster administrador toolimit acesso toocertain das operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura.  Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços. Para saber mais sobre controles de acesso, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).  
 
Olá seguindo exemplo **segurança** seção configura a segurança do Windows usando gMSA e especifica que Olá máquinas *ServiceFabric.clusterA.contoso.com* gMSA fazem parte do cluster hello e que *CONTOSO\usera* tem acesso de cliente do administrador:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Configurar a segurança do Windows usando um grupo de máquinas  
exemplo Hello *ClusterConfig.Windows.MultiMachine.JSON* baixar um arquivo de configuração com hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) autônomo pacote de cluster contém um modelo de configuração de segurança do Windows.  Segurança do Windows é configurada em Olá **propriedades** seção: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Parâmetro de configuração** | **Descrição** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** está definido muito*Windows* se ClusterIdentity Especifica um nome de grupo de computador do Active Directory. |  
| ServerCredentialType |Definir muito*Windows* tooenable a segurança do Windows para clientes.<br /><br />Isso indica que clientes Olá Olá cluster e Olá em si são executados em um domínio do Active Directory. |  
| WindowsIdentities |Contém as identidades de cliente e o cluster de saudação. |  
| ClusterIdentity |Use um nome de grupo do computador, domain\machinegroup, segurança de nó para nó tooconfigure. |  
| ClientIdentities |Configura a segurança de cliente para nó. Uma matriz de contas de usuário do cliente. |  
| Identidade |Adicione o usuário de domínio do hello, domínio \ nomedeusuário para identidade de saudação do cliente. |  
| IsAdmin |Conjunto tootrue toospecify que Olá usuário de domínio tem acesso de administrador do cliente ou falso para acesso de cliente do usuário. |  

[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada por meio de configuração **ClusterIdentity** se você quiser toouse um grupo de computadores em um domínio do Active Directory. Para saber mais, confira [Criar um grupo de máquinas no Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

A [segurança de cliente para nó](service-fabric-cluster-security.md#client-to-node-security) é configurada usando **ClientIdentities**. tooestablish de confiança entre um cliente e hello cluster, você deve configurar Olá cluster tooknow Olá cliente identidades Olá cluster podem confiar. Você pode estabelecer confiança de duas maneiras diferentes:

- Especifique os usuários do grupo de domínio de saudação podem se conectar.
- Especifica usuários de nó do domínio Olá podem se conectar.

Malha do serviço oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário. Controle de acesso permite Olá cluster administrador toolimit acesso toocertain tipos de operações de cluster para diferentes grupos de usuários, que torna o cluster hello mais segura.  Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.  

Olá seguindo exemplo **segurança** seção configura a segurança do Windows, especifica que Olá máquinas *ServiceFabric/clusterA.contoso.com* fazem parte do cluster hello e especifica que  *CONTOSO\usera* tem acesso de cliente do administrador:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> O Service Fabric não devem ser implantado em um controlador de domínio. Certifique-se de que Clusterconfig não incluem o endereço IP de Olá Olá do controlador de domínio ao usar um grupo de computador ou grupo a conta de serviço gerenciada (gMSA).
>
>

## <a name="next-steps"></a>Próximas etapas
Depois de configurar a segurança do Windows em Olá *Clusterconfig* de arquivos, retomar o processo de criação de cluster Olá em [criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).

Para saber mais sobre a segurança de nó para nó, a segurança de cliente para nó e o controle de acesso baseado em função, consulte [Cenários de segurança de cluster](service-fabric-cluster-security.md).

Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter exemplos de conexão usando o PowerShell ou FabricClient.
