=====================================
---------------T-SQL-----------------
=====================================
# creat
    + CREATE DATABASE databasename;

# alter

# drop
    + DROP DATABASE databasename;

# type data SQL
    + số nguyên: số chẵn (âm- dương)
        + bigint
        + int
        + smallint
        + tinyint   [0-255]
        + decimal
        + bit
        + numeric
        + money
        + smallmoney

    + số thực:
        + float
        + real
    
    + date time
        + datetime  [m/d/y]
        + smalldatetime
        + date
        + datetimeoffect
        + datetime2

    + string
        + char  [8000] ko unicode
        + varchar   [8000] ko unicode
        + Varchar(max)  [251] ko unicode
        + text          ko unicode

    + unicode string
        + nchar     [4000]
        + nvarchar      [4000]
        + nvarchar(max)     [2 mủ 30]
        + ntext

    + binary string
        + binary    [8000 byte]
        + varbinary     [8000 byte]
        + varbinary(max)
        + image

# create table
    + create table table_name(
        column1 datatype,
        ....
        columnN datatype,
        PRIMARY KEY ( column_list )
    )

# drop table
    + drop table table_name;

# primary key
    + tạo trong create table
    + tạo khi dùng alter table
        + alter table table_name
            add primary key ( column_list )

    + xóa
        alter table table_name
        drop primary key;

# Foreign key
    + dùng liên kết 2 bảng
    + A(Fk) trỏ đến B(Pk) [A là con của B]
    +   A(ID, NUmber, BID)
        B(ID, Number, Name)
        tạo FK
            alter table A(
                add constraint Fk_BA
                add Foreign key (BID) references B(ID)
            )
    + xóa Fk
        Fk phải có tên mới xóa được
        drop foreign key Fk_name

# ràng buộc check
    + trong create table
        create table name(
            ...
            check (...)
        )
        // or: constraint Check_name check (... AND ...)

    + trong alter
    + xóa check
        drop constraint Check_name

# insert
    insert into table_name [(column1,....)]
    values (value1,...)

    + có thể có or ko column

# select
    select column1,... from table_name;

# where
    select column_list
    from table_name
    where condition1 [and][or] condition2

# update
    update table_name
    set column1 = value1, column2 = value2,....
    where [condition]

# delete
    delete from table_name
    where [condition]
    + chỉ có thể thao tác vs 1 table trong 1 thao tác

# order by
    select column_list
    from table_name
    [where condition]
    [order by column1,...] [asc | desc]

# distinct
    + lọc data bị trùng chỉ để lại 1 data duy nhất
    + select distinct column_list
        from table_name

# union
    + gộp kết quả
    + union
        + gộp lại và bỏ trùng lặp
        + điều kiện:
            + tên column giống nhau
            + thứ tự column giống nhau
            + tổng column giống nhau
        select statement1
        union
        select statement2
    
    + union all
        + giữ lại tất cả data nếu trùng lặp
        select statement1
        union all
        select statement2

# alias (as)
    + select column_name as name

# and / or
# like / not like
    + '_' đại diện cho 1 kí tự bất kì
    + '%' đại diện cho 1 or nhiều kí tự

# in / not in
    + kiểm tra xem có nằm trong dãy data_list ko
    + select
        from
        where column_name in (data_list)

# between / not between
    select
    ...
    where column_name between [not between] value1 and value2

# tích đề cát
    nhân 2 table
    select *
    from A, B

# inner join
    + lấy data từ nhiều table dựa vào mối liên hệ nào đó
    select
    from table1
    inner join table2
    on table1.column = table2.column

# left join
    + lấy all data của table1 và phần on của table2

# right join
    + lấy all data của table2 và phần on của table1

# seft join

# subquery
    + truy vấn trong truy vấn
        + select ...
            from (select ...)

# group by

# having

# exists

# any / all

# stored procedures

=====================================
---------------MySQL-----------------
=====================================
# RDBMS
## basic
    + là hệ thống quản lý csdl

    + là chương trình duy trì csdl

    + là cơ sở cho MySQL, SQL, Oracle,...

    + dùng truy vấn sql -. truy cậ csdl
 
# select
## syntax
    select column,...
    from table_name

## các loại
    + bình thường
        [select CustomerName, City, Country from Customers]

    + chọn all
        [select * from Customers]

    + chọn ko trùng
        [select distinct column1,...
        from table_name]

# where
## syntax
    + dùng để lọc data [dùng trong update, delete {trừ select}]

    select column1,...
    from table_name
    where condition

## condition
    text ['']
    number [1,...]

# and / or / not
## syntax
    + and
        ...
        where condition1 and condition2
    + or
        ...
        where condition1 or condition2
    + not
        ...
        where not condition

# order by
    + sắp xếp theo thứ tự nào đó
    + asc | desc [asc default]

    ...
    order by ... asc|desc

