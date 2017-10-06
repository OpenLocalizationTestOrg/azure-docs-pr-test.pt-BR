---
title: "aaaConnectors em hello Azure o Gerenciador de serviço de sincronização do AD UI | Microsoft Docs"
description: "Entenda o guia conectores Olá Olá Synchronization Service Manager para conexão do AD do Azure."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Usando conectores com hello Azure AD Connect sincronização Service Manager

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

Guia de conectores Olá é usado toomanage todos os mecanismos de sincronização de saudação sistemas está conectado ao.

## <a name="connector-actions"></a>Ações do Conector
| Ação | Comentário |
| --- | --- |
| Criação |Não use. Para conectar-se tooadditional AD florestas, use o Assistente de instalação de saudação. |
| Propriedades |Usado para filtragem de domínio e de UO. |
| [Excluir](#delete) |Tooeither usado excluir dados de Olá Olá conector espaço ou toodelete conexão tooa floresta. |
| [Configurar perfis de execução](#configure-run-profiles) |Exceto para o domínio de filtragem, nada tooconfigure aqui. Você pode usar essa ação perfis de execução toosee já configurado. |
| Executar |Usado toostart um one-off executado de um perfil. |
| Parar |Interrompe um Conector que, atualmente, executa um perfil. |
| Exportar Conector |Não use. |
| Importar Conector |Não use. |
| Atualizar Conector |Não use. |
| Atualizar Esquema |Atualiza o esquema em cache hello. É preferencial toouse Olá opção no Assistente de instalação de saudação em vez disso, desde que também atualizações sincronizar regras. |
| [Pesquisar Espaço do Conector](#search-connector-space) |Toofind objetos usados e muito[siga um objeto e seus dados por meio do sistema Olá](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Exclusão
ação de exclusão de saudação é usada para duas coisas diferentes.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Olá opção **excluir apenas o espaço do conector** remove todos os dados, mas manter Olá configuração.

Olá opção **espaço do conector e excluir o conector** remove dados saudação e configuração de saudação. Essa opção é usada quando você não deseja tooconnect tooa floresta mais.

Ambas as opções sincronizar todos os objetos e atualizar objetos do metaverso hello. Essa ação é uma operação demorada.

### <a name="configure-run-profiles"></a>Configurar perfis de execução
Essa opção permite que você toosee Olá perfis configurados para um conector de execução.

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Pesquisar Espaço do Conector
ação de espaço de conector de pesquisa de saudação é útil toofind objetos e solucionar problemas de dados.

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Comece selecionando um **escopo**. Você pode procurar dados com base em (RDN, DN, âncora, subárvore), ou de estado do objeto de saudação (todas as outras opções).  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Por exemplo, se fizer uma pesquisa em Subárvore, você obterá todos os objetos em uma UO.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
Dessa grade, você pode selecionar um objeto, selecione **propriedades**, e [segui-la](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) do espaço do conector Olá origem, por meio de metaverso Olá e toohello espaço do conector de destino.

### <a name="changing-hello-ad-ds-account-password"></a>Alterar a senha da conta Olá AD DS
Se você alterar a senha da conta Olá, Olá serviço de sincronização deixará de ser capaz de tooimport/exportação tooon alterações locais AD.   Você pode ver o seguinte hello:

- etapa de importação/exportação Olá para Olá conector AD falha com erro de "credenciais de início não".
- Em Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com o evento ID 6000 e a mensagem "Olá toorun de agente"contoso.com"falhado de gerenciamento porque as credenciais de saudação eram inválidas."

Olá tooresolve emitir, conta de usuário Olá AD DS de atualização usando Olá seguintes:


1. Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Vá toohello **conectores** guia.
3. Selecione Olá conector do AD que é configurado toouse hello conta AD DS.
4. Em Ações, selecione **Propriedades**.
5. Na caixa de diálogo pop-up Olá, selecione conectar tooActive diretório floresta:
6. nome da floresta Olá indica Olá correspondente local AD.
7. nome de usuário de saudação indica a conta do hello AD DS usada para sincronização.
8. Digite hello nova senha da conta do hello AD DS na caixa de texto de senha Olá ![do Azure AD conectar-se sincronização criptografia de chave de utilitário](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Clique em nova senha do toosave Okey hello e reinicie Olá serviço de sincronização tooremove Olá senha antiga do cache de memória.



## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
