# Spring Data Jpa

Created: July 12, 2023 3:18 PM
Date: July 14, 2023 12:00 AM
Files & media: https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repository-query-keywords
Select: Spring-Data-Jpa

`#none , Create only , drop ,create-drop, validate, updatespring.jpa.hibernate.ddl-auto=update`

1. none → disable auto ddl tool.
2. create-only → hibernate have to generate create table based on entity
3. drop → drop table using jpa entity
4. create →drop existing and recreate db model
5. create-drop → drop existing and create new and at end of session again drop db
6. validate → just validate against entity in db
7. update → just update against entity

`spring.jpa.show-sql:true`

`sprig.jpa.properties.hibernate.format-sql=true`

shows sql in well format

### ** 1. Adding Unique Constraint

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled.png)

### ** 2. Adding Column Names

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%201.png)

### ** 3. Primary Key generation Strategy

JPA offers 4 different ways to generate primary key values:

1. *`GenerationType.AUTO*:` Hibernate selects the generation strategy based on the used dialect

1. *`GenerationType.IDENTITY*:` Hibernate relies on an auto-incremented database column to generate the primary key,
- not Good For JDBC Batch Operations

1. *`GenerationType.SEQUENCE*:` Hibernate requests the primary key value from a database sequence.
- most commonly used in large applications

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%202.png)

1. *`GenerationType.TABLE*:` Hibernate uses a database table to simulate a sequence.
- slow down application

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%203.png)

### ** 4. Adding Hibernate annotations - @CreationTimestamp and @UpdateTimestamp

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%204.png)

# ∝ Important Spring Data JPA Repository Methods

### ** Important Spring Data JPA Repository Methods

1. **Save() Test Case:**

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%205.png)

![Untitled](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/Untitled%206.png)

```java
package com.udemy.spring.data.jpa.repository;

import com.udemy.spring.data.jpa.entity.Products;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import java.math.BigDecimal;
import java.util.List;
import java.util.Optional;

@SpringBootTest
class ProductRepositoryTest {

    @Autowired
    private ProductRepository productRepository;

    @Test
    void saveMethod() {
        //create product
        Products products = new Products();
        products.setName("Apple");
        products.setDescription("Mobile");
        products.setPrice(new BigDecimal(100));
        products.setActive(true);
        products.setImageUrl("http://www.google.com");
        products.setSku("sku");
        //save Product
        Products savedProduct = productRepository.save(products);

        //display Produxt
        System.out.println(savedProduct.toString());

    }

    @Test
    void updateUsingSave() {
        long id = 1l;
        Products exsitingProduct =
                productRepository.findById(id).get();

        exsitingProduct.setName("Nokia");
        exsitingProduct.setSku("kjsadhajshdkasjhfkj");

        productRepository.save(exsitingProduct);

        System.out.println(exsitingProduct.toString());
    }

    @Test
    void findByIdMethod() {
        long id = 1l;
        Products exsitingProduct =
                productRepository.findById(id).get();
        System.out.println(exsitingProduct.toString());
    }

    @Test
    void saveAllMethod() {
        Products products = new Products();
        products.setName("Apple");
        products.setDescription("Mobile");
        products.setPrice(new BigDecimal(100));
        products.setActive(true);
        products.setImageUrl("http://www.google.com");
        products.setSku("sku1");
        Products products2 = new Products();
        products2.setName("fdsfsdf");
        products2.setDescription("Mobile");
        products2.setPrice(new BigDecimal(100));
        products2.setActive(true);
        products2.setImageUrl("http://www.google.com");
        products2.setSku("sku2");
        //save Product
        Products products3 = new Products();
        products3.setName("sdfsdf");
        products3.setDescription("Mobile");
        products3.setPrice(new BigDecimal(100));
        products3.setActive(true);
        products3.setImageUrl("http://www.google.com");
        products3.setSku("skus");
        //save Product

        productRepository.saveAll(List.of(products, products2, products3));

    }
    @Test
    void findAll(){
        List<Products> all = productRepository.findAll();
        all.forEach(System.out::println);
    }

    @Test
    void deleteMethod(){
        Optional<Products> byId = productRepository.findById(1l);
        Products products = byId.get();
        productRepository.delete(products);
    }

    @Test
    void deleteAll(){
        productRepository.deleteAll();
    }

    @Test
    void count(){
        long count = productRepository.count();
        System.out.println(count);
    }
    @Test
    void existByID(){
        boolean b = productRepository.existsById(1l);
        System.out.println(b);
    }
}
```

