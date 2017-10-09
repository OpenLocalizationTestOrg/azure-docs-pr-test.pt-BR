---
title: "aaaCreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando o portal do Azure de saudação | Microsoft Docs"
description: "Criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure
Regras de firewall de nível de servidor Habilitar administradores tooaccess um banco de dados do Azure para PostgreSQL Server de um endereço IP especificado ou o intervalo de endereços IP. 

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um servidor [Criar um servidor de Banco de Dados do Azure para o PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall de nível de servidor no hello portal do Azure
1. Na folha de servidor Olá PostgreSQL, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para hello Azure banco de dados PostgreSQL.

  ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Clique em **adicionar meu IP** na barra de ferramentas de saudação. Isso criará uma regra de automaticamente com o endereço IP de saudação do seu computador, conforme percebido pelo Olá sistema do Azure.

  ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verifique se o endereço IP antes de salvar a configuração de saudação. Em algumas situações, endereço IP hello observado pelo portal do Azure é diferente do endereço IP hello usado ao acessar Olá internet e servidores do Azure. Portanto, talvez seja necessário toochange Olá IP inicial e final IP toomake Olá regra funcionar como esperado.
Use um mecanismo de pesquisa ou outra ferramenta on-line toocheck seu próprio endereço IP (por exemplo, pesquisa do Bing "qual é o meu IP").

  ![Pesquisa do Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Adicionar outros intervalos de endereço. Em regras de Olá para Olá banco de dados PostgreSQL firewall, você pode especificar um único endereço IP ou um intervalo de endereços. Se você quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final de IP. Abrir firewall Olá permite que administradores e usuários toologin tooany banco de dados em Olá PostgreSQL server toowhich têm credenciais válidas.

  ![Portal do Azure - regras de firewall ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor. Aguarde a confirmação Olá Olá atualização toohello as regras de firewall foi bem-sucedida.

  ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gerenciar regras de firewall de nível de servidor existente por meio de saudação portal do Azure
Repita as regras de firewall Olá etapas toomanage hello.
* tooadd Olá o computador atual, clique botão de saudação muito + **adicionar meu IP**. Clique em **salvar** toosave alterações de saudação.
* os endereços IP adicionais tooadd, digite Olá nome da regra, o endereço IP inicial e o endereço IP final. Clique em **salvar** toosave alterações de saudação.
* toomodify uma regra existente, clique em qualquer um dos campos de saudação na regra hello e modificar. Clique em **salvar** toosave alterações de saudação.
* toodelete uma regra existente, clique botão de reticências Olá [...] e clique em Excluir regra de saudação remover. Clique em **salvar** toosave alterações de saudação.

## <a name="next-steps"></a>Próximas etapas
- Da mesma forma, você pode gerar um script muito[criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando a CLI do Azure](howto-manage-firewall-using-cli.md)
- Para obter ajuda na conexão tooan banco de dados para o servidor PostgreSQL, consulte [bibliotecas de Conexão para o banco de dados do Azure para PostgreSQL](concepts-connection-libraries.md)
