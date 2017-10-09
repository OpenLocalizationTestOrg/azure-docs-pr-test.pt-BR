---
title: "nomes de domínio personalizados aaaManaging no Active Directory do Azure | Microsoft Docs"
description: "Conceitos de gerenciamento e instruções para gerenciar um domínio personalizado no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Gerenciando nomes de domínio personalizados no Azure Active Directory
Um nome de domínio pode ser um identificador importante para muitos recursos de diretório, como parte de:

* Um nome de usuário ou endereço de email de um usuário
* Olá endereço de um grupo
* URI da ID do aplicativo Hello para um aplicativo

Um recurso no Azure Active Directory (AD do Azure) pode incluir um nome de domínio que já é verificado toobe pertencentes a directory Olá que contém o recurso de saudação. Somente um administrador global pode executar tarefas de gerenciamento de domínio no Azure AD.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como toomanage seu nomes de domínio no Centro de administração de saudação do AD do Azure, consulte [gerenciar nomes de domínio personalizado no Active Directory do Azure](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Definir nome de domínio primário de saudação do seu diretório do AD do Azure
Quando o diretório é criado, o nome de domínio inicial hello, como 'contoso.onmicrosoft.com', também é o nome de domínio primário de Olá para seu diretório. domínio primário Olá é o nome de domínio de padrão de saudação para um novo usuário quando você cria um novo usuário no hello [portal clássico do Azure](https://manage.windowsazure.com/), ou outros portais, como o portal de administração do Office 365 de saudação. Isso simplifica o processo de saudação para um administrador toocreate novos usuários no portal de saudação.

nome de domínio primário toochange Olá para seu diretório:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com uma conta de usuário que seja um administrador global do seu diretório do AD do Azure.
2. Selecione **do Active Directory** na barra de navegação à esquerda de saudação.
3. Abra seu diretório.
4. Selecione Olá **domínios** guia.
5. Selecione Olá **alteração principal** botão na barra de comandos de saudação.
6. Selecione o domínio de saudação que você deseje Olá toobe novo domínio primário para seu diretório.

Você pode alterar o nome de domínio primário Olá para o diretório toobe qualquer domínio personalizado verificado que não está federado. Alterar domínio primário de saudação do seu diretório não alterará os nomes de usuário Olá para todos os usuários existentes.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Adicionar nomes de domínio personalizado tooyour AD do Azure
Você pode adicionar o diretório do AD do Azure do too900 domínio personalizado nomes tooeach. Olá processo muito[adicionar um nome de domínio personalizados adicionais](active-directory-add-domain.md) Olá mesmo para o primeiro nome de domínio personalizado hello.

## <a name="add-subdomains-of-a-custom-domain"></a>Adicionar subdomínios de um domínio personalizado
Se você quiser tooadd um nome de domínio de terceiro nível, como 'europe.contoso.com' tooyour directory, você deve primeiro adicionar e verificar o domínio de segundo nível hello, como contoso.com. subdomínio Hello serão automaticamente verificado pelo AD do Azure. foi verificado toosee que Olá subdomínio que você acabou de adicionar, atualizar Olá página no navegador de saudação que lista os domínios de saudação em seu diretório.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Quais toodo se você alterar o registrador de DNS Olá para seu nome de domínio personalizado
Se você alterar o registrador de DNS Olá para seu nome de domínio personalizado, você pode continuar toouse seu nome de domínio personalizado com o Azure AD em si sem interrupção e sem outras tarefas de configuração. Se você usar seu nome de domínio personalizado com o Office 365, Intune, ou outros serviços que dependem de nomes de domínio personalizado no AD do Azure, consulte a documentação de toohello para esses serviços.

## <a name="delete-a-custom-domain-name"></a>Excluir um nome de domínio personalizado
Você pode excluir um nome de domínio do AD do Azure se sua organização não usa esse nome de domínio, ou se você precisar toouse nome de domínio com outro AD do Azure.

toodelete um nome de domínio personalizado, primeiro você deve assegurar que não há recursos no seu diretório se baseia no nome de domínio de saudação. Você não poderá excluir um nome de domínio do diretório se:

* Qualquer usuário tem um nome de usuário, o endereço de email ou o endereço de proxy que incluem o nome de domínio de saudação.
* Qualquer grupo tem um endereço de email ou o endereço de proxy que inclui o nome de domínio de saudação.
* Qualquer aplicativo no AD do Azure tem um URI de identificação que inclui o nome de domínio de saudação do aplicativo.

Você deve alterar ou excluir qualquer esse recurso em seu diretório do AD do Azure antes de excluir o nome de domínio personalizado hello.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Usar nomes de domínio toomanage PowerShell ou API do Graph
A maioria das tarefas de gerenciamento para nomes de domínio no Azure Active Directory também pode ser concluída usando o Microsoft PowerShell ou de forma programática, usando a API do Graph do Azure AD.

* [Usando nomes de domínio do PowerShell toomanage no AD do Azure](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Usando nomes de domínio do API do Graph toomanage no AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre nomes de domínio no Azure AD](active-directory-add-domain-concepts.md)
* [Gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md)

