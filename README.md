# json-server-auth-base
https://docs.google.com/document/d/1_irACkP26cZB7vjjfJQs474knUa8bp8TaMcUWjgZBfs/edit
Documentação: https://www.npmjs.com/package/json-server-auth

****************************************************************************************************************************************************************

Json Server é uma forma de criar API fakes para prototipação, para testar ideias, mas tome cuidado, não utilizamos json-server para produtos em produção, apenas com a finalidade de testar conceitos.

Com o json-server-auth  podemos utilizar o sistema de cadastro de usuário para que o mesmo possa logar e obter um token para ter acessos a determinados end-points/urls da nossa aplicação.


****************************************************************************************************************************************************************

## Como utilizar
Para utilizar basta clonar o projeto num deretório de sua preferência. Depois abra o terminal no diretorio raiz do projeto e digite **yarn install** para instalar as dependências do projeto.

Para rodar o servidor json basta digitar:
**yarn json-server db.json -m ./node_modules/json-server-auth -r routes.json --port=3001**	O servidor ficar rodando na porta 3001.

****************************************************************************************************************************************************************

### Ajuda
Fale comigo:
Email: **alexmiguel95@gmail.com**
Linkedin: **www.linkedin.com/in/alexmiguel95**

****************************************************************************************************************************************************************

**Registrando usuário**
O json-server-auth utiliza 2 rotas padrão para lidar com o cadastro e autenticação do usuário:
POST URL → http://localhost:3001/register

BODY
{
  "email": "luigi@mail.com",
  "password": "123456",
  "name": "Luigi",
  "age": 38
}
Depois de enviar o post, o usuário será adicionado ao arquivo **db.json**.

**Logando com usuário - Obtendo token**
POST URL → http://localhost:3001/login

BODY
{
  "email": "luigi@mail.com",
  "password": "123456"
}

**Cadastrando um produto**
Cada produto cadastrado deve estar associado a um dono, via ID do usuário que está cadastrando.
POST URL → http://localhost:3001/products

BODY
{
  "name": "PS4",
  "userId": 3,
  "price": 500,
  "category":"A"
}

**Deletar produto**
Temos que passar o ID do produto a ser deletado. No Header temos que passar a chave Authorization com um token do usuário que criou aquele produto.
DELETE URL → http://localhost:3001/products/14

**Altera um produto fazendo um PUT**
Para que eu possa editar/deletar um objeto, eu preciso estar logado com o usuário owner do produto, que nesse caso tem ID 3. Isso acontece por conta do tipo de guarda de rota que colocamos em /products. Verifique o arquivo rotas.
PUT URL → http://localhost:3001/products/3
{
		"price": 700,
		"userId": 2
}
Perceba que mudamos o objeto por inteiro. Caso queira alterar somente um das chaves do objeto faça um PATCH:
Quando passamos um atributo que já existe no Body, ele apenas irá fazer sua alteração
PATCH URL → http://localhost:3001/products/6
Body
{
 "weight": 100
}

**Listar todos os produtos**
GET URL → http://localhost:3001/products

**Listar um produto especifico**
Obs: em todas esses requisições precisamos passar o token Authorization no Header.
Lista de acordo um atributo do objeto:
Só vai trazer os produtos cujo a chave category seja igual a D
GET URL → http://localhost:3001/products?category=D
Só vai trazer os produtos cujo a chave userId seja igual a 2
GET URL → http://localhost:3001/products?userId=2
Com o operador _like só vai trazer os dados cujo a chave name conhena impressora. Ele converter maiúsculas em minúsculas.
GET URL→ http://localhost:3001/products?name_like=impressora

Operador _lte. Com ele podemos listar os dados cujo o campo price seja menor que 1000, por exemplo.
GET URL → http://localhost:3001/products?price_lte=1000

Operador _gte. Com ele podemos listar os dados cujo o campo price seja maior que 1000, por exemplo.
GET URL → http://localhost:3001/products?price_gte=1000

