# Vim Editor

### 1. Các chế độ của Vim

Vim có 3 chế độ: 

- Insert Mode
- Visual Mode
- Command Mode (chế độ dòng lệnh bắt đầu từ dấu “ : ”. Đây là chế độ mặc định khi bắt đầu dùng Vim)

### 2. Sử dụng Vim cơ bản

**Thoát**

:q - Đóng file 

:w - Lưu 

:qw - Lưu và đóng file

**Điều hướng**

h j k l - Phím mũi tên, lần lượt: trái xuống lên phải 

**Thoát chế độ chèn** 

Esc - Thoát khỏi chế độ chèn 

**Lưu và thoát VIM**

yy - Copy dòng hiện tại

dd - Cut dòng hiện tại

p - Paste 

v - Chuyển sang chế độ Visual 

V - Chuyển sang chế độ Visual và bôi đen dòng 

:set number - Hiển thị số dòng 

**Nhảy đến đầu dòng và cuối dòng** 

$ - Nhảy về cuối dòng hiện tại

0 - Nhảy về đầu dòng hiện tại

**Di chuyển đến đầu file hoặc cuối file**

gg - Nhảy lên đầu file 

G - Nhảy xuống cuối file 

50G - Nhảy đến đầu dòng 50 của file hiện tại

Ctrl + G: Xem thông tin của dòng hiện tại 

**Tìm kiếm và thay đổi ký tự**

VD: Tìm kiếm chuỗi “Uoc” thay thế bằng “Toe”

:%s/Uoc/Toe/g
