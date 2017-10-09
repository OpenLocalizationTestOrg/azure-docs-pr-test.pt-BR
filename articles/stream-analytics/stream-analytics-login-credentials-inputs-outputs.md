---
title: "Stream Analytics: alternar as credenciais de logon para entradas e saídas | Microsoft Docs"
description: "Saiba como tooupdate Olá credenciais para análise de fluxo de entradas e saídas."
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
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="cc7aa-104">Fazer a rotação de credenciais de logon para entradas e saídas em trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc7aa-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="cc7aa-105">Resumo</span><span class="sxs-lookup"><span data-stu-id="cc7aa-105">Abstract</span></span>
<span data-ttu-id="cc7aa-106">O Azure Stream Analytics atualmente não permite substituindo credenciais Olá em uma entrada/saída ao trabalho hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="cc7aa-107">Azure Stream Analytics dá suporte ao retomar um trabalho da última saída, queremos tooshare Olá todo o processo para minimizar a latência Olá entre Olá parando e iniciando trabalho hello e rotação de credenciais de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="cc7aa-108">Parte 1 - Preparar o novo conjunto de credenciais de saudação:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="cc7aa-109">Esta parte é aplicável toohello entradas/saídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="cc7aa-110">Armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="cc7aa-110">Blob Storage</span></span>
* <span data-ttu-id="cc7aa-111">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cc7aa-111">Event Hubs</span></span>
* <span data-ttu-id="cc7aa-112">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="cc7aa-112">SQL Database</span></span>
* <span data-ttu-id="cc7aa-113">Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="cc7aa-113">Table Storage</span></span>

<span data-ttu-id="cc7aa-114">Para outras entradas/saídas, prossiga para a Parte 2.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="cc7aa-115">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="cc7aa-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="cc7aa-116">Acesse toohello extensão de armazenamento no portal de gerenciamento do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![elementográfico1][graphic1]
2. <span data-ttu-id="cc7aa-118">Localize o armazenamento de saudação usado por seu trabalho e vá para ele:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-118">Locate hello storage used by your job and go into it:</span></span>  
   ![elementográfico2][graphic2]
3. <span data-ttu-id="cc7aa-120">Clique em Olá gerenciar chaves de acesso comando:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-120">Click hello Manage Access Keys command:</span></span>  
   ![elementográfico3][graphic3]
4. <span data-ttu-id="cc7aa-122">Entre Olá chave de acesso primária e hello chave de acesso secundária, **escolher Olá não usado por seu trabalho**.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="cc7aa-123">Regeneração de ocorrência: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-123">Hit regenerate:</span></span>  
   ![elementográfico4][graphic4]
6. <span data-ttu-id="cc7aa-125">Copie a chave de saudação recentemente gerada:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-125">Copy hello newly generated key:</span></span>  
   ![elementográfico5][graphic5]
7. <span data-ttu-id="cc7aa-127">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="cc7aa-128">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cc7aa-128">Event hubs</span></span>
1. <span data-ttu-id="cc7aa-129">Vá toohello extensão de barramento de serviço no portal de gerenciamento do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![elementográfico6][graphic6]
2. <span data-ttu-id="cc7aa-131">Localize Olá Namespace de barramento de serviço usada pelo seu trabalho e vá para ele:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![elementográfico7][graphic7]
3. <span data-ttu-id="cc7aa-133">Se seu trabalho usa uma política de acesso compartilhado em Olá Namespace de barramento de serviço, ir toostep 6</span><span class="sxs-lookup"><span data-stu-id="cc7aa-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="cc7aa-134">Consulte o guia de Hubs de eventos toohello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-134">Go toohello Event Hubs tab:</span></span>  
   ![elementográfico8][graphic8]
5. <span data-ttu-id="cc7aa-136">Localize Olá Hub de eventos usado pelo seu trabalho e vá para ele:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![elementográfico9][graphic9]
6. <span data-ttu-id="cc7aa-138">Vá toohello guia Configurar:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-138">Go toohello Configure Tab:</span></span>  
   ![elementográfico10][graphic10]
7. <span data-ttu-id="cc7aa-140">No hello suspensa Nome da política, localize a política de acesso Olá compartilhada usada por seu trabalho:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![elementográfico11][graphic11]
8. <span data-ttu-id="cc7aa-142">Entre hello chave primária e chave secundária, da saudação **escolher Olá não usado por seu trabalho**.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="cc7aa-143">Regeneração de ocorrência: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-143">Hit regenerate:</span></span>  
   ![elementográfico12][graphic12]
10. <span data-ttu-id="cc7aa-145">Copie a chave de saudação recentemente gerada:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-145">Copy hello newly generated key:</span></span>  
   ![elementográfico13][graphic13]
