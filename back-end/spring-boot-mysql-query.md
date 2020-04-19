### How to use JPA (MySQL) query in Spring Boot

##### 1. Setup dependencies in pom.xml
##### 2. Name your method in @Repository interface using @Query annotion
##### 3. Use it in your controller

```java
import org.springframework.data.jpa.repository.JpaRepository;
import com.southwind.springboottest.entity.Book;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Repository;

import java.util.List;

/**
 * Created by Alex
 * 2020/4/3 2:46
 */
@Repository
// entity name + key name
public interface BookRepository extends JpaRepository<Book,Integer> {
    @Query(value="SELECT * ,ABS(price - (:price))  AS price_ FROM book order by price_ ",
    nativeQuery = true)
    List<Book> findNearestPrice(@Param("price") Double price);
}
```
==========================================================================================
```java
import com.southwind.springboottest.entity.Book;
import com.southwind.springboottest.repository.BookRepository;
import com.southwind.springboottest.service.Bookstore;
import com.southwind.springboottest.vo.BookVO;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.repository.query.Param;
import org.springframework.web.bind.annotation.*;

import javax.validation.constraints.DecimalMin;
import javax.validation.constraints.NotNull;
import java.util.List;
import java.util.Set;

/**
 * Created by Alex
 * 2020/4/14 22:19
 */
@CrossOrigin(origins = "*", allowedHeaders = "*")
@RestController
public class BookController {
    @Autowired
    Bookstore bs;
    @Autowired
    BookRepository br;
    @GetMapping("/book")
    public List all(){
        return bs.findList();
        // 根据什么顺序显示的
    }
    @GetMapping("/book/price/{price}")
    public List nearestPrice(@PathVariable("price") Double price){
        return br.findNearestPrice(price);
        // 根据什么顺序显示的
    }
    @GetMapping("/book/{id}")
    public BookVO getOne(@PathVariable("id") Integer id){
        return (BookVO) bs.findList().get(id-1);
    }

    @GetMapping("/sort")
    public Object sort(){
        return bs.sortprice();
    }

    @GetMapping("/paging")
    public Page<Book> paging(@Param("index") Integer index){
        return bs.paging(index-1);
    }

    @GetMapping("/book/page/{id}/{id2}")
    public String findByIds(@PathVariable @NotNull @DecimalMin("0") Integer id, @PathVariable Integer id2) {
        return "Page = "+id+";"+id2;
    }
}
```
