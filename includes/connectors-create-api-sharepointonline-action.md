Agora que você adicionou um gatilho, seu toodo tempo algo interessante com dados de saudação que são gerados pelo gatilho Olá. Siga essas Olá de tooadd etapas **SharePoint Online - criar o arquivo** ação. Essa ação criará um arquivo no SharePoint Online cada aciona o gatilho tempo Olá novo item. 

tooconfigure Olá esta ação, você precisará Olá tooprovide informações a seguir. Como fornecer essas informações, você notará que é fácil toouse dados gerados pelo gatilho hello como entrada para algumas das propriedades de saudação para o novo arquivo de saudação:

| Criar propriedade do arquivo | Descrição |
| --- | --- |
| URL do site |Esta é a URL de saudação do site do SharePoint Online hello, onde você deseja toocreate Olá novo arquivo. Selecione o site Olá na lista de Olá apresentada. |
| Caminho da pasta |Isso é Olá pasta (Olá URL do Site selecionado na etapa anterior Olá) onde o novo arquivo de saudação será colocado. Procurar e selecionar a pasta de saudação. |
| Nome do arquivo |Este é o nome de saudação do arquivo hello está sendo criado. |
| Conteúdo do arquivo |conteúdo de saudação toohello arquivo será gravado. |

1. Selecione **+ nova etapa** tooadd ação de saudação.  
   ![Imagem de ação 1 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Selecione Olá **adicionar uma ação** link. Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake. Neste exemplo, as ações do SharePoint são pontos de interesse.    
   ![Imagem de ação 2 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Digite *sharepoint* toosearch para tooSharePoint de ações relacionadas.
4. Selecione **SharePoint Online - criar o arquivo** como Olá tootake de ação.   **Observação**: você será solicitado tooauthorize tooaccess de aplicativo sua lógica de conta do SharePoint se você não tiver criado um tooSharePoint conexão Online anteriormente.    
   ![Imagem de ação 3 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Olá **criar arquivo** controlar é aberta.   
   ![Imagem de ação 4 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Selecione **URL do Site** e procurar toofind Olá site onde deseja que o arquivo de saudação do toocreate.     
   ![Imagem de ação 5 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Selecione **caminho da pasta** e procurar toofind Olá pasta onde o novo arquivo de saudação será colocado.  
   ![Imagem de ação 6 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Selecione Olá **nome de arquivo** controlar e insira o nome de saudação do arquivo hello deseja toocreate. Aqui, você pode inserir o nome de arquivo hello diretamente ou você pode usar qualquer uma das propriedades de saudação do gatilho Olá criado anteriormente. Isso é feito selecionando as propriedades da lista de saudação do **saídas de criação de um novo item**. Esta lista é somente exibição depois de selecionar Olá **nome de arquivo** controle. Nesta explicação passo a passo, selecionei ID (ID de saudação do novo item de lista Olá) como nome de saudação do arquivo hello está sendo criado pelo Olá **SharePoint Online - criar o arquivo** ação.    
   ![Imagem de ação 7 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Selecione Olá **o conteúdo do arquivo** controlar e insira conteúdo de saudação que será gravado toohello arquivo que será criado. Para o conteúdo do arquivo hello, observe que você pode usar qualquer uma das propriedades de saudação do gatilho Olá criado anteriormente. Simplesmente selecione Propriedades Olá Olá lista apresentada. Como alternativa, você pode inserir Olá **o conteúdo do arquivo** texto diretamente no controle de saudação. Neste exemplo, selecionei algumas propriedades e adicionei espaços e um hífen entre cada propriedade.        
   ![Imagem de ação 8 do SharePoint Online](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Salvar fluxo de trabalho do hello alterações tooyour  
11. Parabéns, você agora tem um aplicativo totalmente funcional lógica que é disparado quando um novo item é adicionado a lista do SharePoint Online tooa. aplicativo Hello, em seguida, criará um arquivo, usando algumas das propriedades de saudação do novo item de lista hello.  Agora você pode testá-lo criando um novo item na lista do SharePoint hello. 

