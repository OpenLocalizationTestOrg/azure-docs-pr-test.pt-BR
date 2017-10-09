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
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Fazer a rotação de credenciais de logon para entradas e saídas em trabalhos do Stream Analytics
## <a name="abstract"></a>Resumo
O Azure Stream Analytics atualmente não permite substituindo credenciais Olá em uma entrada/saída ao trabalho hello está sendo executado.

Azure Stream Analytics dá suporte ao retomar um trabalho da última saída, queremos tooshare Olá todo o processo para minimizar a latência Olá entre Olá parando e iniciando trabalho hello e rotação de credenciais de logon de saudação.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Parte 1 - Preparar o novo conjunto de credenciais de saudação:
Esta parte é aplicável toohello entradas/saídas a seguir:

* Armazenamento de Blob
* Hubs de Eventos
* Banco de Dados SQL
* Armazenamento de tabela

Para outras entradas/saídas, prossiga para a Parte 2.

### <a name="blob-storagetable-storage"></a>Armazenamento de blob/Armazenamento de tabela
1. Acesse toohello extensão de armazenamento no portal de gerenciamento do Azure hello:  
   ![elementográfico1][graphic1]
2. Localize o armazenamento de saudação usado por seu trabalho e vá para ele:  
   ![elementográfico2][graphic2]
3. Clique em Olá gerenciar chaves de acesso comando:  
   ![elementográfico3][graphic3]
4. Entre Olá chave de acesso primária e hello chave de acesso secundária, **escolher Olá não usado por seu trabalho**.
5. Regeneração de ocorrência:   
   ![elementográfico4][graphic4]
6. Copie a chave de saudação recentemente gerada:  
   ![elementográfico5][graphic5]
7. Continue tooPart 2.

### <a name="event-hubs"></a>Hubs de Eventos
1. Vá toohello extensão de barramento de serviço no portal de gerenciamento do Azure hello:  
   ![elementográfico6][graphic6]
2. Localize Olá Namespace de barramento de serviço usada pelo seu trabalho e vá para ele:  
   ![elementográfico7][graphic7]
3. Se seu trabalho usa uma política de acesso compartilhado em Olá Namespace de barramento de serviço, ir toostep 6  
4. Consulte o guia de Hubs de eventos toohello:  
   ![elementográfico8][graphic8]
5. Localize Olá Hub de eventos usado pelo seu trabalho e vá para ele:  
   ![elementográfico9][graphic9]
6. Vá toohello guia Configurar:  
   ![elementográfico10][graphic10]
7. No hello suspensa Nome da política, localize a política de acesso Olá compartilhada usada por seu trabalho:  
   ![elementográfico11][graphic11]
8. Entre hello chave primária e chave secundária, da saudação **escolher Olá não usado por seu trabalho**.  
9. Regeneração de ocorrência:   
   ![elementográfico12][graphic12]
10. Copie a chave de saudação recentemente gerada:  
   ![elementográfico13][graphic13]
11. Continue tooPart 2.  

### <a name="sql-database"></a>Banco de dados SQL
> [!NOTE]
> Observação: você precisará tooconnect toohello serviço de banco de dados SQL. Vamos tooshow como toodo esse usando Olá experiência de gerenciamento no portal de gerenciamento do Azure hello, mas você pode escolher uma ferramenta de cliente como o SQL Server Management Studio também toouse.
>
> 

1. Vá toohello extensão de bancos de dados SQL no portal de gerenciamento do Azure hello:  
   ![elementográfico14][graphic14]
2. Localizar Olá banco de dados do SQL usado pelo seu trabalho e **clique no servidor de saudação** link Olá mesmo linha:  
   ![elementográfico15][graphic15]
3. Clique em Olá gerenciar comando:  
   ![elementográfico16][graphic16]
4. Digite o Banco de Dados Mestre:   
   ![elementográfico17][graphic17]
5. Digite seu Nome de Usuário, sua Senha e clique em Fazer logon:   
   ![elementográfico18][graphic18]
6. Clique em Nova Consulta:   
   ![elementográfico19][graphic19]
7. Tipo de saudação a seguir consulta substituindo < login_name > com o seu nome de usuário e a substituição <enterStrongPasswordHere> com sua nova senha:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Clique em Executar:   
   ![elementográfico20][graphic20]
9. Voltar toostep 2 e desta vez clique em banco de dados de saudação:  
   ![elementográfico21][graphic21]
10. Clique em Olá gerenciar comando:  
   ![elementográfico22][graphic22]
11. Digite seu Nome de Usuário, sua Senha e clique em Fazer logon:   
   ![elementográfico23][graphic23]
