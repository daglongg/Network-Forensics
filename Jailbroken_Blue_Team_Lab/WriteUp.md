**Q1. What is the IOS version of this device?**

Sử dụng tool `iLEAPP` - một công cụ mã nguồn mở được sử dụng để phân tích và trích xuất dữ liệu từ các thiết bị iOS. 

Link tải: `https://github.com/abrignoni/iLEAPP`

Ở đây em thấy nó đã hiển thị thông tin cơ bản của máy

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/bbd532c8-9f90-4df0-8dce-a3f238a7d0a8)

Vậy đáp án của câu này là: `9.3.5`


Q2. Who is using the iPad? Include their first and last name. (Two words)

Ở đây người ta hỏi first và last name, em thấy ở phần `Account Data` có các username là `tim.apple@fruitinc.xyz` 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/b753831b-4057-4ec0-9bf6-9650bf038381)

Vậy đáp án của câu này: `Tim Apple`

**Q3. When was the last time this device was 100% charged? Format: 01/01/2000 01:01:01 PM

Muốn kiểm tra phần cuối mà thiết bị được sạc 100% là khi nào? Kiểm tra với Cheatsheet IOS của SAN thì file lưu lịch sử của battery sẽ nằm ở `private/var/mobile/Library/Preferences/com.apple.BatteryCenter.BatteryWidget.plist` và sẽ hiển thị lịch sử pin

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/651265e0-23fc-4dc5-9aa8-282564a7463b)

Nhưng có 1 vấn đề là k có đường dẫn nào như vậy. Em đã tìm kiếm thì thấy 1 file db lưu trữ lịch sử pin ở `Jailbroken/private/var/containers/Shared/SystemGroup/4212B332-3DD8-449B-81B8-DBB62BCD3423/Library/BatteryLife/CurrentPowerlog.PLSQL`

Tại đây em sẽ đọc và lọc ra được 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/570534c2-1dea-4aee-be53-04a69e9a5e17)

Vậy đáp án của câu này là: `04/15/2020 06:40:31 PM`



Q4. What is the title of the webpage that was viewed the most? (Three words)

Tiêu đề của trang web được xem nhiều nhất là gì? Tiếp tục sử dung Cheatsheet IOS thì em thấy lịch sử web sẽ được lưu ở `private/var/mobile/Library/Safari/History.db`. 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/3038b26b-7262-46bc-9991-e0d0b3c42ae9)

Ở đây em lại không thấy có đường dẫn nào như vậy cả. Em dùng câu lệnh `Get-ChildItem -Recurse -Filter "History.db"` để tìm thử và may mắn là có file ấy. 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/ac4f4c12-f368-47ea-8140-f0c2b0bf1fb4)

Sử dụng SQL để đọc và em thấy nó đang tìm kiếm `kirby with legs` tận 16 lần

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/638b7c55-4cd0-45ff-b3ed-a45ca5a812cb)

Vậy kết quả của câu này là: `kirby with legs`

Q5. What is the title of the first podcast that was downloaded?

Kiểm tra theo đường dẫn sau
Jailbroken\private\var\mobile\Containers\Shared\AppGroup\80179E24-1812-4B5F-8063-
AECFC3773A7A\Documents
Sử dụng sqlite để kiểm tra thông tin trong file MTLibrary.splite
![image](https://github.com/daglongg/Network-Forensics/assets/138242812/03ccca2a-4b7b-4042-b8f1-4d722027059c)

Vậy đáp án của câu này là `Where are we?`



Q6. What is the name of the WiFi network this device connected to? (Two words)

Sử dụng ILEAPP để kiểm tra các kết nối có trong iphone, e dễ dàng tìm được tên wifi mà thiết bị đã kết nối

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/05f21dd5-adae-4c20-b8ef-64fe173f806b)

Vậy đáp án của câu này là `black lab`

Q7. What is the name of the skin/color scheme used for the game emulator? This should be a filename.

Kiểm tra theo đường dẫn `Jailbroken\Applications`.Ở đây sẽ chứa các ứng dụng được cài đặt trong thiết bị. Em kiểm tra và biết được rằng có 1 bộ mô phỏng ở trên `Appstore` có tên là `GBA4iOS`.Vậy nên e đã kiểm tra các dữ liệu trong file `GBA4iOS.app` và được các file khá thú vị

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/b560593c-44a7-4e2a-b2d2-a0ad482548c7)

File có tên là `Default.gbaskin` trong ứng dụng `GBA4iOS` thể hiện ng dùng sẽ dùng màu mặc định của giả lập

Vậy đáp án của câu này là: `Default.gbaskin`

Q8. How long did the News App run in the background?

Kiểm tra các ứng dụng chạy ngầm thì e sẽ điều tra về việc sử dụng pin trong thiết bị

