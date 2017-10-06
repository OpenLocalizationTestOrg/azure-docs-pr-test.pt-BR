---
title: "aaaAdd seu nome de domínio personalizado e configurar federados do Active Directory entrar tooAzure | Microsoft Docs"
description: "Como tooadd da sua empresa nomes de domínio tooAzure do Active Directory tooset a entrada federada entre o Active Directory do Azure e sua solução de federação no local"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Adicionar seu nome de domínio personalizado tooAzure do Active Directory
Você pode configurar um nome de domínio personalizado, como ‘contoso.com’, para que os usuários em contoso.com possam ter uma experiência de logon único federado da rede corporativa. Se você já tem os serviços de Federação do Active Directory (AD FS) ou um servidor de Federação diferentes em execução em sua rede corporativa, você pode configurar toouse do AD do Azure em seu nome de domínio personalizado usando a ferramenta Azure AD Connect de saudação. Você também pode usar o ambiente do Azure AD Connect toodeploy um novo AD FS e configurar que para federado único logon tooAzure AD.

Se você não tem e não planeje toodeploy do AD FS ou outro servidor de federação, siga estas instruções: [adicionar um nome de domínio personalizado tooAzure do Active Directory](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Adicionar um diretório de tooyour de nome de domínio personalizado
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com uma conta de usuário que seja um administrador global do seu diretório do AD do Azure.
2. Em **do Active Directory**, abra a pasta e selecione Olá **domínios** guia.
3. Na barra de comandos hello, selecione **adicionar**e, em seguida, digite o nome de saudação do seu domínio personalizado, como 'contoso.com'. Ser. com de saudação do se tooinclude, .net ou outra extensão de nível superior.
4. Selecione Olá **planejo tooconfigure esse domínio para logon único com meu Active Directory local** caixa de seleção.
5. Selecione **Adicionar**.

Executar Olá AD do Azure Connect ferramenta tooget Olá DNS entrada que o AD do Azure usará tooverify domínio de saudação. Você verá uma entrada DNS Olá no hello **domínio do AD do Azure** etapa no Assistente de saudação. Você pode ver que essa etapa no Assistente de saudação parece [nestas instruções](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Se você não tiver a ferramenta de conexão de saudação do AD do Azure, você pode [baixá-lo aqui](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Adicionar entrada de DNS de saudação no registrador de nome de domínio Olá para domínio Olá
Olá próxima etapa toouse nome do seu domínio personalizado com o Azure AD é arquivo de zona DNS tooupdate Olá para o domínio de saudação. Isso permite que tooverify do AD do Azure que sua organização possui o nome de domínio personalizado hello.

1. Faça logon no site toohello do registrador de nome de domínio para seu nome de domínio. Se você não tiver acesso toodo isso, peça pessoa hello ou equipe em sua organização que possui esta etapa toocomplete de acesso 2 e toolet que saber quando ela estiver concluída.
2. Atualize o arquivo de zona DNS Olá para o domínio de saudação adicionando Olá DNS entrada fornecida tooyou pelo AD do Azure. Essa entrada DNS permite que tooverify do AD do Azure para sua propriedade de domínio de saudação. Olá entrada DNS não altera qualquer comportamento, como roteamento de email ou hospedagem na web.

Para obter ajuda sobre essa etapa, leia [Instruções para adicionar uma entrada DNS em registradores DNS populares](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificar Olá nome de domínio com o Azure AD
Depois de adicionar entrada DNS Olá, você está pronto tooverify nome de domínio Olá com o Azure AD.

domínio de saudação tooverify, selecione **próximo** em Olá **domínio do AD do Azure** etapa do Assistente para conectar-se de saudação do AD do Azure. AD do Azure irá procurar a entrada DNS Olá no arquivo de zona DNS Olá para o domínio de saudação. O AD do Azure somente verificar nome de domínio de saudação depois que os registros DNS Olá tenham se propagado. A propagação geralmente leva apenas alguns segundos, mas às vezes pode levar uma hora ou mais. Se a verificação não funcionar Olá primeira vez, tente novamente mais tarde.

Em seguida, continue com hello restantes etapas no Assistente de conexão do AD do Azure hello. Isso sincronizará os usuários de sua tooAzure do AD do Windows Server AD. Os usuários sincronizados no domínio Olá que você configurou para federação será capaz de tooget um único logon federado experiência de tooAzure sua rede corporativa AD.

## <a name="troubleshooting"></a>Solucionar problemas
Se você não puder verificar um nome de domínio personalizado, tente o seguinte hello. Vamos começar com hello mais comuns e de trabalho para baixo toohello menos comuns.

1. **Aguarde uma hora**. Os registros de DNS necessário toopropagate antes que o AD do Azure pode verificar o domínio de saudação. Isso pode levar uma hora ou mais.
2. **Certifique-se de saudação registro DNS foi inserido, e se ele está correto**. Conclua esta etapa no site do Olá Olá registrador de nome de domínio de saudação. AD do Azure não pode verificar o nome de domínio de saudação se Olá entrada DNS não está presente no hello arquivo de zona DNS ou se não for uma correspondência exata com entrada DNS Olá que o AD do Azure fornecido. Se você não tiver acesso tooupdate registros DNS para o domínio de saudação no registrador de nome de domínio de saudação, compartilhar a entrada DNS Olá com pessoa hello ou equipe da sua organização que tenha esse acesso e solicite entrada DNS tooadd hello.
3. **Excluir o nome de domínio de saudação do outro diretório no AD do Azure**. Um nome de domínio pode ser verificado apenas em um único diretório. Se um nome de domínio tiver sido verificado anteriormente em outro diretório, deverá ser excluído de lá para poder ser verificado no novo diretório. ler toolearn sobre a exclusão de nomes de domínio, [gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Adicionar mais nomes de domínio personalizados
Se sua organização usa vários nomes de domínio personalizado, como 'contoso.com' e 'contosobank.com', você pode adicioná-los backup tooa máximo 900 nomes de domínio. Use Olá mesmo etapas neste artigo tooadd cada um de seus nomes de domínio.

## <a name="next-steps"></a>Próximas etapas
* [Gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md)
* [Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure](active-directory-add-domain-concepts.md)
* [Mostrar a identidade visual de sua empresa quando os usuários entrarem](active-directory-add-company-branding.md)
* [Use nomes de domínio do PowerShell toomanage no AD do Azure](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