# ∝ Creating Custom Query Methods or Finder Methods:

### ** Rules to create query methods

1. The name of our query method must start with one of the following prefixes: find...By, read... By, query... By, count...By, and get...By.
Examples: `findByName()`, `readByName()`, `queryByName()`, `getByName()`
2. If we want to limit the number of returned query results, we can add the First or the Top keyword before the first By word.
Examples: `findFirstByName()`, `readFirst2ByName()`, `findTop10ByName()`
3. If we want to select unique results, we have to add the Distinct keyword before the first
By word.
Examples: `findDistinctByName()` or `findNameDistinctBy()`
4. Combine property expression with AND and OR.

Examples: `findByNameOrDeacription()`, 

`findByNameAndDeacription()`

### ** Returning Values From Query Methods

![IMG_7468.jpeg](Spring%20Data%20Jpa%20d3a596a3120b4b1abfecb09c241d800e/IMG_7468.jpeg)

### ** **Supported query method subject keywords**

| SR. NO | Keyword | Description |
| --- | --- | --- |
|     1 | find…By, read…By, get…By, query…By, search…By, stream…By | General query method returning typically the repository type, a Collection or Streamable subtype or a result wrapper such as Page, GeoResults or any other store-specific result wrapper. Can be used as findBy…, findMyDomainTypeBy… or in combination with additional keywords. |
|      2 | exists…By | Exists projection, returning typically a boolean result. |
|      3 | count…By | Count projection returning a numeric result. |
|      4 | delete…By, remove…By | Delete query method returning either no result (void) or the delete count. |
|      5 | …First<number>…, …Top<number>… | Limit the query results to the first <number> of results. This keyword can occur in any place of the subject between find (and the other keywords) and by. |
|      6 | …Distinct… | Use a distinct query to return only unique results. Consult the store-specific documentation whether that feature is supported. This keyword can occur in any place of the subject between find (and the other keywords) and by. |
|  |  |  |

# ∝ Query Methods

### ** 1. findByName(String name)

```java
public interface ProductRepository extends JpaRepository<Products,Long> {

   Products findByName(String name);
// no need to write down this one 
		@Override
    Optional<Products> findById(Long aLong);

}

//Test Case

		@Test
    void findByNameMethod() {
        String name = "Apple";
       Products byName = productRepository.findByName(name);
        System.out.println(byName;

    }

		@Test
    void findByIdMethod() {

        Optional<Products> byName = productRepository.findById(1l);
        System.out.println(byName.get());

    }
```

### ** 2. Find by Multiple Field Names

Query method - Find by multiple field names
1. Write a query method to find or retrieve a product by name or description
`select * from products where name = "product 1" or description = "product 1 desc";`

`public List «Product» findByNameOrDescription(String name, String description):`

2. Write a query method to find or retrieve a product by name and description
`select * from products where name = "product 1" and description = "product 1 desc";`
`public List<Product> findByNameAndDescription(String name, String description);`

