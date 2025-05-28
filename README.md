# Proyecto Shopping

Gestión básica de un ecommerce con microservicios. Sirve para gestionar un carrito de la compra.
Hacemos uso de 5 microservicios. Discovery, gateway, user-service, product-service y shopping-service.
El microservicio user-service contiene la entidad usuario. El microservicio product-service contiene
la entidad product. El microservicio shopping-service contiene la entidad cart y cartItem y se encarga
además de comunicarse con los otros microservicios mediante Feign client.
En este proyecto podemos gestionar mediante llamadas a la api las siguientes acciones:
- Gestionar usuarios.
- Gestionar productos.
- Añadir al carrito de compra.
- Eliminar del carrito de compra.
- Limpiar el carrito de compra.
- Actualizar el stock cuando hacemos una venta.

## Trello:
[Tareas de trello](https://trello.com/b/rr8rQcxq/proyectofinal)

## Presentación:

[Presentación](https://docs.google.com/presentation/d/e/2PACX-1vRytWtDc_eOHEHP8A5JWRW1l6Opb4TlfogapQDTar0orZ_5Vxs9QyrjMrB9enxpnHqIMbQSyS5Tsblg/pub?start=false&loop=false&delayms=3000)

## UML:
![](/images/proyecto_final_uml_basico.png)


## Microservicios necesarios en este proyecto:

[discovery](https://github.com/AsterixKo/discovery)

[gateway](https://github.com/AsterixKo/gateway)

[user-service](https://github.com/AsterixKo/user-service)

[product-service](https://github.com/AsterixKo/product-service)

[shopping-service](https://github.com/AsterixKo/shopping-service)

![](/images/dibujo-estructura-microservicios.png)

## Setup for local development:

Primero listemos las dependencias necesarias según los tipos de microservicios.

Discovery:

- Eureka Server
- Lombok

Gateway:

- Eureka Discovery Client
- Reactive Gateway
- Lombok

Microservicios con base de datos:

- Mysql Driver
- Spring Web
- Lombok
- Eureka Discovery Client
- Spring Data JPA
- OpenFeign
- Validation

Los esquemas de bases de datos a crear son los siguientes:

- project_final_product
- project_final_shopping
- project_final_user

Los puertos de cada microservicio (para usar postman podemos usar el puerto 8087, pero recordar levantar todos
los microservicios):

- discovery: 8761
- gateway: 8087
- user-service: 8080
- product-service: 8081
- shopping-service: 8082

### Tecnologías usadas:

Java, Spring, Eureka Server, Lombok, Eureka Discovery Client, 
Reactive Gateway, Lombok, Mysql Driver, Spring Web, Lombok,
Eureka Discovery Client, Spring Data JPA, OpenFeign, Validation.

### Rutas:

user-service -> UserController:

- getAllUsers: GetMapping "/api/user/users"
- getUserById: GetMapping "/api/user/{id}"
- register: PostMapping "/api/user/register" (@RequestBody RegisterDTO registerDTO)

product-service -> ProductController:

- findAllProducts: GetMapping "/api/product/"
- updateStockProduct: PutMapping "/api/product/update/stock/{idProduct}" (@PathVariable("idProduct") Long idProduct, @RequestBody SaleDTO saleDTO)
- saveProduct: PostMapping "/api/product/save" (@RequestBody Product product)
- saveListProduct: PostMapping "/api/product/save/list" (@RequestBody List<Product> products)
- findProductById: GetMapping "/api/product/{idProduct}" (@PathVariable("idProduct") Long idProduct)
- deleteProduct: DeleteMapping "/{idProduct}" (@PathVariable("idProduct") Long idProduct)

shopping-service -> ShoppingController:
- addToCart: PostMapping "/api/shopping/add-to-cart" (@RequestBody RequestAddToCartDTO requestAddToCartDTO)
- removeFromCart: DeleteMapping "/api/shopping/remove-from-cart" (@RequestBody RequestRemoveFromCartDTO requestRemoveFromCartDTO)
- cleanCart: GetMapping "/api/shopping/clear-cart/{idUser}" (@PathVariable Long idUser)

### Trabajo futuro:

Me gustaría implementar más clases como Order y OrderItem y implementar otros microservicios.