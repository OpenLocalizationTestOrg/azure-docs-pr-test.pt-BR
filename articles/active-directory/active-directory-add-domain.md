---
title: "nome de seu domínio personalizado de aaaAdd tooAzure do Active Directory | Microsoft Docs"
description: "Como tooadd da sua empresa nomes de domínio tooAzure do Active Directory, e como tooverify Olá nome de domínio."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Adicionar um nome de domínio personalizado tooAzure do Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-domains-add-azure-portal.md)
> * [Portal clássico do Azure](active-directory-add-domain.md)
> 
> 

Você tem um ou mais nomes de domínio que sua organização usa toodo business e seus usuários entrar na rede corporativa do tooyour usando seu nome de domínio corporativo. Agora que você estiver usando o Azure Active Directory (AD do Azure), você pode adicionar seu domínio corporativo nome tooAzure AD também. Isso permite nomes de usuário tooassign no diretório de saudação que são usuários tooyour familiarizado, como 'alice@contoso.com.' processo de saudação é simple:

1. Adicionar o diretório de tooyour de nome de domínio personalizado Olá
2. Adicionar uma entrada DNS para o nome de domínio Olá no registrador de nome de domínio Olá
3. Verifique se o nome de domínio personalizado Olá no AD do Azure

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para tooadd seu nome de domínio da empresa no Centro de administração de saudação do AD do Azure, consulte [atribuindo funções de administrador no Azure Active Directory](active-directory-domains-add-azure-portal.md).

Se você planejar tooconfigure seu toobe de nome de domínio personalizado usado com os serviços de Federação do Active Directory (AD FS) ou um serviço de token de segurança (STS) em sua rede corporativa, siga as instruções de saudação em [adicionar e configurar um domínio para Federação com o Active Directory do Azure](active-directory-add-domain-federated.md). Isso é útil se você planejar toosynchronize usuários de tooAzure seu diretório corporativo AD, e [sincronização de hash de senha](active-directory-aadconnectsync-implement-password-synchronization.md) não atender às suas necessidades.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Adicionar um diretório de tooyour de nome de domínio personalizado
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com uma conta de usuário que seja um administrador global do seu diretório do AD do Azure.
2. Em **do Active Directory**, abra a pasta e selecione Olá **domínios** guia.
3. Na barra de comandos hello, selecione **adicionar**. Insira o nome de saudação do seu domínio personalizado, como 'contoso.com'. Certifique-se de que tooinclude hello. com, .net ou outra extensão de nível superior e deixe Olá caixa de seleção "logon único" desmarcada (federação).
4. Selecione **Adicionar**.
5. Na segunda página do Assistente para Adicionar domínio de Olá Olá, obter Olá entrada DNS que o AD do Azure usará tooverify se sua organização possui o nome de domínio personalizado hello.

Agora que você adicionou o nome de domínio hello, AD do Azure deve verificar se sua organização possui o nome de domínio hello. Antes de executar essa verificação do AD do Azure, você deve adicionar uma entrada DNS no arquivo de zona DNS Olá Olá nome de domínio. Essa tarefa é executada no site Olá para o registrador de nome de domínio para o nome de domínio hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Adicionar entrada de DNS de saudação no registrador de nome de domínio Olá para domínio Olá
Olá próxima etapa toouse nome do seu domínio personalizado com o Azure AD é arquivo de zona DNS tooupdate Olá para o domínio de saudação. Isso permite que tooverify do AD do Azure que sua organização possui o nome de domínio personalizado hello.

1. Entrar toohello registrador de nome de domínio para o domínio de saudação. Se você não tiver Olá tooupdate de acesso a entrada de DNS, pergunte pessoa hello ou equipe que possui esta etapa toocomplete de acesso 2 e toolet que saber quando ela estiver concluída.
2. Atualize o arquivo de zona DNS Olá para o domínio de saudação adicionando Olá DNS entrada fornecida tooyou pelo AD do Azure. Essa entrada DNS permite que tooverify do AD do Azure para sua propriedade de domínio de saudação. Olá entrada DNS não altera qualquer comportamento, como roteamento de email ou hospedagem na web.

Para obter ajuda com essa entrada DNS adicionando hello, leia [instruções para adicionar uma entrada de DNS em registradores DNS populares](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificar Olá nome de domínio com o Azure AD
Depois de adicionar entrada DNS Olá, você está pronto tooverify nome de domínio Olá com o Azure AD.

Se você ainda tiver Olá **Adicionar domínio** assistente, selecione Abrir, **verificar** na terceira página saudação do Assistente de saudação. Quando você seleciona **verificar**, AD do Azure procurará a entrada DNS Olá no arquivo de zona DNS Olá para o domínio de saudação. O AD do Azure pode verificar o nome de domínio de saudação somente depois que os registros DNS Olá tenham se propagado. Essa propagação geralmente leva apenas alguns segundos, mas às vezes pode levar uma hora ou mais. Se a verificação não funcionar Olá primeira vez, tente novamente mais tarde.

Se hello **Adicionar domínio** assistente não estiver aberto, você pode verificar o domínio Olá Olá [portal clássico do Azure](https://manage.windowsazure.com/):

1. Entre com uma conta de usuário que seja um administrador global do diretório do AD do Azure.
2. Abra seu diretório e selecione Olá **domínios** guia.
3. O nome de domínio Olá selecione que você deseja tooverify e selecione **verificar** na barra de comandos de saudação.
4. Selecione **verificar** na verificação de Olá Olá diálogo caixa toocomplete.

Agora você pode [atribuir nomes de usuário que incluam o nome de domínio personalizado](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Solucionar problemas
Se você não puder verificar um nome de domínio personalizado, tente o seguinte hello. Vamos começar com hello mais comuns e de trabalho para baixo toohello menos comuns.

1. **Aguarde uma hora**. Os registros de DNS necessário toopropagate antes que o AD do Azure pode verificar o domínio de saudação. Isso pode levar uma hora ou mais.
2. **Certifique-se de saudação registro DNS foi inserido, e se ele está correto**. Conclua esta etapa no site do Olá Olá registrador de nome de domínio de saudação. AD do Azure não pode verificar o nome de domínio de saudação se Olá entrada DNS não está presente no hello arquivo de zona DNS ou se não for uma correspondência exata com entrada DNS Olá que o AD do Azure fornecido. Se você não tiver acesso tooupdate registros DNS para o domínio de saudação no registrador de nome de domínio de saudação, compartilhar a entrada DNS Olá com pessoa hello ou equipe da sua organização que tenha esse acesso e solicite entrada DNS tooadd hello.
3. **Excluir o nome de domínio de saudação do outro diretório no AD do Azure**. Um nome de domínio pode ser verificado apenas em um único diretório. Se um nome de domínio tiver sido verificado anteriormente em outro diretório, deverá ser excluído de lá para poder ser verificado no novo diretório. ler toolearn sobre a exclusão de nomes de domínio, [gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Adicionar mais nomes de domínio personalizados
Se sua organização usa vários nomes de domínio personalizado, como 'contoso.com' e 'contosobank.com', você pode adicioná-los backup tooa máximo 900 nomes de domínio. Use Olá mesmo etapas neste artigo tooadd cada um de seus nomes de domínio.

## <a name="next-steps"></a>Próximas etapas
* [Atribuir nomes de usuário que incluem o nome de domínio personalizado](active-directory-add-domain-add-users.md)
* [Gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md)
* [Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure](active-directory-add-domain-concepts.md)
* [Mostrar a identidade visual de sua empresa quando os usuários entrarem](active-directory-add-company-branding.md)
* [Use nomes de domínio do PowerShell toomanage no AD do Azure](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