```java

/*
  >> Write a query method to find or retrieve a product by name and description
    select * from products where name = "product 1" and description = "product 1 desc";
     */
    List<Products> findByNameOrDescription(String name, String description);

    /*
    >> Write a query method to find or retrieve a product by name and description
    select * from products where name = "product 1" and description = "product 1 desc";
     */
    List<Products> findByNameAndDescription(String name, String description);

//these are test below
@Test
    void findByNameOrDesc() {
        List<Products> byNameOrDescription = productRepository.findByNameOrDescription("Apple", "null");
        byNameOrDescription.stream().forEach(System.out::println);
    }

    @Test
    void findAndNameOrDesc() {
    List<Products> byNameOrDescription = productRepository.findByNameAndDescription("Apple", "Mobile");
        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 3. Query method - Find by Distinct

Write a query method to find or retrieve a unique product by name
`select distinct id, active, date_created, description, image_url, last_updated, name, price, sku from where products name="product 1";`

`public Product findDistinctByName(String title);`

```java
		
Products findDistinctByName(String name);

		@Test
    void findDistinctByName() {
        Products byNameOrDescription = productRepository.findDistinctByName("Apple");
        System.out.println(byNameOrDescription);
    }
```

### ** 4. Query method - Find by GreaterThan

Write a query method to find or retrieve products whose price is greater than given price as method parameter
`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`price > 100;`

`List<Product> findByPriceGreaterThan (BigDecimal price);`

```java
List<Products> findByPriceGreaterThan(BigDecimal price);

@Test
    void findByPriceGreaterThan() {
        List<Products> byNameOrDescription = productRepository.findByPriceGreaterThan(new BigDecimal(1));

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 5. Query method - Find by LessThan

Write a query method to find or retrieve products whose price is greater than given price as method parameter
`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`price < 200;`

`List<Product> findByPriceLessThan (BigDecimal price);`

```java
List<Products> findByPriceLessThan(BigDecimal price);

@Test
    void findByPriceLessThan() {
        List<Products> byNameOrDescription = productRepository.findByPriceLessThan(new BigDecimal(1));

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 6. Query method - Find by Containing

Write a query method to find or retrieve products that matches given text

`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`name like %products%`;

`List<Products> findByNameContaining(String name);`

```java
List<Products> findByNameContaining(String name);

@Test
    void findByNameContaining() {
        List<Products> byNameOrDescription = productRepository.findByNameContaining("Apple");

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 7. Query method - Find by LIKE

Write a query method to find or retrieve products that matches given text

`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`name like %products%`;

`List<Products> findByNameContaining(String name);`

```java
List<Products> findByNameLike(String name);

@Test
    void findByNameLike() {
        List<Products> byNameOrDescription = productRepository.findByNameLike("Apple");

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 8. Query method - Between

Write a query method to find or retrieve products based on Price Range

`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`price between 100 and 300`;

`List<Products>` `findByPriceBetween(BigDecimal one, BigDecimal two);`

```java
@Test
    void findByPriceBetween() {
        List<Products> byNameOrDescription = productRepository.findByPriceBetween(new BigDecimal(100),new BigDecimal(300));

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 9. Query method - Between Date Range

Write a query method to find or retrieve products based on Price Range

`select id, active, date_created, description, image_url, last_updated, name, price, sku
from` 

`products`

 `where` 

`date_created between '2022-01-28' and '2022-01-28'`;

`List<Products> findByDateCreatedBetween(LocalDateTime startDate, LocalDateTime endDate);`

```java
		@Test
    void findByDateBetween() {
List<Products> byNameOrDescription = productRepository.findByDateCreatedBetween(LocalDateTime.of(2021,07,19,10,10), LocalDateTime.of(2023,07,19,10,10));

        byNameOrDescription.stream().forEach(System.out::println);
    }
```

### ** 10. Query method - Limiting Query Results

Spring Data JPA supports keywords 'first' or 'top' to limit the query
results.
Example: findFirstByName0, find Top5BySkul

- An optional numeric value can be appended after 'top' or 'first' to limit the maximum number of results to be returned (e.g. findTop3By....).
- If this number is not used then only one entity is returned.
- There's no difference between the keywords 'first' and 'top'.

`List<Products> findFirst2ByOrderByNameAsc();`

```java
@Test
    void findFirst2 () {
        List<Products> byNameOrDescription = productRepository.findFirst2ByOrderByNameAsc();

        byNameOrDescription.stream().forEach(System.out::println);
    }
```