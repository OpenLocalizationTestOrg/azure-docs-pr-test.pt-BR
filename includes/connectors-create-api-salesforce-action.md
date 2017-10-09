Agora que você adicionou uma condição, seu toodo tempo algo interessante com dados de saudação que são gerados pelo gatilho Olá. Siga essas Olá de tooadd etapas **Salesforce - objeto Get** ação. Essa ação obterá dados saudação sempre que é criado um novo cliente potencial. Você também adicionará uma segunda ação que usará dados Olá Olá Salesforce - Get toosend de ação um objeto um email usando o conector Olá Office 365.  

tooconfigure Olá esta ação, você precisará Olá tooprovide informações a seguir. Você notará que é fácil toouse dados gerados pelo gatilho hello como entrada para algumas das propriedades de saudação para o novo arquivo de saudação:

| Criar propriedade do arquivo | Descrição |
| --- | --- |
| Tipo de objeto |Esse é o tipo de saudação do objeto da equipe de vendas que lhe interessam. Alguns exemplos são Cliente Potencial, Conta, etc. |
| ID de objeto |Isso representa um identificador de objeto de saudação. |

1. Selecione o link **Adicionar uma ação** . Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake. Neste exemplo, as ações do Salesforce são pontos de interesse.      
   ![Imagem de ação do Salesforce 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Digite *salesforce* toosearch para toosalesforce de ações relacionadas.
3. Selecione **Salesforce - objeto Get** como Olá tootake de ação.   **Observação**: você será solicitado tooauthorize tooaccess de aplicativo sua lógica sua equipe de vendas de conta, se você não tiver feito isso anteriormente.    
   ![Imagem de ação do Salesforce 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Olá **objeto Get** controlar é aberta.  
5. Selecione *levar* como tipo de objeto hello.
6. Selecione Olá **ID de objeto** controle.
7. Selecione **...**  tooexpand lista de saudação de tokens que podem ser usados como entrada para ações.       
   ![Imagem de ação do Salesforce 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Selecione o controle **ID de Cliente Potencial** para abri-lo.   
   ![Imagem de ação do Salesforce 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Observe que esse token de ID de cliente potencial hello está agora no hello controle de ID de objeto, indicando que Olá Get objeto ação irá procurar por um cliente potencial com uma ID que é igual toohello lead ID de cliente potencial que disparou este aplicativo lógico.  
   ![Imagem de ação do Salesforce 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Salve seu trabalho. Isso é tudo, você adicionou Olá Get objeto ação tooyour lógica aplicativo. O controle Obter objeto deve ser semelhante isso:     
    ![Imagem de ação do Salesforce 6](./media/connectors-create-api-salesforce/action-6.png)  

Agora que você adicionou uma ação tooget um cliente potencial, talvez você queira toodo algo interessante com lead Olá recém-criado. Em uma empresa, convém toosend toonotify um email que foi criado um novo cliente potencial de uma lista de distribuição. Vamos usar Olá Office 365 conector toosend um email com algumas informações relevantes de saudação do novo objeto de cliente potencial Olá no Salesforce.  

1. Selecione **adicionar uma ação** , em seguida, digite *email* no controle de pesquisa de saudação. Isso filtra Olá ações toothose toosending relacionado e receber email.  
2. Selecione Olá **Outlook do Office 365 - enviar um email** item de lista. Se você ainda não tiver criado um *conexão* tooyour conta do Office 365, você vai ser solicitado tooenter seu toocreate de credenciais do Office 365 it agora. Ao terminar, Olá **enviar um email** controlar é aberta.        
   ![Imagem de ação do Salesforce 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Inserir endereço de email de saudação que queira saudação do toosend email tooin **para** controle.
4. Em Olá **assunto** de controle, digite *novo cliente potencial criado* - selecione Olá *empresa* token. Isso exibirá Olá *empresa* campo de saudação novo cliente potencial criado na equipe de vendas.  
5. Em Olá **corpo** controle, você pode selecionar qualquer um dos tokens de saudação do novo objeto de cliente potencial hello e você também pode digitar qualquer texto que você gostaria que toodisplay no corpo de saudação do hello email. Aqui está um exemplo:  
   ![Imagem de ação do Salesforce 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Salve seu fluxo de trabalho.  

É isso. Seu aplicativo lógico está pronto.  

Agora, você pode testar seu aplicativo lógico: no Salesforce, crie um novo cliente potencial que atende a condição de saudação que você criou.  Se você seguiu totalmente esse passo a passo, basta criar um cliente potencial com um endereço de email contendo *amazon.com* . Depois de alguns segundos o lógica de aplicativo deve ser disparado e resultados de saudação podem parecer semelhante toothis:  
![Imagem de ação do Salesforce 9](./media/connectors-create-api-salesforce/action-9.png)  

