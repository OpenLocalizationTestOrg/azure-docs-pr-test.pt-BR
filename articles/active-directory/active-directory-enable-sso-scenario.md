---
title: aaaManaging aplicativos com o Active Directory do Azure | Microsoft Docs
description: "Benefícios de saudação este artigo da integração do Active Directory do Azure com seu local, nuvem e aplicativos SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Gerenciamento de aplicativos com o Active Directory do Azure
Além de fluxo de trabalho real hello ou conteúdo, as empresas têm dois requisitos básicos para todos os aplicativos:

1. produtividade tooincrease, os aplicativos devem ser fácil toodiscover e acesso
2. segurança tooenable e governança, Olá organização precisar de controle e supervisão sobre quem pode e, na verdade, está acessando cada aplicativo

Em Olá mundo de aplicativos em nuvem isso melhor pode ser obtido usando a identidade toocontrol "*que é permitido toodo que*".

Na terminologia de computação:

* *Quem* é conhecido como *identidade* -Olá gerenciamento de usuários e grupos
* *O que* é conhecido como *gerenciamento de acesso* – Olá gerenciamento de recursos de tooprotected de acesso

Ambos os componentes juntos são conhecidos como *identidade e gerenciamento de acesso (IAM)*, que é definido pelo Olá [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) grupo como "*Olá disciplina de segurança que permite que o direito de saudação indivíduos tooaccess Olá direita recursos Olá direita vezes por motivos de direito Olá*".

Okey, o que é o problema de Olá? Se o IAM *não for gerenciado* em um só lugar com uma solução integrada:

* Os administradores de identidade tem tooindividually criar e atualizar contas de usuário em todos os aplicativos separadamente, uma atividade de redundância e demorada.
* Os usuários têm toomemorize vários aplicativos de saudação do tooaccess credenciais precisam toowork com. Como resultado, os usuários tendem a toowrite suas senhas ou usam outras soluções de gerenciamento de senha que apresenta outros riscos de segurança de dados.
* Atividades redundantes, demoradas reduzem a quantidade de saudação de tempo que os usuários e administradores estão trabalhando em atividades de negócios, aumentam a lucratividade.

Portanto, o que geralmente impede que as organizações adotem soluções integradas de IAM?

* Soluções mais técnicas são baseadas em plataformas de software que precisam toobe implantado e adaptado por cada organização para seus próprios aplicativos.
* Aplicativos de nuvem normalmente são adotados a uma taxa mais alta do que a organização de TI pode integrar com as soluções de IAM existentes.
* Ferramentas de monitoramento e de segurança exigem personalização e integração tooachieve abrangente E2E cenários adicionais.

## <a name="azure-active-directory-integrated-with-applications"></a>Active Directory do Azure integrado com aplicativos
O Active Directory do Azure é a solução IDaaS (Identidade como Serviço) abrangente da Microsoft que:

* Habilita o IAM como um serviço de nuvem 
* Fornece gerenciamento de acesso central, logon único (SSO) e relatórios 
* Oferece suporte ao gerenciamento de acesso integrado para [milhares de aplicativos](https://azure.microsoft.com/marketplace/active-directory/) na Galeria de aplicativo hello, incluindo Salesforce, Google Apps, caixa, Concur e muito mais. 

Com o Azure Active Directory, todos os aplicativos que você publicar para seus parceiros e clientes (comercial ou consumidor) têm Olá mesmos recursos de gerenciamento de identidades e acesso.<br> Isso permite que você toosignificantly reduzir os custos operacionais.

Se você precisar tooimplement um aplicativo que ainda não estiver listado na Galeria de aplicativos Olá? Embora esse seja um pouco mais demorado do que a configuração de SSO para aplicativos da Galeria de aplicativo hello, o Azure AD fornece um assistente que ajuda você na configuração de saudação.

valor de saudação do AD do Azure vai além da "simplesmente" aplicativos em nuvem. Você também pode usar com aplicativos locais, fornecendo acesso remoto seguro. Acesso remoto seguro, você pode eliminar a necessidade de saudação de saudação para VPNs ou outras implementações de gerenciamento de acesso remoto tradicionais.

Fornecendo gerenciamento de acesso central e logon único (SSO) para todos os aplicativos, o AD do Azure fornece a solução de saudação problemas de segurança e a produtividade de dados principal toohello.

* Os usuários podem acessar vários aplicativos com um logon fornecendo tooincome de tempo mais negócios ou gerar atividades de operações realizadas.
* Os administradores de identidade podem gerenciar acesso tooapplications em um único local.

Olá benefício para usuário Olá em sua empresa é óbvio. Vamos examinar mais detalhadamente os benefícios de saudação para um administrador de identidade e a organização de saudação.

## <a name="integrated-application-benefits"></a>Benefícios de aplicativos integrados
Olá processo SSO tem duas etapas:

* Autenticação, o processo de saudação de validar a identidade do usuário hello.
* Olá tooenable decisão de autorização, ou bloquear acesso tooa recursos com uma política de acesso.

Ao usar aplicativos de toomanage do AD do Azure e habilitar o SSO:

* A autenticação é feita em do usuário da saudação (por exemplo, AD) local ou conta do AD do Azure.
* Autorização é executado no hello AD do Azure proteção e atribuição de política garantindo a experiência do usuário final consistente e permitindo que você tooadd atribuição, locais e as condições MFA em qualquer aplicativo, independentemente de seus recursos internos.

Importante toounderstand que Olá autorização de saudação de forma é aplicada no aplicativo de destino hello varia, dependendo de como o aplicativo hello foi integrado ao AD do Azure.

* **Aplicativos pré-integrados pelo provedor de serviços** Como o Office 365 e o Azure, estes são aplicativos criados diretamente no AD do Azure e que dependem dele para seus recursos abrangentes de gerenciamento de identidades e de acesso. Os aplicativos do Access toothese é habilitado por meio de emissão de token e de informações de diretório.
* **Aplicativos pré-integrados pela Microsoft e aplicativos personalizados** Estes são aplicativos de nuvem independentes que dependem de um diretório interno de aplicativos e que podem funcionar independentemente do AD do Azure. Aplicativos de toothese de acesso está habilitado por meio de uma conta de aplicativos do aplicativo específico credencial mapeada tooan. Dependendo de recursos do aplicativo hello, credencial Olá pode ser um token de Federação ou o nome de usuário e a senha de uma conta que foi anteriormente provisionada no aplicativo hello.
* **Aplicativos locais** aplicativos publicados por meio do proxy de aplicativo de saudação do AD do Azure principalmente habilitar acesso local tooon aplicativos. Esses aplicativos dependem de um diretório local central, como o Windows Server Active Directory. Aplicativos de toothese de acesso está habilitado disparando Olá toodeliver Olá aplicativo toohello conteúdo final do usuário de proxy respeitar o requisito de logon do local de hello.

Por exemplo, se um usuário ingressar em sua organização, você precisa toocreate uma conta de usuário Olá no AD do Azure para operações de logon principal hello. Se esse usuário requer acesso tooa gerenciado aplicativo como o Salesforce, você também precisará toocreate uma conta para esse usuário no Salesforce e vincule-o trabalho SSO de toomake toohello conta do Azure. Quando o usuário Olá sai da organização, é aconselhável toodelete Olá conta AD do Azure e todas as contas de contraparte Olá repositórios IAM dos aplicativos Olá Olá usuário tem acesso.

## <a name="access-detection"></a>Detecção de acesso
Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos de nuvem Olá que estão sendo usados. Em conjunto com o Cloud App Discovery, AD do Azure fornece uma solução toodetect esses aplicativos.

## <a name="account-management"></a>Gerenciamento de Contas
Tradicionalmente, vários aplicativos de gerenciamento de contas em Olá é um processo manual executado pelo IT ou pessoais na organização de saudação de suporte. O AD do Azure automatizou por completo o gerenciamento de contas em todos os aplicativos integrados do provedor de serviços e os aplicativos pré-integrados pela Microsoft que dão suporte ao provisionamento automatizado de usuários ou JIT do SAML.

## <a name="automated-user-provisioning"></a>Provisionamento automatizado de usuários
Alguns aplicativos fornecem interfaces de automação para a criação e remoção (ou desativação) de contas. Se um provedor oferecer uma interface desse tipo, ele será aproveitado pelo AD do Azure. Isso reduz os custos operacionais porque tarefas administrativas ocorrem automaticamente e melhora a segurança de saudação do seu ambiente porque ele diminui a chance de saudação do acesso não autorizado.

## <a name="access-management"></a>gerenciamento de acesso
Usando o AD do Azure você pode gerenciar o acesso tooapplications usando individuais ou controlado por atribuições de regra. Você também pode delegar acesso gerenciamento toohello direito de pessoas na Olá organização garantir Olá melhor supervisão e reduzindo carga saudação do suporte técnico.

## <a name="on-premises-applications"></a>Aplicativos locais
Olá interna do proxy de aplicativo permite que você toopublish os usuários de tooyour de aplicativos local resultando em ambos consistente acessam experiência com os benefícios de aplicativo e hello nuvem modernos de monitoramento do AD do Azure, relatórios e recursos de segurança .

## <a name="reporting-and-monitoring"></a>Relatórios e monitoramento
O AD do Azure fornece pré-integrados de monitoramento e relatório que permitem que você tooknow quem tem acesso tooapplications e quando eles realmente usavam-los.

## <a name="related-capabilities"></a>Recursos relacionados
Com o AD do Azure, é possível proteger seus aplicativos com políticas de acesso granular e MFA pré-integrado. toolearn mais sobre o Azure MFA, consulte [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Introdução
tooget iniciar a integração de aplicativos com o Azure AD, dê uma olhada Olá [guia de introdução de integração do Active Directory do Azure com aplicativos obtendo](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Consulte também
[Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

