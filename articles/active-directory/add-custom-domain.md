---
title: "aaaAdd tooAzure um domínio personalizado AD | Microsoft Docs"
description: "Explica como tooadd um domínio personalizado no Azure Active Directory."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Início rápido: Adicionar um nome de domínio personalizado tooAzure do Active Directory

Cada diretório do AD do Azure vem com um nome de domínio inicial na forma de saudação de *domainname*. c o m. nome de domínio inicial de saudação não pode ser alterado ou excluído, mas você pode adicionar seu domínio corporativo nome tooAzure AD também. Por exemplo, sua organização provavelmente tem outro domínio nomes usados toodo negócios e os usuários que entrar usando seu nome de domínio corporativo. Adicionar nomes de domínio personalizado tooAzure AD permite nomes de usuário tooassign no diretório de saudação que são usuários tooyour familiarizado, como 'alice@contoso.com.' em vez de "alice@*<domain name>*.onmicrosoft.com". processo de saudação é simple:

1. Adicionar o diretório de tooyour de nome de domínio personalizado Olá
2. Adicionar uma entrada DNS para o nome de domínio Olá no registrador de nome de domínio Olá
3. Verifique se o nome de domínio personalizado Olá no AD do Azure

## <a name="add-your-custom-domain"></a>Adicionar o domínio personalizado
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **Active Directory do Azure** Olá caixa de texto e, em seguida, selecione **Enter**.
   
   ![Abrir o gerenciamento de usuários](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Em Olá ***nome do diretório*** folha, selecione **nomes de domínio**.
4. Em Olá  ***nome do diretório* -nomes de domínio** folha, selecione Olá **adicionar** comando.
   
   ![Selecionando o comando Add a saudação](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Em Olá **nome de domínio** folha, insira o nome de saudação do seu domínio personalizado na caixa de saudação, como "contoso.com" e, em seguida, selecione **Adicionar domínio**. Ser. com de saudação do se tooinclude, .net ou outra extensão de nível superior.
6. Em Olá ***nome de domínio*** folha (com o nome de domínio personalizado no título de saudação), obter Olá informações de entrada DNS toouse tooverify se sua organização possui o nome de domínio personalizado hello.
   
   ![obter informações de entrada DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Se você planejar toofederate local Windows Server AD com o AD do Azure, você precisará Olá tooselect **planejo tooconfigure esse domínio para logon único com meu Active Directory local** caixa de seleção quando você executa a ferramenta de conectar-se de saudação do AD do Azure toosynchronize seus diretórios. Você também precisa tooregister Olá o mesmo nome de domínio que você selecionar para federar com seu diretório local no hello **domínio do AD do Azure** etapa no Assistente de saudação. Você pode ver que essa etapa no Assistente de saudação parece [nestas instruções](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Se você não tiver a ferramenta de conexão de saudação do AD do Azure, você pode [baixá-lo aqui](http://go.microsoft.com/fwlink/?LinkId=615771).

Agora que você adicionou o nome de domínio hello, AD do Azure deve verificar se sua organização possui o nome de domínio hello. Antes de executar essa verificação do AD do Azure, você deve adicionar uma entrada DNS no arquivo de zona DNS Olá Olá nome de domínio. Essa tarefa é executada no site Olá para o registrador de nome de domínio para o nome de domínio hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Adicionar entrada de DNS de saudação no registrador de nome de domínio Olá para domínio Olá
Olá próxima etapa toouse nome do seu domínio personalizado com o Azure AD é arquivo de zona DNS tooupdate Olá para o domínio de saudação. O AD do Azure, em seguida, pode verificar se sua organização possui o nome de domínio personalizado de saudação.

1. Entrar toohello registrador de nome de domínio para o domínio de saudação. Se você não tiver Olá tooupdate de acesso a entrada de DNS, pergunte pessoa hello ou equipe que possui esta etapa toocomplete de acesso 2 e toolet que saber quando ela estiver concluída.
2. Atualize o arquivo de zona DNS Olá para o domínio de saudação adicionando Olá DNS entrada fornecida tooyou pelo AD do Azure. Essa entrada DNS permite que tooverify do AD do Azure para sua propriedade de domínio de saudação. Olá entrada DNS não altera qualquer comportamento, como roteamento de email ou hospedagem na web.

Para obter ajuda com essa entrada DNS adicionando hello, leia [instruções para adicionar uma entrada de DNS em registradores DNS populares](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificar Olá nome de domínio com o Azure AD
Depois de adicionar entrada DNS Olá, você está pronto tooverify nome de domínio Olá com o Azure AD.

Um nome de domínio pode ser verificado apenas depois que os registros DNS Olá tenham se propagado. Essa propagação geralmente leva apenas alguns segundos, mas às vezes pode levar uma hora ou mais. Se a verificação não funcionar Olá primeira vez, tente novamente mais tarde.

1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **procurar**, insira o gerenciamento de usuário na caixa de texto de saudação e, em seguida, selecione **Enter**.
   
   ![Abrir o gerenciamento de usuários](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Em Olá **gerenciamento de usuário - nomes de domínio** folha, nome de domínio não verificado Olá selecione que você deseja tooverify.
4. Em Olá ***nome de domínio*** folha (ou seja, Olá folha que abre com seu novo nome de domínio no título de saudação), selecione **verificar** toocomplete verificação de saudação.

> [!TIP]
> Você pode adicionar os nomes de domínio personalizado too900, mas apenas um pode ser [definido como nome de domínio primário de saudação do seu diretório do AD do Azure](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) usado por padrão quando você criar novas contas.

Agora você pode criar contas de usuário baseadas em nuvem ou atualizar informações de conta de usuário locais sincronizadas anteriormente, usando seu nome de domínio personalizado. Você também pode modificar usuário sincronizado anteriormente conta domínio sufixo informações usando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Solucionar problemas
Se você não puder verificar um nome de domínio personalizado, tente Olá etapas de solução de problemas a seguir:

1. **Aguarde uma hora**. Os registros de DNS necessário toopropagate antes que o AD do Azure pode verificar o domínio de saudação. Isso pode levar uma hora ou mais.
2. **Certifique-se de saudação registro DNS foi inserido, e se ele está correto**. Conclua esta etapa no site do Olá Olá registrador de nome de domínio de saudação. AD do Azure não pode verificar o nome de domínio de saudação se Olá entrada DNS não está presente no hello arquivo de zona DNS ou se não for uma correspondência exata com entrada DNS Olá que o AD do Azure fornecido. Se você não tiver acesso tooupdate registros DNS para o domínio de saudação no registrador de nome de domínio de saudação, compartilhar a entrada DNS Olá com pessoa hello ou equipe da sua organização que tenha esse acesso e solicite entrada DNS tooadd hello.
3. **Excluir o nome de domínio de saudação do outro diretório no AD do Azure**. Um nome de domínio pode ser verificado apenas em um único diretório. Se um nome de domínio tiver sido verificado anteriormente em outro diretório, deverá ser excluído de lá para poder ser verificado no novo diretório. ler toolearn sobre a exclusão de nomes de domínio, [gerenciar nomes de domínio personalizados](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Adicionar mais nomes de domínio personalizados
Se sua organização usa mais de um nome de domínio personalizado, como 'contoso.com' e 'contosobank.com', você pode adicionar o too900 mais, repetindo as etapas de saudação neste artigo para cada um.

### <a name="learn-more"></a>Saiba mais
[Visão geral conceitual de nomes de domínio personalizados no Azure AD](active-directory-add-domain-concepts.md)

[Gerenciar nomes de domínio personalizados](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Próximas etapas
Este guia de início rápido, você aprendeu como tooadd tooAzure um domínio personalizado AD. 

Você pode usar o hello para seguir link tooadd um novo domínio personalizado no AD do Azure de saudação portal do Azure.

> [!div class="nextstepaction"]
> [Adicionar um domínio personalizado](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 