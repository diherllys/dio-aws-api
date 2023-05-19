# dio-aws-api
Passos realizados no projeto
  1-Barra de pesquisa "Search" -> API GateWay
    1.1 CreateAPI - > REST API "SEM VPC" ->
      Choose the protocol: REST
      Create new API: New API
        API Name = dio_live_api_new
        Description = 
        Endpoint Type = Regional
     1.2 Ir no botão Actions "Create Resources"
          Resource Name = Items
          Apertar no botão "Create Resources"
     
 2-Barra de pesquisa "Search" -> DynamoDB
  2.1 Ir no botão "Create table"
    Table name = DIOItems
    Partition key = id [String]
    Deixar o resto como padrão e clicar em -> "Create Table"
    
    
 3-Barra de pesquisa "Search" -> Lambda
  3.1 Ir no botão amarelo "Create function"
    Function name = dio_put_items_function
    Resto põe padrão e clica em "Create function"
  
  3.2 Editado o arquivo index.js (O mesmo esta no repositorio)
 
  3.3 Configuration -> Permissions -> Clicar em "dio_put_items_function-role-sdq15tez"
  
  4- Agora vamos para tela do IAM "Identity and Acess Managament"
    4.1 Vá no botão "Add permissions" -> "Create inline policy"
    4.2 Service = Clique em "Choose a service" -> pesquise e selecione "DynamoDB"
    4.3 Click em "add actions" -> Digite "putItem" e clique em "ADD"
    4.4 Vá em resources  -> ADD ARN
    4.5 vá no DynamoDB e pegue o ARN da tabela e digite na tela anterior em "Tables" -> "DIOItems" -> Overview -> Additional info -> e copie o Amazon Resources Name (ARN)
    4.6 
    
  5-Barra de pesquisa "Search" -> API GateWay
    5.1 Vá em Resources -> botão "Actions"  -> Create Method "POST" e click no botão de confirmar a direita
    5.2 Click em POST
      Marque   "Lambda Function"
      Marque "Use Lambda Proxy integration"
      Lambda Region = is-east-1
      Lambda Function = dio_put_items_function
      Use Default Timeout = Marcado
      Clique em "save"
    5.3 Vá no botão "Action" e clique em "Deploy API"
      Deployment stage
      Stage name = developer
      Stage description = 
      Deployment description = 
      Clique no botão "Deploy"
    5.4 Clique em POST e copie a URL
   
   6-Baixe o POSTMAN e crie uma conta
    6.1 Instale POSTMAN
    6.2 Vá em New - Collection
    6.3 Digite o nome da collection
    6.4 Na collection aperte no botão ...
    6.5 Clique em "Add request"
    6.6 Aonde tem a "GET" mude para "POST"
    6.7 Cole a URL do passo 5.4 no Campo a frente do "POST"
    6.8 Vá em "Body" selecione "raw" e a direita mude de "TEXT" para "JSON"
    6.9 Digite no arquivo a informação abaixo
      {
        "id": "004",
        "price": 600
      }
    6.10 Clique em "SEND"
    	Se tudo funcionou apresentará a mensagem "Item inserido com sucesso"
    6.11 Verifique no DynamoDB se o dado foi inserido
    7-
    
    	
    
    	
   
    
      
      
		
    
   
    
    
    
 


  
