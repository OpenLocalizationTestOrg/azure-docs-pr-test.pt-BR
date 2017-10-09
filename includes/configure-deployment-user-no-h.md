Criar credenciais de implantação com hello [usuário az webapp implantação definido](/cli/azure/webapp/deployment/user#set) comando.

Um usuário de implantação é necessário para FTP e Git implantação tooa o aplicativo web local. Olá nome de usuário e senha são o nível de conta. _Eles são diferentes das credenciais da sua assinatura do Azure._

Olá a seguir de comando, substitua  *\<nome de usuário >* e  *\<senha >* com um novo nome de usuário e senha. nome de usuário Olá deve ser exclusivo. Hello senha deve ter pelo menos oito caracteres, com dois Olá após três elementos: letras, números, símbolos. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Se você receber um ` 'Conflict'. Details: 409` erro, o nome de usuário de saudação de alteração. Se receber um erro ` 'Bad Request'. Details: 400`, use uma senha mais forte.

Você só cria esse usuário de implantação uma vez; é possível usá-lo para todas as implantações do Azure.

> [!NOTE]
> Nome de usuário de saudação do registro e a senha. Você precisa-los toodeploy Olá web aplicativo mais tarde.
>
>