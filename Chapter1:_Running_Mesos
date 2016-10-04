 #Chương này sẽ cung cấp cho bạn một cái nhìn tổng quan ngắn gọn về Apache Mesos và các framework cluster computing. Chúng tôi sẽ hướng dẫn bạn qua các bước để thiết lập Mesos single-node và multi-node. Chúng tôi cũng sẽ xem làm thế nào để thiết lập một cluster Mesos sử dụng Vagrant và trên Amazon EC2. Trong suốt cuốn sách này, chúng tôi sẽ đề cập đến Apache Mesos. Trong chương này, chúng tôi sẽ đề cập đến các chủ đề sau:
•	 Modern data centers (trung tâm dữ liệu mới)
•	 Cluster computing frameworks (Các framework về Cluster computing)
•	 Introducing Mesos (Giới thiệu về Mesos)
•	 Why Mesos? (Tại sao lại sử dụng mesos?)
•	 A single-node Mesos cluster (Một cụm Single-node Mesos)
•	 A multi-node Mesos cluster (Một cụm Cluster-node Mesos)
•	 A Mesos cluster on Amazon EC2 (Một cụm Mesos trên Amazon EC2)
•	 Running Mesos using Vagrant  (Chạy Mesos sử dụng Vagrant)
•	 The Mesos community (Các công ty, đơn vị sử dụng Mesos)

