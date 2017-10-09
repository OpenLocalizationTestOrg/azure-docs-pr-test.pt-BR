No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada parâmetros que contém todos os valores de parâmetro hello.
Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores sempre ficará Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados. 

Ao definir parâmetros, use Olá **allowedValues** toospecify campo quais valores um usuário pode fornecer durante a implantação. Saudação de uso **defaultValue** tooassign campo um parâmetro de toohello valor, se nenhum valor for fornecido durante a implantação.

Descreveremos cada parâmetro no modelo de saudação.

### <a name="sitename"></a>siteName
nome de saudação do aplicativo web de saudação que você deseja toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
nome de saudação de saudação do serviço de aplicativo planejar toouse para hospedar o aplicativo web de saudação.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
Olá preço Olá plano de hospedagem.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

Olá modelo define os valores de saudação que são permitidos para esse parâmetro e atribui um valor padrão (S1) se nenhum valor for especificado.

### <a name="workersize"></a>workerSize
tamanho da instância de saudação da saudação (pequeno, médio ou grande) de plano de hospedagem.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

Olá modelo define os valores de saudação que são permitidos para este parâmetro (0, 1 ou 2) e atribui um valor padrão (0) se nenhum valor for especificado. os valores Hello correspondem toosmall, médio e grande.