12. Clique em Nova Consulta:   
   ![elementográfico24][graphic24]
13. Digite Olá a seguir consulta substituindo < Nome_de_usuário > com um nome pelo qual você deseja tooidentify esse logon no contexto de saudação do banco de dados (você pode fornecer Olá o mesmo valor que você atribuiu para < login_name >, por exemplo) e substituindo < login_name > com seu novo nome de usuário:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Clique em Executar:   
   ![elementográfico25][graphic25]
15. Agora você deve fornecer o novo usuário Olá mesmas funções e privilégios de usuário original tinha.
16. Continue tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Parte 2: Parando Olá trabalho do Stream Analytics
1. Vá extensão de análise de fluxo de toohello no portal de gerenciamento do Azure hello:  
   ![elementográfico26][graphic26]
2. Localize seu trabalho e acesse-o:   
   ![elementográfico27][graphic27]
3. Vá toohello entradas guia ou Olá saídas com base em se você está girando credenciais Olá em uma entrada ou em uma saída.  
   ![elementográfico28][graphic28]
4. Clique em comando de parada hello e confirme a saudação trabalho foi interrompido:  
   ![graphic29][graphic29] aguardar Olá toostop de trabalho.
5. Localizar Olá entrada/saída deseja toorotate credenciais no e vá para ele:  
   ![elementográfico30][graphic30]
6. Continue tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Parte 3: Editar Olá credenciais Olá trabalho do Stream Analytics
### <a name="blob-storagetable-storage"></a>Armazenamento de blob/Armazenamento de tabela
1. Localizar o campo de chave da conta de armazenamento hello e cole sua chave gerada mais recentemente ela:  
   ![elementográfico31][graphic31]
2. Clique Olá salvar comando e confirme a salvar suas alterações:  
   ![elementográfico32][graphic32]
3. Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.
4. Continue tooPart 4.

### <a name="event-hubs"></a>Hubs de Eventos
1. Localizar o campo de chave de política do Hub de eventos hello e cole sua chave gerada mais recentemente ela:  
   ![elementográfico33][graphic33]
2. Clique Olá salvar comando e confirme a salvar suas alterações:  
   ![elementográfico34][graphic34]
3. Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.
4. Continue tooPart 4.

### <a name="power-bi"></a>Power BI
1. Clique em autorização de renovar hello:  

   ![elementográfico35][graphic35]
2. Você obterá Olá confirmação a seguir:  

   ![elementográfico36][graphic36]
3. Clique Olá salvar comando e confirme a salvar suas alterações:  
   ![elementográfico37][graphic37]
4. Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.
5. Continue tooPart 4.

### <a name="sql-database"></a>Banco de dados SQL
1. Localizar Olá campos de nome de usuário e senha e cole o recém-criado conjunto de credenciais-los:  
   ![elementográfico38][graphic38]
2. Clique Olá salvar comando e confirme a salvar suas alterações:  
   ![elementográfico39][graphic39]
3. Um teste de conexão será automaticamente iniciado quando você salvar as alterações, verifique se ele é aprovado.  
4. Continue tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Parte 4: Iniciando o trabalho desde a hora da última interrupção
1. Sair Olá entrada/saída:  
   ![elementográfico40][graphic40]
2. Clique em saudação inicial comando:  
   ![elementográfico41][graphic41]
3. Escolher Olá hora da última interrupção e clique em Okey:  
   ![elementográfico42][graphic42]
4. Continue tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Parte 5: Removendo Olá antigo conjunto de credenciais
Esta parte é aplicável toohello entradas/saídas a seguir:

* Armazenamento de Blob
* Hubs de Eventos
* Banco de Dados SQL
* Armazenamento de tabela

### <a name="blob-storagetable-storage"></a>Armazenamento de blob/Armazenamento de tabela
Repita a parte 1 para Olá chave de acesso que foi usado anteriormente pelo seu trabalho toorenew Olá agora não utilizado de chave de acesso.

### <a name="event-hubs"></a>Hubs de Eventos
Repita a parte 1 para Olá chave que foi usada anteriormente pelo seu trabalho toorenew Olá chave agora não utilizado.

### <a name="sql-database"></a>Banco de dados SQL
1. Volte toohello janela de consulta da parte 1 etapa 7 e digite Olá consulta a seguir, substituindo < previous_login_name > com hello nome de usuário que foi usado anteriormente pelo seu trabalho:  
   `DROP LOGIN <previous_login_name>`  
2. Clique em Executar:   
   ![elementográfico43][graphic43]  

Você deve obter Olá confirmação a seguir: 

    Command(s) completed successfully.

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

