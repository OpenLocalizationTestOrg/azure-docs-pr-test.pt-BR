
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave custos, você pode pausar e retomar computação recursos sob demanda. Por exemplo, se você não usar o banco de dados de saudação durante a noite hello e nos finais de semana, você pode pausá-la durante os horários e retomá-lo durante o dia de saudação. Você não será cobrado para DWUs enquanto o banco de dados de saudação está em pausa.

Quando você pausa um banco de dados:

* Recursos de computação e memória são retornados toohello pool de recursos disponíveis no Centro de dados Olá
* Custo DWU é zero para a duração de saudação do intervalo de saudação.
* O armazenamento de dados não é afetado e seus dados permanecem intactos. 
* O SQL Data Warehouse cancela todas as operações em execução ou em fila.

