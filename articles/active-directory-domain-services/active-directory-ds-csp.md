---
title: Azure Active Directory Domain Services para o Azure Cloud Solution Providers | Microsoft Docs
description: Azure Active Directory Domain Services para o Azure Cloud Solution Providers.
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: mahesh-unnikrishnan
editor: curtand
ms.assetid: 56ccb219-11b2-4e43-9f07-5a76e3cd8da8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: maheshu
ms.openlocfilehash: 313c4853b0f585921739779bb764c50036c9ac8a
ms.sourcegitcommit: 094061b19b0a707eace42ae47f39d7a666364d58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="azure-active-directory-ad-domain-services-for-azure-cloud-solution-providers-csp"></a>Azure Active Directory (AD) Domain Services para o Azure Cloud Solution Providers (CSP)
Este artigo explica como você pode usar os Azure Active Directory Domain Services em uma assinatura do Azure CSP.

## <a name="overview-of-azure-csp"></a>Visão geral do Azure CSP
O Azure CSP é um programa para Microsoft Partners e fornece um canal de licença para vários serviços de nuvem da Microsoft. O Azure CSP permite que os parceiros gerenciem vendas, tenham a propriedade da relação de cobrança, ofereçam suporte técnico e de cobrança e sejam o único ponto de contato dos clientes. Além disso, o Azure CSP fornece um conjunto completo de ferramentas, incluindo um portal de autoatendimento e APIs que o acompanha. Essas ferramentas permitem que os parceiros CSP facilmente provisionem e gerenciem recursos do Azure e forneçam a cobrança para os clientes e suas assinaturas.

