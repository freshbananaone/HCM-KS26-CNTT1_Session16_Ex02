# Bài 2: Quản lý quyền truy cập báo cáo tài chính

## 1. Bối cảnh và vấn đề

Startup đang lưu danh sách ứng viên, trong đó có số điện thoại và mức lương kỳ vọng. Đây là thông tin cá nhân và thông tin tuyển dụng nội bộ, nên không thể chia sẻ giống như một tài liệu thông thường.

Trưởng phòng nhân sự muốn các trưởng bộ phận xem hồ sơ và góp ý. Tuy nhiên, một nhân viên đã gửi nhầm đường dẫn với quyền **Editor** cho một ứng viên bên ngoài. Người này có thể xem, sửa, tải xuống hoặc tiếp tục chia sẻ file. Vì vậy, nhóm cần thu hồi quyền ngay, kiểm tra lịch sử truy cập và thiết lập lại quyền theo nguyên tắc ít quyền nhất.

Em làm bài theo tình huống danh sách ứng viên trong đề. Giả định công ty dùng Google Workspace: dữ liệu gốc được lưu trong Google Sheets, còn phần nhận xét được chuẩn bị trong Google Docs để dùng Suggesting Mode. Google Drive có ba mức quyền **Viewer, Commenter và Editor**; chỉ người cần cập nhật dữ liệu mới được cấp Editor. 

## 2. Quy tắc Cờ Đỏ Bảo mật

Trước khi chia sẻ file, người sở hữu phải kiểm tra các dấu hiệu có thể làm lộ dữ liệu. Em đề xuất dùng quy tắc Cờ Đỏ như một danh sách kiểm tra bắt buộc:

| Cờ đỏ | Dấu hiệu cần chú ý | Cách xử lý |
|---|---|---|
| Người nhận bên ngoài | Email không thuộc tên miền công ty hoặc không nằm trong danh sách tuyển dụng | Không cấp Editor; chỉ chia sẻ thông tin tối thiểu khi thật sự cần. |
| Link công khai | General access đang là “Anyone with the link” | Đổi ngay về **Restricted**, chỉ thêm đúng tài khoản cần dùng. |
| Quyền quá cao | Người chỉ xem hoặc nhận xét nhưng lại được cấp Editor | Hạ xuống Viewer hoặc Commenter. |
| Có thông tin nhạy cảm | File chứa SĐT, lương kỳ vọng, địa chỉ hoặc ghi chú đánh giá | Tách dữ liệu nhạy cảm sang file HR riêng; hạn chế tải xuống, sao chép và in. |
| Có thể chia sẻ tiếp | Editor có thể đổi quyền hoặc gửi tiếp file | Tắt tùy chọn cho Editor thay đổi quyền và chia sẻ. |
| Không rõ ai đang truy cập | Không biết link đã được gửi cho những ai | Mở Manage access và kiểm tra Access Audit Log trước khi tiếp tục. |

