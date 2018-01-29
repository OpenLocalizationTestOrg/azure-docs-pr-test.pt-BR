---
title: "Diretrizes para o exemplo de aplicativo de multilocatário do Banco de Dados SQL - Wingtip SaaS | Microsoft Docs"
description: "Fornece diretrizes e etapas para instalar e executar o aplicativo de multilocatário de exemplo que usa o Banco de Dados SQL do Azure, o exemplo de SaaS do Wingtip Tickets."
keywords: tutorial do banco de dados SQL
services: sql-database
author: MightyPen
manager: craigg
ms.service: sql-database
ms.custom: scale out apps
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/20/2017
ms.author: genemi
ms.openlocfilehash: ebf1c4948816746fa02b867d1ea66afc64b882b0
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2017
---
# <a name="general-guidance-for-working-with-wingtip-tickets-sample-saas-apps"></a>Diretrizes gerais para trabalhar com aplicativos SaaS de exemplo do Wingtip Tickets

Este artigo contém diretrizes gerais para a execução de aplicativos SaaS de exemplo do Wingtip Tickets que utilizam o Banco de Dados SQL do Azure. 

## <a name="download-and-unblock-the-wingtip-tickets-saas-scripts"></a>Baixe e desbloqueie os scripts SaaS do Wingtip Tickets

Conteúdos executáveis (scripts, dlls) podem ser bloqueados pelo Windows quando arquivos zip são baixados de uma fonte externa e extraídos. Ao extrair os scripts de um arquivo zip, **siga as etapas abaixo para desbloquear o arquivo. zip antes da extração**. Isso garante que os scripts podem ser executados.

1. Navegue até o repositório GitHub de SaaS do Wingtip Tickets para o padrão de locação do banco de dados que você deseja explorar: 
    - [WingtipTicketsSaaS-StandaloneApp](https://github.com/Microsoft/WingtipTicketsSaaS-StandaloneApp)
    - [WingtipTicketsSaaS-DbPerTenant](https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant)
    - [WingtipTicketsSaaS-MultiTenantDb](https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDb)
2. Clique em **Clonar ou baixar**.
3. Clique em **Baixar zip** e salve o arquivo.
4. Clique com o botão direito do mouse no arquivo zip e selecione **Propriedades**. O nome do arquivo zip corresponderá com o nome do repositório. (ex. _WingtipTicketsSaaS-DbPerTenant-master.zip_)
5. Na guia **geral**, selecione **Desbloquear**.
6. Clique em **OK**.
7. Extraia os arquivos.

Os scripts estão localizados na pasta *..\\Learning Modules*.


## <a name="working-with-the-wingtip-tickets-powershell-scripts"></a>Trabalhando com scripts do PowerShell do Wingtip Tickets

Para aproveitar ao máximo o exemplo, você precisa saber mais sobre os scripts fornecidos. Utilize pontos de interrupção, avance os scripts ao executar e examine como os diferentes padrões SaaS são implementados. Para percorrer facilmente os módulos e scripts fornecidos para a melhor compreensão, é recomendável usar o [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-the-configuration-file-for-your-deployment"></a>Atualizar o arquivo de configuração para sua implantação

Editar o **UserConfig.psm1** arquivo com o valor de usuário e grupo de recursos que podem ser definidos durante a implantação:

1. Abra o *ISE do PowerShell* e carregue... \\UserConfig.psm1\\ do *Módulo de Aprendizado* 
2. Atualize *ResourceGroupName* e *Nomeie* com os valores específicos para sua implantação (somente nas linhas 10 e 11).
3. Salve as alterações!

Definir esses valores aqui simplesmente impede que você precise atualizar esses valores específicos de implantação em cada script.

### <a name="execute-the-scripts-by-pressing-f5"></a>Execute os scripts pressionando F5

Vários scripts usam *$PSScriptRoot* para permitir a navegação em pastas e *$PSScriptRoot* é avaliada somente quando o script é executado, ao pressionar **F5**.  Realçar e executar uma seleção (**F8**) pode resultar em erros, então pressione **F5** ao executar scripts.

### <a name="step-through-the-scripts-to-examine-the-implementation"></a>Percorrer os scripts para examinar a implementação

É a melhor maneira de entender os scripts, percorrendo-los para ver o que fazem. Confira os scripts para **demonstração** incluídos que apresentam uma forma fácil de seguir o fluxo de trabalho de alto nível. Os script para **demonstração** mostram as etapas necessárias para executar cada tarefa, portanto, defina pontos de interrupção e analise mais detalhadamente em chamadas individuais para ver os detalhes de implementação para os diferentes padrões de SaaS.

Dicas para explorar e depurar scripts do PowerShell:

- Abra os scripts para **demonstração** no ISE do PowerShell.
- Execute ou continue com **F5** (o uso de **F8** não é recomendável porque o *$PSScriptRoot* não é avaliado durante a execução de seleções de um script).
- Coloque pontos de interrupção, clicando ou selecionando uma linha e pressionando **F9**.
- Passe por uma função ou chamada de script usando **F10**.
- Intervenha em uma função ou chamada de script usando **F11**.
- Saia da função atual ou da chamada de script usando **Shift + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Explorar o esquema de banco de dados e executar consultas SQL usando o SSMS

Use o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para se conectar e procurar os servidores e bancos de dados do aplicativo.

Inicialmente, a implantação tem locatários e servidores de Banco de Dados SQL do catálogo para se conectar. A nomenclatura dos servidores depende do padrão de locação do banco de dados (veja abaixo detalhes específicos). 

   - **Aplicativo autônomo:** servidores para cada locatário (ex. servidor *contosoconcerthall-&lt;Usuário&gt;*) e *catalog-sa-&lt;Usuário&gt;*
   - **Banco de dados por locatário:** *tenants1-dpt-&lt;Usuário&gt;*  e servidores *catalog-dpt-&lt;Usuário&gt;*
   - **Base de dados multilocatário:** *tenants1-mt-&lt;User&gt;* e servidores *catalog-mt-&lt;User&gt;*

Para garantir uma conexão de demonstração bem-sucedida, todos os servidores têm uma [regra de firewall](sql-database-firewall-configure.md) permitindo todos os IPs.


1. Abra o *SSMS* e conecte-se aos locatários. O nome do servidor depende do padrão de locação do banco de dados selecionado (veja abaixo detalhes específicos):
    - **Aplicativo autônomo:** servidores de inquilinos individuais (ex. *contosoconcerthall-&lt;Usuário&gt;.database.windows.net*) 
    - **Banco de dados por locatário:** *tenants1-dpt-&lt;Usuário&gt;.database.windows.net*
    - **Banco de dados multilocatário:** *tenants1-mt-&lt;Usuário&gt;.database.windows.net* 
2. Clique em **Conectar** > **Mecanismo de Banco de Dados...**:

   ![servidor catalog](media/saas-tenancy-wingtip-app-guidance-tips/connect.png)

3. As credenciais de demonstração são: logon = *developer*, senha = *P@ssword1*

    A imagem abaixo demonstra o logon para o padrão *Banco de dados por locatário*. 
    ![conexão](media/saas-tenancy-wingtip-app-guidance-tips/tenants1-connect.png)
    
   

4. Repita as etapas 2 - 3 e conecte-se ao servidor do catálogo (veja abaixo os nomes dos servidores específicos com base no padrão de locação do banco de dados selecionado)
    - **Aplicativo autônomo:** *catalog-sa-&lt;Usuário&gt;.database.windows.net*
    - **Banco de dados por locatário:** *catalog-dpt-&lt;Usuário&gt;.database.windows.net*
    - **Banco de dados multilocatário:** *catalog-mt-&lt;Usuário&gt;.database.windows.net*


Após a conexão bem-sucedida, você deverá visualizar todos os servidores. Sua lista de bancos de dados pode ser diferente, dependendo dos locatários provisionados.

A imagem abaixo demonstra o logon para o padrão *Banco de dados por locatário*.

![pesquisador de objetos](media/saas-tenancy-wingtip-app-guidance-tips/object-explorer.png)



## <a name="next-steps"></a>Próximas etapas
- [Implantar o Aplicativo Autônomo SaaS Wingtip Tickets](saas-standaloneapp-get-started-deploy.md)
- [Implantar o aplicativo do Banco de Dados por locatário do SaaS do Wingtip Ticket](saas-dbpertenant-get-started-deploy.md)
- [Implantar o aplicativo do Banco de Dados Multilocatário do SaaS do Wingtip Tickets](saas-multitenantdb-get-started-deploy.md)

