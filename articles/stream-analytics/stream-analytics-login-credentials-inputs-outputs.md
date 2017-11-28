---
title: "Stream Analytics: alternar as credenciais de logon para entradas e saídas | Microsoft Docs"
description: "Saiba como atualizar as credenciais para as entradas e saídas do Stream Analytics."
keywords: credenciais de logon
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="5022f-104">Fazer a rotação de credenciais de logon para entradas e saídas em trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5022f-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="5022f-105">Resumo</span><span class="sxs-lookup"><span data-stu-id="5022f-105">Abstract</span></span>
<span data-ttu-id="5022f-106">No momento, o Azure Stream Analytics não permite a substituição das credenciais em uma entrada/saída durante a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5022f-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="5022f-107">Embora o Azure Stream Analytics ofereça suporte à retomada de um trabalho desde a última saída, queremos compartilhar o processo inteiro para minimizar a latência entre a parada e o início do trabalho e fazer a rotação de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="5022f-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="5022f-108">Parte 1 - Preparar o novo conjunto de credenciais:</span><span class="sxs-lookup"><span data-stu-id="5022f-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="5022f-109">Essa parte é aplicável às seguintes entradas/saídas:</span><span class="sxs-lookup"><span data-stu-id="5022f-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="5022f-110">Armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="5022f-110">Blob Storage</span></span>
* <span data-ttu-id="5022f-111">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5022f-111">Event Hubs</span></span>
* <span data-ttu-id="5022f-112">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5022f-112">SQL Database</span></span>
* <span data-ttu-id="5022f-113">Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="5022f-113">Table Storage</span></span>

<span data-ttu-id="5022f-114">Para outras entradas/saídas, prossiga para a Parte 2.</span><span class="sxs-lookup"><span data-stu-id="5022f-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="5022f-115">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="5022f-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="5022f-116">Vá para a extensão Armazenamento no Portal de Gerenciamento do Azure: </span><span class="sxs-lookup"><span data-stu-id="5022f-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![elementográfico1][graphic1]
2. <span data-ttu-id="5022f-118">Localize o armazenamento usado por seu trabalho e acesse-o: </span><span class="sxs-lookup"><span data-stu-id="5022f-118">Locate the storage used by your job and go into it:</span></span>  
   ![elementográfico2][graphic2]
3. <span data-ttu-id="5022f-120">Clique no comando Gerenciar Chaves de Acesso: </span><span class="sxs-lookup"><span data-stu-id="5022f-120">Click the Manage Access Keys command:</span></span>  
   ![elementográfico3][graphic3]
4. <span data-ttu-id="5022f-122">Entre a Chave de Acesso Primária e a Chave de Acesso Secundária, **escolha a que não é usada por seu trabalho**.</span><span class="sxs-lookup"><span data-stu-id="5022f-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="5022f-123">Regeneração de ocorrência: </span><span class="sxs-lookup"><span data-stu-id="5022f-123">Hit regenerate:</span></span>  
   ![elementográfico4][graphic4]
6. <span data-ttu-id="5022f-125">Copie a chave recém-gerada: </span><span class="sxs-lookup"><span data-stu-id="5022f-125">Copy the newly generated key:</span></span>  
   ![elementográfico5][graphic5]
7. <span data-ttu-id="5022f-127">Prossiga para a Parte 2.</span><span class="sxs-lookup"><span data-stu-id="5022f-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="5022f-128">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5022f-128">Event hubs</span></span>
1. <span data-ttu-id="5022f-129">Vá para a extensão Barramento de Serviço no Portal de Gerenciamento do Azure: </span><span class="sxs-lookup"><span data-stu-id="5022f-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![elementográfico6][graphic6]
2. <span data-ttu-id="5022f-131">Localize o Namespace do Barramento de Serviço usado por seu trabalho e acesse-o: </span><span class="sxs-lookup"><span data-stu-id="5022f-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![elementográfico7][graphic7]
3. <span data-ttu-id="5022f-133">Se seu trabalho usar uma política de acesso compartilhado no Namespace de Barramento de Serviço, vá para a etapa 6</span><span class="sxs-lookup"><span data-stu-id="5022f-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="5022f-134">Vá para a guia Hubs de Eventos: </span><span class="sxs-lookup"><span data-stu-id="5022f-134">Go to the Event Hubs tab:</span></span>  
   ![elementográfico8][graphic8]
