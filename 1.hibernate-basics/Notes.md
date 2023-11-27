## Employee.java
### Entity Class - Employee.java  
public class Employee {  
private int id;  
private String firstName,lastName;  
  
public int getId() {  
    return id;  
}  
public void setId(int id) {  
    this.id = id;  
}  
public String getFirstName() {  
    return firstName;  
}  
public void setFirstName(String firstName) {  
    this.firstName = firstName;  
}  
public String getLastName() {  
    return lastName;  
}  
public void setLastName(String lastName) {  
    this.lastName = lastName;  
}  
}  

### Employee.hbm.xml

<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-mapping PUBLIC  
 "-//Hibernate/Hibernate Mapping DTD 5.3//EN"  
 "http://hibernate.sourceforge.net/hibernate-mapping-5.3.dtd">  
  
 <hibernate-mapping>  
  <class name="com.codewithheeren.entity.Employee" table="emp1000">  
    <id name="id">  
     <generator class="assigned"></generator>  
    </id>   
    <property name="firstName"></property>  
    <property name="lastName"></property>  
  </class>        
 </hibernate-mapping>  

### hibernate.cfg.xml

<?xml version='1.0' encoding='UTF-8'?>  
<hibernate-configuration>  
    <session-factory>  
	<!-- Connection Properties -->
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
        <property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property> 

	<!-- Hibernate Properties -->
        <property name="hbm2ddl.auto">update</property>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  

	<!-- Mapping Files -->
        <mapping resource="employee.hbm.xml"/>  
    </session-factory>  
  
</hibernate-configuration>  

### Main class

package com.codewithheeren.main;    
    
import org.hibernate.Session;    
import org.hibernate.SessionFactory;    
import org.hibernate.Transaction;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;  
  
    
public class StoreData {    
public static void main(String[] args) {    
        
    //Create typesafe ServiceRegistry object    
   StandardServiceRegistry ssr = new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
   Metadata meta = new MetadataSources(ssr).getMetadataBuilder().build();  
   SessionFactory factory = meta.getSessionFactoryBuilder().build();  
   Session session = factory.openSession();  
   Transaction t = session.beginTransaction();   
            
    Employee e1=new Employee();    
    e1.setId(101);    
    e1.setFirstName("Gaurav");    
    e1.setLastName("Chawla");    
        
    session.save(e1);  
    t.commit();  
    System.out.println("successfully saved");    
    factory.close();  
    session.close();    
}    
}   
