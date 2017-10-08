---
title: etapa aaaGeneric etapa por conector do SQL | Microsoft Docs
description: "Este artigo é percorrer você através de um sistema de RH simple usando o passo a passo Olá conector do SQL genérico."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Passo a passo do Conector do SQL Genérico
Este tópico é um guia passo a passo. Ele cria um banco de dados de RH de exemplo simples e o usará para a importação de alguns usuários e sua associação a um grupo.

## <a name="prepare-hello-sample-database"></a>Preparar o banco de dados de exemplo hello
Em um servidor executando o SQL Server, execute o script SQL de saudação encontrado no [Apêndice A](#appendix-a). Esse script cria um banco de dados de exemplo com o nome hello GSQLDEMO. modelo de objeto de saudação do hello criados nesta imagem parece de banco de dados:  
![Modelo de objeto](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Também crie um usuário de banco de dados do toouse tooconnect toohello. Neste passo a passo, usuário Olá é chamado FABRIKAM\SQLUser e localizado no domínio hello.

## <a name="create-hello-odbc-connection-file"></a>Criar arquivo de conexão ODBC Olá
Olá conector do SQL genérico é usando o servidor remoto do ODBC tooconnect toohello. Primeiro, precisamos toocreate um arquivo com hello informações de conexão do ODBC.

1. Inicie o utilitário de gerenciamento de ODBC Olá em seu servidor:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Guia de saudação selecione **DSN de arquivo**. Clique em **Adicionar...**.  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Olá out-of-box drivers funciona bem, para selecioná-lo e clique em **próximo >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Dê um nome de arquivo hello como **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Clique em **Concluir**.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Conexão de saudação do tooconfigure de tempo. Dê a fonte de dados Olá uma descrição válida e fornecer o nome de saudação do servidor de saudação executando o SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Selecione como tooauthenticate com SQL. Nesse caso, usamos a Autenticação do Windows.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Fornecer nome de saudação do banco de dados de exemplo hello, **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Mantenha todas as opções como padrão nesta tela. Clique em **Concluir**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify tudo está funcionando conforme o esperado, clique em **fonte de dados de teste**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Certifique-se de saudação teste for bem-sucedido.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. arquivo de configuração de ODBC Olá agora deve estar visível no DSN de arquivo.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Agora temos arquivo hello precisamos e pode começar a criar hello conector.

## <a name="create-hello-generic-sql-connector"></a>Criar hello conector do SQL genérico
1. No hello UI Synchronization Service Manager, selecione **conectores** e **criar**. Selecione **SQL Genérico (Microsoft)** e dê a ele um nome descritivo.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Localizar o arquivo DSN Olá que você criou na seção anterior hello e carregá-lo toohello server. Fornece o banco de dados do hello credenciais tooconnect toohello.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. Neste passo a passo, estamos facilitando nosso trabalho dizendo que há dois tipos de objeto, **User** e **Group**.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. atributos de saudação toofind, queremos Olá conector toodetect desses atributos, observando a própria tabela hello. Como **usuários** é uma palavra reservada no SQL, é preciso tooprovide-lo no quadrado colchetes [].  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Atributo de âncora tempo toodefine hello e atributo DN de saudação. Para **usuários**, usamos a combinação de saudação do nome de usuário do hello dois atributos e EmployeeID. Para **Group**, usamos GroupName (não realista na vida real, mas funcionará nesse passo a passo).
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Nem todos os tipos de atributo podem ser detectados em um banco de dados SQL. tipo de atributo de referência de saudação em particular não pode. Para o tipo de objeto de grupo hello, precisamos toochange Olá OwnerID e MemberID tooreference.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. atributos de saudação selecionamos como atributos de referência na etapa anterior Olá exigem esses valores são uma referência ao tipo de objeto de Olá. Em nosso caso, Olá tipo de objeto do usuário.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Na página de parâmetros globais hello, selecione **marca d'água** como estratégia de delta hello. Digite também no formato de data/hora Olá **AAAA-MM-dd hh**.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Em Olá **configurar partições e hierarquias** , selecione os dois tipos de objeto.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Em Olá **selecionar tipos de objeto** e **selecionar atributos**, selecione os tipos de objeto e todos os atributos. Em Olá **configurar âncoras** , clique em **concluir**.

## <a name="create-run-profiles"></a>Criar perfis de execução
1. No hello UI Synchronization Service Manager, selecione **conectores**, e **configurar perfis de execução**. Clique em **Novo Perfil**. Começamos com **Importação Completa**.  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Selecione o tipo de saudação **importação completa (somente estágio)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Selecione a partição Olá **objeto = usuário**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Selecione **Tabela** e digite **[USERS]**. Role para baixo da seção de tipo de objeto múltiplos toohello e inserir dados de saudação como Olá figura abaixo. Selecione **concluir** toosave etapa de saudação.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Selecione **Nova Etapa**. Desta vez, selecione **OBJECT=Group**. Na última página de hello, use a configuração de hello como Olá figura abaixo. Clique em **Concluir**.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Opcional: se quiser, você poderá configurar perfis de execução adicionais. Para este passo a passo, Olá importação completa é usada.
7. Clique em **Okey** toofinish alterando perfis de execução.

## <a name="add-some-test-data-and-test-hello-import"></a>Adicione alguns importação de saudação teste dados e de teste
Preencha alguns dados de teste no banco de dados de exemplo. Quando estiver pronto, selecione **Executar** e **Importação completa**.

Aqui está um usuário com dois números de telefone e um grupo com alguns membros.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Apêndice A
**Banco de dados do SQL script toocreate Olá exemplo**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
