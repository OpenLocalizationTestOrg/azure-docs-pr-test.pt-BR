### <a name="prerequisites"></a>Pré-requisitos
* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Um [conta de armazenamento de Blob do Azure](../articles/storage/common/storage-create-storage-account.md) incluindo o nome de conta de armazenamento hello e sua chave de acesso. Essa informação é listada nas propriedades de saudação da conta de armazenamento Olá Olá portal do Azure. Saiba mais sobre o [Armazenamento do Azure](../articles/storage/common/storage-introduction.md).

Antes de usar sua conta de armazenamento de BLOBs do Azure em um aplicativo lógico, conecte-se tooyour conta de armazenamento de BLOBs do Azure. Você pode fazer isso facilmente dentro de seu aplicativo lógica em Olá portal do Azure.  

Conecte-se a conta de armazenamento de BLOBs do Azure tooyour usando Olá etapas a seguir:  

1. Crie um aplicativo lógico. No designer de aplicativos lógicos hello, adicionar um gatilho e, em seguida, adicione uma ação. Selecione **APIs gerenciadas do Microsoft Mostrar** em Olá lista suspensa e, em seguida, digite "blob" na caixa de pesquisa de saudação. Selecione uma das ações de saudação:  
   
    ![Etapa de criação da conexão com o Armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Se você ainda não criou todas as conexões tooAzure armazenamento, você será solicitado para obter detalhes de conexão de saudação:   
   
    ![Etapa de criação da conexão com o Armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Insira os detalhes da conta de armazenamento hello. As propriedades com um asterisco são obrigatórias.
   
   | Propriedade | Detalhes |
   | --- | --- |
   | Nome da Conexão * |Digite um nome para a conexão. |
   | Nome da Conta de Armazenamento do Azure * |Insira o nome de conta de armazenamento hello. nome de conta de armazenamento Olá é exibido nas propriedades de armazenamento Olá Olá portal do Azure. |
   | Chave de Acesso da Conta de Armazenamento do Azure * |Insira a chave de conta de armazenamento hello. chaves de acesso de saudação são exibidas nas propriedades de armazenamento Olá Olá portal do Azure. |
   
    Essas credenciais são usada tooauthorize tooconnect de aplicativo sua lógica e acessam seus dados. 
4. Selecione **Criar**.
5. Aviso Olá conexão foi criado. Agora, continue com hello outra etapas em seu aplicativo lógico: 
   
    ![Etapa de criação da conexão com o Armazenamento de Blobs do Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