#Modern data centers (Các trung tâm dữ liệu mới)
Các ứng dụng hiện đại phụ thuộc rất nhiều vào dữ liệu. Sự gia tăng đa dạng trong các dữ liệu được tạo ra và xử lý bởi các tổ chức liên tục thay đổi cách chúng ta lưu trữ và xử lý nó. Khi lập kế hoạch kiến trúc hiện đại để lưu trữ và xử lý dữ liệu, chúng tôi không thể hy vọng chỉ cần mua phần cứng với cấu hình cao để giải quyết vấn đề. Các Framework khác nhau để xử lý hàng loạt, xử lý dòng, dịch vụ người dùng phải đối mặt, xử lý đồ thị và phân tích quảng cáo hoc là mỗi bit như là quan trọng như các phần cứng mà họ chạy trên. Những framework là các ứng dụng cung cấp năng lượng cho trung tâm dữ liệu.
Dung lượng và các loại của dữ liệu lớn 
Kích cỡ và nhiều loại dữ liệu lớn có nghĩa là chiến lược quy mô-up truyền thống không còn phù hợp với khối lượng công việc hiện đại. Như vậy, các tổ chức lớn đã chuyển sang chế biến phân phối, nơi mà một số lượng lớn các máy tính hoạt động như một máy tính khổng lồ duy nhất. Các cụm được chia sẻ bởi nhiều ứng dụng với yêu cầu tài nguyên khác nhau, và chia sẻ hiệu quả các nguồn tài nguyên ở mức độ này trong nhiều khuôn khổ là chìa khóa để đạt được sử dụng cao. Có một nhu cầu để xem xét tất cả các máy này như một máy tính quy mô kho duy nhất. Mesos được thiết kế để các hạt nhân của máy tính như vậy.
Theo truyền thống, khuôn khổ chạy trong silo và các nguồn lực được tĩnh phân chia giữa họ, dẫn đến việc sử dụng không hiệu quả các nguồn lực. Sự cần thiết phải xem xét một số lượng lớn các máy hàng như một máy tính duy nhất, và khả năng chia sẻ tài nguyên một cách đàn hồi của tất cả các khung đòi hỏi một khuôn khổ tính toán cluster. Mesos được lấy cảm hứng từ ý tưởng chia sẻ các nguồn lực trong một cluster giữa nhiều khung trong khi cung cấp cách ly tài nguyên.
#Cluster computing frameworks
Trong cụm hiện đại, các yêu cầu tính toán của các khuôn khổ khác nhau là hoàn toàn khác nhau, và các tổ chức cần phải chạy nhiều khuôn khổ và chia sẻ dữ liệu và các nguồn lực giữa chúng. quản lý tài nguyên phải đối mặt với những mục tiêu đầy thách thức và cạnh tranh:
• Hiệu quả: hiệu quả chia sẻ các nguồn lực là mục tiêu chính của phần mềm quản lý cụm.
• Cách ly: Khi nhiều nhiệm vụ đang chia sẻ nguồn lực, một trong những cân nhắc quan trọng nhất là phải đảm bảo cách ly tài nguyên. Cô lập kết hợp với lịch trình thích hợp là nền tảng của việc bảo đảm các thỏa thuận cấp độ dịch vụ (SLAs).
• Khả năng mở rộng: Sự tăng trưởng liên tục của các cơ sở hạ tầng hiện đại đòi hỏi các nhà quản lý cluster để mở rộng quy mô tuyến tính. Một khả năng mở rộng số liệu quan trọng là sự chậm trễ có kinh nghiệm trong việc ra quyết định của khuôn khổ này.
• Mạnh mẽ: quản lý cụm là một thành phần trung tâm, và hành vi mạnh mẽ là cần thiết cho hoạt động kinh doanh liên tục. Có rất nhiều khía cạnh góp phần mạnh mẽ, từ mã được kiểm tra để thiết kế chịu lỗi.
• Mở rộng: phần mềm quản lý cụm là một phát triển rất lớn trong bất kỳ tổ chức và đã được sử dụng trong nhiều thập kỷ. Trong một hoạt động, những thay đổi trong các chính sách về tổ chức và / hoặc phần cứng luôn đòi hỏi sự thay đổi trong cách thức tài nguyên nhóm được quản lý. Như vậy, khả năng bảo trì trở thành một yếu tố quan trọng đối với các tổ chức lớn. Nó phải được cấu hình xem xét hạn chế (ví dụ như vị trí, phần cứng) và hỗ trợ nhiều khung.
Introducing Mesos
Mesos là một quản lý cluster hướng tới sử dụng nguồn lực cải thiện bằng cách tự động chia sẻ nguồn lực giữa nhiều khung. Nó được bắt đầu tại Đại học California, Berkeley vào năm 2009 và được sử dụng sản xuất ở nhiều công ty, bao gồm cả Twitter và Airbnb. Nó đã trở thành một dự án cấp cao nhất Apache trong tháng bảy năm 2013 sau gần hai năm trong ấp.
Mesos cổ phần năng lực sẵn có của máy (hoặc nút) trong công việc của bản chất khác nhau, như thể hiện trong hình dưới đây. Mesos có thể được coi như là một hạt nhân cho các trung tâm dữ liệu cung cấp một cái nhìn thống nhất các nguồn lực trên tất cả các nút và truy cập liền mạch để các nguồn lực này một cách tương tự như những gì một hạt nhân hệ điều hành làm cho một máy tính duy nhất. Mesos cung cấp một lõi cho các ứng dụng trung tâm dữ liệu xây dựng và thành phần chính của nó là khả năng mở rộng lên lịch hai giai đoạn. các Mesos
API cho phép bạn thể hiện một loạt các ứng dụng mà không cần đưa thông tin cụ thể, lĩnh vực vào lõi Mesos. Bằng cách còn lại tập trung vào cốt lõi, Mesos tránh các vấn đề được nhìn thấy với schedulers nguyên khối.
Mesos as a data center kernel
Các thành phần sau đây là quan trọng đối với sự hiểu biết tổng thể kiến trúc Mesos. Chúng tôi sẽ mô tả ngắn gọn cho họ ở đây và sẽ thảo luận về kiến trúc tổng thể chi tiết hơn trong Chương 6, Hiểu Mesos Internals.
The master
Các thạc sĩ chịu trách nhiệm cho trung gian giữa các nguồn lực nô lệ và khuôn khổ. Tại bất kỳ điểm nào, Mesos chỉ có một tổng thể hoạt động, được bầu bằng Zookeeper qua sự đồng thuận phân phối. Nếu Mesos được cấu hình để chạy trong một chế độ lỗi khoan dung, một tổng thể được bầu thông qua giao thức cuộc bầu cử lãnh đạo phân phối, và phần còn lại của họ ở chế độ chờ. Theo thiết kế, tổng Mesos 'không có nghĩa là để làm bất cứ nhiệm vụ nâng hạng nặng của chính nó, mà đơn giản hóa việc thiết kế tổng thể. Nó cung cấp các nguồn lực nô lệ cho các khuôn khổ trong các hình thức của tài nguyên cung cấp và giới thiệu các tác vụ trên nô lệ cho Mời chấp nhận. Nó cũng chịu trách nhiệm cho tất cả các thông tin liên lạc giữa các nhiệm vụ và các khuôn khổ.
Slaves
Nô lệ là workhorses thực tế của cụm Mesos. Họ quản lý các nguồn tài nguyên trên các nút riêng biệt và được cấu hình với một chính sách tài nguyên để phản ánh những ưu tiên kinh doanh. Nô lệ quản lý các nguồn tài nguyên khác nhau, chẳng hạn như CPU, bộ nhớ, cổng, và như vậy, và thực hiện các nhiệm vụ do khuôn khổ.
Frameworks
Frameworks là ứng dụng chạy trên Mesos và giải quyết một trường hợp sử dụng cụ thể. Mỗi khung gồm một lịch trình và thực thi. Một lịch có trách nhiệm quyết định có chấp nhận hoặc từ chối cung cấp tài nguyên. Chấp hành viên là người tiêu dùng tài nguyên và chạy trên các nô lệ và có trách nhiệm điều hành công việc.
Why Mesos?
Mesos mang lại lợi ích to lớn cho cả các nhà phát triển và khai thác. Khả năng của mesos để củng cố các khuôn khổ khác nhau trên một cơ sở hạ tầng chung không chỉ tiết kiệm chi phí cơ sở hạ tầng, mà còn cung cấp những lợi ích hoạt động để các đội Ops và đơn giản hóa xem nhà phát triển của cơ sở hạ tầng, cuối cùng dẫn đến sự thành công kinh doanh. Dưới đây là một số lý do cho tổ chức đón nhận Mesos:
• Mesos hỗ trợ một loạt các khối lượng công việc, từ xử lý hàng loạt (Hadoop), phân tích tương tác (Spark), xử lý thời gian thực (Storm, Samza), chế biến đồ thị (Hama), hiệu năng tính toán cao (Bộ KH & ĐT), lưu trữ dữ liệu ( HDFS, Tachyon, và Cassandra), các ứng dụng web (chơi), tích hợp liên tục (Jenkins, GitLab), và một số các khuôn khổ khác. Hơn nữa, các khuôn khổ meta-lập lịch trình, chẳng hạn như Marathon và Aurora có thể chạy hầu hết các ứng dụng hiện có trên Mesos mà không sửa đổi bất kỳ. Mesos là một sự lựa chọn lý tưởng để chạy container theo quy mô. Sự linh hoạt này khiến Mesos rất dễ áp dụng.
• Mesos cải thiện việc sử dụng thông qua việc chia sẻ tài nguyên đàn hồi giữa các khuôn khổ khác nhau. Nếu không có một hệ thống điều hành trung tâm dữ liệu chung, các khuôn khổ khác nhau phải chạy trên phần cứng bị bưng bít. phân vùng tĩnh như các nguồn tài nguyên dẫn đến nguồn lực phân tán, hạn chế việc sử dụng và thông qua. chia sẻ tài nguyên năng động thông qua Mesos ổ đĩa sử dụng cao hơn và thông qua.
• Mesos là một dự án mã nguồn mở với một cộng đồng sôi động. Các Mesos kiến ​​trúc pluggable làm cho nó dễ dàng để tùy chỉnh nó cho nhu cầu của tổ chức. Kết hợp với thực tế là Mesos chạy trên một loạt các hệ thống điều hành và lựa chọn phần cứng, nó cung cấp phạm vi rộng nhất của các tùy chọn và bảo vệ chống lại các nhà cung cấp lock-in. Vì vậy, phát triển chống lại các API Mesos cung cấp nhiều sự lựa chọn của cơ sở hạ tầng cho chạy chúng. Nó cũng có nghĩa là các ứng dụng Mesos sẽ được cầm tay trên trần kim loại, cơ sở hạ tầng ảo hóa, và các nhà cung cấp điện toán đám mây.
• Có lẽ, những lợi ích quan trọng nhất của Mesos được trao quyền cho các nhà phát triển để xây dựng các ứng dụng hiện đại, tăng năng suất. Khi các nhà phát triển di chuyển từ phát triển các ứng dụng cho một máy tính duy nhất để một chương trình so với các trung tâm dữ liệu, họ cần một API cho phép họ tập trung vào logic của họ và không phải trên các chi tiết thực dụng của các cơ sở hạ tầng phân phối. Với Mesos, các nhà phát triển không cần phải lo lắng về các khía cạnh phân phối và có thể tập trung vào logic tên miền cụ thể của ứng dụng. Mesos cung cấp một API giàu để phát triển các ứng dụng phân tán khả năng mở rộng và chịu lỗi, như chúng ta sẽ thấy trong Chương 7, Phát triển Khung về mesos.
• Điều hành một cơ sở hạ tầng lớn là một thách thức. Mesos đơn giản hoá việc quản lý cơ sở hạ tầng bằng cách cung cấp một cái nhìn thống nhất các nguồn lực. Nó mang đến rất nhiều sự nhanh nhẹn và triển khai các dịch vụ mới mất một thời gian ngắn với Mesos vì không có cụm riêng biệt được phân bổ. Mesos là cực kỳ Ops thân thiện và xử lý các nguồn lực cơ sở hạ tầng như gia súc và không vật nuôi. Điều này có nghĩa là Mesos là kiên cường đối mặt với thất bại và có thể tự động đảm bảo tính sẵn sàng cao, mà không cần can thiệp bằng tay. Mesos hỗ trợ triển khai multitenant với cô lập mạnh mẽ, đó là điều cần thiết cho hoạt động ở quy mô. Mesos cung cấp đầy đủ tính năng REST, web, và giao diện dòng lệnh và tích hợp tốt với các
công cụ hiện có, như chúng ta sẽ thấy trong chương 8, Quản Mesos.
• Mesos là trận chiến đã được thử nghiệm ở Twitter, Airbnb, HubSpot, eBay, Netflix, Conviva, Groupon, và một số tổ chức khác. Mesos phục vụ cho các nhu cầu của một loạt các trường hợp sử dụng giữa các công ty khác nhau là bằng chứng của tính linh hoạt của Mesos như một hạt nhân trung tâm dữ liệu.
Mesos cũng mang lại lợi ích đáng kể đối với cơ sở hạ tầng ảo hóa dựa trên truyền thống:
• Hầu hết các ứng dụng không cần cách ly mạnh được cung cấp bởi các máy ảo và có thể chạy trên ly container có trụ sở tại Mesos. Kể từ container có các chi phí thấp hơn nhiều so với các máy ảo, điều này không chỉ dẫn đến hợp nhất cao hơn, nhưng cũng có những lợi ích khác, chẳng hạn như thời gian khởi động nhanh và như vậy.
• Mesos giảm độ phức tạp cơ sở hạ tầng mạnh so với các máy ảo.
• Đạt được khả năng chịu lỗi và sẵn sàng cao sử dụng máy ảo là rất tốn kém và khó khăn. Với Mesos, lỗi phần cứng trong suốt vào các ứng dụng, và các API Mesos giúp các nhà phát triển trong việc ôm lấy thất bại. Bây giờ chúng ta đã thấy những lợi ích của chạy Mesos, hãy tạo một đơn nút Mesos cluster và bắt đầu khám phá Mesos.
Single-node Mesos clusters
Mesos chạy trên Linux và Mac OS X. Một máy Mesos thiết lập duy nhất là cách đơn giản nhất của thử Mesos, vì vậy chúng tôi sẽ đi qua nó lần đầu tiên. Hiện nay, Mesos không cung cấp các gói nhị phân cho các hệ điều hành khác nhau, và chúng ta cần phải biên dịch nó từ nguồn. Có nhiều gói nhị phân có sẵn của cộng đồng.
Mac OS
Homebrew là một người quản lý gói Linux-phong cách cho Mac. Homebrew cung cấp một công thức cho Mesos và biên dịch nó tại địa phương. Chúng tôi cần phải thực hiện các bước sau để cài đặt Mesos trên Mac:
1. Cài đặt Homebrew từ http://brew.sh/.
2. Homebrew yêu cầu Java được cài đặt. Mac có cài đặt Java mặc định, vì vậy chúng tôi chỉ cần có để đảm bảo rằng JAVA_HOME được thiết lập một cách chính xác.
3. Cài đặt Mesos sử dụng Homebrew với lệnh sau đây:
mac@master:~ $ brew install mesos
Mặc dù Homebrew cung cấp một cách để thử Mesos trên Mac, cài đặt sản xuất nên chạy trên Linux.
Fedora
Bắt đầu từ Fedora 21, kho Fedora chứa Mesos gói. Có mesos-master và mesos-slave gói được cài đặt trên chủ và nô lệ tương ứng. Ngoài ra, có một gói mesos, trong đó có cả chủ và nô lệ gói. Để cài đặt các gói mesos trên phiên bản Fedora> = 21, sử dụng lệnh sau đây:
fedora@master:~ $ sudo yum install –y mesos
Bây giờ chúng ta có thể tiếp tục với phần Bắt đầu mesos để chạy Mesos. Dành cho Fedora Version <= 21, chúng ta phải cài đặt các phụ thuộc và Mesos từ nguồn, tương tự như CentOS như đã giải thích ở phần sau.
Cài đặt điều kiện tiên quyết
Mesos đòi hỏi các điều kiện tiên quyết sau đây để được cài đặt:
•	 g++ (>=4.1)
•	 Python 2.6 developer packages
•	 Java Development Kit (>=1.6) and Maven
•	 The cURL library
•	 The SVN development library
•	 Apache Portable Runtime Library (APRL)
•	 Simple Authentication and Security Layer (SASL) library
Ngoài ra, chúng tôi sẽ cần autoconf (Version 1.12) và libtool nếu chúng ta muốn xây dựng Mesos từ kho git. Việc cài đặt của phần mềm này khác với các hệ điều hành khác nhau. Chúng tôi sẽ chỉ cho bạn các bước để cài đặt Mesos trên Ubuntu 14.10 và CentOS 6.5. Các bước cho hệ điều hành khác cũng tương đối giống nhau.
CentOS
Sử dụng các lệnh sau để cài đặt tất cả các phụ thuộc yêu cầu trên CentOS:
1. Hiện nay, các kho lưu trữ mặc định CentOS không cung cấp một thư viện SVN> = 1,8. Vì vậy, chúng ta cần thêm một kho lưu trữ, cung cấp nó. Tạo một tập tin wandisco-svn.repo mới trong /etc/yum.repos.d/ và thêm những dòng sau đây:
centos@master:~ $ sudo vim /etc/yum.repos.d/wandisco-svn.repo
[WandiscoSVN]
name=Wandisco SVN Repo
baseurl=http://opensource.wandisco.com/centos/6/svn-1.8/RPMS/$basearch/
enabled=1
gpgcheck=0
Bây giờ, chúng ta có thể cài đặt libsvn cách sử dụng lệnh sau đây:
centos@master:~ $ sudo yum groupinstall -y "Development Tools"
2. Chúng tôi cần phải cài đặt Maven bằng cách tải nó, giải nén nó, và đặt nó trong PATH. Các lệnh sau đây giải nén nó vào / opt sau khi chúng tôi tải về nó và liên kết mê đến / usr / bin:
centos@master:~ $ wget http://mirror.nexcess.net/apache/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz
centos@master:~ $ sudo tar -zxf apache-maven-3.0.5-bin.tar.gz -C /opt/
centos@master:~ $ sudo ln -s /opt/apache-maven-3.0.5/bin/mvn /usr/bin/mvn
3. Cài đặt các phụ thuộc khác bằng cách sử dụng lệnh sau:
centos@master:~ $ sudo yum install -y python-devel java-1.7.0-
openjdk-devel zlib-devel libcurl-devel openssl-devel cyrus-sasl-
devel cyrus-sasl-md5 apr-devel subversion-devel
Ubuntu
Sử dụng lệnh sau để cài đặt tất cả các phụ thuộc yêu cầu trên Ubuntu:
ubuntu@master:~ $ sudo apt-get -y install build-essential openjdk-6-jdk python-dev python-boto libcurl4-nss-dev libsasl2-dev libapr1-dev libsvn- dev maven
Build Mesos:
Một khi chúng ta đã cài đặt tất cả các phần mềm cần thiết, chúng ta có thể làm theo các bước để xây dựng Mesos:
1. Tải phiên bản ổn định mới nhất từ ​​http://mesos.apache.org/downloads/. Tại thời điểm viết bài, phiên bản mới nhất là 0.21.0. Lưu file mesos-0.21.0.tar.gz ở một số địa điểm. Mở terminal và đi đến các thư mục, nơi mà chúng tôi đã lưu các tập tin hoặc bạn có thể trực tiếp chạy các lệnh sau trên thiết bị đầu cuối để tải Mesos:
ubuntu@master:~$ wget http://www.apache.org/dist/mesos/0.21.0/mesos-0.21.0.tar.gz
2. Mesos Extract với lệnh sau đây và nhập vào các thư mục trích xuất. Lưu ý rằng lệnh thứ hai sẽ loại bỏ các tập tin .tar tải về, và đổi tên tên phiên bản từ thư mục trích xuất:
ubuntu@master:~ $ tar –xzf mesos-*.tar.gz
ubuntu@master:~ $ rm mesos-*.tar.gz ; mv mesos-* mesos
ubuntu@master:~ $ cd mesos
3. Tạo một thư mục xây dựng. Điều này sẽ chứa các tập tin nhị phân Mesos biên soạn. Bước này là tùy chọn, nhưng nó được khuyến khích. Việc xây dựng có thể được phân phối cho các nô lệ thay vì biên dịch lại trên tất cả các nô lệ:
ubuntu@master:~/mesos $ mkdir build
ubuntu@master:~/mesos $ cd build
4. Cấu hình các cài đặt bằng cách chạy các kịch bản cấu hình:
ubuntu@master:~/mesos/build $ ../configure
Các kịch bản cấu hình hỗ trợ điều chỉnh môi trường xây dựng, có thể được liệt kê bằng cách chạy configure --help. Nếu có bất kỳ phụ thuộc mất tích, sau đó kịch bản cấu hình sẽ báo cáo, và chúng ta có thể quay trở lại và cài đặt các gói bị mất tích. Khi cấu hình thành công, chúng ta có thể tiếp tục bước tiếp theo.
5. Biên dịch nó sử dụng thực hiện. Điều này có thể mất một thời gian. Bước thứ hai là thực hiện kiểm tra:
ubuntu@master:~/mesos/build $ make
ubuntu@master:~/mesos/build $ make check
Các bước làm kiểm tra xây dựng các khuôn khổ ví dụ, và bây giờ chúng ta có thể chạy Mesos từ việc xây dựng thư mục trực tiếp mà không cần cài đặt nó.
6. Cài đặt Mesos cách sử dụng lệnh sau đây:
Các danh sách các lệnh Mesos cung cấp như sau:
ubuntu@master:~/mesos/build $ make install
Bây giờ chúng ta có thể bắt đầu các cụm Mesos địa phương sử dụng các lệnh mesos-địa phương, mà sẽ bắt đầu cả chủ và nô lệ trong một quá trình duy nhất và cung cấp một cách nhanh chóng để kiểm tra các cài đặt Mesos.
Bắt đầu Mesos
Bây giờ chúng tôi đã sẵn sàng để bắt đầu quá trình Mesos. Đầu tiên, chúng ta cần tạo một thư mục cho Mesos nhân rộng các bản ghi với quyền đọc-ghi:
ubuntu@master:~ $ sudo mkdir –p /var/lib/mesos
ubuntu@master:~ $ sudo chown `whoami` /var/lib/mesos
Bây giờ, chúng ta có thể bắt đầu các bậc thầy với lệnh sau đây, xác định thư mục chúng tôi tạo ra:
ubuntu@master:~ $ mesos-master --work_dir=/var/lib/mesos
Các đầu ra ở đây liệt kê các phiên bản xây dựng, cấu hình khác nhau mà các thầy đã được sử dụng, và ID tổng thể của cụm. Quá trình nô lệ sẽ có thể kết nối với các bậc thầy. Quá trình nô lệ có thể xác định địa chỉ IP hoặc tên máy chủ bằng cách lựa chọn --master. Trong phần còn lại của cuốn sách, chúng tôi sẽ giả định rằng máy mà chủ đang chạy có chủ hostname và cần được thay thế bằng một tên máy thích hợp hoặc địa chỉ IP.
ubuntu@master:~ $ mesos-slave --master=master:5050
Các đầu ra xác nhận kết nối đến tổng thể và liệt kê các nguồn nô lệ. Bây giờ, các cụm đang chạy với một nô lệ sẵn sàng để chạy các khuôn khổ.
Running test frameworks
Mesos bao gồm khung dụ thử nghiệm khác nhau được viết bằng C ++, Java và Python. Chúng có thể được sử dụng để xác minh rằng các cụm được cấu hình đúng. Các khuôn khổ kiểm tra sau được viết bằng C ++, và nó chạy năm ứng dụng mẫu. Chúng tôi sẽ chạy nó bằng cách sử dụng lệnh sau:
ubuntu@master:~/mesos/build/src $ ./test-framework --master=master:5050
Ở đây, đầu ra cho thấy các khung kết nối với các bậc thầy và nhận được các nguồn cung cấp từ các bậc thầy. Nó cũng cho thấy các quốc gia khác nhau trong những nhiệm vụ nó đã đưa ra. Ví dụ khuôn khổ Java được bao gồm trong thư mục src / example / java:
ubuntu@master:~/mesos/build/src/examples/java $ ./test-framework master:5050
Tương tự như vậy, ví dụ khuôn khổ Python được bao gồm trong src / example / thư mục python và cho thấy các khuôn khổ và các nhiệm vụ khác nhau nói:
ubuntu@master:~/mesos/build/src/examples/python $./test-framework master:5050

Mesos Web UI
Mesos cung cấp một giao diện web để báo cáo thông tin về các cụm Mesos. Nó có thể được truy cập từ <master-host>: <port>; trong trường hợp của chúng tôi, điều này sẽ là http: // chủ: 5050. Điều này bao gồm những người nô lệ, các nguồn lực tổng hợp, khuôn khổ, và như vậy. Dưới đây là ảnh chụp màn hình của giao diện web:
Multi-node Mesos clusters
Chúng tôi có thể lặp lại bước trước để tự bắt đầu mesos-slave trên mỗi nút nô lệ để thành lập các cụm, nhưng điều này là nhiều lao động và dễ bị lỗi cho các cụm lớn. Mesos bao gồm một tập các script trong thư mục triển khai có thể được sử dụng để triển khai Mesos trên một cụm. Những kịch bản dựa trên SSH để thực hiện triển khai. Chúng ta cần phải thiết lập một mật khẩu ít SSH. Chúng tôi sẽ thiết lập một cluster với hai nút nô lệ (slave1, slave2) và một nút chính (master).
Hãy cấu hình cụm của chúng tôi để đảm bảo rằng họ có kết nối giữa chúng sau khi cài đặt tất cả các điều kiện tiên quyết trên tất cả các nút. Các lệnh sau sẽ tạo ra một chìa khóa ssh và sẽ sao chép chúng vào cả những người nô lệ:
ubuntu@master:~ $ ssh-keygen -f ~/.ssh/id_rsa -P ""
ubuntu@master:~ $ ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@slave1
ubuntu@master:~ $ ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@slave2
Chúng tôi cần phải sao chép Mesos biên soạn cho cả các nút ở vị trí tương tự, như trong tổng thể:
ubuntu@master:~ $ scp –R build slave1:[install-prefix]
ubuntu@master:~ $ scp –R build slave2:[install-prefix]
Tạo một tập tin bậc thầy trong [cài đặt-prefix] / var / mesos / triển khai các thư mục / thạc sĩ với một biên tập viên của sự lựa chọn của riêng bạn vào danh sách các bậc thầy mỗi dòng, mà trong trường hợp của chúng ta sẽ chỉ có một:
ubuntu@master:~ $ cat [install-prefix]/var/mesos/deploy/masters
master
Tương tự như vậy, những người nô lệ nộp sẽ liệt kê tất cả các nút mà chúng tôi muốn là nô lệ Mesos:
ubuntu@master:~ $ cat [install-prefix]/var/mesos/deploy/slaves
slave1
slave2
Bây giờ, chúng ta có thể bắt đầu các cluster với các kịch bản mesos-start-cluster và sử dụng mesos- stop-cluster để ngăn chặn nó:
ubuntu@master:~ $ mesos-start-cluster.sh
Điều này, đến lượt nó, gọi mesos-start-thạc sĩ và mesos-start-nô lệ mà sẽ đóng vai các quy trình thích hợp trên chủ và nô lệ nút. Các kịch bản trông cho bất kỳ cấu hình môi trường trong [tiền tố cài đặt-] / var / mesos / triển khai / mesos- deploy-env.sh. Ngoài ra, để quản lý cấu hình tốt hơn, các tùy chọn cấu hình chủ và nô lệ có thể được quy định trong các tập tin riêng biệt trong [cài đặt-prefix] / var / mesos / triển khai / mesos-master-env.sh và [cài đặt-prefix] / var / mesos / triển khai / mesos-slave-env.sh.
Mesos cluster on Amazon EC2

