No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada parâmetros que contém todos os valores de parâmetro hello.
Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores sempre ficará Olá mesmo. Cada valor de parâmetro é usado em Olá Olá de toodefine modelo implantar recursos. 

Ao definir parâmetros, use Olá **allowedValues** toospecify campo quais valores um usuário pode fornecer durante a implantação. Saudação de uso **defaultValue** tooassign campo um parâmetro de toohello valor, se nenhum valor for fornecido durante a implantação.

Descreveremos cada parâmetro no modelo de saudação.

### <a name="logicappname"></a>logicAppName
nome de saudação do hello lógica aplicativo toocreate.

    "logicAppName": {
        "type": "string"
    }