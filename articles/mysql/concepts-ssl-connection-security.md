---
title: aaaSSL conectividade de banco de dados do Azure para MySQL | Microsoft Docs
description: "Informações para configurar o banco de dados do Azure para aplicativos associados tooproperly e MySQL usar conexões SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Conectividade SSL no Banco de Dados do Azure para MySQL
Banco de dados do Azure para MySQL dá suporte à conexão seus aplicativos de tooclient do servidor de banco de dados usando o protocolo (SSL). Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.

## <a name="default-settings"></a>Configurações padrão
Por padrão, o serviço de banco de dados de saudação deve ser toorequire configurado as conexões SSL ao conectar-se tooMySQL.  É recomendável evitar que a opção de SSL Olá sempre que possível. 

Ao provisionar um novo banco de dados do Azure para o MySQL server por meio de saudação portal do Azure e a CLI, imposição de conexões SSL está habilitada por padrão. 

Da mesma forma, cadeias de caracteres de conexão previamente definidas nas configurações de "Cadeias de caracteres de Conexão" hello em seu servidor no portal do Azure de saudação incluem parâmetros de saudação necessária para comuns idiomas tooconnect tooyour servidor usando SSL. Hello parâmetro SSL varia de acordo com o conector hello, por exemplo "ssl = true" ou "sslmode = exigem" ou "sslmode = necessária" e outras variações.

toolearn como tooenable ou desabilitar conexão SSL durante o desenvolvimento de aplicativo, consulte muito[como tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Próximas etapas
[Bibliotecas de conexão para o Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)