5. <span data-ttu-id="5022f-136">Localize o Hub de Eventos usado por seu trabalho e acesse-o: </span><span class="sxs-lookup"><span data-stu-id="5022f-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![elementográfico9][graphic9]
6. <span data-ttu-id="5022f-138">Vá para a guia Configurar: </span><span class="sxs-lookup"><span data-stu-id="5022f-138">Go to the Configure Tab:</span></span>  
   ![elementográfico10][graphic10]
7. <span data-ttu-id="5022f-140">No menu suspenso Nome da Política, localize a política de acesso compartilhado usada por seu trabalho: </span><span class="sxs-lookup"><span data-stu-id="5022f-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![elementográfico11][graphic11]
8. <span data-ttu-id="5022f-142">Entre a Chave Primária e a Chave Secundária, **escolha a que não é usada por seu trabalho**.</span><span class="sxs-lookup"><span data-stu-id="5022f-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="5022f-143">Regeneração de ocorrência: </span><span class="sxs-lookup"><span data-stu-id="5022f-143">Hit regenerate:</span></span>  
   ![elementográfico12][graphic12]
10. <span data-ttu-id="5022f-145">Copie a chave recém-gerada: </span><span class="sxs-lookup"><span data-stu-id="5022f-145">Copy the newly generated key:</span></span>  
   ![elementográfico13][graphic13]
11. <span data-ttu-id="5022f-147">Prossiga para a Parte 2.</span><span class="sxs-lookup"><span data-stu-id="5022f-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="5022f-148">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5022f-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="5022f-149">Observação: será necessário se conectar ao Serviço de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5022f-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="5022f-150">Vamos mostrar como fazer isso usando a experiência de gerenciamento no Portal de Gerenciamento do Azure, mas você também pode optar por usar uma ferramenta do lado cliente, como o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5022f-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="5022f-151">Vá para a extensão Bancos de Dados SQL no Portal de Gerenciamento do Azure: </span><span class="sxs-lookup"><span data-stu-id="5022f-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![elementográfico14][graphic14]
2. <span data-ttu-id="5022f-153">Localize o Banco de Dados SQL usado por seu trabalho e **clique no link do servidor** na mesma linha:</span><span class="sxs-lookup"><span data-stu-id="5022f-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="5022f-154">![elementográfico15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="5022f-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="5022f-155">Clique no comando Gerenciar: </span><span class="sxs-lookup"><span data-stu-id="5022f-155">Click the Manage command:</span></span>  
   ![elementográfico16][graphic16]
4. <span data-ttu-id="5022f-157">Digite o Banco de Dados Mestre: </span><span class="sxs-lookup"><span data-stu-id="5022f-157">Type Database Master:</span></span>  
   ![elementográfico17][graphic17]
5. <span data-ttu-id="5022f-159">Digite seu Nome de Usuário, sua Senha e clique em Fazer logon: </span><span class="sxs-lookup"><span data-stu-id="5022f-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![elementográfico18][graphic18]
6. <span data-ttu-id="5022f-161">Clique em Nova Consulta: </span><span class="sxs-lookup"><span data-stu-id="5022f-161">Click New Query:</span></span>  
   ![elementográfico19][graphic19]
7. <span data-ttu-id="5022f-163">Digite a consulta a seguir, substituindo <login_name> por seu Nome de Usuário e substituindo <enterStrongPasswordHere> por sua nova senha:</span><span class="sxs-lookup"><span data-stu-id="5022f-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="5022f-164">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="5022f-164">Click Run:</span></span>  
   ![elementográfico20][graphic20]
9. <span data-ttu-id="5022f-166">Volte para etapa 2 e, dessa vez, clique no banco de dados: </span><span class="sxs-lookup"><span data-stu-id="5022f-166">Go back to step 2 and this time click the database:</span></span>  
   ![elementográfico21][graphic21]
10. <span data-ttu-id="5022f-168">Clique no comando Gerenciar: </span><span class="sxs-lookup"><span data-stu-id="5022f-168">Click the Manage command:</span></span>  
   ![elementográfico22][graphic22]
11. <span data-ttu-id="5022f-170">Digite seu Nome de Usuário, sua Senha e clique em Fazer logon: </span><span class="sxs-lookup"><span data-stu-id="5022f-170">type in your User Name, Password, and click Logon:</span></span>  
   ![elementográfico23][graphic23]
