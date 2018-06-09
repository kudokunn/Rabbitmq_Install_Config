## Install: Erlang + Rabbitmq:

1.  Erlang:
+ Nếu cài từ repo epel được bản: erlang-erts-R16B-03.18.el7. Bản này là bản khá cũ, cài rabbit-mq sẽ bị lỗi ngay, vậy cần xóa mà xóa. Nhưng khi xóa nó bằng yum remove erlang thì chỉ xóa các nó và các gói phụ thuộc,vậy thì làm sao mất được các file đi cùng.

B1: xác định các file của nó bằng lệnh: rpm -ql (query_file) <name_package>

         rpm -ql rpm -ql erlang-erts-R16B-03.18.el7

B2: Sau khi xác định thì xóa bằng tay hoặc cài mới package lên và replace nó: 

         rpm -ivh --replacefiles <package.rpm>

2. Cài đặt:

         curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | sudo bash
         sudo yum install erlang-20.2.2-1.el7.centos.x86_64

3. Rabbitmq:
           
           yum install socat -y
           wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.5/rabbitmq-server-3.7.5-1.el7.noarch.rpm
           yum install rabbitmq-server-3.7.5-1.el7.noarch.rpm

4. Start service

           service rabbitmq-server start
           cp /usr/share/doc/rabbitmq-server-3.5.2/rabbitmq.config.example /etc/rabbitmq/
           mv /etc/rabbitmq/rabbitmq.config.example  /etc/rabbitmq/rabbitmq.config
           
 5. Kích hoạt web giao diện
 
Rabbitmq có đi kèm một plugin cho phép quản trị hoạt động qua một web interface trông rất trực quan và thân thiện. Nhưng mặc định, plugin này không được enable thực hiện lệnh sau:

         rabbitmq-plugins enable rabbitmq_management
         
6. Thêm user để đăng nhập:

Add user:

         sudo rabbitmqctl add_user admin[<username>] admin[<password>]

Set tags:

         sudo rabbitmqctl set_user_tags admin[<username>] management

Set permission for user with vhost:

         sudo rabbitmqctl set_permissions admin[<username>] ".*" ".*" ".*"
         

