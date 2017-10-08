---
title: "banco de dados ao aaaManage, funções e usuários no Azure Analysis Services | Microsoft Docs"
description: "Saiba como toomanage banco de dados funções e usuários em um servidor do Analysis Services no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Gerenciar usuários e funções de banco de dados

No nível de banco de dados de modelo hello, todos os usuários devem pertencer a função tooa. As funções definem os usuários com permissões específicas para o banco de dados de modelo de saudação. Qualquer usuário ou grupo de segurança adicionadas tooa função deve ter uma conta em um locatário do AD do Azure no hello mesma assinatura que o servidor de saudação.

Como definir funções é diferente dependendo ferramenta Olá usada, mas efeito Olá é Olá mesmo.

As permissões de função incluem:
*  **Administrador** -os usuários têm permissões completas de banco de dados de saudação. Funções de banco de dados com permissões de administrador são diferentes dos administradores do servidor.
*  **Processo** -os usuários podem se conectar a tooand executar operações de processo no banco de dados de saudação e analisar dados de banco de dados de modelo.
*  **Leitura** -os usuários podem usar um cliente de aplicativo tooconnect tooand analisar dados de banco de dados de modelo.

Ao criar um projeto de modelo de tabela, você pode criar funções e adiciona usuários ou grupos de funções de toothose usando o Gerenciador de funções no SSDT. Quando implantado tooa server, você usa o SSMS, [cmdlets do PowerShell do Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), ou [linguagem de script de modelo de tabela](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) ou remover funções e membros de usuário.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd ou gerenciar funções e usuários no SSDT  
  
1.  No SSDT > **Gerenciador de Modelos Tabular**, clique com o botão direito do mouse em **Funções**.  
  
2.  No **Gerenciador de Funções**, clique em **Novo**.  
  
3.  Digite um nome para a função hello.  
  
     Por padrão, o nome de saudação da função de padrão de saudação é numerado incrementalmente para cada nova função. É recomendável que você digite um nome que claramente Identifique o tipo de membro hello, por exemplo, gerentes financeiros ou especialistas de recursos humanos.  
  
4.  Selecione uma saudação as seguintes permissões:  
  
    |Permissão|Descrição|  
    |----------------|-----------------|  
    |**Nenhum**|Membros não é possível modificar o esquema de modelo hello e não é possível consultar dados.|  
    |**Ler**|Os membros podem consultar dados (com base em filtros de linha) mas não é possível modificar o esquema de modelo de saudação.|  
    |**Ler e Processar**|Os membros podem consultar dados (com base em filtros de nível de linha) e executadas operações de processar e processar tudo, mas não é possível modificar o esquema de modelo de saudação.|  
    |**Processo**|Os membros podem executar as operações Processar e Processar Tudo. Não é possível modificar o esquema de modelo hello e não é possível consultar dados.|  
    |**Administrador**|Os membros podem modificar o esquema de modelo Olá e consultar todos os dados.|   
  
5.  Se a função hello que você está criando leu ou permissão de leitura e processo, você pode adicionar filtros de linha usando uma fórmula DAX. Clique em Olá **filtros de linha** guia, selecione uma tabela, clique Olá **filtro DAX** campo e, em seguida, digite uma fórmula DAX.
  
6.  Clique em **Membros** > **Adicionar Externo**.  
  