Running Mesos using Vagrant
Vagrant cung cấp một cách tuyệt vời của việc tạo ra các môi trường ảo di động và do đó cung cấp một cách dễ dàng để thử Mesos chạy trong một máy ảo. Chúng tôi sẽ xem làm thế nào để tạo ra một đơn nút và nút đa Mesos cluster trên máy ảo sử dụng Vagrant:
1. Tải về và cài đặt Vagrant từ https://www.vagrantup.com/
downloads.html. Vagrant hoạt động trên tất cả các hệ điều hành chính.
2. thiết lập Vagrant này sử dụng plugin Vagrant bổ sung. Cài đặt chúng bằng
các lệnh sau đây:
ubuntu @ địa phương: ~ $ lang thang các plugin cài đặt lang thang-omnibus
lang thang-berkshelf lang thang-host lang thang-cachier lang thang-AWS
3. Tải Vagrant cấu hình từ https://github.com/everpeace/
lang thang-mesos / hoặc sao chép chúng bằng cách sử git và cd vào thư mục:
ubuntu @ địa phương: ~ $ git clone https://github.com/everpeace/vagrant-
mesos.git; cd lang thang-mesos
4. Đối với một thiết lập cụm single-node, cd vào thư mục độc lập và chạy
Vagrant lên lệnh. Điều này sẽ tạo ra một máy ảo sẽ chạy
các trường hợp Mesos chủ, nô lệ, và Zookeeper. Các Mesos UI sẽ là
có sẵn tại http://192.168.33.10:5050:
ubuntu @ địa phương: ~ $ cd độc; Vagrant lên
5. Đối với một thiết lập nhiều nút, cd vào thư mục mutlinode. Chúng tôi có thể cấu hình
có bao nhiêu máy ảo có thể được tạo ra cho các Mesos chủ, nô lệ,
và trường hợp Zookeeper trong file cluster.yml. Theo mặc định, nó sẽ tạo ra
năm máy ảo mà chạy như một Zookeeper, hai chủ Mesos, và
hai trường hợp nô lệ Mesos. Các giao diện web Mesos trong thiết lập nhiều nút sẽ được
có sẵn tại http://172.31.1.11:5050:
ubuntu @ địa phương: ~ $ cd multinode; Vagrant lên
6. Cụm Mesos nên được và chạy. Chúng tôi có thể đăng nhập vào các
máy thông qua ssh sử dụng ssh lang thang. Một thiết lập đơn nút gán cho họ
master và slave như tên máy chủ, trong khi một nút đa tên thiết lập các
hosts như Master1, slave1, vv:
ubuntu @ địa phương: ~ $ ssh lang thang master # để đăng nhập để làm chủ
ubuntu @ địa phương: ~ $ lang thang ssh nô lệ # để đăng nhập để nô lệ
7. Chúng tôi có thể mang xuống máy ảo bằng cách sử dụng lệnh dừng lại. Điều này cho phép các máy ảo được khởi động lại với tất cả mọi thứ thiết lập bằng cách sử dụng lệnh lên. Cuối cùng, phá hủy lệnh sẽ tiêu diệt tất cả các máy ảo được tạo ra bởi Vagrant. Lưu ý rằng chúng ta phải thực hiện các lang thang phá hủy lệnh từ độc lập hoặc thư mục multinode cho phù hợp:
ubuntu @ địa phương: ~ $ lang thang dừng
ubuntu @ địa phương: ~ $ lang thang phá hủy
thiết lập Vagrant này cũng cho phép nhiều cấu hình khác nhau và cũng hỗ trợ bạn để khởi động các cụm Mesos trên Amazon EC2. Các file lang thang và tập tin README nằm trong kho sẽ cung cấp cho bạn biết thêm chi tiết.
The Mesos community
Mặc dù là một dự án tương đối trẻ, Mesos có một cộng đồng lớn (http://mesos.apache.org/community/). Có một số câu chuyện thành công của việc sử dụng Mesos bởi cả hai công ty nhỏ và lớn (http://mesos.apache.org/ tài liệu / mới nhất / powered-by-mesos /). Các công ty sử dụng Mesos trường hợp sử dụng khác nhau, từ phân tích dữ liệu để phục vụ web để lưu trữ dữ liệu khuôn khổ.
Case studies
Mesos được sử dụng bởi một số công ty sản xuất để đơn giản hóa quản lý cơ sở hạ tầng. Ở đây, chúng tôi sẽ xem làm thế nào một số các công ty Mesos đòn bẩy.
Twitter
Twitter là nhận con nuôi đầu tiên của Mesos và giúp đỡ để trưởng thành dự án trong quá trình ủ Apache. Twitter là một thời gian thực trò chuyện nền tảng xã hội. Twitter giải quyết được nổi tiếng không vấn đề cá, nhờ vào độ tin cậy của các cơ sở hạ tầng. Twitter coi Mesos như là cơ sở của nó cho toàn bộ cơ sở hạ tầng và điều hành một loạt các công việc trên nền tảng Mesos, bao gồm phân tích, nền tảng quảng cáo, dịch vụ typeahead, và cơ sở hạ tầng nhắn tin. Tất cả các dịch vụ mới được xây dựng tại Twitter sử dụng Mesos, và quan trọng hơn, nó đã thay đổi cách phát triển nghĩ về nguồn lực trong môi trường phân tán. Phát triển có thể nghĩ về một hồ bơi chia sẻ các nguồn tài nguyên thay vì nghĩ về máy cá nhân. Twitter cũng được xây dựng khuôn khổ lịch Aurora để quản lý các dịch vụ dài chạy trên Mesos.
HubSpot
HubSpot làm cho tiếp thị sản phẩm trong nước. HubSpot chạy Mesos trên Amazon EC2 để hỗ trợ hơn 150 loại khác nhau của dịch vụ. Mesos cải thiện việc sử dụng tài nguyên và bảo đảm tính sẵn sàng cao mà không cần chạy nhiều bản sao của các dịch vụ, dẫn đến chi phí cơ sở hạ tầng thấp hơn. HubSpot lưu ý rằng với Mesos, các nhà phát triển có thể khởi động các dịch vụ mới nhanh hơn nhiều và dịch vụ rộng đã trở nên đáng tin cậy hơn và dễ dàng hơn để mở rộng quy mô. HubSpot tạo ra khuôn khổ Singularity trên Mesos và xây dựng Platform-as-a-Service (PaaS) để tạo điều kiện triển khai tiêu chuẩn hóa của các dịch vụ.
Airbnb
Airbnb là một công ty cho thuê dựa vào cộng đồng và là một trong những người sớm chấp nhận của Mesos. Airbnb sử dụng Mesos chạy phân tích dữ liệu sử dụng Hadoop, Spark, Kafka cũng như các dịch vụ, chẳng hạn như Cassandra và Rails. Airbnb cũng tạo ra khuôn khổ lịch Chronos cho Mesos. Chúng tôi sẽ tìm hiểu chi tiết về Aurora và Chronos trong Chương 5, Running Services trên Mesos.
chồng của Twitter được xây dựng trên Ruby on Rails và khung JBoss-esque, mà chủ yếu dựa trên dịch vụ trong tự nhiên, trong khi Airbnb, mặt khác, được sử dụng Mesos hơn cho xử lý dữ liệu và ETL trong tự nhiên. Twitter chạy Mesos trên trần kim loại sử dụng khu Solaris trong một cơ sở hạ tầng tư nhân, trong khi Airbnb chạy nó trên máy ảo bằng VMware và Xen hypervisor trên AWS. Những xác nhận rằng Mesos cung cấp nói chung và dễ dàng để sử dụng API như một hạt nhân của cơ sở hạ tầng phân phối hiện đại có thể chạy trên một loạt các lựa chọn phần cứng và phục vụ một loạt các khung trên đầu trang.
Mailing lists
Mesos duy trì tài liệu rất dễ tiếp cận với các tài liệu http://mesos.apache.org/ / / mới nhất, chi tiết nhất các bộ phận của mesos. Khi các tài liệu là không đủ, các danh sách gửi thư Mesos cung cấp một phương tiện tuyệt vời để tương tác với các thành viên khác và là một phần thiết yếu của cộng đồng Mesos. Người sử dụng danh sách gửi thư (user@mesos.apache.org) và danh sách gửi thư phát triển (dev@mesos.apache.org) tích cực thảo luận về sự phát triển và sử dụng Mesos.
Summary
Trong chương này, chúng tôi đã đưa ra một cái nhìn tổng quan về các yêu cầu của một khuôn khổ quản lý cụm hiện đại và chứng minh làm thế nào để thiết lập Mesos cụm. Chúng tôi đã sẵn sàng để chạy các khuôn khổ khác nhau trên Mesos, đó là nơi mà chúng tôi sẽ chuyển đến trong các chương để làm theo. Chúng tôi sẽ bắt đầu với khung Hadoop trên Mesos trong chương tiếp theo.
