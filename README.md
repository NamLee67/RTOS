# RTOS Real-time Operating System
RTOS là hệ điều hành dành riêng cho thiết bị vi điều khiển, đối với STM32 có hỗ trợ hệ điều hành freeRTOS
1. Thông thường chúng ta sử dụng kĩ thuật polling( chạy liên tục trong while(1), và có thê interrupt để xử lý các task quan trọng). Nhưng đối với các dự án lớn, yêu cầu nhiều task thì sử dụng polling + interrupt sẽ là không hợp lý, sẽ không đáp ứng đúng yêu cầu về thời gian.
2. Thay vào đó hệ điều hành RTOS sẽ đáp ứng được yêu cầu đó, dáp ứng được trong khoảng thời gian mong muốn
3. RTOS có tính năng lập lịch, để việc thực thi các task gần như là song song, và các task sẽ không phải đợi quá lâu để được thực thi.
4. Hard Real-time : Hệ thống thực hiện task trong khoảng thời gian quy định một cách chính xác
   vd: Túi khí ở trên ô tô cần bật lên trong khoảng thời gian rất nhỏ khi cảm biến nhận được tín       hiệu va chạm nguy hiểm.
5. Soft Real-time : Hệ thống không yêu cầu quá gắt gao về thời gian như Hard Real-time
   
     ![image](https://github.com/user-attachments/assets/f9dfa7a3-9c94-48c7-b91d-9cea2a4b347f)
