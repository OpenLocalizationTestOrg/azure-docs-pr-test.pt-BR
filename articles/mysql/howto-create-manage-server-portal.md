---
title: aaaCreate e gerenciar o banco de dados do Azure para o MySQL server usando o portal do Azure | Microsoft Docs
description: "Este artigo descreve como você pode rapidamente criar um novo banco de dados do Azure para o MySQL server e gerenciar o servidor de saudação usando Olá Portal do Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure
Este artigo descreve como você pode rapidamente criar um novo banco de dados do Azure para o MySQL server e gerenciar o servidor de saudação usando Olá Portal do Azure. Gerenciamento de servidor inclui exibindo detalhes do servidor e bancos de dados, a redefinição de senha e excluindo o servidor de saudação.

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure
Faça logon no toohello [portal do Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Criar um servidor de Banco de Dados do Azure para MySQL
Siga essas etapas toocreate um banco de dados do Azure para o servidor MySQL chamado "mysqlserver4demo"

1 Clique **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

Selecione 2 **bancos de dados** de saudação nova página e selecione **banco de dados do Azure para MySQL** da página de bancos de dados de saudação.

> Um Banco de Dados do Azure para MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md). saudação de banco de dados criada em um grupo de recursos do Azure e em um banco de dados do Azure para o MySQL server.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - preencha hello banco de dados do Azure para o formulário do MySQL com hello informações a seguir:

| **Campo de Formulário** | **Descrição do Campo** |
|----------------|-----------------------|
| *Nome do servidor* | azure-mysql (o nome do servidor é globalmente exclusivo) |
| *Assinatura* | MySQLaaS (selecione na lista suspensa) |
| *Grupo de recursos* | myresource (crie um novo grupo de recursos ou use um existente) |
| *Logon de administrador do servidor* | myadmin (nome de conta do administrador de configuração) |
| *Senha* | configurar senha da conta do administrador |
| *Confirmar senha* | confirmar senha da conta do administrador |
| *Localidade* | Europa Setentrional (escolha entre o Europa Setentrional e Oeste dos EUA) |
| *Versão* | 5.6 (escolha uma versão do servidor de Banco de Dados do Azure para MySQL) |

4 Clique **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo servidor. Unidade de Computação pode ser configurada entre 50 e 100 no Tipo básico, 100 e 200 no Tipo Standard, e o armazenamento pode ser adicionado com base na quantidade incluída. Para este guia de instruções, vamos escolher 50 Unidades de Computação e 50 GB. Clique em **Okey** toosave sua seleção.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5 Clique **criar** tooprovision servidor de saudação. O provisionamento demora alguns minutos.

> Verificar Olá **toodashboard Pin** opção tooallow facilidade no rastreamento de suas implantações.
> [!NOTE]
> Embora o too1000GB na camada básica e 10000GB no padrão camada terá suporte para o armazenamento, para visualização pública, armazenamento máximo hello está temporariamente too1000GB ainda limitado. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Atualizar um servidor de Banco de Dados do Azure para MySQL
Depois que o novo servidor é configurado, o usuário tem 2 tooedit de opções um servidor existente: redefinir a senha de administrador ou de escala para cima/para baixo do servidor de saudação alterando Olá as unidades de computação.

### <a name="change-hello-administrator-user-password"></a>Alterar senha de usuário de administrador Olá
1 - no servidor de saudação **visão geral** folha, clique em **Redefinir senha** toopopulate uma janela de entrada e a confirmação de senha.

2 - Insira a nova senha e Confirmar senha Olá na janela hello como abaixo: ![redefinição de senha](./media/howto-create-manage-server-portal/reset-password.png)

3 Clique **Okey** nova senha do toosave hello.

### <a name="scale-updown-by-changing-compute-units"></a>Escalar verticalmente alterando as Unidades de Computação

1 - na folha do servidor de saudação, em **configurações**, clique em **preço** folha de camada de preços tooopen Olá para hello banco de dados para o servidor MySQL.

A etapa 2-siga 4 **criar um banco de dados do Azure para o MySQL server** toochange unidades de computação em Olá mesma camada de preços.

## <a name="delete-an-azure-database-for-mysql-server"></a>Excluir um servidor de Banco de Dados do Azure para MySQL

1 - no servidor de saudação **visão geral** folha, clique em **excluir** folha de confirmação de exclusão do comando botão tooopen hello.

Nome do servidor correto Olá 2-tipo na caixa de entrada da folha de saudação confirmação duplo.

3 Clique **excluir** novamente tooconfirm ação de exclusão e aguarde o pop-up "Excluindo sucesso" na barra de notificação de saudação.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Lista hello banco de dados do Azure para bancos de dados MySQL
No servidor de saudação **visão geral** folha, role para baixo até ver o banco de dados de saudação lado a lado na parte inferior da saudação. Todos os bancos de dados hello serão listados na tabela de saudação. Clique em **excluir** folha de confirmação de exclusão do comando botão tooopen hello.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Mostrar detalhes de um servidor de Banco de Dados do Azure para MySQL
Clique em **propriedades** em **configurações** no servidor de saudação folha será aberta, Olá **propriedades** folha. Em seguida, você pode exibir todas as informações detalhadas sobre o servidor de saudação.

## <a name="next-steps"></a>Próximas etapas

[Início rápido: criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
