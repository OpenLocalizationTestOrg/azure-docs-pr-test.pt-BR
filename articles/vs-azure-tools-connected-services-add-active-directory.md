---
title: "aaaAdding um Azure Active Directory usando serviços conectados no Visual Studio | Microsoft Docs"
description: "Adicionar um Active Directory do Azure usando a caixa de diálogo do Visual Studio adicionar conectado serviços Olá"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Adicionando um Active Directory do Azure usando Serviços Conectados no Visual Studio
Ao usar o Azure AD (Azure Active Directory), você pode oferecer suporte ao SSO (Logon Único) para aplicativos Web MVC ASP.NET ou Autenticação do Active Directory nos serviços da API Web. Com a autenticação do Azure Active Directory, os usuários podem usar suas contas de aplicativos web do Active Directory do Azure tooconnect tooyour. as vantagens de saudação de autenticação do Active Directory do Azure com a API da Web incluem segurança aprimorada de dados ao expor uma API de um aplicativo web. Com o AD do Azure, você não tem toomanage um sistema de autenticação separado com sua própria conta e gerenciamento de usuários.

## <a name="prerequisites"></a>Pré-requisitos
- Conta do Azure – se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Conecte-se tooAzure do Active Directory usando os serviços conectados Olá caixa de diálogo
1. No Visual Studio, crie ou abra um projeto ASP.NET MVC ou um projeto de API Web ASP.NET.

1. De Olá Gerenciador de soluções, clique com botão direito Olá **serviços conectados** nó e, no menu de contexto hello, selecione **adicionar serviços conectados**.

1. Em Olá **serviços conectados** página, selecione **autenticação com o Active Directory do Azure**.
   
    ![Página Serviços Conectados](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. Em Olá **Introdução** página de saudação **configurar o Azure AD Authentication** assistente, selecione **próximo**.
   
    ![Página Introdução](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. Em Olá **logon único do** página de saudação **configurar o Azure AD Authentication** assistente, selecione um domínio de saudação **domínio** lista suspensa. lista de Olá de domínios contém todos os domínios acessíveis pelas contas Olá listadas na caixa de diálogo de configurações de conta de saudação. Como alternativa, você pode inserir um nome de domínio se você não encontrar um você está procurando, como Olá `mydomain.onmicrosoft.com`. Você pode escolher Olá opção toocreate um aplicativo do Active Directory do Azure ou usar configurações de saudação de um aplicativo existente do Active Directory do Azure. Quando terminar, escolha **Avançar**.
   
    ![Página Logon único](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Em Olá **acesso ao diretório** página de saudação **configurar o Azure AD Authentication** assistente, certifique-se de que Olá **ler dados do diretório** opção estiver marcada. 
   
    ![Página Acesso ao diretório](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Selecione **concluir** tooadd Olá tooenable de referências a código e configuração necessárias seu projeto para a autenticação do AD do Azure. Você pode ver o domínio do Active Directory Olá no hello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. O Visual Studio exibirá um [o que aconteceu](#how-your-project-is-modified) artigo tooshow você como seu projeto foi modificado. Se você quiser toocheck tudo funcionou, abra um dos arquivos de configuração de saudação modificado e verifique que configurações Olá mencionadas no artigo Olá existem. 

## <a name="how-your-project-is-modified"></a>Como o projeto é modificado
Quando você executa o Assistente de saudação, o Visual Studio adiciona o Azure Active Directory e o projeto de tooyour de referências associadas. Arquivos de configuração e arquivos de código em seu projeto também são modificadas tooadd suporte do AD do Azure. modificações específicas de saudação que o Visual Studio faz dependem do tipo de projeto de saudação. Para obter informações detalhadas sobre como os projetos MVC ASP.NET são modificados, consulte [O que aconteceu — projetos MVC](http://go.microsoft.com/fwlink/p/?LinkID=513809). Para projetos de API Web, confira [O que aconteceu — projetos API Web](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Próximas etapas
* [Fórum do MSDN do Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Documentação do Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Postagem do blog: Introdução tooAzure do Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

