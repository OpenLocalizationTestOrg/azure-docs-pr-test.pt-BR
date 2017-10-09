---
title: "API de relatório aaaPrerequisites tooaccess Olá AD do Azure | Microsoft Docs"
description: "Saiba sobre a API de relatório do hello pré-requisitos tooaccess Olá AD do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de relatório pré-requisitos tooaccess Olá AD do Azure

Olá [reporting APIs do AD do Azure](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornece acesso programático toohello dados por meio de um conjunto de APIs com base em REST. Você pode chamar essas APIs de várias ferramentas e linguagens de programação.

Olá reporting API usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) APIs da web do toohello tooauthorize acesso. 

tooget acessar dados de relatório toohello por meio da API de Olá, é necessário toohave uma saudação funções atribuídas a seguir:

- Leitor de segurança
- Administrador de Segurança
- Administrador global


tooprepare seu toohello acesso API de relatório, você deve:

1. Registrar um aplicativo 
2. Conceder permissões 
3. Reunir definições de configuração 

Em caso de dúvidas, problemas ou comentários, [registre um tíquete de suporte](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Registrar um aplicativo do Azure Active Directory

É necessário tooregister um aplicativo, mesmo se você estiver acessando Olá API usando um script de relatório. Isso lhe dá uma **ID do aplicativo**, que é necessário para uma chamada de autorização e possibilita que os tokens de tooreceive seu código.

tooconfigure seu diretório tooaccess Olá AD do Azure reporting API, você deve entrar no toohello portal do Azure com uma conta de administrador do Azure que também é um membro da saudação **Administrador Global** função de diretório em seu locatário do AD do Azure .

> [!IMPORTANT]
> Aplicativos em execução sob as credenciais com privilégios de "admin" como isso podem ser muito poderosos, portanto as credenciais de ID/segredo do aplicativo de saudação de tookeep-se de que seja seguro.
> 


**tooregister um aplicativo do Active Directory do Azure:**

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Em Olá **Active Directory do Azure** folha, clique em **registros do aplicativo**.

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Em Olá **registros do aplicativo** folha, na barra de ferramentas Olá superior hello, clique em **novo registro de aplicativo**.

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Em Olá **criar** folha, executar Olá etapas a seguir:

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. Em Olá **nome** caixa de texto, tipo `Reporting API application`.

    b. Como **Tipo de aplicativo**, selecione **Aplicativo/API Web**.

    c. Em Olá **URL de logon** caixa de texto, tipo `https://localhost`.

    d. Clique em **Criar**. 


## <a name="grant-permissions"></a>Conceder permissões 

objetivo de saudação desta etapa é toogrant seu aplicativo **ler dados do diretório** permissões toohello **Windows Azure Active Directory** API.

![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant a saudação de toouse de permissão do aplicativo API:**

1. Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.

2. Em Olá **aplicativo de API Reporting** folha, na barra de ferramentas Olá superior hello, clique em **configurações**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Em Olá **configurações** folha, clique em **as permissões necessárias**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Em Olá **as permissões necessárias** folha em Olá **API** lista, clique em **Windows Azure Active Directory**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Em Olá **habilitar acesso** folha, selecione **ler dados do diretório**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Na barra de ferramentas de saudação na parte superior do hello, clique em **salvar**.

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Reunir definições de configuração 
Esta seção mostra como Olá tooget seguir as configurações de seu diretório:

* Nome de domínio
* ID do cliente
* Segredo do cliente

Você precisa esses valores quando configurar chamadas toohello reporting API. 

### <a name="get-your-domain-name"></a>Obter seu nome de domínio

**tooget seu nome de domínio:**

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Em Olá **Active Directory do Azure** folha, clique em **nomes de domínio**.

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Copie o nome de domínio da lista de saudação de domínios.


### <a name="get-your-applications-client-id"></a>Obtenha a ID do cliente do aplicativo

**tooget ID do cliente do aplicativo:**

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.

3. Em Olá **aplicativo de API Reporting** blade, a saudação **ID do aplicativo**, clique em **clique toocopy**.

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Obter seu segredo do cliente do aplicativo
tooget cliente do aplicativo segredo, você precisa toocreate uma nova chave e salve seu valor ao salvar a nova chave de saudação porque ele não é possível tooretrieve este valor posteriormente mais.

**tooget segredo do cliente do aplicativo:**

1. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.


3. Em Olá **aplicativo de API Reporting** folha, na barra de ferramentas Olá superior hello, clique em **configurações**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Em Olá **configurações** folha em Olá **APIR acesso** seção, clique em **chaves**. 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Em Olá **chaves** folha, executar Olá etapas a seguir:

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. Em Olá **descrição** caixa de texto, tipo `Reporting API`.

    b. Como **Expira**, selecione **Em 2 anos**.

    c. Clique em **Salvar**.

    d. Copie o valor da chave hello.


## <a name="next-steps"></a>Próximas etapas
* Seria você como tooaccess Olá dados de saudação do AD do Azure API de relatório de modo programático? Check-out [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).
* Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).  

