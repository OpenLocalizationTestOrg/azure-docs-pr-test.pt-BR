---
title: "Serviços de domínio do AD do Azure: Controladores de domínio serviços de domínio de AD do Azure comparar tooDIY | Microsoft Docs"
description: "Comparando os controladores de domínio do Azure Active Directory Domain Services tooDIY"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Como toodecide se serviços de domínio do AD do Azure é adequada para seu caso de uso
Com os serviços de domínio do AD do Azure, você pode implantar suas cargas de trabalho nos serviços de infraestrutura do Azure, sem ter que tooworry sobre a manutenção da infraestrutura de identidade no Azure. Esse serviço gerenciado é diferente de uma implantação típica do Windows Server Active Directory que você implanta e administra sozinho. serviço de saudação é fácil toodeploy e fornece monitoramento de integridade automatizada e correção. Podemos estão em constante evolução Olá serviço tooadd suporte a cenários comuns de implantação.

toodecide se os serviços de domínio do AD do Azure toouse recomendamos Olá material de leitura a seguir:

* Consulte a lista de saudação do [recursos oferecidos pelos serviços de domínio do AD do Azure](active-directory-ds-features.md).
* Examine os [Cenários de implantação comuns dos Azure AD Domain Services](active-directory-ds-scenarios.md).
* Por fim, [comparar a opção de serviços de domínio do AD do Azure de tooa AD tipo faça você mesmo](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Comparar o domínio de tooDIY AD de serviços de domínio do AD do Azure no Azure
Olá tabela a seguir ajuda você a decidir entre usar serviços de domínio do AD do Azure e gerenciar sua própria infraestrutura do AD no Azure.

| **Recurso** | **Azure AD Domain Services** | **AD "faça você mesmo" em VMs do Azure** |
| --- |:---:|:---:|
| [**Serviço gerenciado**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**&#x2715;** |
| [**Implantações seguras**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |Administrador precisa de implantação de saudação toosecure. |
| [**Servidor DNS**](active-directory-ds-comparison.md#dns-server) |**&#x2713;** (serviço gerenciado) |**&#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&#x2715;** |**&#x2713;** |
| [**Ingresso no domínio**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**Autenticação de domínio usando Kerberos e NTLM**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Delegação restrita de Kerberos**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|baseado em recursos|baseado em recursos e em conta|
| [**Estrutura de UO personalizada**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**Extensões de esquema**](active-directory-ds-comparison.md#schema-extensions) |**&#x2715;** |**&#x2713;** |
| [**Relações de confiança de floresta/domínio do AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&#x2715;** |**&#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**LDAP Seguro (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&#x2715;** |**&#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**Implantações com distribuição geográfica**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&#x2715;** |**&#x2713;** |

#### <a name="managed-service"></a>Serviço gerenciado
Os domínios dos Azure AD Domain Services são gerenciados pela Microsoft. Você não tem tooworry sobre a aplicação de patches, atualizações, monitoramento, backups e garantir a disponibilidade do seu domínio. Essas tarefas de gerenciamento são oferecidas como um serviço pelo Microsoft Azure para seus domínios gerenciados.

#### <a name="secure-deployments"></a>Implantações seguras
domínio gerenciado Olá com segurança é bloqueado de acordo com as recomendações de segurança da Microsoft para implantações do AD. Essas recomendações derivam de décadas da equipe de produto Olá AD de experiência de engenharia e suporte a implantações do AD. Para implantações de tipo faça você mesmo, você precisa tootake específicas de implantação etapas toolock para baixo/proteger a implantação.

#### <a name="dns-server"></a>Servidor DNS
Um domínio gerenciado dos Azure AD Domain Services inclui serviços de DNS gerenciados. Membros Olá ' AAD DC' do grupo de administradores podem gerenciar DNS no domínio Olá gerenciado. Os membros deste grupo recebem privilégios totais de administração do DNS para o domínio gerenciado hello. Gerenciamento de DNS pode ser executado usando Olá 'Console de administração do DNS' incluído no pacote de ferramentas de administração de servidor remoto (RSAT) hello.
[Mais informações](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Privilégios de administrador corporativo ou de domínio
Esses privilégios elevados não são oferecidos em um domínio gerenciado de DS AAD. Aplicativos que exigem esses privilégios elevados não podem ser implantados em domínios gerenciados do AAD DS. Um subconjunto menor de privilégios administrativos é toomembers disponíveis do grupo de administração delegada Olá chamado 'Administradores de controlador de domínio do AAD'. Esses privilégios incluem privilégios tooconfigure DNS, configurar a política de grupo, obtém privilégios de administrador em computadores que ingressaram no domínio etc.

#### <a name="domain-join"></a>Ingresso no domínio
Você pode adicionar máquinas virtuais toohello gerenciados domínio toohow semelhante unir o domínio dos computadores tooan AD.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Autenticação de domínio usando Kerberos e NTLM
Com os serviços de domínio do AD do Azure, você pode usar tooauthenticate suas credenciais corporativas com domínio gerenciado hello. As credenciais são mantidas em sincronia com seu locatário do Azure AD. Para locatários sincronizados, do Azure AD Connect garante que as alterações feitas de toocredentials local sincronizado tooAzure AD. Com uma configuração de tipo faça você mesmo domínio, talvez seja necessário tooset um domínio de AD relação de confiança com suas instalações AD para usuários tooauthenticate com suas credenciais corporativas. Como alternativa, talvez seja necessário tooset backup tooensure de replicação do AD que as senhas de usuário sincronizem tooyour máquinas de virtuais de controladores de domínio do Azure.

#### <a name="kerberos-constrained-delegation"></a>Delegação restrita de Kerberos
Você não tem privilégios de "Administrador do Domínio" em um domínio gerenciado pelo Active Directory Domain Services. Portanto, você não pode configurar a delegação restrita do Kerberos baseada em conta (tradicional). No entanto, você pode configurar hello mais segura baseada em recursos de delegação restrita.
[Mais informações](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Estrutura de UO personalizada
Membros Olá ' AAD DC' do grupo de administradores podem criar UOs personalizados no domínio Olá gerenciado. Os usuários que criam UOs personalizados recebem privilégios administrativos completos sobre Olá UO.
[Mais informações](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Extensões de esquema
Você não pode estender o esquema de base de saudação de um domínio gerenciado do serviços de domínio do AD do Azure. Portanto, aplicativos que dependem do esquema de tooAD extensões (por exemplo, novos atributos no objeto de usuário Olá) não podem ser eliminados e deslocada domínios tooAAD DS.

#### <a name="ad-domain-or-forest-trusts"></a>Relações de confiança de floresta ou domínio do AD
Domínios gerenciados não podem ser configurado tooset (entrada/saída) de relacionamentos de confiança com outros domínios. Portanto, cenários de implantação de florestas de recursos não podem usar o Azure AD Domain Services. Da mesma forma, as implantações em que você preferir não toosynchronize senhas tooAzure AD não podem usar os serviços de domínio do AD do Azure.

#### <a name="ldap-read"></a>Leitura LDAP
Olá gerenciados domínio oferece suporte a LDAP ler cargas de trabalho. Portanto, você pode implantar aplicativos que executam operações em relação ao domínio gerenciado Olá de leitura de LDAP.

#### <a name="secure-ldap"></a>LDAP seguro
Você pode configurar os serviços de domínio do AD do Azure tooprovide segura LDAP acesso tooyour gerenciado Olá de domínio, inclusive pela internet.
[Mais informações](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Gravação LDAP
domínio gerenciado Olá é somente leitura para objetos de usuário. Portanto, os aplicativos que executam operações de gravação de LDAP em atributos de objeto de usuário de saudação não funcionam em um domínio gerenciado. Além disso, as senhas de usuário não podem ser alteradas no domínio gerenciado hello. Outro exemplo seria a modificação de associações de grupo ou atributos de grupo no domínio gerenciado hello, que não é permitido. No entanto, todas as alterações toouser atributos ou senhas feitas no AD do Azure (por meio do portal do Azure PowerShell /) ou AD são sincronizados no local toohello AAD DS gerenciados domínio.

#### <a name="group-policy"></a>Política de grupo
Há um interno GPO cada para contêineres de "Computadores AADDC" e "AADDC Users" hello. Você pode personalizar esses política de grupo tooconfigure GPOs internos. Membros Olá ' AAD DC' do grupo de administradores também podem criar GPOs personalizadas e vinculá-los em OUs tooexisting (incluindo OUs personalizadas).
[Mais informações](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Implantações geograficamente dispersas
Os domínios gerenciados dos Azure AD Domain Services estão disponíveis em uma única rede virtual no Azure. Para cenários que exigem os toobe do controladores de domínio disponível em várias regiões do Azure em Olá, mundo, configurar controladores de domínio em VMs de IaaS do Azure pode ser melhor alternativa de saudação.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Opções de implantação de AD do tipo DIY (faça você mesmo)
Você pode ter os casos de uso de implantação em que você precisa de alguns dos recursos de saudação oferecidos por uma instalação do AD do Windows Server. Nesses casos, considere uma saudação tipo faça você mesmo (DIY) as opções a seguir:

* **Domínio de nuvem autônomo:** você pode configurar um "domínio de nuvem" autônomo usando máquinas virtuais do Azure que foram configuradas como controladores de domínio. Essa infraestrutura não se integra ao seu ambiente local do AD. Essa opção requer um conjunto diferente de credenciais de nuvem toologin/administrar VMs em nuvem hello.
* **Implantação de floresta de recursos:** você pode configurar um domínio na topologia de floresta de recurso hello, usando máquinas virtuais do Azure configuradas como controladores de domínio. Em seguida, você pode configurar uma relação de confiança do AD com seu ambiente local do AD. Você pode floresta de recursos de toothis-ingresso no domínio (máquinas virtuais do Azure) de computadores na nuvem hello. Autenticação de usuário ocorra em um um diretório local de tooyour de conexão de VPN/rota expressa.
* **Estender seu tooAzure de domínio local:** você pode se conectar a uma rede de local de tooyour de rede virtual do Azure usando uma conexão VPN/rota expressa. Essa configuração permite que máquinas virtuais do Azure toobe tooyour unidas AD local. Outra alternativa é toopromote réplicas de controladores de domínio do seu domínio local no Azure como uma máquina virtual. Você pode, em seguida, configurá-lo tooreplicate em um diretório local de tooyour de conexão de VPN/rota expressa. Este modo de implantação efetivamente estende sua tooAzure de domínio local.

> [!NOTE]
> Você pode determinar se uma opção de DIY é mais adequada para seus casos de uso de implantação. Considere [compartilhar comentário](active-directory-ds-contact-us.md) toohelp nos entender o que ajuda a recursos você escolheu o serviços de domínio do AD do Azure no hello futuras. Esses comentários nos ajudam a desenvolver naipe de toobetter serviço Olá que necessidades de sua implantação e casos de uso.
>
>

Publicadas [diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp facilitar DIY instalações.

## <a name="related-content"></a>Conteúdo relacionado
* [Recursos – Azure AD Domain Services](active-directory-ds-features.md)
* [Cenários de implantação – Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
