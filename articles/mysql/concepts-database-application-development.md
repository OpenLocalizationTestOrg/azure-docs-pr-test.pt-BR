---
title: "Visão geral de desenvolvimento de aplicativo aaaDatabase banco de dados do Azure para MySQL | Microsoft Docs"
description: "Apresenta considerações de design que um desenvolvedor deve seguir ao escrever aplicativos código tooconnect tooAzure banco de dados para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Visão geral de desenvolvimento de aplicativo para o Banco de Dados do Azure para MySQL 
Este artigo aborda considerações de design que um desenvolvedor deve seguir ao escrever aplicativos código tooconnect tooAzure banco de dados para MySQL 

> [!TIP]
> Para um tutorial mostrando você como toocreate um servidor, criar um firewall baseado em servidor, exibir propriedades de servidor, cria banco de dados, se conectar e consulta usando o workbench e mysql.exe, consulte [criar seu primeiro banco de dados MySQL do Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Linguagem e plataforma
Há exemplos de código disponíveis para uma variedade de plataformas e linguagens de programação. Você pode encontrar links toohello exemplos de código em: [bibliotecas de conectividade usados tooconnect tooAzure banco de dados para MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Ferramentas
Banco de dados do Azure para MySQL usa a versão de comunidade MySQL hello, compatível com as ferramentas de gerenciamento comuns MySQL como utilitários Workbench ou MySQL como mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)e outros. Você também pode usar o hello portal do Azure, CLI do Azure e toointeract de APIs REST com o serviço de banco de dados de saudação.

## <a name="resource-limitations"></a>Limitações de recursos
Banco de dados MySQL Azure gerencia Olá recursos disponíveis tooa server usando dois mecanismos diferentes: 
- Governança de recursos 
- Imposição de limites.

## <a name="security"></a>Segurança
O Banco de Dados MySQL do Azure fornece recursos para limitar o acesso, proteger os dados, configurar usuários e funções e monitorar atividades em um Banco de Dados MySQL.

## <a name="authentication"></a>Autenticação
O Banco de Dados MySQL do Azure oferece suporte à autenticação de usuários e logons do servidor.

## <a name="resiliency"></a>Resiliência
Quando ocorre um erro temporário durante a conexão tooMySQL banco de dados, seu código deverá repetir a chamada de saudação. Recomendamos o uso de lógica de repetição Olá a lógica, para que não sobrecarregue Olá banco de dados SQL com vários clientes simultaneamente repetir.

- Exemplos de código: para exemplos de código que ilustram a lógica de repetição, consulte exemplos para o idioma de saudação de sua preferência em: [bibliotecas de conectividade usados tooconnect tooAzure banco de dados para MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Gerenciando conexões
Conexões de banco de dados são um recurso limitado, portanto, é recomendável uso adequado de conexões ao acessar o banco de dados MySQL tooachieve melhor desempenho.
- Banco de dados Access hello usando conexões persistentes ou pool de conexão.
- Banco de dados Access hello usando conexão curto tempo de vida útil. 
- Use a lógica de repetição em seu aplicativo no ponto de saudação da tentativa de conexão hello, toocatch falhas devido a conexões tooconcurrent atingiu o máximo de saudação permitido. Em Olá lógica de repetição, defina um pequeno atraso e aguarde um tempo aleatório antes de tentativas de conexão adicionais hello.
