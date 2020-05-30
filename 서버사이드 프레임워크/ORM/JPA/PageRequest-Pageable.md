### PageRequest
- PageRequest의 생성에는 찾을 page와 한 페이지의 size를 필수 인자로 받는다.
``` java
public List<Book> findBooksByPageRequest(Integer page, Integer size) {
        PageRequest pageRequest = PageRequest.of(page,size);
        return bookRepository.findAll(pageRequest).getContent();
}

// BookService class
public List<Book> findBooksByPageRequest(Integer page, Integer size) {
        PageRequest pageRequest = PageRequest.of(page, size, Sort.by("createdAt").descending());
        return bookRepository.findAll(pageRequest).getContent();
}
```

### pageable
```java
Pageable pageable = PageRequest.of(1, 10, new Sort(Direction.DESC, "Age"));
Page<Student> studentPage = studentRepository.findAll(pageable);
results.setStudentList(studentPage.getContent());
```