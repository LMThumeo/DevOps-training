# Text-Fu

## Basic

### 1. stdout (Standard Out)

- **>** điều hướng chuẩn đầu ra

- file description: 0

- VD ```echo text > file``` ghi đoạn *text* vào *file*. Nếu trong file đã có dữ liệu thì sẽ ghi đè (có thể dùng flag để ngăn chặn ghi đè). Nếu file chưa tồn tại thì sẽ tự tạo mới

![stdout](picture\stdout.png)

> Nếu sử dụng thêm một dấu > sẽ giúp ghi đoạn text tiếp nối vào cuối của file

![stdout2](picture\stdout2.png)

### 2. stdin (Standard In)

- **<** điều hướng chuẩn đầu vào

- file description: 1

- VD ```cat < file1 > file2``` file1 trở thành stdin, file2 trở thành stdout, output của cat file1 trở thành input của files2, tức là lệnh này sẽ đọc nội dung của file1 sau đó ghi vào file2

![stdin](picture\stdin.png)

### 3. stderr (Standard Error)

- file description: 2

- **2>** Khi bạn thực thi một câu lệnh và nó bị lỗi thì lỗi sẽ hiển thị ngay trên màn hình. Nhưng nếu muốn ghi lỗi đó vào trong một file thì cần sdterr.

- VD ```ls /fake/dir 2> coconut.txt```

  ![stderr](picture\stderr.png)

> Nếu muốn thấy cả stderr và stdout trong file, có thể sử dụng 2>&1 hoặc &>.
>
> VD: ```ls /fake/dir > coconut.txt 2>&1``` 
>
>hoặc ```ls /fake/dir &> coconut.txt```

### 4. pipe and tee

- **|** pipe operator cho phép lấy stdout của lệnh và biến nó thành stdin của một tiến trình khác.

  VD: ```ls -la /etc | less``` lệnh này lấy kết quả của ls -la /etc sau đó đẩy vào lệnh less.

  ![pipe](picture\pipe.png)

- **tee** có thể kết hợp với **|** để viết output vào nhiều luồng

  ![tee](picture\tee.png)

### 5. env (Environment)

**env** đưa ra tất cả thông tin biến môi trường hiện tại đã đặt

![env](picture\env.png)

> có thể hiển thị riêng biến môi trường mà bạn muốn.
>
> VD: ```echo $HOME``` hiển thị đường dẫn tới thư mục chính
>
>hoặc ```echo $PATH``` hiển thị các đường dẫn, cách nhau bởi dấu hai chấm.

### 6. cut

- **cut** trích xuất các phần văn bản từ một file

- flag

  - -c theo mỗi dòng

  ![cut1](picture\cut1.png)

  - -f theo trường, mặc định thì dấu Tab được coi là dấu phân cách (delimiter)

  ![cut2](picture\cut2.png)

  - -d định nghĩa một delimiter mới

  ![cut3](picture\cut3.png)

### 7. paste

- **paste** gộp các dòng từ file với nhau và hiển thị ra màn hình

- VD: có một file với các dòng riêng lẻ, lệnh *paste* sẽ đưa các dòng đó ra màn hình trên một dòng và mặc định cách nhau bởi dấu Tab

> Các dòng trong file không thay đổi

![paste1](picture\paste1.png)

> - Nếu muốn thay đổi dấu phân cách mặc định, có thể dùng cờ -d
>
>   ![paste2](picture\paste2.png)
>
> - Có thể dùng paste với nhiều file, kết quả tương tự như trường hợp chỉ một file

### 8. head & tail

- **head** hiển thị một số dòng đầu của file, mặc định là 10

  ![head](picture\head.png)

- **tail** hiển thị một số dòng cuối file, mặc định là 10

  ![tail](picture\tail.png)

>Có thể thay đổi số dòng muốn hiển thị với cờ -n. VD ```head -n 15 Dockerfile```

### 9. expand & unexpand

- **expand** biến đổi dấu tab trong file thành một vài dấu cách

  ![expand](picture\expand.png)

- **unexpand** ngược với expand, lệnh này biến đổi một nhóm các dấu cách về dấu tab

### 10. join & split

- **join** gộp nhiều file bằng trường chung

  - Mặc định gộp bằng trường đầu tiên

    ![join1](picture\join1.png)

  - Chỉ định trường gộp

    ![join2](picture\join2.png)

- **split** lệnh này sẽ tự động tách file ra các file khác khi nó đạt đến 1000 dòng, tên file ngầm định sẽ là x**

