# http protocol\*

# SSR & CSR

    - server side rendering
        mã html/css được render ở đây
        tối ưu SEO
        lần truy cập đầu tiên nhanh hơn
    - client side rendering
        mã html/css được render ở đây

    cách nhận biết:
        response trả về html/css là ssr

# Express & start web server

    tạo procject:
        npm init
        npm i express

    nodemon & debug:
    add git repository
        git init
        git add .
        git commit -m
        git push
    morgan:
    template engine
        handlebars
    static files &scss
        scss
            watch: input output
        static file
    use bootstrap
    basic routing
        set routing random
        syntax
            req, response
        GET method
            xảy ra khi truy cập vào web
            request đến server ==> phân biệt dựa vào route
            - truyền dưới dạng query parameter trên thanh url
            - khi lấy ra dữ liệu bên phía server thì .query.(tên cái cần lấy)
        form default behavior
            khi submit form tra ve theo method: GET, POST,...
            action mặc định là tại form
                có thể setups action trả kết quả request về trang khác khi submit form
        POST method
            - truyền dưới dạng form data(ẩn dưới thanh url)
            - khi cần lấy ra bên phía server thì .body.(cái gì đó)
            - .body trong server chưa được lưu g/trị của form data gửi về:
                vì thành phần ở giữa browser và controller là 1 middleware
                g/trị body nhận được bên phía server là undefined
    MVC
        ưu điểm: bóc tách các thành phần riêng biệt
        Model       : phần tương tác với data (mysql mongodb)
        View        : chửa file view(html,css)
        Controllers : phần trung gian giữa model và view
                        browser -> web server -> router -> dispatch(controller) ->
                        model -> controller -> view -> controller -> web server(response, http protocol) -> browser
    Routes & Controllers
        web server: có khi chạy npm start( node file js)
                    express cấu hình sẵn web server rồi nên chỉ cần gọi app...
                    sau khi chạy thì các require/import đã được nạp vào RAM
        Routes  : sau khi có request từ client gửi về -> trỏ vào file js -> tìm kiếm route hợp lệ
        dispatcher:   action(hợp lệ) -> dispatcher -> function handle
        browser (send req)-> web server -> router -> dispatcher -> Controllers -> ................
        quy ước tạo file:
    prettier
        làm đẹp code
        prettier --single-quote --trailing-comma all --tab-width 4 --write src/**/*.{js,json,scss}
    lint-staged
        chạy những file được add vào git
    husky

    Model
        mongoose

    App
        - home
        - detail
    CRUD
        soft delete
