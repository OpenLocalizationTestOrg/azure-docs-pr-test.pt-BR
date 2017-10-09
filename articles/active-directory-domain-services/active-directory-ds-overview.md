---
title: aaaOverview do Azure Active Directory Domain Services | Microsoft Docs
description: "Visão geral de Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Visão geral
Serviços de infraestrutura do Azure permitem que você toodeploy uma ampla gama de soluções de computação de uma maneira ágil. Com as máquinas virtuais do Azure, você pode implantar quase instantaneamente e você pagará apenas por minuto hello. Usando suporte para Windows, Linux, SQL Server, Oracle, IBM, SAP e BizTalk, você pode implantar qualquer carga de trabalho, qualquer linguagem, em praticamente qualquer sistema operacional. Esses benefícios habilitar tooAzure de local de aplicativos herdados implantados toomigrate, toosave em despesas operacionais.

Um aspecto importante da migração no local tooAzure de aplicativos está lidando com necessidades de identidade Olá desses aplicativos. Aplicativos com reconhecimento de diretório podem confiar em LDAP para acesso de leitura ou gravação toohello de diretório corporativo ou contar com os usuários finais de tooauthenticate autenticação integrada do Windows (autenticação Kerberos ou NTLM). Aplicativos de LOB (linha de negócios) em execução no Windows Server normalmente são implantados em computadores ingressados no mesmo domínio, para que possam ser gerenciados com segurança usando a Política de Grupo. shift e too'lift' nuvem de toohello de aplicativos local, essas dependências na infraestrutura de identidade corporativa Olá necessário toobe resolvido.

Os administradores geralmente ativar tooone de saudação necessidades de identidade de saudação soluções toosatisfy dos aplicativos implantados no Azure a seguir:

* Implante uma conexão de VPN site a site entre as cargas de trabalho em execução no Azure Infrastructure Services e Olá directory corporativo local.
* Estenda a infraestrutura de domínio ou na floresta de saudação AD corporativa Configurando controladores de domínio de réplica usando máquinas virtuais do Azure.
* Implantar um domínio autônomo no Azure usando controladores de domínio implantados como máquinas virtuais do Azure.

Todas essas abordagens tem o defeito de ser de alto custo e gerar sobrecarga administrativa. Os administradores são controladores de domínio necessários toodeploy usando máquinas virtuais no Azure. Além disso, eles precisam toomanage, segurança, patch, monitor, backup e solucionar essas máquinas virtuais. a dependência de saudação de toohello de conexões de VPN local diretório faz com que as cargas de trabalho implantadas em pequenos problemas de rede do Azure toobe tootransient vulnerável ou interrupções. Essas interrupções de rede, por sua vez, resultam em menor tempo de disponibilidade e em confiabilidade reduzida para esses aplicativos.

Criamos uma alternativa mais fácil de tooprovide de serviços de domínio do AD do Azure.

## <a name="introducing-azure-ad-domain-services"></a>Apresentando os Serviços de Domínio do AD do Azure
Os Serviços de Domínio do Azure AD fornecem serviços de domínio gerenciado, como ingresso no domínio, política de grupo, LDAP, autenticação Kerberos/NTLM e outros, que são totalmente compatíveis com o Active Directory do Windows Server. Você pode consumir esses serviços de domínio sem necessidade de saudação para você toodeploy, gerenciar e controladores de domínio na nuvem de saudação do patch. Serviços de domínio do AD do Azure integra-se com seu locatário do AD do Azure existente, tornando possível para os usuários toolog usando suas credenciais corporativas. Além disso, você pode usar os grupos existentes e tooresources de acesso de toosecure de contas de usuário, garantindo, assim, um mais suave 'levantar shift e' de recursos de local tooAzure serviços de infraestrutura.