Tiếp tục kiểm tra đường dẫn `Jailbroken\private\var\containers\Shared\SystemGroup\4212B332- 3DD8-449B-81B8-DBB62BCD3423\Library\BatteryLife` và sử dụng sqlite để tìm thông tin

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/dcfb9876-f809-4801-be1f-bc41f0e57474)


Vậy đáp án của câu này là: `197.810275`

Q9. What was the first app download from AppStore? (Two words)

E sử dụng ILEAPP kiểm tra mục apps-Itunes(nơi chứa các thông tin dữ liệu trong đó có các ứng dụng được tải về và cài đặt )

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/21e196fe-2c0e-4d2f-b655-5590da49c2f0)

Ở đây em thấy được rằng ứng dụng được tải xuống đầu tiên là: `Cookie run`

Q10. What app was used to jailbreak this device?

Tiếp tục sử dụng ILEAPP để kiểm tra các app có trong thiết bị

Sau khi dò 1 lượt e thấy các app đều rất là phổ thông cho đến khi nhìn thấy app có tên là phoenix rất lạ lùng

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/669935f8-1ceb-40c4-b656-27839a66f4bc)

Tìm hiểu về nó e thấy được 1 bài viết khá hay về cách tấn công này `https://tinhte.vn/thread/moi- thu-ban-can-biet-ve-phoenix-jailbreak.2716609/` và e suy đoán đây chính là app dùng để bẻ khóa thiết bị

Vậy đáp án của câu này là: `phoenix`
 
 Q11. How many applications were installed from the app store?

Câu này rất đơn giản ta chỉ cần kiểm tra mục apps-Itunes và dễ dàng biết dc là có 2 ứng dụng được cài đặt

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/47e565c6-088e-497c-9801-9a0ba3e2e705)

Vậy đáp án của câu này là: `2`

Q12. How many save states were made for the emulator game that was most recently obtained?

Kiểm tra đường dẫn `Jailbroken\private\var\mobile\Documents`. E thấy 1 file được GBA (trình giả lập sử dụng ) nên e nghĩ chỉ có 1 trạng thái lưu 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/0d8e4e0e-6833-418a-beeb-229d10e3dcc8)

Vậy đáp án của câu này là: `1`

Q13. What language is the user trying to learn?

Dựa vào dữ liệu đã tìm hiểu e thấy ng dùng nghe rất nhiều podcast có tiếng anh trên `Duolingo` nhưng thi thoảng xuất hiện 1 vài ngôn ngữ khá lạ

Tìm hiểu thêm thông tin về cái podcast ng dùng nghe thì e biết được ng dùng đang trong khóa học tiếng tây ban nha cho người anh

Tìm hiểu các file podcast trong đường dẫn `Jailbroken\private\var\mobile\Media\Podcasts`

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/cf083438-3926-40ce-9a21-f2333b16a12d)

Vậy đáp án của câu này là: `Spanish`

Q14. The user was reading a book in real life but used their IPad to record the page that they had left off on. What number was it?

Sử dung đường dẫn `Jailbroken\private\var\mobile\Media\DCIM`

Lần mò trong đó e tìm được 1 video ng dùng lưu lại số trang sách đang đọc

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/406cc037-2191-4b14-8a94-39b28d8742fb)

Vậy đáp án của câu này là: `85`

Q15. If you found me, what should I buy?

If you found me, what should I buy?”. Người dùng iPad này muốn lưu lại thông tin liên quan đến việc nếu gặp một ai đó được nhắc tới sẽ muốn được mua một món đồ. Rất có thể người dùng iPad sẽ lưu lại món đồ muốn mua trên Notes. Có thể `/private/var/mobile/Containers/Shared/AppGroup/4466A521-8AF9-4E09-800B-C3203BB70E0E/` cơ sở dữ liệu `NoteStore.sqlite` sẽ là nơi lưu lại thông tin đã được viết. Tuy nhiên chúng ta không thể tìm thấy thông tin cần thiết. 

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/cc065d53-fe14-46ab-b8fc-1643cc1a7824)

Vây kết quả của câu này là: `Crash Bandicoot Nitro-Fueled Racing"`

Q16. There was an SMS app on this device's dock. Provide the name in bundle format: com.provider.appname

Tiếp tục sử dụng ileapp để tìm hiểu về các app trong thiết bị cung cấp gói tin `SMS`

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/e6e8af2c-6cf2-4cda-8e14-1f48acfa08ec)

Vậy đáp án của câu này là: `com.apple.MobileSMS`

Q17. A reminder was made to get something, what was it?

Để tìm kiếm các lời nhắc trên ios ta sẽ truy cập theo đường dẫn Jailbroken\private\var\mobile\Library\Calendar

Sử dụng sqlite e dễ dàng tìm dc lời nhắc cảu ng dùng lưu lại trong thiết bị

![image](https://github.com/daglongg/Network-Forensics/assets/138242812/8d114c25-b0d5-4755-af47-647334d5ebfc)

Vậy đáp anc ủa câu này là: `milk`

