---
title: "mascaramento de dados dinâmicos do banco de dados SQL aaaAzure | Documentos da Microsoft"
description: "Mascaramento de dados dinâmicos do banco de dados SQL limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Máscara de dados dinâmicos do Banco de Dados SQL

Mascaramento de dados dinâmicos do banco de dados SQL limita a exposição de dados confidenciais mascarando-os usuários privilegiados toonon. 

Mascaramento de dados dinâmicos ajuda a impedir que os dados de toosensitive de acesso não autorizado, permitindo que os clientes toodesignate quanto da saudação dados confidenciais tooreveal com impacto mínimo sobre a camada de aplicativo hello. É um recurso de segurança baseado em políticas que oculta os dados confidenciais de saudação no conjunto de resultados de saudação de uma consulta em relação aos campos do banco de dados designados, enquanto Olá dados no banco de dados de saudação não são alterados.

Por exemplo, um representante do serviço em um call center pode identificar os chamadores usando vários dígitos de seu número de cartão de crédito, mas esses dados itens não devem ser totalmente expostos toohello representante. Uma regra de mascaramento pode ser definida se mascarar todos exceto Olá últimos quatro dígitos de qualquer número de cartão de crédito no conjunto de resultados de saudação de qualquer consulta. Como outro exemplo, uma máscara de dados apropriado pode ser definido tooprotect dados de informações de identificação pessoal (PII), para que um desenvolvedor pode consultar os ambientes de produção para fins de solução de problemas sem violar os regulamentos de conformidade.

## <a name="sql-database-dynamic-data-masking-basics"></a>Noções básicas sobre a máscara de dados dinâmicos do Banco de Dados SQL
Você configurar um política de saudação de mascaramento de dados dinâmicos portal do Azure, selecionando a operação na folha de configuração de banco de dados SQL ou folha de configurações de mascaramento de dados dinâmicos do hello.

### <a name="dynamic-data-masking-permissions"></a>Permissões de mascaramento de dados dinâmico
Mascaramento de dados dinâmicos pode ser configurado por Olá administrador de banco de dados, administrador do servidor ou funções de diretor de segurança.

### <a name="dynamic-data-masking-policy"></a>Política de mascaramento de dados dinâmico
* **Usuários SQL excluídos do mascaramento** - um conjunto de usuários do SQL ou identidades do AAD que recebe dados não mascarados Olá SQL resultados da consulta. Os usuários com privilégios de administrador são sempre excluídos do mascaramento e ver dados original de saudação sem qualquer máscara.
* **Regras de mascaramento** -um conjunto de regras que definem Olá designado toobe campos mascarado e hello mascaramento de função que é usada. Olá designado campos pode ser definido usando um nome de esquema de banco de dados, o nome da tabela e o nome da coluna.
* **Funções de mascaramento** -um conjunto de métodos que controlam a exposição de saudação de dados para cenários diferentes.

| Função de mascaramento | Lógica de mascaramento |
| --- | --- |
| **Padrão** |**Mascaramento completo de dados de acordo toohello tipos de saudação designado campos**<br/><br/>• Use XXXX ou menos Xs se o tamanho de saudação do campo Olá for menor que 4 caracteres para tipos de dados de cadeia de caracteres (nchar, ntext, nvarchar).<br/>• Use um valor zero para tipos de dados numéricos (bigint, bit, decimal, int, money, numérico, smallint, smallmoney, tinyint, float, real).<br/>• Use 01-01-1900 para os tipos de dados de data/hora (data, datetime2, datetime, datetimeoffset, smalldatetime, time).<br/>• Para o valor padrão Olá SQL variant, do tipo atual de saudação é usado.<br/>• Para o documento XML de saudação <masked/> é usado.<br/>• Use um valor vazio para tipos de dados especiais (timestamp table, hierarchyid, GUID, binary, image, varbinary spatial types). |
| **Cartão de crédito** |**Método de mascaramento, que expõe Olá últimos quatro dígitos do hello designado campos** e adiciona uma cadeia de caracteres constante como um prefixo na forma de saudação de um cartão de crédito.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Email** |**Método de mascaramento, que expõe a primeira letra do hello e substitui o domínio Olá com XXX.com** usando um prefixo de cadeia de caracteres constante na forma de saudação de um endereço de email.<br/><br/>aXX@XXXX.com |
| **Número aleatório** |**Método de mascaramento, que gera um número aleatório** toohello de acordo com limites e tipos de dados reais selecionados. Se Olá designado limites forem igual, Olá função de máscara é um número constante.<br/><br/>![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Texto personalizado** |**Método, que expõe Olá primeiro e último caracteres de máscara** e adiciona uma cadeia de caracteres de preenchimento personalizada no meio de saudação. Se a cadeia de caracteres original Olá é menor que o sufixo e prefixo Olá exposto, apenas Olá preenchimento de cadeia de caracteres é usada. <br/>prefixo[preenchimento]sufixo<br/><br/>![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Campos recomendados toomask
Olá mecanismo recomendações DDM sinaliza determinados campos do banco de dados como potencialmente confidenciais e campos, que podem ser bons candidatos para mascaramento. Na folha mascaramento de dados dinâmico Olá no portal de hello, você verá Olá recomendado colunas do banco de dados. Você só precisa toodo é clicar **Adicionar máscara** para uma ou mais colunas e, em seguida, **salvar** tooapply uma máscara para esses campos.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Configurar a máscara de dados dinâmica para o banco de dados usando cmdlets do Powershell
Confira [Cmdlets do Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Configurar a máscara de dados dinâmica para o banco de dados usando a API REST
Confira [Operações para Bancos de Dados SQL do Azure](https://msdn.microsoft.com/library/dn505719.aspx).