A funcionalidade dos Serviços de Domínio do Azure AD funciona perfeitamente, esteja o locatário do Azure AD somente em nuvem ou sincronizado com o Active Directory local.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Serviços de domínio do AD do Azure para organizações somente em nuvem
Um AD do Azure somente em nuvem de locatário (geralmente chamados tooas ' gerenciado locatários') não tem nenhum espaço de identidade local. Em outras palavras, as contas de usuário, senhas e associações de grupo são todos os toohello nativo nuvem - ou seja, criadas e gerenciadas no AD do Azure. Considere por um momento que a Contoso é um locatário somente em nuvem do Azure AD. Conforme mostrado na ilustração a seguir de saudação, o administrador da Contoso configurou uma rede virtual no Azure Infrastructure Services. Aplicativos e cargas de trabalho de servidor são implantados nessa rede virtual em máquinas virtuais do Azure. Como a Contoso é um locatário somente em nuvem, todas as identidades de usuário, suas credenciais e associações de grupo são criadas e gerenciadas no Azure AD.

![Visão geral dos Serviços de Domínio do AD do Azure](./media/active-directory-domain-services-overview/aadds-overview.png)

A Contoso administrador de TI pode habilitar os serviços de domínio do AD do Azure para seu locatário do AD do Azure e escolha toomake serviços de domínio disponíveis na rede virtual. Depois disso, serviços de domínio do AD do Azure provisiona um domínio gerenciado e o torna disponível na rede virtual hello. Todas as contas, associações de grupo e credenciais do usuário disponíveis no locatário Azure AD da Contoso também estão disponíveis nesse domínio recém-criado. Esse recurso permite aos usuários em Olá organização toosign no domínio toohello usando suas credenciais corporativas - por exemplo, ao conectar-se remotamente toodomain-computadores que ingressaram por meio da área de trabalho remota. Os administradores podem provisionar acesso tooresources no domínio hello usando associações de grupo existentes. Aplicativos implantados em máquinas virtuais na rede virtual Olá podem usar recursos como ingresso no domínio, leitura LDAP, ligação LDAP, autenticação Kerberos e NTLM e política de grupo.

Alguns aspectos principais da saudação domínio gerenciado que é provisionado por serviços de domínio do AD do Azure são da seguinte maneira:

* A Contoso administrador de TI não precisa toomanage, patch ou monitorar este domínio ou controladores de domínio para este domínio gerenciado.
* Não há nenhuma replicação de toomanage AD necessário para este domínio. Contas de usuário, associações de grupo e credenciais de locatário do Azure AD da Contoso ficam automaticamente disponíveis nesse domínio gerenciado.
* Desde que o domínio de saudação é gerenciado pelo AD do Azure serviços de domínio Contoso administrador de TI não tem privilégios de administrador corporativo ou de administrador de domínio nesse domínio.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Serviços de Domínio do AD do Azure para organizações híbridas
Organizações com uma infraestrutura de TI híbrida consomem uma combinação de recursos de nuvem e recursos locais. Essas organizações sincronizam informações de identidade de seu locatário do local do directory tootheir AD do Azure. Como organizações híbrida toomigrate mais de sua nuvem de toohello de aplicativos local, especialmente aplicativos herdados de reconhecimento de diretório, serviços de domínio do AD do Azure podem ser útil toothem.

Litware Corporation implantou [do Azure AD Connect](../active-directory/active-directory-aadconnect.md), toosynchronize informações de identidade de seu locatário do local do directory tootheir AD do Azure. informações de identidade Olá sincronizada incluem contas de usuário, seus hashes de credenciais para autenticação (sincronização de senha) e associações de grupo.

> [!NOTE]
> **Sincronização de senha é obrigatória para híbrida organizações toouse serviços de domínio do AD do Azure**. Esse requisito é porque as credenciais do usuário são necessárias em Olá gerenciado domínio fornecida pelos serviços de domínio do AD do Azure, tooauthenticate esses usuários por meio de métodos de autenticação NTLM ou Kerberos.
>
>