12. <span data-ttu-id="5022f-172">Clique em Nova Consulta: </span><span class="sxs-lookup"><span data-stu-id="5022f-172">Click New Query:</span></span>  
   ![elementográfico24][graphic24]
13. <span data-ttu-id="5022f-174">Digite a consulta a seguir, substituindo <user_name> por um nome pelo qual você deseja identificar esse logon no contexto desse banco de dados (é possível fornecer o mesmo valor atribuído para <login_name>, por exemplo) e substituindo <login_name> por seu novo nome de usuário:</span><span class="sxs-lookup"><span data-stu-id="5022f-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="5022f-175">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="5022f-175">Click Run:</span></span>  
   ![elementográfico25][graphic25]
15. <span data-ttu-id="5022f-177">Agora, você deve fornecer ao novo usuário as mesmas funções e privilégios que o usuário original tinha.</span><span class="sxs-lookup"><span data-stu-id="5022f-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="5022f-178">Prossiga para a Parte 2.</span><span class="sxs-lookup"><span data-stu-id="5022f-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="5022f-179">Parte 2: Interrompendo o trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5022f-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="5022f-180">Vá para a extensão Stream Analytics no Portal de Gerenciamento do Azure: </span><span class="sxs-lookup"><span data-stu-id="5022f-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![elementográfico26][graphic26]
2. <span data-ttu-id="5022f-182">Localize seu trabalho e acesse-o: </span><span class="sxs-lookup"><span data-stu-id="5022f-182">Locate your job and go into it:</span></span>  
   ![elementográfico27][graphic27]
3. <span data-ttu-id="5022f-184">Vá para a guia Entradas ou para a guia Saídas se você estiver fazendo uma rotação das credenciais em uma Entrada ou em uma Saída.</span><span class="sxs-lookup"><span data-stu-id="5022f-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![elementográfico28][graphic28]
4. <span data-ttu-id="5022f-186">Clique no comando Parar e confirme se o trabalho foi interrompido: </span><span class="sxs-lookup"><span data-stu-id="5022f-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="5022f-187">![graphic29][graphic29] Aguarde a interrupção do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5022f-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="5022f-188">Localize a entrada/saída em que você deseja fazer a rotação de credenciais e acesse-a: </span><span class="sxs-lookup"><span data-stu-id="5022f-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![elementográfico30][graphic30]
6. <span data-ttu-id="5022f-190">Prossiga para a Parte 3.</span><span class="sxs-lookup"><span data-stu-id="5022f-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="5022f-191">Parte 3: Editando as credenciais no trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5022f-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="5022f-192">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="5022f-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="5022f-193">Localize o campo Chave da Conta de Armazenamento e cole sua chave recém-gerada nele: </span><span class="sxs-lookup"><span data-stu-id="5022f-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![elementográfico31][graphic31]
2. <span data-ttu-id="5022f-195">Clique no comando Salvar e confirme o salvamento das alterações: </span><span class="sxs-lookup"><span data-stu-id="5022f-195">Click the Save command and confirm saving your changes:</span></span>  
   ![elementográfico32][graphic32]
3. <span data-ttu-id="5022f-197">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="5022f-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="5022f-198">Prossiga para a Parte 4.</span><span class="sxs-lookup"><span data-stu-id="5022f-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="5022f-199">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5022f-199">Event hubs</span></span>
1. <span data-ttu-id="5022f-200">Localize o campo Política de Hub de Eventos e cole sua chave recém-gerada nele: </span><span class="sxs-lookup"><span data-stu-id="5022f-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![elementográfico33][graphic33]
2. <span data-ttu-id="5022f-202">Clique no comando Salvar e confirme o salvamento das alterações: </span><span class="sxs-lookup"><span data-stu-id="5022f-202">Click the Save command and confirm saving your changes:</span></span>  
   ![elementográfico34][graphic34]
3. <span data-ttu-id="5022f-204">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="5022f-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="5022f-205">Prossiga para a Parte 4.</span><span class="sxs-lookup"><span data-stu-id="5022f-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="5022f-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="5022f-206">Power BI</span></span>
1. <span data-ttu-id="5022f-207">Clique em Renovar autorização:</span><span class="sxs-lookup"><span data-stu-id="5022f-207">Click the Renew authorization:</span></span>  

   ![elementográfico35][graphic35]
2. <span data-ttu-id="5022f-209">Você obterá a seguinte confirmação:</span><span class="sxs-lookup"><span data-stu-id="5022f-209">You will get the following confirmation:</span></span>  

   ![elementográfico36][graphic36]
