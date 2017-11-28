
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="d591e-101">Para economizar custos, é possível pausar e retomar os recursos de computação sob demanda.</span><span class="sxs-lookup"><span data-stu-id="d591e-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="d591e-102">Por exemplo, se você não usar banco de dados durante a noite e nos finais de semana, você poderá pausá-lo durante esses períodos e retomá-lo durante o dia.</span><span class="sxs-lookup"><span data-stu-id="d591e-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="d591e-103">Você não será cobrado por DWUs enquanto o banco de dados estiver em pausa.</span><span class="sxs-lookup"><span data-stu-id="d591e-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="d591e-104">Quando você pausa um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="d591e-104">When you pause a database:</span></span>

* <span data-ttu-id="d591e-105">Recursos de computação e memória são retornados ao pool de recursos disponíveis no data center</span><span class="sxs-lookup"><span data-stu-id="d591e-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="d591e-106">Os custos de DWU são zero durante a pausa.</span><span class="sxs-lookup"><span data-stu-id="d591e-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="d591e-107">O armazenamento de dados não é afetado e seus dados permanecem intactos.</span><span class="sxs-lookup"><span data-stu-id="d591e-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="d591e-108">O SQL Data Warehouse cancela todas as operações em execução ou em fila.</span><span class="sxs-lookup"><span data-stu-id="d591e-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

