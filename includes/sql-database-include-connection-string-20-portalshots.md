
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="729a5-101">Obter a cadeia de conexão no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="729a5-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="729a5-102">Obtenha no [portal do Azure](https://portal.azure.com/) a cadeia de conexão necessária para o seu programa cliente interagir com o Banco de Dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="729a5-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="729a5-103">Clique em **PROCURAR** > **bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="729a5-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="729a5-104">Insira o nome do banco de dados na caixa de texto de filtro próximo ao canto superior esquerdo da folha dos **bancos de dados SQL** .</span><span class="sxs-lookup"><span data-stu-id="729a5-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="729a5-105">Clique na linha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="729a5-105">Click the row for your database.</span></span>
4. <span data-ttu-id="729a5-106">Depois que a folha aparecer para o banco de dados, para conveniência visual, você pode clicar nos controles padrão de minimização para recolher as folhas usadas para navegação e filtragem do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="729a5-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![Filtrar para isolar o banco de dados][10-FilterDatabase]
5. <span data-ttu-id="729a5-108">Na folha do banco de dados, clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="729a5-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="729a5-109">Se você pretende usar a biblioteca de conexão do ADO.NET, copie a cadeia de caracteres rotulada **ADO**.</span><span class="sxs-lookup"><span data-stu-id="729a5-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![Copie a cadeia de conexão do ADO do banco de dados][20-CopyAdoConnectionString]
7. <span data-ttu-id="729a5-111">Em um formato ou outro, cole as informações da cadeia de conexão no código do programa cliente.</span><span class="sxs-lookup"><span data-stu-id="729a5-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="729a5-112">Para obter mais informações, veja:</span><span class="sxs-lookup"><span data-stu-id="729a5-112">For more information, see:</span></span><br/><span data-ttu-id="729a5-113">[Cadeias de conexão e arquivos de configuração](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="729a5-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