3. <span data-ttu-id="5022f-211">Clique no comando Salvar e confirme o salvamento das alterações: </span><span class="sxs-lookup"><span data-stu-id="5022f-211">Click the Save command and confirm saving your changes:</span></span>  
   ![elementográfico37][graphic37]
4. <span data-ttu-id="5022f-213">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="5022f-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="5022f-214">Prossiga para a Parte 4.</span><span class="sxs-lookup"><span data-stu-id="5022f-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="5022f-215">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5022f-215">SQL Database</span></span>
1. <span data-ttu-id="5022f-216">Localize os campos Nome de usuário e Senha e cole seu conjunto de credenciais recém-criado neles: </span><span class="sxs-lookup"><span data-stu-id="5022f-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![elementográfico38][graphic38]
2. <span data-ttu-id="5022f-218">Clique no comando Salvar e confirme o salvamento das alterações: </span><span class="sxs-lookup"><span data-stu-id="5022f-218">Click the Save command and confirm saving your changes:</span></span>  
   ![elementográfico39][graphic39]
3. <span data-ttu-id="5022f-220">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="5022f-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="5022f-221">Prossiga para a Parte 4.</span><span class="sxs-lookup"><span data-stu-id="5022f-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="5022f-222">Parte 4: Iniciando o trabalho desde a hora da última interrupção</span><span class="sxs-lookup"><span data-stu-id="5022f-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="5022f-223">Navegue para fora da Entrada/Saída: </span><span class="sxs-lookup"><span data-stu-id="5022f-223">Navigate away from the Input/Output:</span></span>  
   ![elementográfico40][graphic40]
2. <span data-ttu-id="5022f-225">Clique no comando Iniciar: </span><span class="sxs-lookup"><span data-stu-id="5022f-225">Click the Start command:</span></span>  
   ![elementográfico41][graphic41]
3. <span data-ttu-id="5022f-227">Selecione a Hora da Última Interrupção e clique em OK: </span><span class="sxs-lookup"><span data-stu-id="5022f-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![elementográfico42][graphic42]
4. <span data-ttu-id="5022f-229">Prossiga para a Parte 5.</span><span class="sxs-lookup"><span data-stu-id="5022f-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="5022f-230">Parte 5: Removendo o conjunto de credenciais antigo</span><span class="sxs-lookup"><span data-stu-id="5022f-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="5022f-231">Essa parte é aplicável às seguintes entradas/saídas:</span><span class="sxs-lookup"><span data-stu-id="5022f-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="5022f-232">Armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="5022f-232">Blob Storage</span></span>
* <span data-ttu-id="5022f-233">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5022f-233">Event Hubs</span></span>
* <span data-ttu-id="5022f-234">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5022f-234">SQL Database</span></span>
* <span data-ttu-id="5022f-235">Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="5022f-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="5022f-236">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="5022f-236">Blob storage/Table storage</span></span>
<span data-ttu-id="5022f-237">Repita a Parte 1 da Chave de Acesso usada anteriormente por seu trabalho para renovar a Chave de Acesso agora não utilizada.</span><span class="sxs-lookup"><span data-stu-id="5022f-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="5022f-238">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5022f-238">Event hubs</span></span>
<span data-ttu-id="5022f-239">Repita a Parte 1 da Chave usada anteriormente por seu trabalho para renovar a Chave agora não utilizada.</span><span class="sxs-lookup"><span data-stu-id="5022f-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="5022f-240">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5022f-240">SQL Database</span></span>
1. <span data-ttu-id="5022f-241">Vá para a janela de consulta da Parte 1 Etapa 7 e digite a consulta a seguir, substituindo <previous_login_name> pelo Nome de Usuário usado anteriormente por seu trabalho:</span><span class="sxs-lookup"><span data-stu-id="5022f-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="5022f-242">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="5022f-242">Click Run:</span></span>  
   ![elementográfico43][graphic43]  

<span data-ttu-id="5022f-244">Você deverá obter a seguinte confirmação:</span><span class="sxs-lookup"><span data-stu-id="5022f-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="5022f-245">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="5022f-245">Get help</span></span>
<span data-ttu-id="5022f-246">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5022f-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5022f-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5022f-247">Next steps</span></span>
* [<span data-ttu-id="5022f-248">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5022f-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5022f-249">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5022f-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5022f-250">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5022f-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5022f-251">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5022f-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5022f-252">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5022f-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

