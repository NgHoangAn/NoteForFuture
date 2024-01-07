=== Read input User data ===
- Buffered Reader: đọc 1 chuỗi ký tự
    +   BufferedReader reader = new BufferedReader(
            new InputStreamReader(System.in));
        String name;
        name = reader.readLine(); 
        System.out.println("Name=" + name);

- Scanner
    +   import java.util.Scanner; 
        Scanner scn = new Scanner(System.in);
    + nextInt *
    + nextFloat *
    + next
    + nextLine

- Sự khác biệt giữa BufferedReader và Scanner *
+ bufferedReader thường dùng để đọc 1 dòng ký tự. nhanh hơn scanner

=== System.out.println ===

- System.out.print: in trên 1 hàng và ko xuống dòng. phải có ít nhất 1 tham số đầu vào

- System.out.println: in trên 1 hàng và xuống dòng. ko cần thiết phải có tham số đầu vào

=== System.out.printf ===
- có thể nhận nhiều đối số
- DecimalFormat: định dạng số thập phân
    + DecimalFormat ft = new DecimalFormat("$###,###.##");
    System.out.println("your Formatted Dream Income : "
                           + ft.format(income));
        // $23.456,79

- SimpleDateForma: định dạng ngày tháng
    +  SimpleDateFormat ft
            = new SimpleDateFormat("dd-MM-yyyy");