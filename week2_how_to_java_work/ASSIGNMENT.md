# Week 2: How to Java Work

1. JDK, JVM, và JRE khác nhau như thế nào? Vai trò của từng thành phần trong hệ sinh thái Java?

    Answer:JDK là công cụ để phát triển các ứng dụng, phền mềm java, chứa jre,javac. Jre là 1 phần của jdk, là môi trường để chạy byte code java Jvm là 1 phần của Jre,dịch và thực thi byte code java trên từng hệ đh,. quản lý bộ nhớ.


2. JDK có những công cụ nào quan trọng cho lập trình viên Java?

    Answer: thư viện, debug, compiler

3. JVM hoạt động như thế nào khi bạn chạy một chương trình Java?

    Answer: chuyển đổi byte code --> mã máy, quản lý bộ nhớ , tối ưu hiệu suất JIT

4. Có những thành phần quan trọng nào bên trong JVM?

	Answer: Class loader, execution engine, runtime memory area

5. JVM quản lý bộ nhớ như thế nào? Các vùng nhớ quan trọng trong JVM là gì?

    Answer: phân vùng bộ nhớ để qly. Method area lưu static,class method,var, Heap memory lưu các object, Stack memory lưu local variable, PC trỏ tới dòng lệch tiếp theo để thực thi,Native method stack là 1  phương thức liên kết với hệ thống máy, đc viết bởi C/C++ và khai báo = từ khoá native

6. Class Metadata (Method Area) trong JVM có vai trò gì?

    Answer:lưu metadata của class, byte code method, constrant pool, code của method/constructor,static variable

7. PermGen và Metaspace khác nhau như thế nào? Tại sao Java chuyển từ PermGen sang Metaspace từ Java 8?

    Answer:

8. Heap và Stack trong JVM khác nhau như thế nào?

    Answer:

10. Garbage Collection trong JVM là gì? Tại sao nó quan trọng?

    Answer:

11. Những thuật toán chính của Garbage Collection mà JVM sử dụng là gì?

    Answer:

12. JVM có những loại Garbage Collector nào? Khác nhau ở điểm nào?

    Answer:

13. Sự khác biệt giữa Minor GC, Major GC và Full GC là gì?

    Answer:

14. Bộ nhớ Stack có bị thu hồi bởi Garbage Collector không? Nếu không, nó được quản lý như thế nào?

    Answer:

15. Làm thế nào để tránh Memory Leak trong Java?

    Answer:

16. JIT Compiler trong JVM là gì? Nó cải thiện hiệu năng như thế nào?

    Answer:

17. Khi nào JIT Compiler dịch mã bytecode sang mã máy thực thi?

    Answer:

18. Khi ứng dụng Java chạy chậm, bạn sẽ kiểm tra gì đầu tiên?

    Answer:

20. Làm thế nào để debug lỗi liên quan đến bộ nhớ Heap và Stack?

    Answer: