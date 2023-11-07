# Junit & MocKito

Created: September 16, 2023 12:01 PM
Date: September 16, 2023
Select: Junit
Tags: Daily, Ramesh Fadtare

<aside>
💡 Here that header index will Come

</aside>

# Section 1: Hello Junit..!

![Untitled](Junit%20&%20MocKito%20aead0536e7a3462fafa035672580d500/Untitled.png)

# Section 2: AssertJ Overview:

1. AssertJ is a Java library that provides a rich set of assertions and truly
helpful error messages, improves test code readability, and is designed to
be super easy to use within your favorite IDE.
2. When we want to write assertions with AssertJ, we have to use the static
`assertThat()` method of the `org.assertj.core.api.Assertions class.
AssertJ` Overview
3. Spring boot starter test dependency internally provides assertj-core
dependency so we don’t have to add assertj-core dependency manually in
our Spring boot project

## You can use JUnit 5 assertions

1. JUnit 5 assertAll
2. JUnit 5 assertArrayEquals
3. JUnit 5 assertEquals
4. JUnit 5 assertNotEquals
5. JUnit 5 assertNotSame
6. JUnit 5 assertNull and assertNotNull
7. JUnit 5 assertSame
8. JUnit 5 assertThrows
9. JUnit 5 assertTimeout
10. JUnit 5 assertFalse
11. JUnit 5 assertTrue

## Why I use AssertJ?

1. Easy to learn: Quick start
2. Easy to use: you just need to add a dependency and static import in your
test class to start using AssertJ.
3. Fluent APIs: AssertJ helps you to diversify your assertions.
4. More readable code auto-completion: AssertJ provides auto-completion
in IDEs. So you don't need to remember all method names

## What is Unit Testing

In Java, JUnit framework is used for unit testing Java applications
Most of the times one component will depend on other component(s),
so while implementing unit tests we should mock the dependencies
with the desired behaviour using frameworks like Mockito.

## Integration Testing

As the name suggests, integration tests focus on integrating different layers of the
application. That also means no mocking is involved.
Basically, we write integration tests for testing a feature which may involve
interaction with multiple components.

<aside>
💡

`EmployeeController → EmployeeService → EmployeeRepository → DB`

</aside>

# Section 3: Spring Boot - Unit Testing Repository Layer:

## 3.1. Repository layer Unit testing overview:

> write multiple methods
> 

![Untitled](Junit%20&%20MocKito%20aead0536e7a3462fafa035672580d500/Untitled%201.png)

![Untitled](Junit%20&%20MocKito%20aead0536e7a3462fafa035672580d500/Untitled%202.png)

## 3.2. Spring Boot @DataJpaTest annotation:

1. Spring Boot provides the `@DataJpaTest` annotation to test the persistence
layer components that will autoconfigure in-memory embedded database
for testing purposes.
2. `@DataJpaTest` annotation
The `@DataJpaTest` annotation doesn’t load other Spring beans
(`@Components, @Controller, @Service`, and annotated beans) into
ApplicationContext.
3. By default, it scans for `@Entity` classes and configures Spring Data JPA
repositories annotated with `@Repository` annotation 
4. By default, tests annotated with `@DataJpaTest` are transactional and roll
back at the end of each test.

## 3.3. Unit test for save employee operation:

```java
package com.example.junit.Junit.repository;

import com.example.junit.Junit.model.Employee;
import static org.assertj.core.api.Assertions.*;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;

@DataJpaTest // to test repository layer
class EmployeeRepositoryTest {

    @Autowired
    private EmployeeRepository employeeRepository;

   /*
   void given_when_then(){

    ..this is the naming convention that we will be following

    }
     */
   @Test // junit test for save employee operation
   @DisplayName("Unit test case For Save Employee Operation")
    void givenEmployeeObject_whenSave_thenReturnSavedEmployeeObject(){
        //1. given- precondition or setup

        Employee employee = Employee.builder()
                .id(1l)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();
        //2. when - Behaviour or action that we are going to test
        Employee savedEmployee = employeeRepository.save(employee);

        //3. then - verify object
        //import org.assertj.core.api.Assertions;
        assertThat(savedEmployee).isNotNull();
       assertThat(savedEmployee.getId()).isPositive();

    }

}
```

## 3.4 Unit test for get all employees operation:

```java
@Test
    void givenEmployeeList_whenFindAll_thenEmployeeList(){
       //given
        Employee employee = Employee.builder()
                .id(1l)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();
        Employee employee1 = Employee.builder()
                .id(2l)
                .firstName("prata")
                .lastName("Ramaaaasdsdsesh")
                .email("rameasawssdsh@gmail.com")
                .build();

        employeeRepository.save(employee);
        employeeRepository.save(employee1);
        //when
        List<Employee> listOfEMployeee = employeeRepository.findAll();

        //then
        assertThat(listOfEMployeee).isNotNull();
        assertThat(listOfEMployeee.size()).isEqualTo(2);

    }
```

## 3.5 Unit test for get employee by id operation

