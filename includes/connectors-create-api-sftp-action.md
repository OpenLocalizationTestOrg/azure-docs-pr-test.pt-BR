Agora que você adicionou um gatilho, seu toodo tempo algo interessante com dados de saudação que são gerados pelo gatilho Olá. Siga essas etapas tooadd uma saudação **SFTP - pasta de extração** ação. Essa ação extrairá o conteúdo de saudação de um arquivo se Olá definido condições. 

tooconfigure Olá esta ação, você precisará Olá tooprovide informações a seguir. Você notará que é fácil toouse dados gerados pelo gatilho hello como entrada para algumas das propriedades de saudação para o novo arquivo de saudação:

| SFTP - extrair propriedade da pasta | Descrição |
| --- | --- |
| Caminho do arquivo de origem |Este é o caminho de saudação para o arquivo hello sendo extraído. Você pode selecionar um dos tokens de saudação de uma ação anterior ou procurar o caminho do arquivo hello SFTP server toofind hello. |
| Caminho da pasta de destino |Este é o caminho de saudação onde os arquivos extraído de saudação serão colocados. Pode selecione um dos tokens de saudação de uma ação anterior como caminho de destino hello ou procurar o servidor SFTP hello e selecione um caminho. |
| Substituir? |Indica se um arquivo com hello mesmo nome como arquivo extraído Olá é encontrado no caminho de pasta de destino Olá se o arquivo existente Olá deve ser substituído ou não. |

Vamos começar adicionando arquivos de Olá Olá ação tooextract se condição Olá definida anteriormente avalia muito*True*. 

1. Escolha **Adicionar uma ação**.        
   ![Imagem de condição de ação de SFTP 6](./media/connectors-create-api-sftp/condition-6.png)   
2. Selecione Olá **SFTP - pasta de extração** ação      
   ![Imagem de condição de ação de SFTP 7](./media/connectors-create-api-sftp/condition-7.png)   
3. Selecione **Caminho do arquivo de origem**              
   ![Imagem de condição de ação de SFTP 9](./media/connectors-create-api-sftp/condition-9.png)   
4. Selecione Olá **caminho do arquivo** token. Isso indica que você usará o caminho do arquivo hello do arquivo Olá Olá encontrado como o caminho do arquivo de arquivo de origem de saudação do gatilho.           
   ![Imagem de condição de ação de SFTP 10](./media/connectors-create-api-sftp/condition-10.png)   
5. Selecione **Caminho da pasta de destino**           
   ![Imagem de condição de ação de SFTP 11](./media/connectors-create-api-sftp/condition-11.png)   
6. Selecione Olá **caminho do arquivo** token. Isso indica que você usará o caminho do arquivo hello do arquivo Olá Olá encontrado como caminho de destino Olá para arquivos extraído de saudação do gatilho.   
7. Digite *\ExtractedFile* em Olá **caminho de pasta de destino** controle. Faça isso apenas após o token de caminho de arquivo hello em Olá controle de caminho de pasta de destino.         
   ![Imagem de condição de ação de SFTP 12](./media/connectors-create-api-sftp/condition-12.png)   
8. Digite *True* em hello **substituir?* tooindicate de controle que os arquivos existentes devem ser substituídos se eles tiverem Olá mesmo nome como Olá extraiu os arquivos.      
   ![Imagem de condição de ação de SFTP 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Salvar fluxo de trabalho do hello alterações tooyour  

