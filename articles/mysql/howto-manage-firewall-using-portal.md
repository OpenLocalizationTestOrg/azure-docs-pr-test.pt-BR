---
title: "aaaCreate e gerenciar o banco de dados MySQL para regras de firewall usando o portal do Azure de saudação | Microsoft Docs"
description: "Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure
Regras de firewall de nível de servidor Habilitar administradores tooaccess um banco de dados do Azure para MySQL Server de um endereço IP especificado ou o intervalo de endereços IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall de nível de servidor no hello portal do Azure

1. Na folha de servidor MySQL hello, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para Olá banco de dados do Azure para MySQL.

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Clique em **adicionar meu IP** em Olá barra de ferramentas toocreate uma regra com o endereço IP de saudação do seu computador, conforme percebido pelo Olá sistema do Azure.

   ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verifique se o endereço IP antes de salvar a configuração de saudação. Em algumas situações, endereço IP hello observado pelo portal do Azure é diferente do endereço IP hello usado ao acessar Olá internet e servidores do Azure. Portanto, talvez seja necessário toochange Olá IP inicial e final IP toomake Olá regra funcionar como esperado.

   Use um mecanismo de pesquisa ou outra ferramenta on-line toocheck seu próprio endereço IP (por exemplo, procure "qual é o endereço IP").

   ![Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Adicionar outros intervalos de endereço. Em regras de saudação para Olá banco de dados do Azure para o firewall do MySQL, você pode especificar um único endereço IP ou um intervalo de endereços. Se você quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final de IP. Abrir o firewall Olá permite tooaccess administradores e usuários qualquer banco de dados Olá MySQL server toowhich têm credenciais válidas.

   ![Portal do Azure - regras de firewall ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor. Aguarde a confirmação Olá Olá atualização toohello as regras de firewall foi bem-sucedida.

   ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gerenciar regras de firewall de nível de servidor existente por meio de saudação portal do Azure
Repita as regras de firewall Olá etapas toomanage hello.
* tooadd Olá o computador atual, clique em **+ adicionar meu IP**.
* os endereços IP adicionais tooadd, digite Olá **o nome da regra**, **IP inicial**, e **IP final**.
* toomodify uma regra existente, clique em qualquer um dos campos de saudação na regra hello e modificar.
* regra de toodelete existente, clique botão de reticências Olá […] e clique em **excluir**.
* Clique em **salvar** toosave alterações de saudação.

## <a name="next-steps"></a>Próximas etapas
- Para obter ajuda na conexão tooan banco de dados do Azure para o MySQL server, consulte [bibliotecas de Conexão para o banco de dados do Azure para MySQL](./concepts-connection-libraries.md)
