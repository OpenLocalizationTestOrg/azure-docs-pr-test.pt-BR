---
title: "saudação de toouse aaaHow pacote conteúdo do Azure Active Directory Power BI | Microsoft Docs"
description: "Saiba como toouse Olá pacote conteúdo do Azure Active Directory Power BI"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Como toouse Olá pacote conteúdo do Azure Active Directory Power BI

Entender como os usuários adotam e usam os recursos do Azure Active Directory é essencial para você como administrador de TI. Ele permite que você tooplan seu uso tooincrease da comunicação e infraestrutura de TI e tooget hello mais dos recursos do AAD. Pacote de conteúdo do Power BI para Active Directory do Azure fornece Olá capacidade toofurther analisar sua toounderstand de dados como você pode usar esse dados toogather mais rica aprofundar-se que está acontecendo com seu Active Directory do Azure para Olá diversos recursos você muito dependem.  Com a integração de saudação das APIs do Azure Active Directory para o Power BI, você pode facilmente baixar pacotes de conteúdo predefinidos hello e obter ideias atividades de saudação tooall no Active Directory do Azure usando o Power BI oferece de experiência de visualização avançada. Você pode criar seu próprio painel e compartilhá-lo facilmente com qualquer pessoa em sua organização. 

Este tópico fornece instruções passo a passo sobre como tooinstall e use Olá conteúdo compactar em seu ambiente.

## <a name="installation"></a>Instalação  

**Olá tooinstall pacote de conteúdo do Power BI:**

1. Faça logon no [Power BI](https://app.powerbi.com/groups/me/getdata/services) com sua conta do Power BI (Isso é hello mesma conta do O365 ou a conta do AD do Azure).

2. Na parte inferior do Olá Olá esquerdo do painel de navegação, selecione **obter dados**.

    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. Em Olá **serviços** , clique em **obter**.
   
    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Pesquise o **Azure Active Directory**.

    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Quando solicitado, digite sua ID de locatário do Azure AD e clique em **Avançar**.

    > [!TIP] 
    > Uma saudação de maneira rápida tooget Id de locatário para seu locatário do Office 365 / Azure AD é toologin toohello Portal do AD do Azure, fazer drill down toohello diretório e copiem ID Olá Olá URL a seguir: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart

    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Clique em **Entrar**. 
 
    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Insira seu nome de usuário e senha e clique em **Entrar**.
 
    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  No diálogo de consentimento de aplicativo hello, clique em **aceitar**.
 
9.  Quando o painel de logs de atividade do Azure Active Directory for criado, clique nele.
 
    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>O que posso fazer com esse pacote de conteúdo?

Antes de entramos que você pode fazer com este pacote de conteúdo, a visualização rápida do aqui de saudação vários relatórios no conteúdo de saudação pacote. Relatório de dados volta toohello **últimos 30 dias**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Relatórios incluídos nesta versão do pacote de conteúdo de logs do Azure Active Directory

**Relatório de uso do aplicativo e a tendência**: obter ideias sobre aplicativos Olá usados em sua organização e quais estão sendo usadas mais hello e quando. Você pode usar este relatório toogather um panorama de como um aplicativo que você distribuiu recentemente em sua organização está sendo usado ou descobrir quais aplicativos são populares. Ao fazer isso, você pode melhorar o uso se você vir se Olá aplicativo não está sendo usado.

**Entradas por local e os usuários**: obter informações sobre todos os Olá entradas executadas usando a identidade do Azure e fornece ideias para identidade de saudação de usuários de saudação. Com isso, você poderá se aprofundar em entradas individuais e responder a perguntas como:

- Onde é feita a entrada de determinado usuário?
- Qual o usuário tem Olá a maioria das entradas e onde eles entrar de? 
- Foi Olá entrada bem-sucedida?  
 
Você pode analisar detalhes clicando em uma data ou um local específico.

**Usuários exclusivos por aplicativo**: veja todos os usuários exclusivos que usam determinado aplicativo. Isso inclui apenas os usuários que entraram "*com êxito*" em um aplicativo.

**Entradas de dispositivo**: Obtenha uma exibição do tipo de saudação do sistema operacional e navegadores estão sendo usados por usuários em sua organização com informações detalhadas sobre os usuários de saudação incluindo:

- Nome de usuário
- Endereço IP
- Local 
- Status de entrada 

Com este relatório, você pode entender Olá vários perfis de dispositivo usado em sua organização e determinam as políticas de dispositivo com base no que é usado

**Funil SSPR**: entenda como redefinições de senha estão sendo feitas em sua organização. Obter um pico em senha quantas redefinições foram tentadas por meio da ferramenta SSPR hello e quantos deles foram bem-sucedidas. Falha de redefinições de senha hello usando funil SSPR Olá se aprofundar e compreender por que determinadas falhas ocorreram. Esse relatório fornece uma compreensão mais profunda de como ferramenta SSPR Olá é usada dentro de sua organização para que você possa tomar decisões de saudação à direita.

## <a name="customizing-azure-ad-activity-content-pack"></a>Personalizando o pacote de conteúdo da Atividade do Azure AD

**Alterar a visualização**: você pode alterar uma visualização de relatório clicando **Editar relatório** e selecione a visualização de saudação desejado.
 
![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Incluir campos adicionais**: você pode adicionar um relatório do campo toohello ou removê-lo selecionando Olá toowhich visual que você deseja tooadd/remover Olá campo. O exemplo hello abaixo, estou adicionando "status de entrada" campo toohello visualização de tabela. 
 
![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Painel de controle do PIN visualizações tooyour**: você pode personalizar seu painel e incluir seu próprio relatório toohello de visualizações e fixá-lo toohello painel. O exemplo hello abaixo, adicionei um novo filtro chamado "Status de entrada" e incluídos-Olá relatório. Também alterado visualização de saudação do gráfico de linhas do gráfico de barras tooa e pode fixar este novo painel toohello visual.

![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Compartilhar seu dashboard**: depois de criar conteúdo Olá desejado, você pode compartilhar painel Olá com usuários de saudação em sua organização. Lembre-se de que depois que você compartilhar o relatório de hello, eles podem ver campos Olá selecionados no relatório de saudação.
 
![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Agendar uma atualização diária de seu relatório do Power BI

tooschedule uma atualização diária de seu relatório do Power BI, vá muito**conjuntos de dados > Configurações > agendar atualização** e defina-o conforme mostrado abaixo.
 
![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Atualização da versão toonewer do pacote de conteúdo

Se você quiser tooupdate seu pacote de conteúdo tooget uma versão mais recente:

- Baixe o novo pacote de conteúdo hello e configurá-lo de acordo com as instruções listadas neste artigo.

- Depois de você ter configurá-lo, vá muito**fonte de dados > Configurações > credenciais da fonte de dados** e digite novamente suas credenciais, conforme mostrado abaixo

    ![Pacote de Conteúdo do Power BI do Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Assim que a nova versão Olá do pacote de conteúdo Olá estiver funcionando, você pode remover a versão antiga do hello se necessário, excluindo relatórios subjacentes hello e conjuntos de dados associados a esse pacote de conteúdo.

## <a name="still-having-issues"></a>Ainda está com problemas? 

Confira nosso [guia de solução de problemas](active-directory-reporting-troubleshoot-content-pack.md). Para obter ajuda geral com o Power BI, confira esses [artigos de ajuda](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral de emissão de relatórios, consulte Olá [reporting do Active Directory do Azure](active-directory-reporting-azure-portal.md).
