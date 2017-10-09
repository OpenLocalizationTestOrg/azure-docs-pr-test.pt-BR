---
title: conceitos de aaaServer no banco de dados do Azure para MySQL | Microsoft Docs
description: "Este tópico fornece diretrizes e considerações para trabalhar com o Banco de Dados do Azure para servidores MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Conceitos de servidor no Banco de Dados do Azure para MySQL
Este tópico fornece diretrizes e considerações para trabalhar com o Banco de Dados do Azure para servidores MySQL.

## <a name="what-is-an-azure-database-for-mysql-server"></a>O que é um Banco de Dados do Azure para servidor MySQL?

Um Banco de Dados do Azure para servidor MySQL é um ponto administrativo central para vários bancos de dados. É Olá mesmo construção do servidor MySQL que talvez você esteja familiarizado com em Olá, mundo local. Especificamente, Olá banco de dados do Azure para o serviço do MySQL é gerenciado, oferece garantias de desempenho, expõe os recursos no nível de servidor e acesso.

Um Banco de Dados do Azure para servidor MySQL:

- É criado dentro de uma assinatura do Azure.
- É o recurso pai de saudação para bancos de dados.
- Fornece um namespace para bancos de dados.
- É um contêiner com semântica de tempo de vida forte - excluir um servidor e ele exclui os bancos de dados Olá contido.
- Coloca recursos em uma região.
- Fornece um ponto de extremidade de conexão para acesso ao servidor e ao banco de dados.
- Fornece o escopo de saudação para políticas de gerenciamento que se aplicam a bancos de dados tooits: logon, firewall, os usuários, funções, configurações, etc.
- Está disponível em várias versões. Para saber mais, confira [Banco de Dados do Azure com suporte para versões de banco de dados MySQL](./concepts-supported-versions.md).

Dentro de um banco de dados do Azure para o servidor MySQL, você pode criar um ou mais bancos de dados. Você pode aceitar toocreate um único banco de dados por servidor tooutilize todos os recursos de hello, ou criar tooshare de bancos de dados de vários recursos hello. Olá preços são estruturada por servidor, com base na configuração de saudação da camada de preço, unidades de armazenamento (GB) de computação. Para obter mais informações, consulte [Tipos de preço](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Como se conectar e autenticar tooan banco de dados do Azure para o MySQL server?

Olá elementos a seguir ajudam a garantir segurança tooyour banco de dados.

|||
| :-- | :-- |
| **Autenticação e autorização** | O Banco de Dados do Azure para servidor MySQL oferece suporte à autenticação de MySQL nativa. Você pode se conectar e autenticar tooserver com logon de administrador do servidor de saudação. |
| **Protocolo** | serviço de saudação dá suporte a um protocolo de mensagem usado pelo MySQL. |
| **TCP/IP** | há suporte a protocolo de saudação sobre TCP/IP e em soquetes do domínio do Unix. |
| **Firewall** | toohelp proteger seus dados, uma regra de firewall impede que todos os servidores de banco de dados do access tooyour ou bancos de dados de tooits, até que você especifique quais computadores têm permissão. Confira [Regras de firewall do Banco de Dados do Azure para servidor MySQL](./concepts-firewall-rules.md). |
| **SSL** | serviço de saudação dá suporte a impor conexões SSL entre os aplicativos e o servidor de banco de dados.  Consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Como posso gerenciar um servidor?
Você pode gerenciar o banco de dados do Azure para servidores de MySQL usando Olá portal do Azure ou Olá CLI do Azure.

## <a name="next-steps"></a>Próximas etapas
- Para obter uma visão geral do serviço hello, consulte [banco de dados do Azure para visão geral do MySQL](./overview.md)
- Para saber mais sobre cotas e limitações específicas de recursos com base em sua **camada de serviço**, confira [Camadas de serviço](./concepts-service-tiers.md)
- Para obter informações sobre o serviço de toohello de conexão, consulte [bibliotecas de Conexão para o banco de dados do Azure para MySQL](./concepts-connection-libraries.md).