```java
@Test
    @DisplayName("Unit test case FindById")
    void givenEmployeeObject_whenFindByID_thenReturnEmployeeObject() {
        //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1l)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();
        Employee employee1 = Employee.builder()
                .id(2l)
                .firstName("prata")
                .lastName("Ramaaaasdsdsesh")
                .email("rameasawssdsh@gmail.com")
                .build();

        employeeRepository.save(employee);
        employeeRepository.save(employee1);
        //2. when - Behaviour or action that we are going to test
        Optional<Employee> byId = employeeRepository.findById(1l);

        //3. then - verify object

        //import org.assertj.core.api.Assertions;
        assertThat(byId.get()).isNotNull();
    }
```

## 3.6 Unit test for get employee by email operation (Spring Data JPA query method)

```java

@Test
    @DisplayName("Find By Email Operation")
    void givenEmployeeEmail_whenFindByEmail_thenReturnEmployeeObject() {
        //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1l)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();

        employeeRepository.save(employee);

        //2. when - Behaviour or action that we are going to test
        Optional<Employee> byEmail = employeeRepository.findByEmail("ramesh@gmail.com");
        //3. then - verify object
        assertThat(byEmail.get()).isNotNull();
        //import org.assertj.core.api.Assertions;

    }
```

## 3.7 Unit test for update employee operation

```java
@Test
    @DisplayName("Update Operation")
    void givenEmployeeObject_whenUpdateEmployee_thenReturnUpdatedEmployee() {
        //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();

        employeeRepository.save(employee);
        //2. when - Behaviour or action that we are going to test
        Employee updatedEmployee = employeeRepository.findById(employee.getId()).get();
        updatedEmployee.setEmail("Pratap");
        updatedEmployee.setFirstName("pratap");

        Employee saved = employeeRepository.save(updatedEmployee);

        //3. then - verify object
        assertThat(saved).isNotNull();
        assertThat(saved.getEmail()).isEqualTo("Pratap");
        //import org.assertj.core.api.Assertions;

    }
```

## 3.8 Unit test for delete employee operation

```java
@Test
    @DisplayName("Delete")
    void given_when_then() {
        //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();

        employeeRepository.save(employee);
        //2. when - Behaviour or action that we are going to test
        employeeRepository.delete(employee);
        //3. then - verify object
        assertThat(employeeRepository.findAll().size()).isLessThan(1);
        //import org.assertj.core.api.Assertions;

    }
```

## 3.9 Unit test Spring Data JPA custom query method using JPQL with index parameters

```java
@DisplayName("Unit test case Name")
        void givenFirstNameAndLastName_whenUsingJPQL_thenReturnEmployee(){
            //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();

        employeeRepository.save(employee);
        Employee employee1= Employee.builder()
                .id(2L)
                .firstName("pratap")
                .lastName("pratap")
                .email("ramesh@gmail1.com")
                .build();

        employeeRepository.save(employee1);
            //2. when - Behaviour or action that we are going to test
        Employee employeeRepositoryByJPQL = employeeRepository.findByJPQL("pratap", "pratap");

        //3. then - verify object
            //import org.assertj.core.api.Assertions;
assertThat(employeeRepositoryByJPQL).isNotNull();
        }
```

## 3.10 Unit test Spring Data JPA custom query method using JPQL with named parameters

```java
@Test
    @DisplayName("Unit test case Name")
    void givenFirstNameAndLastName_whenUsingJPQLNamedParam_thenReturnEmployee() {
        //1. given- precondition or setup
        Employee employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();

        employeeRepository.save(employee);
        Employee employee1 = Employee.builder()
                .id(2L)
                .firstName("pratap")
                .lastName("pratap")
                .email("ramesh@gmail1.com")
                .build();

        employeeRepository.save(employee1);
        //2. when - Behaviour or action that we are going to test
        Employee employeeRepositoryByJPQL = employeeRepository.findByJPQLNamedParams("pratap", "pratap");

        //3. then - verify object
        //import org.assertj.core.api.Assertions;
        assertThat(employeeRepositoryByJPQL).isNotNull();
    }
```

## 3.11 Before Each:

```java
@BeforeEach
    void setUp() {
        employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail.com")
                .build();
    }
```

# Section 4: Spring Boot - Unit Testing Service Layer:

![Untitled](Junit%20&%20MocKito%20aead0536e7a3462fafa035672580d500/Untitled%203.png)

## 4.1 Save Employee Method→ Using mock Methods

```java
package com.example.junit.Junit.service.internal;

import com.example.junit.Junit.model.Employee;
import com.example.junit.Junit.repository.EmployeeRepository;
import com.example.junit.Junit.service.EmployeeService;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.mockito.BDDMockito;
import org.mockito.Mockito;

import java.util.Optional;

class EmployeeServiceImplTest {

    private EmployeeRepository employeeRepository;

    private EmployeeService employeeService;

    @BeforeEach
    public void setup() {
        employeeRepository = Mockito.mock(EmployeeRepository.class);
        employeeService = new EmployeeServiceImpl(employeeRepository);
    }

    @Test
    @DisplayName("Unit test case Name")
    void givenEmployeeObject_whenSaveEmploye_thenReturnEmployee() {
        Employee employee = Employee.builder()
                .id(1l)
                .firstName("Pratap")
                .lastName("Adhav")
                .email("email@email")
                .build();
        //stubbing methods
        BDDMockito.given(employeeRepository.findByEmail(employee.getEmail()))
                .willReturn(Optional.empty());
        BDDMockito.given(employeeRepository.save(employee)).willReturn(employee);

        //when
        Employee savedEmployee = employeeService.saveEmployee(employee);

        //then
        Assertions.assertThat(savedEmployee).isNotNull();

    }

}
```

