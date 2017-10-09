trabalho de saudação produz um arquivo de saída JSON que contém metadados sobre as faces detectados e controladas. Olá metadados incluem coordenadas que indica o local de saudação de faces, bem como um face ID número indicando Olá controle dessa pessoa. Números de identificação de face são propensas a tooreset em circunstâncias quando face frontal Olá for perdido ou sobreposta no quadro hello, resultando em algumas pessoas ser atribuídas a várias IDs.

saudação de saída que JSON inclui Olá seguintes atributos:

| Elemento | Descrição |
| --- | --- |
| version |Isso se refere a versão toohello de saudação API de vídeo. |
| índice | (Aplica-se apenas tooAzure Redactor de mídia) define o índice do quadro de saudação do evento atual hello. |
| escala de tempo |"Tiques" por segundo de vídeo hello. |
| deslocamento |Este é o deslocamento de horário de saudação de carimbos de hora. Na versão 1.0 das APIs de Vídeo, sempre será 0. Em cenários futuro para os quais oferecemos suporte, esse valor poderá ser alterado. |
| taxa de quadros |Quadros por segundo do hello vídeo. |
| fragmentos |Olá metadados está em bloco para cima em diferentes segmentos de chamadas de fragmentos. Cada fragmento contém um início, uma duração, um número de intervalo e evento(s). |
| iniciar |Olá hora de início do primeiro evento Olá 'ticks'. |
| duration |comprimento de saudação do fragmento hello, em "tiques". |
| intervalo |intervalo de saudação de cada entrada de evento de fragmento hello, em "tiques". |
| events |Cada evento contém as faces Olá detectada e rastreada dentro dessa duração de tempo. É uma matriz de matriz de eventos. matriz externa Olá representa um intervalo de tempo. matriz interna Olá consiste em 0 ou mais eventos que ocorreram nesse momento. Um colchete vazio [] significa que nenhuma face foi detectada. |
| ID |ID de saudação de face de saudação que está sendo rastreado. Esse número pode mudar inadvertidamente se uma face se tornar indetectável. Um indivíduo fornecido deve ter Olá mesmo ID durante saudação geral, mas isso não pode ser garantido devido toolimitations no algoritmo de detecção de saudação (oclusão, etc.) |
| x, y |Olá superior esquerda X e Y do rosto Olá caixa delimitadora em uma escala normalizada do too1.0 0.0. <br/>-X e Y coordenadas são toolandscape relativo sempre, para que se você tiver um retrato vídeo (ou de cabeça para baixo, no caso de saudação do iOS), você terá tootranspose Olá coordenadas adequadamente. |
| largura, altura |largura de Hello e a altura da caixa delimitadora em uma escala normalizada do too1.0 0.0 de face de saudação. |
| facesDetected |Isso é encontrado no final de saudação do resultados JSON de saudação e resume o número de saudação de faces algoritmo Olá detectado durante a saudação vídeo. Porque Olá IDs pode ser redefinido inadvertidamente se uma face se torna não detectada (por exemplo, face fica fora da tela, parece ausente), esse número não pode sempre igual a saudação true inúmeros faces vídeo hello. |

