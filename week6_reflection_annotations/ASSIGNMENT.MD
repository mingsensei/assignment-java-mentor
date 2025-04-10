
# Week 6: Java Reflection and Annotations

1. Reflection có thể thay đổi các thành phần final trong một lớp được không? Code ví dụ minh hoạ cách thay đổi một biến static final.

- Answer: Vẫn thay đổi được , code minh hoạ : 
        Demo obj = new Demo();

        Field field = Demo.class.getDeclaredField("secret");
        field.setAccessible(true);

        // Bỏ modifier "final"
        Field modifiersField = Field.class.getDeclaredField("modifiers");
        modifiersField.setAccessible(true);
        modifiersField.setInt(field, field.getModifiers() & ~Modifier.FINAL);

        // Gán giá trị mới
        field.set(obj, "Change");


2. Reflection có ảnh hưởng như thế nào đến hiệu suất của một ứng dụng Java?

- Answer:Reflection ảnh hưởng hiệu suất vì 
  1.Nó bỏ qua check khi compiler-time
    Ví dụ : Khi gọi method bình thường, JVM sẽ biên dịch , kiểm tra method có tồn tại không, kiểm tra kiểu dữ liệu -> JVN biết method nào sẽ chạy / biến nào sẽ được gọi nên nhanh 
            Khi gọi qua reflection , JVM ko biết method/biến nào sẽ được gọi cho đến khi run-time, phải tìm lại biến,  method  , vì thế nên thời gian chạy sẽ lâu hơn 
  2.Reflection truy cập metadata của class, nên JVM mất thời gian đọc/xử lý metadata , nếu như dùng setAccessible(true) thì nó sẽ phá vỡ tính đóng gói, rồi JVM phải check security xem class đó đc phép truy cập/Field  có được truy cập ko
  3. Ko tối ưu tốc độ = JIT được vì gọi method như bình thường thì nếu method đc gọi nhiều , JVM sẽ dùng cơ chế JIT để tói ưu , còn Reflection thì ko biết method nào sẽ được gọi nên khỏi tối ưu.


3. Rủi ro về bảo mật khi sử dụng reflection? Làm thế nào để giảm thiểu rủi ro này?

- Answer: Dùng Reflection  có thể làm vỡ tính đòng gói khi xài combo getDeclaredField() + set Accessible(true), cho nên gây ra lỗ hổng bảo mật. Để fix thì  chỉ có thể kiểm soát các Reflection, hoặc trong Spring có thể xài các annotation @Secured, @PreAuthorize.

4. Làm thế nào để truy cập thông tin về nested classes và anonymous classes bằng Reflection? 

- Answer: để truy cập nested class thì dùng getDeclaredClasses();, nó sẽ trả về 1 obj Class<?> . còn lấy thông tin về anonymous class thì chia ra 2 trường hợp: 1 là nếu nó đc khai báo là 1 biến trong class outer thì chỉ việc lấy Field ( là cái biến đc sinh ra từ anonymous đó) rồi đọc metadata bằng ( getName / getInterface/getSuperClass/...) . 2 là nếu nó đc khai báo trong 1 method của 1 class thì hơi bị căng thẳng, vẫn có cách nhưng rối.

5. Cơ chế hoạt động của setAccessible(true)?

- Answer: khi gọi setAccessible(true) , JVM cắm 1 cái cờ vô object Field/Constructor/Method đó, rồi đến lúc JVM chạy thì nó check coi có cái flag đó ko, nếu có thì đc truy cập, ko có thì chịu.

6. Giải thích cơ chế hoạt động của Annotation Processor? Làm thế nào chúng được tích hợp vào quá trình biên dịch?

- Answer: Annotation Processor là một cơ chế cho phép xử lý các annotation trong quá trình biên dịch (compile-time) thông qua API javax.annotation.processing. Khi biên dịch thì ctrinh sẽ quét qua các annotation  processor đc triển khai ( kế thừa AbstractProcessor và Override method process) , đến processor nào thì chạy processor đó, tuỳ thuộc vào loại annotation đc khai báo(source / class / runtime), nó sẽ đọc annotation đc khai báo, check,sau đó  file .class tương ứng sẽ đc tạo ra và tồn tại trong compile-time/runtime.
-Để mà tích hợp annotation processort vào quá trình biên dịch : Tạo Annotation/AnnotationProcessor -> tạo EmptyFile ( tức là file ko có đuôi gì hết) tên là javax.annotation.processing.Processor trong META-INF/services, sau đó ghi đúng cái đường dẫn đến file AnnotationProcessor vừa mới tạo , lúc chạy thì java c sẽ tự động quét ra và chạy các annotation processor -> generate file.java tương ứng.


7. Annotation processors có ảnh hưởng như thế nào đến quá trình biên dịch?

- Answer:Annotation mở rộng khả năng của javac ( tạo code, tạo file, kiểm tra exception, hoặc dừng luôn quá trình biên dịch nếu có lỗi do annotation)

8.  Làm thế nào để tạo một annotation có thể được kế thừa?

- Answer: khai báo @Inherit khi tạo annotation là được, class cha triển khai annotation đó thì class con sẽ tự động triển khai annotation đó luôn

9. Phân biệt các loại RetentionPolicy của @Retention?

- Answer:source: chỉ tồn tại trong lúc biên dịch , biên dịch xong thì ko đc viết vào file .class 
          .class : đc ghi vào file .class nhưng ko truy xuất = reflection được
          .runtime: tồn tại cả trong runtime, dùnng reflection .getAnnotation() được

10. Sự khác biệt giữa reflection và annotation processors trong việc xử lý annotation?

- Answer: reflection chỉ xử lý annotation trong runtime, chỉ truy vấn meta-data của annotation đó, còn processor thì xử lý annotation trong compile-time , chạy, tạo code , tạo file .java,.class, kiểm tra annotation các kiểu
