---
title: aaaSecure um cluster do Service Fabric | Microsoft Docs
description: "Descreve cenários de segurança de saudação para um Service Fabric tooimplement de tecnologias diferentes usadas cluster e hello esses cenários."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Cenários de segurança do cluster do Service Fabric
Um cluster do Service Fabric é um recurso que pertence a você. Clusters devem ser protegido tooprevent não autorizado usuários conectem cluster tooyour, especialmente quando ele tiver cargas de trabalho de produção em execução. Embora seja possível toocreate um cluster não seguro, isso permite que os usuários anônimos tooconnect tooit, se ela expõe toohello de pontos de extremidade de gerenciamento Internet pública. 

Este artigo fornece uma visão geral da saudação cenários de segurança para os clusters em execução no Azure ou autônomo e Olá tooimplement de várias tecnologias usadas esses cenários. Olá cenários de segurança de cluster são:

* Segurança de nó para nó
* Segurança de cliente para nó
* RBAC (Controle de Acesso Baseado em Função)

## <a name="node-to-node-security"></a>Segurança de nó para nó
Protege a comunicação entre VMs hello ou máquinas no cluster hello. Isso garante que somente os computadores autorizados toojoin Olá cluster podem participar de hospedar aplicativos e serviços em cluster hello.

![Diagrama de comunicação de nó para nó][Node-to-Node]

Os clusters em execução no Azure ou clusters autônomos em execução no Windows podem usar a [Segurança de Certificado](https://msdn.microsoft.com/library/ff649801.aspx) ou então a [Segurança do Windows](https://msdn.microsoft.com/library/ff649396.aspx) para computadores Windows Server.

### <a name="node-to-node-certificate-security"></a>Segurança de certificado de nó para nó
Serviço de malha usa certificados x. 509 do servidor que você especificar como parte das configurações de tipo de nó hello quando você cria um cluster. Uma visão geral de quais são esses certificados e como você pode adquirir ou criá-los é fornecida no final deste artigo hello.

Certificado de segurança é configurada durante a criação de cluster Olá por meio de saudação portal do Azure, modelos do Azure Resource Manager ou um modelo JSON autônoma. É possível especificar um certificado primário e um certificado secundário opcional que é usado para substituições de certificado. Olá certificados primários e secundários que você especificar devem ser diferentes do cliente do administrador de saudação e certificados de cliente somente leitura especificado para [segurança do nó do cliente](#client-to-node-security).

Para ler os Azure [configurar um cluster usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn como tooconfigure certificado segurança em um cluster.

Para Windows Server autônomo, leia [Proteger um cluster autônomo no Windows usando certificados X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Segurança do Windows de nó para nó
Para Windows Server autônomo, leia [Proteger um cluster autônomo no Windows usando a segurança do Windows](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Segurança de cliente para nó
Autentica clientes e protege a comunicação entre um cliente e nós individuais Olá cluster. Esse tipo de segurança autentica e protege as comunicações de cliente, o que garante que apenas usuários autorizados possam acessar o cluster hello e aplicativos de saudação implantados no cluster de saudação. Os clientes são identificados exclusivamente por meio de suas credenciais de segurança do Windows ou pelas credenciais de segurança do certificado deles.

![Diagrama de comunicação de cliente para nó][Client-to-Node]

Os clusters em execução no Azure ou clusters autônomos em execução no Windows podem usar a [Segurança de Certificado](https://msdn.microsoft.com/library/ff649801.aspx) ou então a [Segurança do Windows](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>Segurança de certificado de cliente para nó
 Segurança de certificado de cliente para o nó é configurada durante a criação de cluster Olá por meio de saudação portal do Azure, modelos do Gerenciador de recursos ou um modelo JSON autônomo, especificando um certificado de cliente de administração e/ou um certificado de cliente do usuário.  Olá administrador usuário cliente certificados de cliente e você especificar devem ser diferentes do hello primário e secundários certificados que você especificar para [segurança de nó para nó](#node-to-node-security) como uma prática recomendada. Por padrão, os certificados de cluster de Olá para segurança de nó para nó são adicionados toohello permitido Admin lista de certificados do cliente.

Clientes que se conectam usando Olá administrador certificado de cluster de toohello têm recursos de toomanagement de acesso completo.  Clientes que se conectam toohello cluster usando o certificado de cliente de usuário somente leitura Olá têm apenas os recursos de toomanagement acesso de leitura. Em outras palavras, esses certificados são usados para Olá bases de controle de acesso função (RBAC) descrito posteriormente neste artigo.

Para ler os Azure [configurar um cluster usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn como tooconfigure certificado segurança em um cluster.

Para Windows Server autônomo, leia [Proteger um cluster autônomo no Windows usando certificados X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Segurança do AAD (Azure Active Directory) de cliente para nó no Azure
Clusters em execução no Azure também podem proteger acesso a pontos de extremidade de gerenciamento toohello usando o Azure Active Directory (AAD). Consulte [configurar um cluster usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obter informações sobre como toocreate Olá artefatos necessários do AAD, como toopopulate-los durante o cluster de criação e como tooconnect toothose clusters posteriormente.

## <a name="security-recommendations"></a>Recomendações de Segurança
Para clusters do Azure, é recomendável que você use o AAD segurança tooauthenticate clientes e certificados para segurança de nó para nó.

Para clusters do Windows Server autônomos, será recomendável usar a segurança do Windows com GMA (contas gerenciadas de grupo) se você tiver o Windows Server 2012 R2 e o Active Directory. Caso contrário, ainda use a segurança do Windows com contas do Windows.

## <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Controle de acesso permite Olá administrador toolimit acesso toocertain cluster as operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura. Dois tipos de controle de acesso diferentes têm suporte para clientes que se conectam cluster tooa: função de administrador e a função de usuário.

Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação). Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.

Você especificar funções Administrador e usuário saudação do cliente em tempo de saudação da criação do cluster, fornecendo identidades separadas (certificados, etc. do AAD) para cada. Para obter mais informações sobre configurações de controle de acesso padrão hello e como toochange Olá configurações padrão, consulte [controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>Certificados X.509 e Service Fabric
Certificados digitais x. 509 são usadas tooauthenticate clientes e servidores e tooencrypt e assinem digitalmente as mensagens. Para obter mais detalhes sobre esses certificados, vá muito[trabalhar com certificados](http://msdn.microsoft.com/library/ms731899.aspx).

Tooconsider algumas coisas importantes:

* Os certificados usados em clusters que executam cargas de trabalho de produção devem ser criados por meio de um serviço de certificado do Windows Server configurado corretamente ou obtidos por meio de uma [AC (Autoridade de Certificação)](https://en.wikipedia.org/wiki/Certificate_authority)aprovada.
* Nunca use nenhum certificado temporário ou de teste em produção criado com ferramentas como MakeCert.exe.
* Você pode usar um certificado autoassinado, mas deve fazer isso somente para clusters de teste e não em produção.

### <a name="server-x509-certificates"></a>Certificados X.509 do servidor
Certificados de servidor têm a tarefa primária Olá de autenticação tooclients um servidor (nó) ou autenticação de um servidor (nó) tooa server (nó). Uma das verificações de saudação inicial quando um cliente ou um nó autentica um nó é o valor de saudação de toocheck do nome comum de saudação no campo de assunto hello. Esse nome comum ou um dos nomes alternativos da entidade dos certificados Olá deve estar presente na lista de saudação de nomes comuns permitidos.

Olá artigo a seguir descreve como toogenerate certificados com nomes alternativos da entidade (SAN): [como tooadd um tooa de nome alternativo do assunto proteger o certificado LDAP](http://support.microsoft.com/kb/931351).

campo de assunto Olá pode conter vários valores, cada prefixado com um tipo de valor inicialização tooindicate hello. Mais comumente, inicialização Olá é "CN" para o nome comum; Por exemplo, "CN = www.contoso.com". Também é possível toobe de campo de assunto de saudação em branco. Se o campo de nome alternativo da entidade opcional Olá estiver preenchido, ele deve conter o nome comum de saudação do certificado hello e uma entrada por nome alternativo da entidade. Eles são inseridos como valores de Nome DNS.

valor de saudação do campo de finalidades de saudação do certificado Olá deve incluir um valor apropriado, como "Autenticação do servidor" ou "Autenticação do cliente".

### <a name="client-x509-certificates"></a>Certificados X.509 do cliente
Normalmente, os certificados de cliente não são emitidos por uma autoridade de certificação de terceiros. Em vez disso, hello repositório pessoal do local do usuário atual Olá normalmente contém certificados de cliente incluídos por uma autoridade raiz, com a finalidade de "Autenticação do cliente". cliente de saudação pode usar esse certificado quando a autenticação mútua é necessária.

> [!NOTE]
> Todas as operações de gerenciamento no cluster do Service Fabric exigem certificados de servidor. Certificados de cliente não podem ser usados para gerenciamento.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Próximas etapas
Este artigo fornece informações conceituais sobre a segurança de cluster. Em seguida,


1.  [crie um cluster no Azure usando um modelo do Resource Manager](service-fabric-cluster-creation-via-arm.md) 
2.  [Portal do Azure](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