11. <span data-ttu-id="cc7aa-147">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="cc7aa-148">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="cc7aa-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="cc7aa-149">Observação: você precisará tooconnect toohello serviço de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="cc7aa-150">Vamos tooshow como toodo esse usando Olá experiência de gerenciamento no portal de gerenciamento do Azure hello, mas você pode escolher uma ferramenta de cliente como o SQL Server Management Studio também toouse.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="cc7aa-151">Vá toohello extensão de bancos de dados SQL no portal de gerenciamento do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![elementográfico14][graphic14]
2. <span data-ttu-id="cc7aa-153">Localizar Olá banco de dados do SQL usado pelo seu trabalho e **clique no servidor de saudação** link Olá mesmo linha:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="cc7aa-154">![elementográfico15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="cc7aa-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="cc7aa-155">Clique em Olá gerenciar comando:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-155">Click hello Manage command:</span></span>  
   ![elementográfico16][graphic16]
4. <span data-ttu-id="cc7aa-157">Digite o Banco de Dados Mestre: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-157">Type Database Master:</span></span>  
   ![elementográfico17][graphic17]
5. <span data-ttu-id="cc7aa-159">Digite seu Nome de Usuário, sua Senha e clique em Fazer logon: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![elementográfico18][graphic18]
6. <span data-ttu-id="cc7aa-161">Clique em Nova Consulta: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-161">Click New Query:</span></span>  
   ![elementográfico19][graphic19]
7. <span data-ttu-id="cc7aa-163">Tipo de saudação a seguir consulta substituindo < login_name > com o seu nome de usuário e a substituição <enterStrongPasswordHere> com sua nova senha:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="cc7aa-164">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-164">Click Run:</span></span>  
   ![elementográfico20][graphic20]
9. <span data-ttu-id="cc7aa-166">Voltar toostep 2 e desta vez clique em banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![elementográfico21][graphic21]
10. <span data-ttu-id="cc7aa-168">Clique em Olá gerenciar comando:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-168">Click hello Manage command:</span></span>  
   ![elementográfico22][graphic22]
11. <span data-ttu-id="cc7aa-170">Digite seu Nome de Usuário, sua Senha e clique em Fazer logon: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-170">type in your User Name, Password, and click Logon:</span></span>  
   ![elementográfico23][graphic23]
12. <span data-ttu-id="cc7aa-172">Clique em Nova Consulta: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-172">Click New Query:</span></span>  
   ![elementográfico24][graphic24]
13. <span data-ttu-id="cc7aa-174">Digite Olá a seguir consulta substituindo < Nome_de_usuário > com um nome pelo qual você deseja tooidentify esse logon no contexto de saudação do banco de dados (você pode fornecer Olá o mesmo valor que você atribuiu para < login_name >, por exemplo) e substituindo < login_name > com seu novo nome de usuário:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="cc7aa-175">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-175">Click Run:</span></span>  
   ![elementográfico25][graphic25]
15. <span data-ttu-id="cc7aa-177">Agora você deve fornecer o novo usuário Olá mesmas funções e privilégios de usuário original tinha.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="cc7aa-178">Continue tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="cc7aa-179">Parte 2: Parando Olá trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc7aa-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="cc7aa-180">Vá extensão de análise de fluxo de toohello no portal de gerenciamento do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![elementográfico26][graphic26]
2. <span data-ttu-id="cc7aa-182">Localize seu trabalho e acesse-o: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-182">Locate your job and go into it:</span></span>  
   ![elementográfico27][graphic27]
3. <span data-ttu-id="cc7aa-184">Vá toohello entradas guia ou Olá saídas com base em se você está girando credenciais Olá em uma entrada ou em uma saída.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![elementográfico28][graphic28]
4. <span data-ttu-id="cc7aa-186">Clique em comando de parada hello e confirme a saudação trabalho foi interrompido:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="cc7aa-187">![graphic29][graphic29] aguardar Olá toostop de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="cc7aa-188">Localizar Olá entrada/saída deseja toorotate credenciais no e vá para ele:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![elementográfico30][graphic30]
6. <span data-ttu-id="cc7aa-190">Continue tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="cc7aa-191">Parte 3: Editar Olá credenciais Olá trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc7aa-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="cc7aa-192">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="cc7aa-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="cc7aa-193">Localizar o campo de chave da conta de armazenamento hello e cole sua chave gerada mais recentemente ela:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![elementográfico31][graphic31]
2. <span data-ttu-id="cc7aa-195">Clique Olá salvar comando e confirme a salvar suas alterações:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![elementográfico32][graphic32]
3. <span data-ttu-id="cc7aa-197">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="cc7aa-198">Continue tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="cc7aa-199">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cc7aa-199">Event hubs</span></span>
1. <span data-ttu-id="cc7aa-200">Localizar o campo de chave de política do Hub de eventos hello e cole sua chave gerada mais recentemente ela:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![elementográfico33][graphic33]
2. <span data-ttu-id="cc7aa-202">Clique Olá salvar comando e confirme a salvar suas alterações:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![elementográfico34][graphic34]
3. <span data-ttu-id="cc7aa-204">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="cc7aa-205">Continue tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="cc7aa-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="cc7aa-206">Power BI</span></span>
1. <span data-ttu-id="cc7aa-207">Clique em autorização de renovar hello:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-207">Click hello Renew authorization:</span></span>  

   ![elementográfico35][graphic35]
2. <span data-ttu-id="cc7aa-209">Você obterá Olá confirmação a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-209">You will get hello following confirmation:</span></span>  

   ![elementográfico36][graphic36]
3. <span data-ttu-id="cc7aa-211">Clique Olá salvar comando e confirme a salvar suas alterações:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![elementográfico37][graphic37]
4. <span data-ttu-id="cc7aa-213">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="cc7aa-214">Continue tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="cc7aa-215">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="cc7aa-215">SQL Database</span></span>
1. <span data-ttu-id="cc7aa-216">Localizar Olá campos de nome de usuário e senha e cole o recém-criado conjunto de credenciais-los:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![elementográfico38][graphic38]
2. <span data-ttu-id="cc7aa-218">Clique Olá salvar comando e confirme a salvar suas alterações:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![elementográfico39][graphic39]
3. <span data-ttu-id="cc7aa-220">Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="cc7aa-221">Continue tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="cc7aa-222">Parte 4: Iniciando o trabalho desde a hora da última interrupção</span><span class="sxs-lookup"><span data-stu-id="cc7aa-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="cc7aa-223">Sair Olá entrada/saída:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-223">Navigate away from hello Input/Output:</span></span>  
   ![elementográfico40][graphic40]
2. <span data-ttu-id="cc7aa-225">Clique em saudação inicial comando:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-225">Click hello Start command:</span></span>  
   ![elementográfico41][graphic41]
3. <span data-ttu-id="cc7aa-227">Escolher Olá hora da última interrupção e clique em Okey:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![elementográfico42][graphic42]
4. <span data-ttu-id="cc7aa-229">Continue tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="cc7aa-230">Parte 5: Removendo Olá antigo conjunto de credenciais</span><span class="sxs-lookup"><span data-stu-id="cc7aa-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="cc7aa-231">Esta parte é aplicável toohello entradas/saídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="cc7aa-232">Armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="cc7aa-232">Blob Storage</span></span>
* <span data-ttu-id="cc7aa-233">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cc7aa-233">Event Hubs</span></span>
* <span data-ttu-id="cc7aa-234">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="cc7aa-234">SQL Database</span></span>
* <span data-ttu-id="cc7aa-235">Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="cc7aa-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="cc7aa-236">Armazenamento de blob/Armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="cc7aa-236">Blob storage/Table storage</span></span>
<span data-ttu-id="cc7aa-237">Repita a parte 1 para Olá chave de acesso que foi usado anteriormente pelo seu trabalho toorenew Olá agora não utilizado de chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="cc7aa-238">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cc7aa-238">Event hubs</span></span>
<span data-ttu-id="cc7aa-239">Repita a parte 1 para Olá chave que foi usada anteriormente pelo seu trabalho toorenew Olá chave agora não utilizado.</span><span class="sxs-lookup"><span data-stu-id="cc7aa-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="cc7aa-240">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="cc7aa-240">SQL Database</span></span>
1. <span data-ttu-id="cc7aa-241">Volte toohello janela de consulta da parte 1 etapa 7 e digite Olá consulta a seguir, substituindo < previous_login_name > com hello nome de usuário que foi usado anteriormente pelo seu trabalho:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="cc7aa-242">Clique em Executar: </span><span class="sxs-lookup"><span data-stu-id="cc7aa-242">Click Run:</span></span>  
   ![elementográfico43][graphic43]  

<span data-ttu-id="cc7aa-244">Você deve obter Olá confirmação a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc7aa-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="cc7aa-245">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="cc7aa-245">Get help</span></span>
<span data-ttu-id="cc7aa-246">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="cc7aa-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc7aa-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc7aa-247">Next steps</span></span>
* [<span data-ttu-id="cc7aa-248">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc7aa-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cc7aa-249">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc7aa-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cc7aa-250">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc7aa-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cc7aa-251">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc7aa-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cc7aa-252">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc7aa-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