### 11. sort

**sort** sắp xếp các dòng theo

- mặc định: sắp xếp bằng cách so sánh các kí tự từ trái qua phải theo acsii

  ![sort1](picture\sort1.png)

- dùng cờ -r để đảo ngược

  ![sort2](picture\sort2.png)

### 12. tr (Translate)

**tr** chuyển đổi một chuỗi kí tự từ tập kí tự này sang tập kí tự khác

![tr](picture\tr.png)

### 13. uniq (Unique)

- **uniq** hữu ích khi làm việc với tệp có những dòng giống nhau

- VD:

  ![uniq1](picture\uniq1.png)

  - Loại bỏ các dòng bị lặp lại

    ![uniq2](picture\uniq2.png)
  
  - Đếm tần xuất của các dòng

    ![uniq3](picture\uniq3.png)

  - Lấy các dòng mà chỉ xuất hiện một lần

    ![uniq4](picture\uniq4.png)

> Lưu ý, *uniq* chỉ hoạt động khi các từ lặp lại (nếu có) đứng sát nhau. Vì vậy trong trường hợp chúng không đứng sát nhau, cần sử dụng kết hợp với *sort*. VD  ```sort reading.txt | uniq```

### 14. wc & nl

- **wc** (word count) đưa ra lần lượt số dòng, số từ, số byte của file

  ![wc](picture\wc.png)

>Có thể dùng các cờ -l -w -c để lấy ra các trường tương ứng

- **nl** (number lines) đưa ra số dòng của một file

  ![nl](picture\nl.png)

### 16. grep

**grep** sử dụng để tìm kiếm một tệp nào đó theo mẫu nhất định hoặc tìm kiếm xem file có chứa chuỗi đó không

  ![grep1](picture\grep1.png)

  > cờ -i đánh dấu việc tìm kiếm không phân biệt chữ hoa chữ thường

## Advanced

### 1. regex (Regular Expressions)

- regular expressions là một công cụ manh mẽ để thực hiện lựa chọn dựa trên mẫu

- Một số regex thông dụng

  - **^**   bắt đầu của một dòng với ^. VD *^by* sẽ khớp với các dòng bắt đầu bằng *by*

  - **$**   kết thúc một dòng với $. VD *you$* sẽ khớp với các dòng kết thúc bằng *you*

  - **.**   khớp với bất kì kí tự đơn nào. VD *b.* sẽ khớp với by hoặc be...

  - **[]**   khớp với các kí tự trong ngoặc
  
    - VD1 *d[iou]g* sẽ khớp với dig, dog hoặc dug.

    - VD2 *d[a-c]g* sẽ khớp với dag, dbg hoăc dcg

    - VD3 *d[^i]g* khi có dấu ^ có nghĩa là bất kí tự ngoại trừ các kí tự trong ngoặc

### 2. Vim (Vi Improved)

#### a. Khởi động và thoát

- *vim* khởi động chế độ vim

- **:qa** thoát chế độ vim

#### b. Vim Search Patterns

- **/** sau dấu / gõ các kí tự bạn muốn tìm kiếm và nhấn enter, sau đó bạn có thể nhấn "n" để đi xuống kết quả dưới và "N" để đi lên kết quả phái trên

- **?** tương tự như / nhưng tìm kiếm từ dưới lên

#### c. Vim Navigation

không thẻ dùng chuột trong vim, muốn di chuyển, hãy sử dụng các mũi tên trên bàn phím

#### d. Vim Appending Text

Bình thường vim sẽ ở chế độ lệnh, tức là không thể sửa văn bản. Vậy để chuyển sang chế độ chèn, có thể nhập:

- *i*: chèn trước con trỏ

- *O*: chèn lên dòng phía trên

- *o*: chèn vào dòng tiếp theo

- *a* nối sau con trỏ

- *A* nối vào cuối dòng

Để thoát chế độ chèn, nhấn phím Esc

#### e. Vim Editing

- **x** dùng để cắt đoạn văn bản hoặc xóa các kí tự

- **dd** xóa dòng hiện tại

- **y** kéo hoặc sao chép bất cứ thứ gì được chọn

- **yy** kéo hoặc sao chép dòng hiện tại

- **p** dán phần văn bản được sao chép trước con trỏ

#### f. Vim Saving and Exiting

- **:w** viết hoặc lưu file

- **:q** thoát chế độ vim

- **:wq** hoặc **ZZ** ghi và thoát

- **:q!** thoát vim mà không lưu file

- **u** undo

- **Ctrl+r** redo