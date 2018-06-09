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
