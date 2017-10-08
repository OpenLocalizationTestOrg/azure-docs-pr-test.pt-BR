---
title: "aaaHow tooconfigure usuário Provisionando o aplicativo de galeria tooan AD do Azure | Microsoft Docs"
description: "Como você pode rapidamente configurar conta de usuário avançado, provisionamento e desprovisionamento tooapplications já está listado no hello Galeria de aplicativos do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Como usuário tooconfigure Provisionando o aplicativo de galeria tooan AD do Azure

*Provisionamento de conta de usuário* é Olá ato de criar, atualizar e/ou desabilitando os registros de conta de usuário no repositório de perfil de usuário local do aplicativo. A maioria dos aplicativos SaaS e nuvem armazenam a função hello usuários e permissões em seu próprio armazenamento de perfil de usuário local e a presença de um registro de usuário em seu repositório local é *necessária* para toowork única de logon e acesso.

No portal do Azure de Olá, Olá **provisionamento** guia no painel de navegação à esquerda de saudação de um aplicativo Empresarial exibe quais modos de provisionamento têm suporte para esse aplicativo. Existem dois valores válidos:

## <a name="configuring-an-application-for-manual-provisioning"></a>Configurar um aplicativo para o provisionamento manual

*Manual* provisionamento significa que as contas de usuário devem ser criadas manualmente usando os métodos Olá fornecidos por esse aplicativo. Isso pode significar fazendo logon em um portal administrativo para que o aplicativo e adicionar usuários usando uma interface do usuário baseada na web. Ou ele pode carregar uma planilha com detalhes da conta de usuário, usando um mecanismo fornecido pelo aplicativo. Consulte a documentação de saudação fornecido pelo app hello, ou contato Olá mecanismos do desenvolvedor toodetermine wat estão disponíveis.

Se Manual é modo somente Olá mostrado para um determinado aplicativo, isso significa que nenhum conector de provisionamento do AD do Azure automática foi criado para o aplicativo hello ainda. Ou, isso significa que aplicativo de saudação não não suporte Olá usuário pré-requisito API de gerenciamento ao qual toobuild um conector de provisionamento automatizado.

Se você quiser toorequest suporte para o provisionamento automático para um determinado aplicativo, você pode preencher uma solicitação em <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Configurar um aplicativo para o provisionamento automático

*Automático* significa que o conector de provisionamento do Azure AD foi desenvolvido para este aplicativo. Para obter mais informações sobre Olá AD do Azure, o provisionamento de serviço e como ele funciona, consulte [tooSaaS automatizar o provisionamento de usuário e desprovisionamento aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Para obter mais informações sobre como tooprovision determinados usuários e aplicativos de tooan de grupos, consulte [Gerenciando o provisionamento de conta de usuário para aplicativos corporativos](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Olá tooenable necessárias etapas reais e configurar o provisionamento automático variam de acordo com o aplicativo hello.

>[!NOTE]
>Você deve começar encontrando Olá toosetting tutorial específicas de instalação o provisionamento para seu aplicativo e seguir essas etapas tooconfigure aplicativo hello e toocreate do AD do Azure Olá provisionamento de conexão. 
>
>

Tutoriais de aplicativo podem ser encontrados em [lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Tooconsider uma coisa importante quando a configuração de provisionamento ser tooreview e configurar mapeamentos de atributo hello e fluxos de trabalho que definem quais fluxo de propriedades de usuário (ou grupo) do aplicativo de toohello do AD do Azure. Isso inclui a configuração hello "correspondência da propriedade" ser toouniquely usada identificar e corresponder usuários/grupos entre sistemas Olá dois. Para obter mais informações sobre esse processo importante.

## <a name="next-steps"></a>Próximas etapas
[Personalizar os mapeamentos de atributos de provisionamento de usuário para aplicativos SaaS no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

