
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="24003-101">toosave custos, você pode pausar e retomar computação recursos sob demanda.</span><span class="sxs-lookup"><span data-stu-id="24003-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="24003-102">Por exemplo, se você não usar o banco de dados de saudação durante a noite hello e nos finais de semana, você pode pausá-la durante os horários e retomá-lo durante o dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="24003-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="24003-103">Você não será cobrado para DWUs enquanto o banco de dados de saudação está em pausa.</span><span class="sxs-lookup"><span data-stu-id="24003-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="24003-104">Quando você pausa um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="24003-104">When you pause a database:</span></span>

* <span data-ttu-id="24003-105">Recursos de computação e memória são retornados toohello pool de recursos disponíveis no Centro de dados Olá</span><span class="sxs-lookup"><span data-stu-id="24003-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="24003-106">Custo DWU é zero para a duração de saudação do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="24003-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="24003-107">O armazenamento de dados não é afetado e seus dados permanecem intactos.</span><span class="sxs-lookup"><span data-stu-id="24003-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="24003-108">O SQL Data Warehouse cancela todas as operações em execução ou em fila.</span><span class="sxs-lookup"><span data-stu-id="24003-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

