# Kết nối tới dịch vụ AWS sử dụng thư viện Boto3

## Mở đầu
Hôm nay chúng ta sẽ sử dụng ngôn ngữ Python để viết các chức năng sử dụng thư viện về AI của các nhà cung cấp Cloud Computing (Điện toán đám mây), cụ thể ở đây là AWS (Amazon Web Services).


## Giải thích những khái niệm cần đề cập
### AWS
Vậy AWS là gì ?
AWS là viết tắt của "Amazon Web Services," đây là một nhánh của tập đoàn thương mại điện tử lớn Amazon. AWS cung cấp một loạt các dịch vụ đám mây (cloud computing services), cho phép các tổ chức và cá nhân thuê sử dụng tài nguyên máy chủ, lưu trữ, cơ sở dữ liệu, máy học, công cụ phân tích, và nhiều dịch vụ khác thông qua internet.

Dịch vụ của AWS được cung cấp theo mô hình trả tiền theo sử dụng, điều này có nghĩa là khách hàng chỉ phải trả tiền cho những tài nguyên và dịch vụ họ thực sự sử dụng, giúp giảm chi phí cơ sở hạ tầng và quản lý.

Một số dịch vụ nổi tiếng của AWS bao gồm:

* Amazon EC2 (Elastic Compute Cloud): Cho phép thuê máy ảo (instances) để chạy ứng dụng.

* Amazon S3 (Simple Storage Service): Dịch vụ lưu trữ đám mây để lưu trữ và truy cập dữ liệu từ mọi nơi trên internet.

* Amazon RDS (Relational Database Service): Cung cấp cơ sở dữ liệu quan hệ quản lý.

* Amazon Lambda: Dịch vụ tính toán không máy chủ, cho phép chạy mã mà không cần quản lý máy chủ.

* Amazon DynamoDB: Dịch vụ cơ sở dữ liệu NoSQL quản lý.

AWS đã trở thành một trong những nhà cung cấp dịch vụ đám mây lớn nhất và phổ biến nhất trên thế giới, phục vụ hàng triệu khách hàng từ các doanh nghiệp lớn đến các start-up và cá nhân.
### Amazon S3
Dịch vụ của AWS mà chúng ta sẽ làm việc hôm nay là Amazon S3, là một dịch vụ lưu trữ đám mây của Amazon Web Services (AWS). Nó cung cấp khả năng lưu trữ và truy cập dữ liệu từ bất kỳ đâu trên internet.
### Boto3
Và chúng ta sẽ sử dụng Boto3, là một thư viện Python được phát triển để tương tác với các dịch vụ của Amazon Web Services (AWS). Thư viện này là một phần quan trọng của việc phát triển ứng dụng Python trong môi trường đám mây AWS.



## Cài đặt
* Trước hết cần cài đặt module boto3 bằng Python bằng lệnh ```pip install boto3``` trên Command Prompt trên Windows:

![image](https://github.com/m01000xd/AWS/assets/122852491/1865226e-7a76-4932-8f06-d924768b663b)

## Thực hiện 1 số chức năng cơ bản của Amazon S3 bằng Boto3

### Bucket là gì?
Về cơ bản, Amazon S3 cũng khá giống với Goole Drive hay 1 số dịch vụ lưu trữ thông tin khác. Như thông thường, 1 thư mục (folder) sẽ chứa
các loại tài liệu. Còn đối với Amazon S3, thư mục được gọi là ```Bucket```

### Upload file lên bucket

```python
import boto3
s3 = boto3.client('s3', aws_access_key_id='AKIAYEZXHKI7RVQFY6VJ',
                         aws_secret_access_key='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',
                      region_name = 'ap-southeast-2'
                  )
buckets = s3.list_buckets()
my_bucket = 'haaws-bucket'
with open('./bucket_test.txt', 'rb') as f:
s3.upload_fileobj(f, my_bucket, "new_bucket_test.txt", ExtraArgs={"ACL": "public-read"})
```

### Download file từ bucket về máy
```python
import boto3
s3 = boto3.client('s3', aws_access_key_id='AKIAYEZXHKI7RVQFY6VJ',
                         aws_secret_access_key='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',
                      region_name = 'ap-southeast-2'
                  )
buckets = s3.list_buckets()
my_bucket = 'haaws-bucket'
s3.download_file(my_bucket, "bucket_test.txt", "download_bucket.txt")
```

### In ra màn hình tất cả các bucket đang có
```python
import boto3
s3 = boto3.client('s3', aws_access_key_id='AKIAYEZXHKI7RVQFY6VJ',
                         aws_secret_access_key='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',
                      region_name = 'ap-southeast-2'
                  )
buckets = s3.list_buckets()
for bucket in buckets['Buckets']:
    print(bucket)
```

### In ra màn hình các file có trong 1 bucket
```python
import boto3
s3 = boto3.client('s3', aws_access_key_id='AKIAYEZXHKI7RVQFY6VJ',
                         aws_secret_access_key='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',
                      region_name = 'ap-southeast-2'
                  )
buckets = s3.list_buckets()
my_bucket = 'haaws-bucket'
objects = s3.list_objects_v2(Bucket=my_bucket)
for obj in objects['Contents']:
    print(obj)
```
