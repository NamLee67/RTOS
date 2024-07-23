# RTOS Real-time Operating System
RTOS là hệ điều hành dành riêng cho thiết bị vi điều khiển, đối với STM32 có hỗ trợ hệ điều hành freeRTOS
1. Thông thường chúng ta sử dụng kĩ thuật polling( chạy liên tục trong while(1), và có thê interrupt để xử lý các task quan trọng). Nhưng đối với các dự án lớn, yêu cầu nhiều task thì sử dụng polling + interrupt sẽ là không hợp lý, sẽ không đáp ứng đúng yêu cầu về thời gian.
2. Thay vào đó hệ điều hành RTOS sẽ đáp ứng được yêu cầu đó, dáp ứng được trong khoảng thời gian mong muốn
3. RTOS có tính năng lập lịch, để việc thực thi các task gần như là song song, và các task sẽ không phải đợi quá lâu để được thực thi.
4. Hard Real-time : Hệ thống thực hiện task trong khoảng thời gian quy định một cách chính xác
   vd: Túi khí ở trên ô tô cần bật lên trong khoảng thời gian rất nhỏ khi cảm biến nhận được tín hiệu va chạm nguy hiểm.
5. Soft Real-time : Hệ thống không yêu cầu quá gắt gao về thời gian như Hard Real-time
   
      ![image](https://github.com/user-attachments/assets/f9dfa7a3-9c94-48c7-b91d-9cea2a4b347f)

# RTOS - Multi-Task & Scheduling
1. Với chương trình bình thường, chúng ta chạy lần lượt các task trong một vòng while(1) - Super Loop, và có thể dùng ngắt khi cần.

      ![image](https://github.com/user-attachments/assets/c6cb7d19-6b39-491e-8aee-6fcef1640eef)

2. Còn đối với RTOS, các task này sẽ cần được thực hiện gần như "song song". Vì vậy, mỗi task cần có một "chương trình riêng", ứng với mỗi func có một chức năng nhất định. Việc thực hiện đa tác vụ trên cùng một chương trình điều khiển ( vi điều khiển chỉ có 1 core) gọi là Multi-Task

      ![image](https://github.com/user-attachments/assets/45193892-2717-45e1-977a-89fcdab6d7d7)

3. Để nhân 1 core có thể thực hiện các task "gần như song song" thì cần có cơ chế lập lịch (Schedulling)
4. Cơ chế lập lịch - Scheduling: cơ chế này sẽ xác định ở một thời điểm thì task nào được thực thi. Về cơ bản, một task sẽ có 4 trạng thái chính: READY / RUNNING / BLOCKED / SUSPENDED. Scheduling sẽ quyết định task nào ở trạng thái RUNNING, task nào ở trạng thái SUSPENDED / BLOCKED.Nhờ có bộ lập lịch mà chúng ta có thể điều khiển các task hoạt động theo yêu cầu, không task nào bị miss

      ![image](https://github.com/user-attachments/assets/52f028c5-c0af-42b8-ab45-517259941e3e)

# Thuật toán lập lịch RTOS
1. Kernel - hay gọi là Nhân của hệ điều hành
   - Kernel sẽ điều phối hoạt động của các Task dựa vào bộ lập lịch - Scheduler và các thuật toán lập lịch (do con người code).
   - Kernel sẽ quản lý tài nguyên phần cứng - bộ nhớ, để lưu trữ hoạt động của các task.
   - kernel quản lý công việc giao tiếp giữa các task, xử lý ngắt,...
     
      ![image](https://github.com/user-attachments/assets/1a778273-c43b-494e-b776-766c4341714f)
2. Một số thuật toán lập lịch RTOS
	- vd hệ thống có 3 task 1,2,3. Khí task 1 kết thức hoặc hết thời gian thực hiện, thì kernel sẽ gọi bộ lập lịch để biết task tiếp theo là task nào.
  	- Round-Robin : Lập lịch theo kiểu công bằng, tức là mỗi task sẽ có một thời gian thực thi nhất định và tương đương với nhau, gọi là Time Slice, hết thời gian này thì sẽ tới task khác. Với STM32 sử dụng bộ lập lịch này trong freeRTOS. Tuy nhiên, vấn đề xảy ra là nếu như có một Task quan trọng, cần thực hiện ngay, mà chưa tới lượt thực thi thì phải đợi tới lượt. Nên đã có một thuật toán khác ra đời.
     
  
       ![image](https://github.com/user-attachments/assets/03458994-5f76-4894-a57f-dfb56572c917)
   
	- Preemptive : Gán cho những task mức độ ưu tiên. Và task nào có mức độ ưu tiên cao hơn thì được ưu tiên trước. Task bị chiếm quyền sẽ đưa vào trạng thái chờ, cho đến khi task có mức độ ưu tiên hơn thực thi xong.

		![image](https://github.com/user-attachments/assets/761f2e6e-7a53-4e8e-ad86-887a0d41f56f)

 	- 