O [Portal Partner Center](https://docs.microsoft.com/azure/cloud-solution-provider/overview/partner-center-overview) atua como um ponto de entrada para todos os parceiros Azure CSP. Ele fornece recursos de gerenciamento de clientes avançado, processamento automatizado e muito mais. Parceiros Azure CSP podem usar recursos do Centro de Parceiros usando uma interface de usuário baseada na Web ou usando o PowerShell e várias chamadas de API.

O diagrama a seguir ilustra como o modelo CSP funciona em um alto nível. A Contoso tem um Azure AD Active Directory. Eles têm uma parceria com um CSP, que implanta e gerencia os recursos na sua assinatura do Azure CSP. A Contoso também pode ter assinaturas regulares (diretas) do Azure, que são cobradas diretamente para a Contoso.

![Visão geral do modelo CSP](./media/csp/csp_model_overview.png)

O locatário do parceiro CSP tem três grupos especiais de agentes: Agentes administradores, Agentes de Suporte técnico e Agentes de Vendas. O grupo de agentes Administradores é atribuído à função de administrador de locatários no diretório do Microsoft Azure Active Directory da Contoso. Como resultado, um usuário que pertence ao grupo de agentes Administradores do parceiro CSP tem privilégios de administrador de locatários no diretório do Microsoft Azure Active Directory da Contoso. Quando o parceiro CSP provisiona uma assinatura do Azure CSP para a Contoso, seu grupo de agentes administradores é atribuído à função de proprietário para essa assinatura. Como resultado, os agentes administradores do parceiro CSP possuem os privilégios necessários para provisionar recursos do Azure como máquinas virtuais, redes virtuais e Azure Active Directory Domain Services em nome da Contoso.

Para saber mais, confira a [Visão geral do Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-overview)

## <a name="benefits-of-using-azure-ad-domain-services-in-an-azure-csp-subscription"></a>Benefícios de usar Azure Active Directory Domain Services uma assinatura do Azure CSP
Os Azure Active Directory Domain Services fornecem serviços compatíveis do AD no Azure como LDAP, autenticação Kerberos/NTLM, ingresso no domínio, política de grupo e DNS. Por décadas, muitos aplicativos foram criados para funcionar no AD usando esses recursos. Muitos fornecedores de software independentes (ISVs) têm criado e implantado aplicativos nos locais de seus clientes. Esses aplicativos possuem suporte oneroso, já que geralmente exige acesso aos diferentes ambientes em que esses aplicativos são implantados. Com assinaturas de Azure CSP, você tem uma alternativa mais simples com a escala e a flexibilidade do Azure.

O Azure AD Domain Services agora oferece suporte a assinaturas do Azure CSP. Agora é possível implantar seu aplicativo em uma assinatura do Azure CSP ligada ao diretório do Microsoft Azure Active Directory do seu cliente. Como resultado, os funcionários (equipe de suporte) podem gerenciar, administrar e fazer a manutenção das máquinas virtuais em que seu aplicativo é implantado usando credenciais corporativas da sua organização. Além disso, você pode provisionar um domínio gerenciado do Azure Active Directory Domain Services para o diretório do Azure AD do seu cliente. Seu aplicativo é conectado ao domínio gerenciado do cliente. Portanto, os recursos dentro de seu aplicativo que dependem de Kerberos/NTLM, LDAP ou a [API System.DirectoryServices](https://msdn.microsoft.com/library/system.directoryservices) funcionam perfeitamente em relação ao diretório de seu cliente. Os clientes finais muito se beneficiam consumindo seu aplicativo como um serviço, sem precisar se preocupar com a manutenção da infraestrutura em que de aplicativo é implantado.

Todas as cobranças para recursos do Azure que consumem essa assinatura, incluindo Azure Active Directory Domain Services, serão feitas a você. Você pode manter o controle total sobre a relação com o cliente quando se trata de vendas, cobrança, suporte técnico etc. Com a flexibilidade da plataforma Azure CSP, uma equipe pequena de agentes de suporte pode atender muitos clientes que possuem instâncias de seu aplicativo implantadas.


## <a name="csp-deployment-models-for-azure-ad-domain-services"></a>Modelos de implantação do CSP para serviços de domínio do Microsoft Azure Active Directory
Há duas formas em que é possível usar o Azure Active Directory Domain Services com uma assinatura do Asure CSP. Escolha a correta com base nas considerações com segurança e simplicidade que seus clientes têm.

### <a name="direct-deployment-model"></a>Modelo de implantação direta
Nesse modelo de implantação, os Azure Active Directory Domain Services são habilitados em uma rede virtual que pertence à assinatura do Azure CSP. Agentes administradores do parceiro CSP têm os privilégios a seguir:
* Privilégios de administrador global no diretório do Microsoft Azure Active Directory do cliente.
* Privilégios de proprietário da assinatura na assinatura do Azure CSP.

![Modelo de implantação direta](./media/csp/csp_direct_deployment_model.png)

Nesse modelo de implantação, os agentes administradores do provedor CSP podem administrar identidades para o cliente. Esses agentes administradores têm a capacidade de provisionar novos usuários, grupos, adicionar aplicativos dentro do diretório do Microsoft Azure Active Directory do cliente etc. Esse modelo de implantação pode ser adequado para organizações menores que não têm um administrador de identidades dedicado ou preferem que o parceiro CSP administre as identidades em seu nome.


### <a name="peered-deployment-model"></a>Modelo de implantação emparelhada
Nesse modelo de implantação, os Azure Active Directory Domain Services são habilitados em uma rede virtual que pertence ao cliente – isto é, uma assinatura Azure direta paga pelo cliente. O parceiro CSP pode, então, implantar aplicativos em uma rede virtual que pertencem à assinatura do CSP do cliente. As redes virtuais podem ser conectadas usando o emparelhamento de rede virtual do Azure. Como resultado, as cargas de trabalho/aplicativos implantados pelo parceiro CSP na assinatura do Azure CSP podem ser conectados ao domínio gerenciado do cliente, provisionado na assinatura do Azure direta do cliente.

![Modelo de implantação emparelhada](./media/csp/csp_peered_deployment_model.png)

Esse modelo de implantação fornece uma separação de privilégios e permite que os agentes de suporte técnico do parceiro CSP administrem a assinatura do Azure e implantem e gerenciar recursos dentro dele. No entanto, os agentes de suporte técnico do parceiro CSP não precisam ter privilégios de administrador global no diretório do Microsoft Azure Active Directory do cliente. Os administradores de identidades do cliente podem continuar a gerenciar identidades para sua organização.

Esse modelo de implantação pode ser adequado para cenários onde um ISV (fornecedor independente de software) fornece uma versão hospedada de seu aplicativo local, que também precisa ser conectada ao AD do cliente.


## <a name="administering-azure-ad-domain-services-managed-domains-in-csp-subscriptions"></a>Administração dos domínios gerenciados do Azure Active Directory Domain Services em assinaturas de CSP
As considerações importantes a seguir se aplicam ao administrar um domínio gerenciado em uma assinatura do Azure CSP:

* **Agentes administradores do CSP podem provisionar um domínio gerenciado usando suas credenciais:** Azure Active Directory Domain Services oferecem suporte a assinaturas do Azure CSP. Portanto, os usuários que pertencem ao grupo de agentes administradores do parceiro CSP podem provisionar um novo domínio gerenciado de Azure Active Directory Domain Services.

* **CSPs podem gerar scripts de criação de novos domínios gerenciados para seus clientes usando o PowerShell:** consulte [Como habilitar o domínio do Azure Active Directory Domain Services usando o PowerShell](active-directory-ds-enable-using-powershell.md) para obter detalhes.

* **Agentes administradores do CSP não podem executar tarefas de gerenciamento em andamento usando suas credenciais de domínio gerenciado:** usuários administradores do CSP não podem executar tarefas rotineiras de gerenciamento dentro do domínio gerenciado usando suas credenciais. Esses usuários são externos ao diretório do AD do Azure do cliente e suas credenciais não estão disponíveis no diretório do Microsoft Azure Active Directory do cliente. Portanto, os Azure Active Directory Domain Services não têm acesso aos hashes de senha de Kerberos e NTLM para esses usuários. Como resultado, esses usuários não podem ser autenticados em domínios gerenciados de Azure Active Directory Domain Services.

  > [!WARNING]
  > **Você deve criar uma conta de usuário no diretório do cliente para executar tarefas de administração contínuas no domínio gerenciado.**
  > Você não pode entrar no domínio usando as credenciais de um usuário administrador do CSP. Use as credenciais de uma conta de usuário que pertencem ao diretório do Microsoft Azure Active Directory do cliente para fazer isso. Você precisará de credenciais para tarefas como adicionar máquinas virtuais ao domínio gerenciado, administrar DNS, administrar Política de Grupo etc.
  >

* **A conta de usuário criada para administração contínua deve ser adicionada ao grupo “Administradores de controlador de domínio do AAD”:** o grupo “Administradores de controlador de domínio do AAD” não tem privilégios para realizar certas tarefas de administração delegadas no domínio gerenciado. Essas tarefas incluem configurar o DNS, criar unidades organizacionais, administrar a política de grupo etc. Para um parceiro CSP executar tarefas em um domínio gerenciado, uma conta de usuário precisa ser criada no diretório do Microsoft Azure Active Directory do cliente. As credenciais para esta conta devem ser compartilhadas com agentes administradores do parceiro CSP. Além disso, essa conta de usuário deve ser adicionada ao grupo “Administradores de controlador de domínio do AAD” para habilitar tarefas de configuração para o domínio a ser executado usando essa conta de usuário.


## <a name="next-steps"></a>Próximas etapas
* [Registre-se no programa Azure CSP](https://partnercenter.microsoft.com/partner/programs) e iniciar a criação de negócios por meio Azure CSP.
* Revise a lista de [serviços do Azure disponíveis no Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).
* [Habilitar o Azure AD Domain Services com o PowerShell](active-directory-ds-enable-using-powershell.md)
* [Introdução aos Serviços de Domínio do Azure AD](active-directory-ds-getting-started.md)