# insert into
    insert into table_name(column1,...)
    values(value1,...)

# null value
    null = ko có g/trị

    null # 0 # ""
    + test null / not null
        [...
        where column_name is null]

        [...
        where column_name is not null]


# update
    update table_name
    set column1 = value1,...
    where condition

# delete
    delete from table_name where condition

# limit
    + chỉ định số lượng record trả về

    [select column_name,..
    from table_name
    where condition
    limit number]

# min / max
    + [select min(column_name)
        from table_name
        where condition]

    + [select max(column_name)
        from table_name
        where condition]

# count / avg / sum
    + [select count(column_name)
        from table_name
        where condition]

    + [select avg(column_name)
        from table_name
        where condition]

    + [select sum(column_name)
        from table_name
        where condition]

# like
    + dùng trong where
    + '%': zero, 0, multi char
    + '_': one, single char
    [select column1,...
        from table_name
        where columnN like pattern]

# wildcard

# in
    + dùng trong where
    + là viết tắt của nhiều 'or'

    [select column_name
    from table_name
    where column_name in (select statement)]

    [select column_name
    from table_name
    where column_name in (value1, value2,..)]

# between
    ...
    where column_name between value1 and value2

    ...
    where column_name not between value1 and value2

# AS

# join
    + inner join
        + lấy phần chung của cả 2
        select column_name
        from table1
        inner join table2
        on table1.column_name = table2.column_name

    + left join
        + lấy all bên trái và phần chung
        [...
        from table1
        left join table2
        on table1.column_name = table2.column_name]

    + right join
        + lấy all bên phải và phần chung
        [...
        from table1
        right join table2
        on ...]

    + cross join
        + lấy all 2 bảng
        [...
        from table1
        cross join table2]

    + self join
        + lấy trong 1 bảng theo đk

        [select column_name
        from table1 T1, table1 T2
        where condition]

        // t1, t2 là các table aliases

# union
    + select column_name from table1
    union
    select column_name from table2

    // union: ko trùng
    // union all : chọn all trùng

# group by
    + select column_name
    from table_name
    where condition
    group by column_name
    order by column_name

# having
    dùng khi where ko đáp ứng được các hàm kết hợp(group by)

# exist
    select column_name
    from table
    where exist
        (select column_name from table_name where condition)

# any / all
    any return boolean value
        return true khi subquery thõa dk
        select ...
        ...
        where column_name operator any/all
            (select...
            from...
            where...)

# insert into select

    insert into table2
    select * from table1
    where condition

# case
    case
        when condition then result1
        ...
        when conditionN then resultN
        else result
    end

# ifnull / coalesce

# create data base
    create database databaseName

# drop data base
    drop database databaseName

# create table
    create table table_name(
        column1 datatype
        ...
    )

# drop table
    drop table table_name

# truncate table
    truncate table table_name
    // chỉ xóa data, ko xóa bảng

# alter table
    alter table_name
    add/modify ...

# constraints
    create table table_name(
        column1 datatype constraint,
        ...
    )
    + not null [default null]
    + unique
    + primary
    + foreign key
    + check
    + default
    + create index

# dates
    date        -> yyyy-mm-dd
    datetime        -> yyyy-mm-dd HH:MI:SS
    timestamp        -> yyyy-mm-dd hh:mi:ss
    year        -> yyyy or yy

# create view
    create view view_name as
    select column1, column2,...
    from table_name
    where condition

# create or replace view
    update view
        create or replace view view_name as
        select...
        where...

# fn
    + string fn
    + number fn
    + date fn
    + adv fn


=====================================
---------------MongoDB---------------
=====================================
# query API
    
# create database
    db.createCollection("_name_")
# create collection
    db.createCollection("posts")
# insert
    db.posts.insertOne({
        "name":"Huy"
        age: 20,
        tag:["news", "events"],
        date: Date()
    })

    db.posts.insertMany([
        {},
        {},
        ...
    ])



# find
    db.posts.find()

    db.posts.findOne()

    db.posts.find( {category: "News"} )

    db.posts.find({}, {title: 1, date: 1})

    db.posts.find({}, {_id: 0, title: 1, date: 1})

        ko thể dùng 0 và 1 trong cùng 1 object
            ( trừ _id có thể dùng )
            db.posts.find({}, {category: 0})

            db.posts.find({}, {title: 1, date: 0}) // error

# update
    db.posts.updateOne( { name:"Huy" }, { $set: { age:15 } } ) 

    db.posts.updateMany({}, { $inc: { likes: 1 } })
# delete
    db.posts.deleteOne({ title: "Post Title 5" })

    db.posts.deleteMany({ category: "Technology" })
# query operator

# update operator

# aggregation

# indexing/search

# update operator

https://onecompiler.com/mongodb/3ysasx4ca

