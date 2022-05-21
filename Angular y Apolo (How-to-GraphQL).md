## [Introducción](https://www.howtographql.com/angular-apollo/0-introduction/)

alternativamente https://hasura.io/learn/graphql/angular-apollo/introduction/

### Visión de Conjunto
Ejemplo similar a [Hackernews](https://news.ycombinator.com/).

#### Tecnologías
##### Interfaz
- Angular.
- [Cliente Apolo](https://github.com/apollographql/apollo-client). Es un cliente GraphQL de almacenamiento en caché listo para producción.

##### Back-end
- [GraphCool](https://www.graph.cool/): plataforma de backénd. Combina graphQL + Serverless.

### ¿Porqué un cliente GraphQL?
Para enviar consultas y mutaciones (updates) sin preocuparse de los detalles de red.
#### Clientes GraphQL relevantes
-  [Apollo Client](https://github.com/apollographql/apollo-client).
- [Relay](https://facebook.github.io/relay/)

#### Apolo vs Relay
##### Relay
-  Desarrollado por Facebook
-  Alto rendimiento.
-  Curva de aprendizaje notable.
##### Apollo Client
- Desarrollado por la comunidad.
- Fácil de entender.
- Flexible y potente.
- Cliente con enlaces para React, Angular, Ember o Vue.

## Empezando
### Back-end
[Graphcool](https://www.graph.cool/) proporciona una API GraphQL lista para usar.

#### El modelo de datos
Está escrito en el lenguaje de definición de esquemas GraphQL ([SDL](http://graphql.org/learn/schema/))
```SDL
type User @model {
  id: ID! @isUnique     # required system field (read-only)
  createdAt: DateTime!  # optional system field (read-only)
  updatedAt: DateTime!  # optional system field (read-only)

  email: String! @isUnique # for authentication
  password: String!        # for authentication

  name: String!
  links: [Link!]! @relation(name: "UsersLinks")
  votes: [Vote!]! @relation(name: "UsersVotes")
}

type Link @model {
  id: ID! @isUnique     # required system field (read-only)
  createdAt: DateTime!  # optional system field (read-only)
  updatedAt: DateTime!  # optional system field (read-only)

  description: String!
  url: String!
  postedBy: User! @relation(name: "UsersLinks")
  votes: [Vote!]! @relation(name: "VotesOnLink")
}

type Vote @model {
  id: ID! @isUnique     # required system field (read-only)
  createdAt: DateTime!  # optional system field (read-only)

  user: User! @relation(name: "UsersVotes")
  link: Link! @relation(name: "VotesOnLink")
}
```

Algunas cosas a tener en cuenta: 
- Cada tipo anotado con `@model` *se asignará* a la base de datos y las operaciones CRUD asociadas se agregarán a la API GraphQL del servicio Graphcool.
- `@isUnique` indica que el campo no puede tenr valores duplicados. Dado que este campo es de solo lectura #PENDIENTE , Graphcool gestionará esta restricción.
- `createAt` y `updateAt` son campos especiales administrados por Graphcool.

#### Creación del servidor GraphQL
Empezaremos usando el tipo `Link`

-  Instalamos Graphcool CLI
```shell
   npm install -g graphcool-framework
```

 Creamos el servidor:
	 1. Creación de la estructura de datos local con `graphcool-framework init`.
	 2. Configurar el modelo de datos con `graphcool-framework deploy`

*  Crear la estructura de archivos local necesaria.
```shell
   graphcool-framework init server
```

Esto creará un nuevo directorio llamado `server`:
- `graphcool.yml`: archivo de [configuración raiz](https://www.graph.cool/docs/reference/service-definition/graphcool.yml-foatho8aip). Indica a Graphcool donde encontrar el modelo de datos, especifica las [reglas de permisos](https://www.graph.cool/docs/reference/auth/authorization/overview-iegoo0heez) y proporciona información sobre [funciones serverless](https://www.graph.cool/docs/reference/functions/overview-aiw4aimie9).
- `types.graphql`:  especifica el modelo de datos para la aplicación. Escrito en GraphQL DSL.
- `package.json`:  enumera las dependencias *serverless* **del servidor GraphQL**.
- `src`:  almacena el código de las funciones *serverless* integradas en el servidor GraphCool. 

Se empieza editando `types.graphql` para introducir la definición de `Link`.
```graphql
	type Link @model {
	  id: ID! @isUnique     # required system field (read-only)
	  createdAt: DateTime!  # optional system field (read-only)
	  updatedAt: DateTime!  # optional system field (read-only)
	
	  description: String!
	  url: String!
	}
```
En el terminal , navegamos a `server` y ejecutamos:
```shell
   graphcool-framework deploy
```
Este comando solicitará una serie de mensajes de confirmación.
Tan solo tener en cuenta la opción **Shared Clusters** y seleccionar `shared-eu-west`, dejando el resto con su opción por defecto.

#### Rellenar la base de datos y GraphQL Playgrounds
[GraphQL Playground](https://github.com/graphcool/graphql-playground) es un entorno interactivo que permite enviar consultas y mutaciones. Útil para explorar las capacidades de un API de GraphQL.

Proporciona un editor de consultas y mutaciones. Copie el siguiente código: 
```graphQL
	mutation CreateGraphcoolLink {
	  createLink(
	    description: "The coolest GraphQL backend 😎",
	    url: "https://graph.cool") {
	    id
	  }
	}
	
	mutation CreateApolloLink {
	  createLink(
	    description: "The best GraphQL client",
	    url: "http://dev.apollodata.com/") {
	    id
	  }
	}
```
Esto creará dos registros `Link` en la base de datos. Para comprobarlo usar la consulta:
```graphQL
{
	allLinks{
		id
		description
		url
	}
}
```

### Interfaz
#### Crear la aplicación
Se utiliza `angular-cli`.
```shell
   ng new hackernews-angular-apollo
   cd hackernews-angular-apollo
   npm install
   npm start
   ```