Ngoài việc cài đặt trên file, thư mục cha cũng phải được kiểm tra. Nếu một người đã được cấp Editor ở thư mục cha thì họ có thể thừa hưởng quyền đó đối với file bên trong. Khi cần bảo vệ riêng file ứng viên, nên chuyển file vào thư mục giới hạn quyền thay vì để trong thư mục dùng chung quá rộng. [Google Drive: quyền ở thư mục được kế thừa](https://support.google.com/drive/answer/7166529?hl=en).

## 3. Bản thiết kế phân quyền

File gốc đặt trong thư mục riêng của HR. Trưởng bộ phận nhận bản Google Docs chỉ gồm ứng viên thuộc vị trí họ phụ trách; SĐT và mức lương kỳ vọng chỉ đưa vào nếu cần cho nhiệm vụ. Ban giám đốc nhận báo cáo tổng hợp phù hợp nhu cầu. Bảng quyền đề xuất như sau:

| Đối tượng | Mức quyền | Có thể làm gì | Lý do chọn |
|---|---|---|---|
| Trưởng phòng nhân sự | Editor; giữ vai trò Owner nếu là chủ file | Cập nhật dữ liệu, duyệt góp ý; chủ file quản lý chia sẻ | Chịu trách nhiệm về hồ sơ. Owner là vai trò sở hữu riêng, không đồng nghĩa Editor. |
| Nhân viên HR được phân công cập nhật | Editor | Cập nhật hồ sơ theo nhiệm vụ | Chỉ cấp cho người thực sự nhập hoặc sửa dữ liệu. |
| Trưởng các bộ phận | Commenter trên bản Docs được phân công; không truy cập file gốc | Xem hồ sơ cần đánh giá, nhận xét và đề xuất | Góp ý mà không tự sửa dữ liệu gốc hoặc xem hồ sơ ngoài phạm vi. |
| Ban giám đốc cần theo dõi | Viewer trên báo cáo tổng hợp | Chỉ xem, không sửa hoặc bình luận | Cung cấp đủ thông tin phục vụ quyết định. |
| Ứng viên | Không cấp quyền vào file gốc | Chỉ nhận thông tin riêng liên quan đến hồ sơ của mình | Tránh lộ dữ liệu của các ứng viên khác. |
| Người ngoài không liên quan | Không có quyền | Không xem được file | Không gửi link chung ra bên ngoài. |

**Cách dùng Suggesting Mode:** HR tạo bản Google Docs đã lược bỏ thông tin không cần thiết, ghi mã ứng viên và ngày trích xuất, rồi cấp Commenter cho đúng trưởng bộ phận. Người nhận mở Docs và chọn **Suggesting**, đề xuất thay đổi hoặc để lại nhận xét. HR xem từng đề xuất, chọn **Accept** hoặc **Reject**; chỉ đề xuất được chấp nhận mới thay đổi nội dung bản Docs. 

Ví dụ, trưởng bộ phận đề nghị chuyển ứng viên UV012 từ “chờ đánh giá” sang “mời phỏng vấn”. HR kiểm tra, duyệt đề xuất rồi cập nhật file Sheets gốc. Hai file không tự đồng bộ với nhau. Google Sheets không có Suggesting Mode như Docs; nếu góp ý trực tiếp trong Sheets thì dùng bình luận. Không cấp Editor rồi chỉ yêu cầu người nhận tự bật Suggesting, vì họ vẫn có thể chuyển sang sửa trực tiếp.

### Thiết lập bảo vệ bổ sung

- Đặt **General access = Restricted**.
- Tắt quyền cho Editor thay đổi quyền truy cập và chia sẻ file.
- Với Viewer và Commenter, bỏ tùy chọn tải xuống, sao chép và in nếu công việc không cần các thao tác này.
- Dùng tài khoản công ty, không dùng link ẩn danh.
- Nếu tài khoản công ty hỗ trợ, đặt ngày hết hạn cho quyền truy cập của người cộng tác tạm thời.
- Tách cột SĐT và mức lương kỳ vọng khỏi bản báo cáo tổng hợp gửi rộng hơn.

Các cài đặt này làm giảm khả năng rò rỉ nhưng không thể ngăn tuyệt đối việc chụp màn hình hoặc chép lại bằng phương tiện bên ngoài. Google cũng lưu ý rằng giới hạn tải xuống, sao chép và in chỉ kiểm soát các thao tác ngay trong Drive. 

## 4. Rà soát quyền và Access Audit Log

Mỗi tuần, HR nên rà soát file theo các bước sau:

1. Mở **Share → Manage access**, kiểm tra từng email, vai trò và ngày hết hạn.
2. Kiểm tra General access có còn là Restricted hay không và xem file có đang thừa hưởng quyền từ thư mục cha không.
3. Quản trị viên kiểm tra log theo mã file và thời gian cần rà soát, đối chiếu các hoạt động với nhiệm vụ được giao.
4. Đối chiếu danh sách trong log với danh sách người được HR phê duyệt. Quyền không còn cần thiết phải được gỡ bỏ ngay.
5. Ghi lại ngày rà soát, người thực hiện, quyền đã thay đổi và các sự kiện bất thường.

Danh sách quyền cho biết ai **đang được phép** truy cập; Audit Log giúp tìm hoạt động **đã xảy ra**. Hai nội dung này cần được kiểm tra riêng. Việc tra cứu log cần quyền quản trị phù hợp và gói Workspace hỗ trợ; tài khoản cá nhân hoặc bảng Activity thông thường không thay thế được nhật ký quản trị. 

## 5. Kịch bản xử lý sự cố khi gửi nhầm quyền Editor

Khi phát hiện ứng viên bên ngoài đã nhận link Editor, xử lý theo đúng ba bước sau:

### Bước 1: Thu hồi quyền và khóa đường chia sẻ

Người sở hữu mở **Share**, chọn tài khoản ứng viên → **Remove access**, đặt **General access = Restricted** và lưu thay đổi ngay. Tiếp tục kiểm tra quyền qua nhóm, thư mục cha, Shared drive và các tài khoản được chia sẻ thêm. Gỡ các đường cấp quyền không hợp lệ ở đúng nơi; nếu file đã được xuất bản công khai thì dừng xuất bản. Đồng thời tắt khả năng chia sẻ tiếp của Editor theo cấu hình hỗ trợ. Không chờ điều tra xong mới thu hồi quyền.

Kiểm tra lại danh sách quyền sau khi lưu. Thử mở link bằng cửa sổ chưa đăng nhập để kiểm tra truy cập công khai, nhưng vẫn phải rà soát quyền theo tài khoản và nhóm. Đổi tên file hoặc xóa tin nhắn chứa link không thu hồi quyền. Giữ file và bằng chứng phục vụ kiểm tra; quyền bị gỡ không xóa được nội dung đã tải về hoặc đang được lưu trên thiết bị bên ngoài.

### Bước 2: Kiểm tra log và đánh giá dữ liệu đã bị lộ

Quản trị viên vào **Admin console → Reporting → Audit and investigation → Drive log events**. Lọc theo **Document ID** và khoảng thời gian từ lúc chia sẻ sai đến lúc thu hồi; kiểm tra toàn bộ người truy cập trước khi lọc riêng email ứng viên, vì hoạt động bên ngoài có thể hiện ẩn danh. Tìm **View, Download, Source Copy** với Copy Type **External**, hoạt động sửa và đổi quyền. Xuất kết quả để lưu bằng chứng. [Hướng dẫn tra cứu log của Google](https://knowledge.workspace.google.com/admin/reports/drive-log-events).

Có dấu hiệu tải hoặc sao chép thì đánh giá nguy cơ lộ dữ liệu theo ngữ cảnh. Không có sự kiện không chứng minh an toàn: log có độ trễ, không bao phủ mọi thao tác, không ghi việc in trực tiếp file Docs/Sheets hay chụp màn hình. Nếu chưa có đủ log, ghi “chưa đủ bằng chứng xác định”, rồi kiểm tra lại. [Giới hạn của nhật ký Drive](https://knowledge.workspace.google.com/admin/reports/drive-log-events).

HR lập biên bản gồm thời điểm phát hiện, thời gian link được gửi, phạm vi dữ liệu, hành động ghi nhận trong log và người chịu trách nhiệm xử lý. Nếu dữ liệu cá nhân đã bị truy cập, báo cho người phụ trách bảo mật/pháp chế theo chính sách của startup.

### Bước 3: Khôi phục file và phòng ngừa lặp lại

Nếu ứng viên đã chỉnh sửa file, chủ sở hữu dùng Version History để khôi phục phiên bản trước thời điểm sự cố, sau khi giữ lại một bản sao phục vụ điều tra. Kiểm tra lại danh sách ứng viên, đặc biệt là SĐT, mức lương kỳ vọng và ghi chú đánh giá.

Sau đó, thiết lập lại quyền theo bảng phân loại: HR cập nhật file gốc, trưởng bộ phận góp ý trên bản Docs phù hợp và người chỉ theo dõi xem báo cáo tổng hợp. Kiểm tra quyền bằng tài khoản thử được công ty cho phép. Nếu có khả năng dữ liệu đã ra ngoài, người phụ trách liên hệ ứng viên yêu cầu xóa bản sao và không chuyển tiếp; lời xác nhận của họ không phải bằng chứng kỹ thuật rằng mọi bản sao đã bị xóa.

Nhóm nhắc lại quy tắc trước khi gửi: kiểm tra người nhận, mức quyền và nội dung nhạy cảm. HR rà soát quyền hằng tuần và khi kết thúc đợt tuyển dụng; quản trị viên có thể giới hạn chia sẻ ra ngoài hoặc bật cảnh báo nếu gói dịch vụ hỗ trợ.

