# Cronjob in Linux

Cron là một chương trình để xử lý các tác vụ lặp đi lặp lại ở lần sau. Cronjob đưa ra một lệnh để lên lịch làm việc cho một hành động cụ thể, tại một thời điểm cụ thể mà cần lặp đi lặp lại

Cron là một daemon, nó hoạt động dưới nền để thực thi những tác vụ không cần tương tác.

File cron là file text đơn giản chứa các lệnh được chạy trong thời gian cụ thể. File cron mặc định trong hệ thống là /etc/crontab và nằm trong thư mục crontab /etc/cron.*/. Chỉ quản trị viên mới có thể chỉnh sửa file crontab trên hệ thống. 

Một số lệnh và khai báo cơ bản của cron task 

- Sử dụng lệnh dưới đây để mở file crontab và thiết lập những lịch biểu:

```bash
crontab -e
```

- Sử dụng để xem nội dung file đó đang có những lịch nào

```bash
crontab -l
```

**Thực hành: Backup thư mục /home/toe** 

```bash
0 0 1 1 * rsync -av /home/toe /home/backup/$(date +\%Y\%m\%d)
```


Backup thư mục /home/toe mỗi năm một lần vào ngày 01/01
