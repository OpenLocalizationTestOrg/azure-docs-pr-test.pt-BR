---
title: "tooAzure de serviço de aplicativo do Azure existente aaaConnect banco de dados MySQL | Microsoft Docs"
description: "Instruções sobre como tooproperly se conectar a um tooAzure de serviço de aplicativo do Azure banco de dados existente para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Conecte-se um tooAzure do serviço de aplicativo do Azure banco de dados existente para o MySQL server
Este documento explica como tooconnect uma tooyour do serviço de aplicativo do Azure existente do Azure banco de dados para o servidor MySQL.

## <a name="before-you-begin"></a>Antes de começar
Faça logon no toohello [portal do Azure](https://portal.azure.com). Criar um servidor de Banco de Dados do Azure para MySQL. Para obter detalhes, consulte muito[como toocreate Azure banco de dados para o MySQL server do Portal](quickstart-create-mysql-server-database-using-azure-portal.md) ou [como toocreate Azure banco de dados para o MySQL server usando a CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Atualmente, há duas soluções tooenable acesso de um serviço de aplicativo do Azure de tooan banco de dados MySQL. Ambas as soluções envolvem a configuração de regras de firewall de nível de servidor.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Solução 1: criar um tooallow de regra de firewall de todos os IPs
Banco de dados do Azure para MySQL fornece segurança de acesso usando um firewall tooprotect seus dados. Ao conectar-se de um banco de dados do tooAzure do serviço de aplicativo do Azure para MySQL server, tenha em mente que Olá saída IPs de serviço de aplicativo são dinâmicos por natureza. 

disponibilidade de saudação tooensure do seu serviço de aplicativo do Azure, recomendamos usar tooallow essa solução todos os IPs.

> [!NOTE]
> A Microsoft está trabalhando para um tooavoid solução a longo prazo permitindo todos os IPs de serviços do Azure tooconnect tooAzure banco de dados MySQL.

1. Na folha de servidor MySQL hello, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para Olá banco de dados do Azure para MySQL.

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Digite **NOME DA REGRA**, **IP INICIAL** e **IP FINAL**. Em seguida, clique em **Salvar**.
   - Nome da regra: Permitir-Todos os-IPs
   - IP inicial: 0.0.0.0
   - IP final: 255.255.255.255

   ![Portal do Azure – adicionar todos os IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Solução 2: criar um firewall tooexplicitly de regra permitir saída IPs
Você pode adicionar explicitamente que todos Olá IPs de saída do seu serviço de aplicativo do Azure.

1. Na folha de propriedades do serviço de aplicativo hello, exibir seu **endereço de IP de saída**.

   ![Portal do Azure – exibir IPs de saída](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Na folha de segurança de Conexão MySQL hello, adicione saída IPs uma.

   ![Portal do Azure – adicionar IPs explícitos](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Lembre-se muito**salvar** suas regras de firewall.

Embora a saudação do serviço de aplicativo do Azure tenta tookeep IP endereços constante ao longo do tempo, há casos em que os endereços IP de saudação podem mudar. Por exemplo, quando Olá reciclagem de aplicativo, ocorre uma operação em escala ou quando são adicionados novos computadores no Azure dados regionais centros de capacidade de saudação tooincrease. Quando endereços IP hello forem alterados, o aplicativo hello pode apresentar tempo de inatividade em caso de Olá não pode se conectar toohello MySQL server. Considere essa possibilidade ao escolher uma saudação anterior soluções.

## <a name="ssl-configuration"></a>Configuração de SSL
O Banco de Dados do Azure para MySQL tem SSL habilitado por padrão. Se seu aplicativo não estiver usando o banco de dados do SSL tooconnect toohello, você precisa toodisable SSL no servidor MySQL. Para obter detalhes sobre como tooconfigure SSL, consulte [usando SSL com o banco de dados do Azure para MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre cadeias de caracteres de conexão, consulte muito[cadeias de caracteres de Conexão](howto-connection-string.md).