Ordenar a lista com os operadores _sort e  _order
Perceba que utilizamos duas propriedades, a primeira é _sort e passamos qual o atributo do nosso objeto ele deve ter como base e depois o _order que pode receber **asc** para valores ascendentes e **desc** para descendente:
GET URL → http://localhost:3001/products?_sort=price&_order=asc

Podemos combinar os operadores, exemplo:
GET URL→ http://localhost:3001/products?_sort=price&_order=asc&_page=1&_limit=5


****************************************************************************************************************************************************************




Documentation: https://www.npmjs.com/package/json-server-auth

**************************************************** **************************************************** ****************************************************

Json Server is a way to create API fakes for prototyping, to test ideas, but be careful, we don't use json-server for products in production, just for the purpose of testing concepts.

With json-server-auth we can use the user registration system so that it can log in and obtain a token to access certain end-points / urls of our application.


******************************************************************************************************** ****************************************************

## How to use
To use it, just clone the project in a directory of your choice. Then open the terminal in the project's root directory and type ** yarn install ** to install the project dependencies.

To run the json server just type:
** yarn json-server db.json -m ./node_modules/json-server-auth -r routes.json --port = 3001 ** The server will be running on port 3001.

************************************************************************************************************************************************************ 

### Help
Talk to me:
Email: **alexmiguel95@gmail.com**
Linkedin: **www.linkedin.com /in/alexmiguel95**

***************************************************************************************************************************************************************

**Registering user**
Json-server-auth uses 2 standard routes to handle user registration and authentication:
POST URL → http: // localhost: 3001 / register

BODY
{
  "email": "luigi@mail.com",
  "password": "123456",
  "name": "Luigi",
  "age": 38
}
After sending the post, the user will be added to the file ** db.json **.

** Logging in with user - Getting token **
POST URL → http: // localhost: 3001 / login

BODY
{
  "email": "luigi@mail.com",
  "password": "123456"
}

**Registering a product**
Each registered product must be associated with an owner, via the user ID that is registering.
POST URL → http: // localhost: 3001 / products

BODY
{
  "name": "PS4",
  "userId": 3,
  "price": 500,
  "category": "A"
}

**Delete product**
We have to pass the product ID to be deleted. In the Header we have to pass the Authorization key with a token of the user who created that product.
DELETE URL → http: // localhost: 3001 / products / 14

** Change a product by making a PUT **
In order for me to edit / delete an object, I need to be logged in with the user owner of the product, which in this case has ID 3. This happens because of the type of route guard we put in / products. Check the routes file.
PUT URL → http: // localhost: 3001 / products / 3
{
"price": 700,
"userId": 2
}
Notice that we have changed the object entirely. If you want to change only one of the object's keys, do a PATCH:
When we pass an attribute that already exists in the Body, it will only make its change
PATCH URL → http: // localhost: 3001 / products / 6
Body
{
 "weight": 100
}

**List all products**
GET URL → http: // localhost: 3001 / products

**List a specific product**
Note: in all these requests we need to pass the Authorization token in the Header.
List according to an object attribute:
It will only bring products whose category key is equal to D
GET URL → http: // localhost: 3001 / products? Category = D
It will only bring products whose userId key is equal to 2
GET URL → http: // localhost: 3001 / products? UserId = 2
With the _like operator you will only bring the data whose name key knows the printer. It convert uppercase to lowercase.
GET URL → http: // localhost: 3001 / products? Name_like = printer

_Lte operator. With it we can list the data whose price field is less than 1000, for example.
GET URL → http: // localhost: 3001 / products? Price_lte = 1000

_Gte operator. With it we can list the data whose price field is greater than 1000, for example.
GET URL → http: // localhost: 3001 / products? Price_gte = 1000

Sort the list with the _sort and _order operators
Note that we use two properties, the first is _sort and we pass which attribute of our object it should be based on and then the _order that can receive **asc** for ascending values and **desc** for descending:
GET URL → http: // localhost: 3001 / products? _Sort = price & _order = asc

We can combine operators, example:
GET URL→ http://localhost:3001/products?_sort=price&_order=asc&_page=1&_limit=5
