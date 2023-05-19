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
      </br>
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
    7-Barra de pesquisa "Search" ->  Amazon Cognito
    	7.1 Clique em User pools
	7.2 Clique no botão "Create user pool"
	7.3 Cognito user pool sign-in options -> Marque a opção de "Email" para login do usuário
    	7.4 Em "Password policy mode" - > Marque Custom
	7.5 Maque as opções abaixo
		Contains at least 1 number
		Contains at least 1 special character
		Contains at least 1 uppercase letter
		Contains at least 1 lowercase letter
    		MFA enforcement = "No MFA"
		User account recovery = "Enable self-service account recovery - Recommended" -> "Email only"
		Self-service sign-up -> Self-registration (MARQUE)
    		Cognito-assisted verification and confirmation
			(MARQUE) Allow Cognito to automatically send messages to verify and confirm - Recommended 
    			(MARQUE) Send email message, verify email address
   		Verifying attribute changes
			(MARQUE) Keep original attribute value active when an update is pending - Recommended
    		Required attributes
			Additional required attributes (Não precisa por nada)
		Email provider	
			Marque "Send email with Cognito"
		Clique no Botão "Next"
		Clique no Botão "Next"
      		User pool name = DIOLiveUserPool
		Initial app client
			Marque a opção em App type
				Public client
			App client name = DIOLiveAppClient
			Tags = não precisam ser adicionadas
		Clique em "Next"
		Revise e crie a pool
	7.6 Vá em "App client" -> Selecione DIOLiveAppClient
		Edit Hosted UI
			digite na URL  = https://example.com
		Identity providers
			Cognito user pool
		OAuth 2.0 grant types
			Authorization code grant
			Implicit grant
      		OpenID Connect scope
			Email, OpenID
		Clique no botão "Save changes"
	7.7 Volte em "Amazon Cognito -> User pools -> DIOLiveUserPool
		Procure a opção "DomainInfo"
		Em "Domain" -> Clique no botão "Actions" -> Create custom domain
    			Custom Domain = [https://diolivenew2023](https://diolivenew2023.auth.us-east-1.amazoncognito.com)
   	8 Vá no postman crie uma nova requsição como "GET"
		8.1 Vá em Authorization
			Type: OAuth 2.0
			Add authorization = Request
				Token =  token
				user Token type = Acess token
				Header Prefix = Bearer
				Auto-refresh token = 
				Share token = 
				Configure New Token
					Token name = Token
					Grant Type = Implicit
					Callback URL = https://example.com/
					Authorize using browser = 
					Auth URL = https://diolivenew2023.auth.us-east-1.amazoncognito.com/login
					Client ID = seu ID de cliente do "App client id"
					Scope = Email OpenID
					State = State
					Client Authentication = Send client credentials in body
		8.2 Faça o processo de cadastro	e login		
		8.3 Vai gerar o token. Copie e guarde o TOKEN
	9 Vá em AMAZON API Gateway
		9.1 Selecione dio_live_api_new
			Vá em Authorizers -> Create New Authorizer
				Name = DIOCognitoAuthorizer
				Cognito User Pool = DIOLiveUserPool
				Token Source = Authorization
				Token Validation =
				Clique em "Create"
		9.2 Selecione "Resources" e atualize a pagina 
		9.3  Clique em "POST" -> "Method Request"	
			Authorization = DIOCognitoAuthorizer
			OAuth Scopes = NONE
			Request Validator = NONE
			API Key Required = false
			Confirme
		9.4 Faça o "deploy da API" para salvar
    	10 Vá no postman
		10.1 no metodo POST vá em Authorization -> Marque Bearer -> Ponha o Token que você salvou -> e Clique em "Send"
		10.2 Verifique se o item foi adicionado e se esta tudo OK
	
    
    
 


  
