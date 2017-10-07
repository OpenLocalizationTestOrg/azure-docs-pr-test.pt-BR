---
title: dados pessoais de aaaManage no Microsoft Azure | Microsoft Docs
description: "orientação sobre como toocorrect, atualizar, excluir e exportar dados pessoais no Active Directory do Azure e banco de dados do SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Gerenciar dados pessoais no Microsoft Azure

Este artigo fornece orientação sobre como toocorrect, atualizar, excluir e exportar dados pessoais no Active Directory do Azure e banco de dados do SQL Azure.

## <a name="scenario"></a>Cenário

Uma empresa Dublin fornece um único lugar para casamentos de destino de alto nível da Irlanda e Olá mundo para ambos os uma base de clientes locais e internacionais. Eles têm escritórios, clientes, funcionários e fornecedores espalhados locais Olá mundo toofully serviço Olá oferecem.

Entre muitos outros itens, empresa Olá controla de RSVPs que incluem alergias alimentos e preferências dieta. Convidados do casamento podem registrar para várias atividades, como a cavalo riding, navegar, barco percursos, etc. e até mesmo interagir entre si em uma página da web central durante os meses de saudação levam toohello eventos. empresa Olá coleta informações pessoais dos funcionários, fornecedores, clientes e convidados casamento. Devido a saudação internacional natureza da empresa de saudação de negócios Olá deve estar em conformidade com vários níveis de regulamentação.

## <a name="problem-statement"></a>Problema declarado

- Administradores de dados devem ser toocorrect capaz de imprecisas pessoal informações e atualização incompletas ou alteradas informações pessoais.

- Necessidade de administradores de dados deve ser capaz de toodelete informações pessoais mediante solicitação saudação de uma entidade de dados.

- Administradores de dados precisam tooexport dados e fornecem-la tooa assunto de dados em um formato comum, estruturado após a sua solicitação.

## <a name="company-goals"></a>Metas da empresa

- As informações pessoais incorretas ou incompletas de clientes, convidados do casamento, funcionários e fornecedores devem ser corrigidas ou atualizadas no Azure Active Directory e no Banco de Dados SQL do Azure.

- Informações pessoais devem ser excluídas no Active Directory do Azure e banco de dados do SQL Azure mediante solicitação saudação de uma entidade de dados.

- Dados pessoais devem ser exportados em um formato comum, estruturado mediante solicitação saudação de uma entidade de dados.

## <a name="solutions"></a>Soluções

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory: retificar/corrigir dados pessoais incorretos ou incompletos e apagar/excluir dados pessoais/perfis do usuário

O [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft.
Você pode corrigir, atualizar ou excluir perfis de usuário do cliente e do funcionário e informações de trabalho do usuário que contêm dados pessoais, como nome, nome do cargo, endereço ou número de telefone, um usuário em sua [Active Directory do Azure](https://azure.microsoft.com/services/active-directory/) (AAD) ambiente usando Olá [portal do Azure](https://portal.azure.com/).

Você deve entrar com uma conta que seja um administrador global para o diretório de saudação.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Como fazer para corrigir ou atualizar o perfil do usuário e as informações de trabalho no Azure Active Directory?

1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.

2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. Em Olá **usuários e grupos** folha, selecione **usuários**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. Em Olá **usuários e grupos, usuários** folha, selecione um usuário na lista de saudação e, em seguida, na folha de saudação do usuário selecionado hello, selecione **perfil** tooview Olá informações perfil do usuário que precisa toobe corrigido ou atualizados.

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. Corrigir ou atualizar as informações de saudação e, em seguida, na barra de comandos hello, selecione **salvar.**

6.  Na folha de saudação do usuário selecionado hello, selecione **informações de trabalho** tooview informações de trabalho de usuário que precisa toobe corrigido ou atualizado.

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. Corrigir ou atualizar informações de trabalho do usuário hello e, em seguida, na barra de comandos hello, selecione **salvar.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Como fazer para excluir um perfil do usuário do Azure Active Directory?

1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.

2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

    ![](media/manage-personal-data-azure/image001.png)

3. Em Olá **usuários e grupos** folha, selecione **usuários**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. Em Olá **usuários e grupos, usuários** folha, selecione um usuário na lista de saudação.

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. Na folha de saudação do usuário selecionado hello, selecione **visão geral**e, em seguida, na barra de comandos hello, selecione **excluir**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>Banco de Dados SQL: retificar/corrigir dados pessoais incorretos ou incompletos; apagar/excluir dados pessoais; exportar dados pessoais 

O [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) é um banco de dados de nuvem que ajuda os desenvolvedores a criar e manter aplicativos.

Os dados pessoais podem ser atualizados no [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando consultas SQL padrão e eles também podem ser excluídos. Além disso, os dados pessoais podem ser exportados do banco de dados SQL usando uma variedade de métodos, incluindo hello importação do Azure SQL Server e o Assistente de exportação e em uma variedade de formatos, incluindo um arquivo BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Como fazer para corrigir, atualizar ou apagar dados pessoais do Banco de Dados SQL?

toolearn como toocorrect ou atualização de dados pessoais no banco de dados SQL, visite Olá [atualização (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [atualizar texto](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [atualizar com expressão de tabela comum](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), ou [ Atualizar gravar texto](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentação.

toolearn como dados pessoais de toodelete no banco de dados SQL, visite Olá [excluir (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentação.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Como Exportar arquivo BACPAC tooa dados pessoais no banco de dados SQL?

Um arquivo BACPAC inclui os metadados e dados do banco de dados SQL de saudação e é um arquivo zip com uma extensão. BACPAC. Isso pode ser feito usando Olá [portal do Azure](https://portal.azure.com/), Olá SQLPackage o utilitário de linha de comando, o SQL Server Management Studio (SSMS) ou o PowerShell.

toolearn como tooexport tooa BACPAC arquivo de dados Olá visite [exportar um arquivo de BACPAC de tooa de banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) página, que inclui instruções detalhadas para cada método listados acima.

Como exportar dados pessoais do banco de dados SQL com hello importação do SQL Server e o Assistente para exportação?

Este assistente ajuda você a copiar dados de um origem tooa destino. Assistente de toohello uma introdução, incluindo como tooget, informações sobre permissões e como ajudar a tooget com ferramenta hello, visite Olá [Import e exportar dados com hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) página da web.

Para obter uma visão geral das etapas de assistente hello, visite Olá [as etapas no Assistente de exportação e saudação do SQL Server Import](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) página da web.

## <a name="next-steps"></a>Próximas etapas:

[Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Active Directory do Azure](https://azure.microsoft.com/services/active-directory/)