## 4.1.1 Save Employee Method→ Using @Mock and @InjectMocks annotations to mock the object

```java
package com.example.junit.Junit.service.internal;

import com.example.junit.Junit.model.Employee;
import com.example.junit.Junit.repository.EmployeeRepository;
import com.example.junit.Junit.service.EmployeeService;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import static org.mockito.BDDMockito.given;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Optional;

@ExtendWith(MockitoExtension.class)
class EmployeeServiceImplTest {

    @Mock
    private EmployeeRepository employeeRepository;

    @InjectMocks
    private EmployeeServiceImpl employeeService;
    private Employee employee ;
    @BeforeEach
    public void setup() {
         employee = Employee.builder()
                .id(1l)
                .firstName("Pratap")
                .lastName("Adhav")
                .email("email@email")
                .build();
    }

    @Test
    @DisplayName("Unit test case Name")
    void givenEmployeeObject_whenSaveEmploye_thenReturnEmployee() {

        //stubbing methods
        given(employeeRepository.findByEmail(employee.getEmail()))
                .willReturn(Optional.empty());
        given(employeeRepository.save(employee)).willReturn(employee);

        //when
        Employee savedEmployee = employeeService.saveEmployee(employee);

        //then
        Assertions.assertThat(savedEmployee).isNotNull();

    }

}
```

## 4.1.2 Unit test for saveEmployee method which throws Exception:

```java
@Test
	    @DisplayName("Exception throws")
	    void givenExistingEmail_whenSaveEmploye_thenThrowsException() {

        //stubbing methods
        given(employeeRepository.findByEmail(employee.getEmail()))
                .willReturn(Optional.of(employee));
        
        org.junit.jupiter.api.Assertions.assertThrows(ResourceNotFoundException.class,()->{
            employeeService.saveEmployee(employee);
        });
        // this last method should not get executed in the class
        verify(employeeRepository, never()).save(any(Employee.class));

    }
```

## 4.2 Get All EMployee List

```java

@Test
    @DisplayName("All Employee")
    void givenEmployeeList_whenGetAllEmployee_thenReturnEmployeeLists() {
        Employee employee2 = Employee.builder()
                .id(2l)
                .firstName("Pratap1")
                .lastName("Adhav1")
                .email("email@email1")
                .build();
        Employee employee3 = Employee.builder()
                .id(3l)
                .firstName("Pratap2")
                .lastName("Adhav2")
                .email("email@email2")
                .build();
        Employee employee4 = Employee.builder()
                .id(4l)
                .firstName("Pratap3")
                .lastName("Adhav3")
                .email("email@email3")
                .build();
        given(employeeRepository.findAll()).willReturn(Arrays.asList(employee4, employee3, employee2, employee));

//when
        List<Employee> allEmployee = employeeService.getAllEmployee();

        Assertions.assertThat(allEmployee.size()).isEqualTo(4);
    }
```

## 4.2.1 Get All Employee List -Negative Scenario:

```java
@Test
    @DisplayName("All Employee - Negative Senarioa")
    void givenEmployeeList_whenGetAllEmployee_thenReturnEmptyEmployeeLists() {
        Employee employee2 = Employee.builder()
                .id(2l)
                .firstName("Pratap1")
                .lastName("Adhav1")
                .email("email@email1")
                .build();
        Employee employee3 = Employee.builder()
                .id(3l)
                .firstName("Pratap2")
                .lastName("Adhav2")
                .email("email@email2")
                .build();
        Employee employee4 = Employee.builder()
                .id(4l)
                .firstName("Pratap3")
                .lastName("Adhav3")
                .email("email@email3")
                .build();
        given(employeeRepository.findAll()).willReturn(Collections.emptyList());

//when
        List<Employee> allEmployee = employeeService.getAllEmployee();

        Assertions.assertThat(allEmployee.size()).isEqualTo(0);
    }
```

## 4.3 Unit test for Employee-Service get-Employee-Id method:

```java
@Test
        @DisplayName("Get Employee By id")
        void givenEmployee_whenFindById_thenReturnEmployee(){

        given(employeeRepository.findById(employee.getId())).willReturn(Optional.of(employee));

        Employee employeeByID = employeeService.getEmployeeByID(employee.getId());

        Assertions.assertThat(employeeByID).isNotNull();

    }
```

## 4.4 Unit test for Employee-Service updateEmployee method

```java
@Test
    @DisplayName("Update Employee By id")
    void givenEmployee_whenUpdate_thenReturnEmployee() {

        given(employeeRepository.save(employee)).willReturn(employee);

        Employee employeeByID = employeeService.updateEmployee(employee);

        assertThat(employeeByID).isNotNull();

    }
```