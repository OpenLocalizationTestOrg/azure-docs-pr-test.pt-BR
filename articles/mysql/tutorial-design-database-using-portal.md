---
title: aaaDesign do Azure primeiro banco de dados para o banco de dados MySQL - Portal do Azure | Microsoft Docs
description: Este tutorial explica como toocreate e gerenciar o banco de dados do Azure para o MySQL server e banco de dados usando o Portal do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL
Banco de dados do Azure para MySQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados MySQL altamente disponíveis na nuvem hello. Usando Olá portal do Azure, você pode facilmente gerenciar seu servidor e criar um banco de dados.

Neste tutorial, você usar Olá toolearn portal do Azure como para:

> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para MySQL
> * Configurar o firewall do servidor de saudação
> * Usar a ferramenta de linha de comando de mysql toocreate um banco de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

## <a name="sign-in-toohello-azure-portal"></a>Entrar toohello portal do Azure
Abra seu navegador favorito e visite Olá [portal do Microsoft Azure](https://portal.azure.com/). Insira sua credenciais toosign no portal de toohello. exibição padrão de saudação é seu painel de serviço.

## <a name="create-an-azure-database-for-mysql-server"></a>Criar um servidor de Banco de Dados do Azure para MySQL
Um Banco de Dados do Azure para o servidor MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md). Olá servidor será criado dentro de um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Navegue muito**bancos de dados** > **banco de dados do Azure para MySQL**. Se você não encontrar o servidor MySQL em **bancos de dados** categoria, clique em **ver todos os** tooshow disponível todos os serviços de banco de dados. Você também pode digitar **banco de dados do Azure para MySQL** no tooquickly de caixa de pesquisa Olá localizar o serviço de saudação.
![2-1 Navegue tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Clique no bloco **Banco de Dados do Azure para MySQL** e, em seguida, clique em **Criar**.

Em nosso exemplo, preencha hello banco de dados do Azure para o formulário do MySQL com hello informações a seguir:

| **Configuração** | **Valor sugerido** | **Descrição do Campo** |
|---|---|---|
| *Nome do servidor* | myserver4demo  | Nome do servidor tem toobe globalmente exclusivo. |
| *Assinatura* | mysubscription | Selecione sua assinatura na lista suspensa hello. |
| *Grupo de recursos* | myresourcegroup | Crie um Grupo de recursos ou use um grupo existente. |
| *Logon de administrador do servidor* | myadmin | Nome da conta do administrador de configuração. |
| *Senha* |  | Defina uma senha de conta de administrador de alta segurança. |
| *Confirmar senha* |  | Confirme a senha da conta de administrador hello. |
| *Localidade* |  | Selecione uma região disponível. |
| *Versão* | 5.7 | Escolha a versão mais recente do hello. |
| *Configurar o desempenho* | Básico, 50 unidades de computação, 50 GB  | Escolha **Tipo de preço**, **Unidades de Computação**, **Armazenamento (GB)**e clique em **OK**. |
| *PIN tooDashboard* | Verificação | Recomendado toocheck essa caixa para que você pode encontrar o servidor de saudação facilmente no futuro |
Em seguida, clique em **Criar**. Em um ou dois minutos, um novo banco de dados do Azure para o MySQL server está em execução na nuvem hello. Você pode clicar em **notificações** botão no processo de implantação do hello barra de ferramentas toomonitor hello.

## <a name="configure-firewall"></a>Configurar o firewall
Os Banco de Dados do Azure para MySQL são protegidos por um firewall. Por padrão, todas as conexões toohello server Olá bancos de dados e no servidor de saudação são rejeitados. Antes de conectar tooAzure banco de dados para MySQL para Olá primeira vez, configure o endereço IP da rede pública da máquina do cliente Olá tooadd Olá firewall (ou intervalo de endereços IP).

1. Clique em seu servidor recém-criado e depois clique em **Segurança de conexão**.
   ![3-1 Segurança da conexão](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Você pode **Adicionar Meu IP** ou configurar regras de firewall aqui. Lembre-se de tooclick **salvar** depois de criar regras de saudação.
Agora você pode conectar o servidor de toohello usando a ferramenta de linha de comando do mysql ou MySQL Workbench GUI.

> [!TIP]
> O Banco de Dados do Azure para servidor MySQL se comunica pela porta 3306. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 3306 talvez não consigam pelo firewall da rede. Nesse caso, você não pode se conectar tooAzure MySQL server, a menos que o departamento de TI abre a porta 3306.

## <a name="get-connection-information"></a>Obter informações de conexão
Olá Get totalmente qualificado **nome do servidor** e **nome de logon de administrador do servidor** para seu banco de dados do Azure para o MySQL server de saudação portal do Azure. Você usa Olá totalmente qualificado nome tooconnect tooyour server usando a ferramenta de linha de comando do mysql. 

1. Em [portal do Azure](https://portal.azure.com/), clique em **todos os recursos** do menu esquerdo Olá, nome do tipo hello e pesquisa para seu banco de dados do Azure para o MySQL server. Selecione detalhes de Olá tooview do nome de servidor de saudação.

2. Em configurações de saudação do título, clique em **propriedades**. Anote o **NOME DO SERVIDOR** e o **NOME DE LOGON DO ADMINISTRADOR DO SERVIDOR**. Você pode clicar Olá copiar botão Avançar tooeach campo toocopy toohello área de transferência.
   ![4-2 Propriedades do servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

Neste exemplo, o nome do servidor de saudação é *myserver4demo.mysql.database.azure.com*, e o logon de administrador do servidor de saudação é  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Conecte-se o servidor toohello usando mysql
Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour uma conexão banco de dados do Azure para o MySQL server. Você pode executar a ferramenta de linha de comando do mysql Olá de saudação Shell de nuvem do Azure no navegador de saudação ou de sua própria máquina usando ferramentas do mysql instaladas localmente. Olá toolaunch Shell de nuvem do Azure, clique em Olá `Try It` botão em um bloco de código neste artigo, ou visite Olá portal do Azure e Olá `>_` ícone Olá superior direita da barra de ferramentas. 

Digite hello tooconnect de comando:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Criar um banco de dados vazio
Quando estiver conectado toohello server, crie um toowork de banco de dados em branco com.
```sql
CREATE DATABASE mysampledb;
```

No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toothis recém-criada:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Criar tabelas no banco de dados de saudação
Agora que você sabe como tooconnect toohello banco de dados para o banco de dados MySQL, podemos ir como toocomplete algumas tarefas básicas.

Primeiro, criamos uma tabela e a carregamos com alguns dados. Vamos criar uma tabela que armazena informações de inventário.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Carregar dados em tabelas de saudação
Agora que temos uma tabela, podemos inserir alguns dados nela. Na janela de prompt de comando aberta hello, execute Olá tooinsert de consulta a seguir algumas linhas de dados.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Agora você tem duas linhas de dados de exemplo na tabela de saudação criado anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar e atualizar dados Olá nas tabelas de saudação
Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.
```sql
SELECT * FROM inventory;
```

Você também pode atualizar dados Olá nas tabelas de saudação.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

linha de saudação obtém atualizada quando você recuperar dados.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar um ponto anterior do banco de dados tooa no tempo
Imagine que você excluiu acidentalmente uma tabela de banco de dados importantes e não é possível recuperar dados de saudação facilmente. Banco de dados do Azure para MySQL permite toorestore Olá server tooa ponto no tempo, criando uma cópia de bancos de dados Olá no novo servidor. Você pode usar esse novo toorecover de servidor os dados excluídos. Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.

1. No hello portal do Azure, localize o banco de dados do Azure para MySQL. Em Olá **visão geral** , clique em **restaurar** na barra de ferramentas de saudação. Olá restauração de página é aberta.

   ![10-1 restaurar um banco de dados](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Preencha Olá **restaurar** formulário com informações de saudação necessária.
   
   ![10-2 formulário de restauração](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Ponto de restauração**: selecione um point-in-time que você deseja toorestore, dentro do período de saudação listado. Verifique se tooconvert tooUTC seu fuso horário local.
   - **Restaurar o servidor toonew**: forneça um novo nome de servidor que você deseja toorestore para.
   - **Local**: Olá região é o mesmo que o servidor de origem hello e não pode ser alterado.
   - **Camada de preços**: Olá preço é hello igual Olá servidor de origem e não pode ser alterado.
   
3. Clique em **Okey** toorestore Olá servidor muito[tooa ponto de restauração pontual](./howto-restore-server-portal.md) antes Olá tabela foi excluída. Restaurar um servidor cria uma nova cópia do servidor de saudação, a partir de saudação ponto no tempo que você especificar. 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usar Olá toolearned portal do Azure como para:

> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para MySQL
> * Configurar o firewall do servidor de saudação
> * Usar a ferramenta de linha de comando de mysql toocreate um banco de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

> [!div class="nextstepaction"]
> [Como tooconnect aplicativos tooAzure banco de dados para MySQL](./howto-connection-string.md)
