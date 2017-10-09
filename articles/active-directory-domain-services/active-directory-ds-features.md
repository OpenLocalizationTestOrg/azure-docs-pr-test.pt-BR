---
title: 'Azure Active Directory Domain Services: recursos | Microsoft Docs'
description: "Recursos dos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>Recursos
Olá recursos a seguir está disponível nos serviços de domínio do AD do Azure gerenciados.

* **Experiência de implantação simples:** com apenas alguns cliques você pode habilitar os Serviços de Domínio do AD do Azure para seu locatário do AD do Azure. Independentemente de seu locatário do AD do Azure ser um locatário de nuvem ou sincronizado com o diretório local, seu domínio gerenciado pode ser provisionado rapidamente.
* **Suporte para associação de domínio:** computadores podem ser facilmente-ingresso no domínio em Olá rede virtual do Azure, seu domínio gerenciado está disponível no. experiência de ingresso no domínio Olá no cliente do Windows e sistemas operacionais de servidor funciona perfeitamente nos domínios atendidas pelos serviços de domínio do AD do Azure. Você também pode usar as ferramentas do ingresso no domínio automatizado com relação a esses domínios.
* **Uma instância de domínio por diretório do AD do Azure:** você pode criar um único domínio do Active Directory para cada diretório do AD do Azure.
* **Criar domínios com nomes personalizados:** você pode criar domínios com nomes personalizados (por exemplo, 'contoso100.com') usando os Azure AD Domain Services. Você pode usar qualquer nome de domínio verificado ou não. Opcionalmente, você também pode criar um domínio com o sufixo de domínio interno hello (ou seja, ' *. c o m ') oferecidos pelo seu diretório do AD do Azure.
* **Integrado ao AD do Azure:** não precisa tooconfigure ou gerenciar a replicação dos serviços de domínio tooAzure AD. As contas de usuário, as associações de grupo e as credenciais de usuário (senhas) do seu diretório do Azure AD estão automaticamente disponíveis nos Azure AD Domain Services. Novos usuários, grupos ou tooattributes alterações do seu locatário do AD do Azure ou seu diretório local são sincronizada automaticamente tooAzure AD os serviços de domínio.
* **Autenticação NTLM e Kerberos:** com suporte para autenticação NTLM e Kerberos, você pode implantar aplicativos que dependem da autenticação Integrada do Windows.
* **Usar suas credenciais corporativas/senhas:** senhas de usuários em seu locatário do AD do Azure funcionam com os Serviços de Domínio do AD do Azure. Usuários podem usar máquinas de junção toodomain suas credenciais corporativas, faça logon interativamente ou pela área de trabalho remota e autenticar no domínio gerenciado hello.
* **Suporte de leitura de ligação LDAP & LDAP:** você pode usar aplicativos que dependem de ligações LDAP tooauthenticate usuários em domínios atendidos pelos serviços de domínio do AD do Azure. Além disso, os aplicativos que usam LDAP operações de leitura de atributos de usuário/computador tooquery do diretório Olá também podem funcionar em relação aos serviços de domínio do AD do Azure.
* **LDAP seguro (LDAPS):** você pode habilitar a acessar o diretório toohello sobre LDAP seguro (LDAPS). Acesso LDAP seguro está disponível na rede virtual de saudação por padrão. No entanto, você também pode habilitar acesso LDAP seguro por Olá internet.
* **Política de grupo:** você pode usar um único interno GPO cada Olá usuários e computadores conformidade de tooenforce contêineres com políticas de segurança necessárias para contas de usuários e computadores do domínio. Você também pode criar GPOs personalizadas e atribuí-los unidades organizacionais toocustom muito[Gerenciar política de grupo](active-directory-ds-admin-guide-administer-group-policy.md).
* **Gerenciar DNS:** os membros do grupo 'Administradores de controlador de domínio do AAD' hello podem gerenciar DNS para seu domínio gerenciado usando a administração do DNS familiar ferramentas como Olá snap-in MMC de administração do DNS.
* **Criar personalizado unidades organizacionais (OUs):** membros Olá ' AAD DC' do grupo de administradores podem criar UOs personalizados no domínio gerenciado hello. Esses usuários recebem privilégios administrativos totais sobre UOs personalizadas, de modo que podem adicionar ou remover contas de serviço, computadores, grupos etc. dessas OUs personalizadas.
* **Disponível em várias regiões do Azure:** consulte Olá [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/) tooknow página Olá regiões do Azure, na qual os serviços de domínio do AD do Azure está disponível.
* **Alta disponibilidade:** os Azure AD Domain Services oferecem alta disponibilidade para seu domínio. Esse recurso oferece a garantia de saudação do toofailures mais altos de tempo de atividade e a resiliência de serviço. Ofertas de correção automatizado de falhas de monitoramento por ativar ou desativar novas instâncias de tooreplace falhado de instâncias e tooprovide interna de integridade continuou o serviço para seu domínio.
* **Usar as ferramentas de gerenciamento conhecidos:** você pode usar ferramentas de gerenciamento do Active Directory do Windows Server familiares como domínios de saudação Centro Administrativo do Active Directory ou Active Directory PowerShell tooadminister gerenciado.
