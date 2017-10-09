---
title: "Executando novamente o Assistente para instalação do conectar Olá AD do Azure | Microsoft Docs"
description: "Explica como o Assistente de instalação Olá funciona Olá segunda vez que você executá-lo."
keywords: "Assistente de instalação do Hello AD do Azure Connect permite configurar Olá de configurações de manutenção segunda vez que você executá-lo"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Sincronização do Azure AD Connect: executando o Assistente de instalação de saudação uma segunda vez
Olá primeira vez que executar o Assistente de instalação do hello Azure AD Connect, ele orienta como tooconfigure sua instalação. Se você executar o Assistente de instalação Olá novamente, ele oferece opções para manutenção.

Você pode encontrar o Assistente de instalação Olá no menu de início Olá denominado **do Azure AD Connect**.

![Menu Iniciar](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Quando você inicia o Assistente de instalação hello, você pode ver uma página com as seguintes opções:

![Página com uma lista de tarefas adicionais](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Se tiver instalado o ADFS com o Azure AD Connect, você terá ainda mais opções. Olá opções adicionais disponíveis para AD FS estão documentados em [gerenciamento do ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Selecione uma das tarefas de saudação e clique em **próximo** toocontinue.

> [!IMPORTANT]
> Com o Assistente de instalação Olá aberto, todas as operações no mecanismo de sincronização de saudação são suspensos. Verifique se que você fechar o Assistente de instalação de saudação assim que você concluiu as alterações de configuração.
>
>

## <a name="view-current-configuration"></a>Exibir a configuração atual
Essa opção fornece uma visão rápida das opções configuradas no momento.

![Página com uma lista de todas as opções e seus estados](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Clique em **anterior** toogo novamente. Se você selecionar **Exit**, feche o Assistente de instalação de saudação.

## <a name="customize-synchronization-options"></a>Personalizar opções de sincronização
Essa opção é a configuração de sincronização de toohello toomake usado alterações. Você verá um subconjunto das opções do caminho de instalação de configuração personalizada de saudação. Você vê essa opção mesmo que tenha usado a instalação expressa inicialmente.

* [Adicionar mais diretórios](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Para remover um diretório, consulte [Excluir um Conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Alterar a filtragem de domínio e de unidade organizacional](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Remova a filtragem de grupo.
* [Alterar recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features).

Olá outras opções de instalação de saudação inicial não podem ser alteradas e não estão disponíveis. Essas opções são:

* Alterar Olá atributo toouse para userPrincipalName e sourceAnchor.
* Alterar Olá unindo o método para objetos de floresta diferente.
* Habilite a filtragem baseada em grupo.

## <a name="refresh-directory-schema"></a>Atualizar esquema de diretório
Essa opção é usada se você tiver alterado o esquema de saudação em uma das suas instalações florestas do AD DS. Por exemplo, você deve ter instalado o Exchange ou atualizar esquema tooa Windows Server 2012 com objetos de dispositivo. Nesse caso, você precisa tooinstruct do Azure AD Connect tooread Olá esquema novamente do AD DS e atualizar seu cache. Essa ação também regenera Olá regras de sincronização. Se você adicionar o esquema de saudação do Exchange, como um exemplo, regras de sincronização de saudação do Exchange são adicionadas toohello configuração.

Quando você seleciona essa opção, todos os diretórios de saudação em sua configuração são listados. Você pode manter a configuração padrão de saudação e atualizar todas as florestas ou desmarque algumas delas.

![Página com uma lista de todos os diretórios no ambiente de saudação](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Configurar modo de preparo
Essa opção permite que você tooenable e desabilitar o modo de preparo no servidor de saudação. Encontre mais informações sobre o modo de preparo e como ele é usado em [Operações](active-directory-aadconnectsync-operations.md#staging-mode).

opção Olá mostra se o preparo está habilitado ou desabilitado no momento:  
![Opção que também está mostrando o estado atual de saudação do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Olá estado, selecione essa opção e marque ou desmarque Olá caixa de seleção.  
![Opção que também está mostrando o estado atual de saudação do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Alterar a entrada do usuário
Essa opção permite que você toochange de toofederation de sincronização de senha ou Olá oposto. Você não pode alterar muito**não configurar**.

Para obter mais informações sobre essa opção, consulte [entrada do usuário](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o modelo de configuração de saudação usado pela sincronização do Azure AD Connect em [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
