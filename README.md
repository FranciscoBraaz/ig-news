
# Ignews

#### Aplicação JAMStack, desenvolvida com o objetivo de praticar conceitos dentro do ecossistema do nextJS. Consiste num serviço de assinatura, que possibilita aos assinantes o acesso aos artigos publicados.
<img src="https://i.imgur.com/aiaeL8A.png" alt="Home do site, com feed de fotos" width="80%"/>

## 🛠️ Tencologias utilizadas

 - NextAuth: para autenticação com provedores (Github);
 - FaunaDB: armazenamento dos dados do usuário e informações sobre a assinatura;
 - Stripe: Gerenciar assinaturas e pagamentos 
 - NextJS: SSG e SSR

### 💻 Previews:

#### - Preview 1:
<img src="/gifs/preview1.gif?raw=true" width="100%">

#### - Preview 2:
<img src="/gifs/preview2.gif?raw=true" width="100%">


## 👷  Executando o projeto

 ### Baixando repositório para sua máquina
    # Clone o repositório com:
    git clone https://github.com/FranciscoBraaz/ig-news
    
    # Navegue para a pasta raíz com:
    cd ignews

    
   ### Instalando dependências
   

    # Baixe as dependências com:
    yarn install

### Configurando aplicações de terceiros

#### Stripe

 - É necessário criar uma conta no stripe e criar um novo produto dentro
   da plataforma. Após a criação do novo produto, é preciso copiar as
   keys (privada e pública) vinculadas a esse produto.
   
 - Em seguida crie um arquivo "env.local" na pasta raiz do projeto e crie as seguintes variáveis com os valores das keys já obtidas (Ignore os asteriscos):
  ```
   STRIPE_API_KEY=*Sua key privada*
   NEXT_PUBLIC_STRIPE_PUBLIC_KEY = *Sua key pública*
   STRIPE_SUCCESS_URL = http://localhost:3000/posts
   STRIPE_CANCEL_URL = http://localhost:3000/
  ``` 

 
 - Posteriormente, baixe o stripe cli para sua máquina - [Stripe CLI](https://stripe.com/docs/stripe-cli) - e execute o arquivo baixado. Em seguida, abra o prompt de comando e execute o comando:
	 - `stripe login`
	 
 -  Após autorizar a aplicação, execute:
	 - `stripe listen --forward-to localhost:3000/api/webhooks`


 - Após isso, copie a chave disponibilizada na linha "Ready! Your webhook signing secret is..." e atribua seu valor para uma nova variável no arquivo 'env.local' criado anteriormente, desse modo:
	 - `STRIPE_WEBHOOK_SECRET = *Chave obtida*`

### Github

 - Crie uma aplicação OAuth no github e copie a chave e o id disponibilizados. Com isso em mãos, coloque no arquivo 'env.local' deste modo:
  ```
   GITHUB_CLIENT_ID = *Seu id*
   GITHUB_CLIENT_SECRET = *Sua chave*
  ```

### FaunaDB

 - É necessário ter uma conta no FaunaDB e criar um um novo banco. Esse banco deve possuir:
	 - Collections: 
		 - subscriptions
		 - users
	- Indexs:
		- subscription_by_id
		- subscription_by_status
		- subscription_by_user_ref
		- user_by_email
		- user_by_stripe_customer_id
 - Obtenha a key desse banco criado e a coloque no arquivo 'env.local':
	 - `FAUNADB_KEY = *Sua key*`
	
	
 ### PrismicCMS
 
 - É preciso possuir uma conta no PrismicCMS e criar alguns artigos para popular a aplicação. Após a criação da conta e dos artigos, copie suas credencias e coloque-as no arquivo 'env.local'. 
  ```
   PRISMIC_ENDPOINT = Seu endpoint
   PRISMIC_ACCESS_TOKEN 
  ```

 
    

#### Scripts
Para executar o projeto:

    # Na pasta raíz do projeto, execute:
    yarn dev
