---
title: "Sincronização do Azure AD Connect: impedir exclusões acidentais | Microsoft Docs"
description: "Este tópico descreve Olá impedir que o recurso de exclusões acidentais (impedindo exclusões acidentais) no Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Sincronização do Azure AD Connect: impedir exclusões acidentais
Este tópico descreve Olá impedir que o recurso de exclusões acidentais (impedindo exclusões acidentais) no Azure AD Connect.

Ao instalar o Azure AD Connect, evitar acidental exclusões é habilitado por padrão e toonot configurado permitir uma exportação com mais de 500 exclusões. Esse recurso é projetado tooprotect de configuração acidental alterações e alterações de diretório local tooyour que possa afetar vários usuários e outros objetos.

## <a name="what-is-prevent-accidental-deletes"></a>O que é impedir exclusões acidentais
Os cenários comuns quando você vê muitas exclusões incluem:

* Alterações muito[filtragem](active-directory-aadconnectsync-configure-filtering.md) onde toda uma [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) ou [domínio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) não estiver selecionada.
* Todos os objetos em uma UO são excluídos.
* Uma unidade Organizacional é renomeada para que todos os objetos são considerados toobe fora do escopo de sincronização.

valor de padrão de saudação 500 objetos pode ser alterado com o PowerShell usando `Enable-ADSyncExportDeletionThreshold`. Você deve configurar esse tamanho de saudação do valor toofit da sua organização. Desde que o Agendador de sincronização de saudação é executado a cada 30 minutos, o valor de Olá é número de saudação de exclusões visto dentro de 30 minutos.

Se houver muitos toobe de exclusões preparadas exportado tooAzure AD, e em seguida, hello de exportação será interrompido e você receberá um email assim:

![Impedir exclusões de email acidentais](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Saudação (contato técnico). Em (tempo) Olá serviço de sincronização de identidade detectou que o número Olá de exclusões excedeu o limite de exclusão configurado hello (nome da organização). Um total de (número) objetos foram enviados para exclusão nesta execução da sincronização de Identidade. Isso atingido ou excedido o valor de limite de exclusão de saudação configurada de objetos (número). Precisamos confirmação tooprovide que essas exclusões devem ser processados antes que possa continuar. Consulte Olá impedindo exclusões acidentais para obter mais informações sobre o erro Olá listado nesta mensagem de email.*
>
> 

Você também pode ver o status de saudação `stopped-deletion-threshold-exceeded` quando você examinar Olá **Synchronization Service Manager** interface do usuário para o perfil de exportação de saudação.
![Impedir exclusões acidentais na interface do usuário do Synchronization Service Manager](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Caso isso não seja esperado, investigue e tome medidas corretivas. toosee quais objetos são sobre toobe excluído, Olá a seguir:

1. Iniciar **serviço de sincronização** de saudação Menu Iniciar.
2. Vá muito**conectores**.
3. Selecione Olá conector com o tipo **Active Directory do Azure**.
4. Em **ações** toohello à direita, selecione **espaço do conector de pesquisa**.
5. Em Olá pop-up sob **escopo**, selecione **desconectado porque** e escolha um horário em Olá anterior. Clique em **Pesquisar**. Esta página fornece uma exibição de todos os objetos sobre toobe excluído. Ao clicar em cada item, você pode obter informações adicionais sobre o objeto de saudação. Você também pode clicar em **coluna configuração** tooadd adicional atributos toobe visível na grade de saudação.

![Pesquisar Espaço do Conector](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Se todas as exclusões de saudação forem desejadas, em seguida, Olá a seguir:

1. tooretrieve Olá exclusão limite atual, execute o cmdlet do PowerShell Olá `Get-ADSyncExportDeletionThreshold`. Forneça uma conta e senha de Administrador Global do Azure AD. valor padrão de saudação é 500.
2. tootemporarily desabilitar essa proteção e permitem que as exclusões percorrer, execute o cmdlet do PowerShell Olá: `Disable-ADSyncExportDeletionThreshold`. Forneça uma conta e senha de Administrador Global do Azure AD.
   ![Credenciais](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Com hello Azure Active Directory Connector ainda selecionado, selecione a ação de saudação **executar** e selecione **exportar**.
4. toore-habilitar a proteção hello, execute o cmdlet do PowerShell Olá: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Substitua 500 valor Olá observado ao recuperar o limite atual de exclusão de saudação. Forneça uma conta e senha de Administrador Global do Azure AD.

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
