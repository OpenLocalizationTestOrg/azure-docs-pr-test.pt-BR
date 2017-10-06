---
title: "provisionamento de gerenciamento para aplicativos de empresa no Active Directory do Azure de saudação do aaaUser | Microsoft Docs"
description: "Saiba como usuário toomanage provisionamento de conta para aplicativos de empresa usando Olá Active Directory do Azure"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Gerenciar a conta de usuário de provisionamento para aplicativos da empresa no hello portal do Azure
Este artigo descreve como Olá toouse [portal do Azure](https://portal.azure.com) categoria de conta de usuário automático toomanage provisionamento e cancelamento de provisionamento para aplicativos que dão suporte a ele, especialmente aqueles que tenham sido adicionados de saudação "recursos" Olá [Galeria de aplicativos do Active Directory do Azure](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn mais sobre o provisionamento de conta de usuário automático e como ele funciona, consulte [tooSaaS automatizar o provisionamento de usuário e desprovisionamento aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Localizando seus aplicativos no portal de saudação
Todos os aplicativos que são configurados para logon único em um diretório, por um administrador de diretório usando Olá [Galeria de aplicativos do Active Directory do Azure](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), podem ser exibidas e gerenciadas no hello [portal do Azure](https://portal.azure.com). aplicativos Olá podem ser encontrados no hello **mais serviços** &gt; **aplicativos empresariais** seção do portal de saudação. Aplicativos empresariais são aplicativos que são implantados e usados dentro da sua organização.

![Folha de Aplicativos Empresariais][0]

Olá selecionando **todos os aplicativos** link Olá esquerda mostra uma lista de todos os aplicativos que tiverem sido configurados, incluindo aplicativos que tinham sido adicionados da Galeria de saudação. Selecionar um aplicativo carrega a folha de recursos Olá para esse aplicativo, onde os relatórios podem ser exibidos para esse aplicativo e uma variedade de configurações que pode ser gerenciada.

Configurações de provisionamento de conta de usuário pode ser gerenciada selecionando **provisionamento** Olá esquerda.

![Folha de recursos do aplicativo][1]

## <a name="provisioning-modes"></a>Modos de provisionamento
Olá **provisionamento** folha começa com um **modo** menu, que mostra quais modos de provisionamento têm suporte para um aplicativo corporativo e permite que eles toobe configurado. Olá as opções disponíveis incluem:

* **Automático** -esta opção será exibida se o AD do Azure dá suporte ao provisionamento automático baseado em APIs e/ou cancelamento de provisionamento do aplicativo de toothis de contas de usuário. Selecionar este modo exibe uma interface que orienta os administradores por meio da configuração da API de gerenciamento de usuário do aplicativo do AD do Azure tooconnect toohello, Criando mapeamentos de conta e fluxos de trabalho que definem como os dados da conta de usuário devem fluir entre o Azure AD e aplicativo Hello e gerenciando Olá serviço de provisionamento de AD do Azure.
* **Manual** -esta opção é mostrada se AD do Azure não suporta o provisionamento automático do aplicativo de toothis de contas de usuário. Esta opção significa que os registros de conta de usuário armazenados no aplicativo hello devem ser gerenciados usando um processo externo, com base nos produtos de recursos de gerenciamento e provisionamento de usuário Olá fornecidos por esse aplicativo (que pode incluir o provisionamento de SAML just-in-).

## <a name="configuring-automatic-user-account-provisioning"></a>Configurar o provisionamento de contas de usuário automático
Olá selecionando **automáticas** opção exibe uma tela que é dividida em quatro seções:

### <a name="admin-credentials"></a>Credenciais de administrador
Isso é onde as credenciais Olá necessárias para a API de gerenciamento de usuário do aplicativo do AD do Azure tooconnect toohello são inseridas. entrada Hello necessária varia dependendo do aplicativo hello. toolearn sobre tipos de credencial de saudação e os requisitos para aplicativos específicos, consulte Olá [tutorial de configuração para o aplicativo específico](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Olá selecionando **Conexão de teste** botão permite que você as credenciais de saudação tootest fazendo com que o AD do Azure tente tooconnect toohello aplicativo de provisionamento do aplicativo usando as credenciais de saudação fornecida.

### <a name="mappings"></a>Mapeamentos
Isso é onde os administradores podem exibir e editar o fluxo de atributos de usuário entre o Azure AD e o aplicativo de destino hello, quando as contas de usuário são provisionadas ou atualizadas.

Há um conjunto predefinido de mapeamentos entre objetos de usuário do Azure AD e objetos de usuário de cada aplicativo SaaS. Alguns aplicativos gerenciam outros tipos de objetos, como grupos ou contatos. Selecionando um desses mapeamentos na tabela Olá mostra o editor de mapeamento de saudação toohello direita, onde podem ser exibidas e personalizadas.

![Folha de recursos do aplicativo][2]

As personalizações com suporte incluem:

* Habilitando e desabilitando mapeamentos para objetos específicos, como o objeto de usuário de saudação do AD do Azure usuário objeto toohello SaaS do aplicativo.
* Editar fluam de quais atributos de objeto de usuário do aplicativo da toohello do objeto de usuário da saudação do AD do Azure. Para obter mais informações sobre mapeamento de atributos, confira [Noções básicas sobre tipos de mapeamento de atributos](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Saudação de filtro provisionamento ações que executa o AD do Azure em Olá direcionou um aplicativo. Em vez de ter o AD do Azure totalmente-sincronizar objetos, você pode limitar ações Olá executadas. Por exemplo, selecionando apenas **Atualizar**, o Azure AD atualiza apenas contas de usuário existentes em um aplicativo e não cria novas. Selecionando apenas **Criar**, o Azure só cria novas contas de usuário, mas não atualiza as existentes. Esse recurso permite que administradores toocreate diferentes mapeamentos de conta de fluxos de trabalho de criação e atualização.

### <a name="settings"></a>Configurações
Esta seção permite que administradores toostart e Olá parar o serviço de provisionamento do Azure AD para o aplicativo hello selecionado, bem como o provisionamento de hello, opcionalmente, desmarque cache e reinicie o serviço de saudação.

Se o provisionamento está sendo habilitado para Olá primeira vez para um aplicativo, ativar o serviço de saudação alterando Olá **Status de provisionamento** muito**em**. Isso faz com que Olá AD do Azure provisionamento serviço tooperform uma sincronização inicial, onde ele lê a usuários de saudação atribuídos em Olá **usuários e grupos** seção, consultas de aplicativo de destino hello para eles e executa Olá provisionamento as ações definidas no AD do Azure de saudação **mapeamentos** seção. Durante esse processo, Olá serviço de configuração armazena em cache dados sobre quais contas de usuário que está gerenciando, para que contas não gerenciados em aplicativos de destino Olá nunca no escopo de atribuição não são afetadas por operações de cancelamento do provisionamento. Depois de saudação a sincronização inicial, Olá automaticamente o serviço de configuração sincroniza objetos de usuário e grupo em um intervalo de dez minutos.

Olá alteração **Status de provisionamento** muito**Off** simplesmente pausa Olá serviço de provisionamento. Nesse estado, Azure não criar, atualizar ou remover qualquer usuário ou objetos de grupo no aplicativo hello. Alterar Olá estado back tooon faz com que o hello serviço toopick onde parou.

Olá selecionando **limpar o estado atual e reinicie a sincronização** caixa de seleção e salvando paradas Olá serviço de provisionamento, despejos Olá armazenado em cache dados sobre as contas do AD do Azure está gerenciando, reinicia os serviços hello e executa Olá sincronização inicial novamente. Essa opção permite que os administradores toostart Olá processo de implantação de provisionamento novamente.

### <a name="synchronization-details"></a>Detalhes da sincronização
Esta seção fornece detalhes de adição sobre Olá Olá provisionamento de serviço, incluindo o serviço de provisionamento vezes e o sobrenome Olá Olá executou em aplicativo hello e quantos objetos de usuário e grupo que estão sendo gerenciados.

São fornecidos links toohello **relatório de atividade de provisionamento**, que fornece um log de todos os usuários e grupos criados, atualizado e removido entre o AD do Azure e o aplicativo de destino hello e toohello **erro de provisionamento relatório** que fornece mais detalhadas de mensagens de erro para o usuário e grupo de objetos que toobe com falha de leitura, criado, atualizado ou removido. 

##<a name="feedback"></a>Comentários

Esperamos que você goste de sua experiência com o Azure AD. Mantenha comentários Olá vindo! Poste seus comentários e ideias para a melhoria nos Olá **Portal de administração** seção do nosso [Fórum de comentários](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Nos estiver contentes sobre a criação de novo e interessante diariamente e usar tooshape sua orientação e definir o que devemos construir a seguir.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
