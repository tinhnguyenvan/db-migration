# rs-migration
    - php create database width migration 

# Phinx
    - Tham khảo tài liệu hướng dẫn http://docs.phinx.org/en/latest/install.html
    - Type column table phinx support
        biginteger
        binary
        boolean
        date
        datetime
        decimal
        float
        integer
        string
        text
        time
        timestamp
        uuid
    
# Hướng dẫn cài đặt
    - Cài đặt bằng composer add vào required "robmorgan/phinx": "^0.8.1"
    - run composer update
    - Kiểm tra phinx đã cài đặt chưa dụng lệnh: php vendor/bin/phinx
    - Mỗi database sẽ tự động tạo 1 table phinxlog (được cấu hình trong file phinx.yml của từng module default_migration_table: phinxlog)
    
# Hướng dẫn sử dụng
    - Convention:
        + Do hệ thống quản lý theo module nên khi thực hiện 1 cmd nào đó nên add thêm đường dẫn "-c phinx.yml"
            - company là tên thư mục module
        + Table collation (defaults to ``utf8_general_ci``)
            
    - Tạo mới 1 migration theo module
        + Quy ước đặt tên khi tạo 1 migration bằng command line. Tên Migration khi chạy cmd phải được đặt bằng CamelCase
        + Ví dụ: 
            php vendor/bin/phinx create UpdateTableUser -c phinx.yml
                - UpdateTableUser là tên migration được tạo
                - company là tên module
                - File được tạo ra ở thư mục db/migration/20171006022515_update_table_user.php
                
    - Chạy lệnh update database
        + php vendor/bin/phinx migrate -c phinx.yml
        
    - NOTE: source hiện tại đang dùng docker nên phải login vào docker để run command line docker exec -it _IMAGE_ bash

    - Cách tạo seed
        + cmd: php vendor/bin/phinx seed:create UserSeeder -c phinx.yml
            - UserSeeder: tên seed được tạo ra trong folder seeds/UserSeeder.php
            - phinx.yml được tạo từ module user
    - Chạy một lệnh seed
        + cmd: php vendor/bin/phinx seed:run -c phinx.yml
            - seed:run chậy tất cả các seed hiện có của module user
            - phinx.yml: lấy câu hình của module user
        
# Setup
    - The first: create database
        + rs-migration
        
    - The second
        + cmd: php vendor/bin/phinx migrate -c phinx.yml
        + cmd: php vendor/bin/phinx seed:run -c phinx.yml => create data login

# NOTE
    - khi chạy trên môi trường production hoặc development thêm -e development
    - Ví dụ môi trường development
        php vendor/bin/phinx migrate -c phinx.yml -e development
        
    - Mặc định là environment local nên không cần thêm -e local