8.  Em **Adicionar Membro Externo**, insira usuários ou grupos no seu locatário do Azure AD pelo endereço de email. Depois que você clicar em OK e fechar o Gerenciador de Funções, as funções e membros da função aparecem no Gerenciador de Modelos Tabular. 
 
     ![Funções e usuários no Gerenciador de Modelos Tabular](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Implante o servidor de serviços de análise do Azure tooyour.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd ou gerenciar funções e usuários no SSMS
tooadd tooa de usuários e funções implantadas banco de dados modelo, você deve ser o servidor toohello conectado como um administrador de servidor ou já está em uma função de banco de dados com permissões de administrador.

1. No Pesquisador de Objetos, clique com o botão direito do mouse em **Funções** > **Nova Função**.

2. Em **Criar Função**, insira um nome de função e uma descrição.

3. Selecione uma permissão.
   |Permissão|Descrição|  
   |----------------|-----------------|  
   |**Controle total (Administrador)**|Os membros podem modificar o esquema de modelo hello, processar e consultar todos os dados.| 
   |**Processar banco de dados**|Os membros podem executar as operações Processar e Processar Tudo. Não é possível modificar o esquema de modelo hello e não é possível consultar dados.|  
   |**Ler**|Os membros podem consultar dados (com base em filtros de linha) mas não é possível modificar o esquema de modelo de saudação.|  
  
4. Clique em **Associação**, em seguida, insira um usuário ou grupo no seu locatário do Azure AD pelo endereço de email.

     ![Adicionar usuário](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Se a função hello que está criando tem permissão de leitura, você pode adicionar filtros de linha usando uma fórmula DAX. Clique em **filtros de linha**, selecione uma tabela e, em seguida, digite uma fórmula DAX Olá **filtro DAX** campo. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd funções e usuários usando um script TMSL
Você pode executar um script TMSL na janela XMLA Olá no SSMS ou usando o PowerShell. Saudação de uso [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) comando e hello [funções](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objeto.

**Exemplo de script TMSL**

Neste exemplo, um usuário externo B2B e um grupo são adicionados toohello a função de analista com permissões de leitura para o banco de dados do hello SalesBI. Ambos Olá usuário externo e o grupo deve estar no mesmo locatário do AD do Azure.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd funções e usuários usando o PowerShell
Olá [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) módulo fornece banco de dados específicos de tarefa gerenciamento cmdlets e hello geral cmdlet Invoke-ASCmd que aceita uma consulta de linguagem de script de modelo Tabular (TMSL) ou um script. Olá cmdlets a seguir é usado para gerenciar usuários e funções de banco de dados.
  
|Cmdlet|Descrição|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Adicione um membro da função de banco de dados tooa.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Remover um membro de uma função de banco de dados.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Executar um script TMSL.|

## <a name="row-filters"></a>Filtros de linha  
Os filtros de linha definem quais linhas em uma tabela podem ser consultadas por membros de uma função específica. Os filtros de linha são definidos para cada tabela em um modelo usando fórmulas DAX.  
  
Os filtros de linha podem ser definidos somente para funções com as permissões Ler e Ler e Processar. Por padrão, se um filtro de linha não está definido para uma tabela específica, membros podem consultar todas as linhas na tabela hello, a menos que a filtragem cruzada se aplica de outra tabela.
  
 Os filtros de linha exigem uma fórmula DAX, que deve ser avaliada tooa valor TRUE/FALSE, linhas de saudação toodefine que podem ser consultadas por membros daquela função específica. Não não possível consultar as linhas não incluídas na fórmula DAX de saudação. Por exemplo, Olá tabela Customers com hello expressão de filtros de linha, a seguir *= clientes [País] = "EUA"*, membros da função de vendas Olá só podem consultar clientes nos Olá EUA.  
  
Filtros de linha aplicam toohello especificado linhas e linhas relacionadas. Quando uma tabela tiver várias relações, os filtros aplicam segurança para a relação de saudação que está ativa. Os filtros de linha são interseccionados com outros filtros de linha definidos para tabelas relacionadas, por exemplo:  
  
|Tabela|Expressão DAX|  
|-----------|--------------------|  
|Região|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|Transações|=Transactions[Year]=2016|  
  
 efeito de saudação é membros podem consultar as linhas de dados em que cliente hello está nos EUA hello, Olá categoria de produto for bicicletas e ano Olá é 2016. Os usuários não podem consultar transações fora do EUA hello, transações que não são Bicicletas ou transações não 2016, a menos que fossem membros de outra função que concede estas permissões.
  
 Você pode usar o filtro de saudação *=FALSE()*, toodeny acessem as linhas tooall para uma tabela inteira.

## <a name="next-steps"></a>Próximas etapas
  [Gerenciar administradores de servidor](analysis-services-server-admins.md)   
  [Gerenciar o Azure Analysis Services com PowerShell](analysis-services-powershell.md)  
  [Referência de TMSL (Linguagem de Scripts do Modelo Tabular)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