![Serviços de domínio do AD do Azure para a Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hello ilustração anterior mostra como as organizações com uma combinação de infraestrutura de TI, como Litware Corporation, podem usar os serviços de domínio do AD do Azure. Os aplicativos e cargas de trabalho de servidor da Litware que exigem serviços de domínio são implantados em uma rede virtual nos Serviços de Infraestrutura do Azure. Do Litware administrador de TI pode habilitar os serviços de domínio do AD do Azure para seu locatário do AD do Azure e escolha toomake um domínio gerenciado disponível nessa rede virtual. Como Litware é uma organização com uma infraestrutura de TI híbrida, credenciais, grupos e contas de usuário são locatário tootheir sincronizado do AD do Azure do seu diretório local. Esse recurso permite que os usuários toosign no domínio toohello usando suas credenciais corporativas - por exemplo, ao conectar-se remotamente toomachines ingressados no domínio toohello via área de trabalho remota. Os administradores podem provisionar acesso tooresources no domínio hello usando associações de grupo existentes. Aplicativos implantados em máquinas virtuais na rede virtual Olá podem usar recursos como ingresso no domínio, leitura LDAP, ligação LDAP, autenticação Kerberos e NTLM e política de grupo.

Alguns aspectos principais da saudação domínio gerenciado que é provisionado por serviços de domínio do AD do Azure são da seguinte maneira:

* domínio gerenciado Olá é um domínio autônomo. Não é uma extensão do domínio local da Litware.
* Do Litware administrador de TI não precisa toomanage, patch ou controladores de domínio do monitor para esse domínio gerenciado.
* Não há nenhum domínio de toothis necessidade toomanage AD replicação. As credenciais do diretório de local da Litware, associações de grupo e contas de usuário são sincronizado tooAzure AD por meio do Azure AD Connect. Essas contas de usuário, associações de grupo e as credenciais estão automaticamente disponíveis no domínio gerenciado hello.
* Desde que o domínio de saudação é gerenciado pelo AD do Azure serviços de domínio, Litware administrador de TI não tem privilégios de administrador corporativo ou de administrador de domínio nesse domínio.

## <a name="benefits"></a>Benefícios
Com os serviços de domínio do AD do Azure, você pode aproveitar Olá benefícios a seguir:

* **Simples** – você pode atender a necessidades de identidade de saudação de máquinas virtuais implantadas tooAzure serviços de infraestrutura com alguns cliques. Você não precisa toodeploy e gerenciar infraestrutura de identidade no Azure ou instalação infraestrutura de identidade de local de tooyour back conectividade.
* **Integrados** – Os Serviços de Domínio do Azure AD são profundamente integrados ao seu locatário do Azure AD. Agora você pode usar o AD do Azure como um diretório de empresa integrado baseado em nuvem que atende às necessidades de toohello de seus aplicativos modernos e de aplicativos com reconhecimento de diretório tradicionais.
* **Compatível com** – serviços de domínio do AD do Azure baseia-se na infraestrutura de classificação Olá enterprise comprovadas do Windows Server Active Directory. Portanto, os aplicativos podem contar com um maior grau de compatibilidade com os recursos do Active Directory do Windows Server. Nem todos os recursos disponíveis no AD do Windows Server estão atualmente disponíveis nos Serviços de Domínio do Azure AD. No entanto, os recursos disponíveis são compatíveis com recursos de Windows Server AD correspondentes Olá que dependem na sua infraestrutura local. Olá LDAP, Kerberos, NTLM, política de grupo e domínio recursos de junção constituem uma oferta madura que foram testada e ao longo de várias versões do Windows Server.
* **Econômico** – com os serviços de domínio do AD do Azure, você pode evitar a sobrecarga de gerenciamento e infraestrutura Olá que está associada com o gerenciamento de identidade infraestrutura toosupport tradicional directory aplicativos com reconhecimento de. Você pode mover tooAzure esses aplicativos serviços de infraestrutura e se beneficiam da maior economia em despesas operacionais.
