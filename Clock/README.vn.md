# Clock Module

*Đọc ở các ngôn ngữ khác: [English](README.md), [Tiếng Việt](README.vn.md)*

## SR Latch

(Hướng dẫn cách hoạt động của SR latch sẽ bổ sung sau)

## 555 Timer Circuit

Có rất nhiều cách để tạo một module clock cho máy tính. Nhưng cái ta cần ở module là tính linh hoạt. Chúng ta cần có thể điều chỉnh được tốc độ nhanh chậm của đồng hồ. Không muốn nó trở nên quá nhanh và khó thấy được. Hoặc trở nên quá chậm và tốn thời gian. Có một cách để tạo đồng hồ điều chỉnh được là dùng chip 555.

![Simple Timer Image](SimpleTimer.jpg "Simple Timer")

Chip 555 được cấp điện bằng dòng điện 5V từ pin 5 và nối đất ở pin 1. Để điều khiển được tốc độ nhanh chậm chúng ta có 2 điện trở, một là điện trờ 1K Ohm từ nguồn 5V đến pin 7 và cái còn lại là điện trở 1M Ohm nối giữa pin 6 và 7. Pin 6 và pin 2 được nối với nhau bằng sợi dây màu tím như hình. Một tụ điện 1μF nối từ pin 2 tới đất. Và đầu ra của chip (Pin 3) được nối với một đèn LED.

![Diagram](Diagram.gif "Diagram")

Sơ đồ phía trên mô tả cách hoạt động của chip 555.

Bên trong chip chúng ta có ba điện trở 5K Ohm (Đoán xem vì sao nó có tên 555 timer). Chúng được mắc nối tiếp nhau và nối từ nguồn điện 5V rồi trực tiếp nối đất. Điều này có nghĩa là điện thế ở điểm sau điện trở đầu tiên sẽ là 3.33V. Điện thế ở điểm giữa điện trở thứ hai và thứ ba là 1.67V. Chú ý điều này là rất quan trọng trong việc điều khiển chip 555.

Khi chúng ta mới kết nối mạch với nguồn điện, điện thế ở pin 6 và 2 bằng điện thế của tụ điện và bằng 0V. Điều này sẽ đặt trạng thái ban đầu của hai mạch so sánh (Mạch so sánh, kí hiệu hình tam giác, là mạch so sánh điện thế ở hai đầu âm dương nếu điện thế đầu âm cao hơn thì sẽ cho ra tín hiệu thấp hoặc là 0 còn nếu điện thế ở đầu dương cao hơn thì sẽ cho ra tín hiệu cao hoặc là 1). Đầu tiền, ở mạch so sánh phía trên, đầu dương sẽ có điện thế là 0V đầu âm sẽ có điện thế là 3.33V, điều này có nghĩa là nó sẽ cho ra tín hiệu 0. Còn mạch so sánh phía dưới thì ngược lại, đầu dương sẽ có điện thế là 1.67V còn đầu âm thì 0V, và nó sẽ cho ra tín hiệu 1. Tín hiệu 1 ở mạch phía dưới sẽ bật flip-flop (SR latch) lên và đầu ra Q của flip-flop sẽ cho ra tín hiệu 1, làm sáng đèn LED.

Sau đó dòng điện sẽ chạy từ nguồn, rồi đến điện trở thứ nhất (1K) đến điện trở thứ hai (1M) và sạc tụ điện. Khi tụ điện sạc, thì điện thế của tụ điện tăng dần, cùng với đó là điện thế ở pin 2 và pin 6. Tụ điện được sạc cho đến khi điện thế tụ điện vượt qua 3.33V. Khi đó thì các mạch so sánh có sự thay đổi. Mạch so sánh phía dưới đầu âm sẽ có hiệu điện thế cao hơn 3.33V và cho ra tín hiệu 0. Còn mạch so sánh phía trên đầu dương sẽ có điện thế cao hơn 3.33V nên sẽ cho ra tín hiệu 1. Và sẽ đặt lại (Reset) flip-flop, đầu ra Q sẽ là 0 và ngược lại đầu not(Q) sẽ là 1.

Khi đầu not(Q) là 1, nó sẽ kích hoạt bán dẫn ở pin 7 và cho phép dòng điện chạy trực tiếp từ pin 7 xuống đất. Ở trạng thái này, cà dòng điện từ nguồn và dòng điện từ tụ điện điều xả điện thông qua pin 7. Điện thế của tụ điện (hay nói cábmkjkiktyujuhb7iruch khác là pin 2 và pin 6) sẽ giảm từ từ, đến một lúc điện thế sẽ giảm xuống dưới 1.67V. Lúc này bạn có thể đoán được là chuyện gì sẽ xảy ra. Trạng thái bang đầu sẽ xảy ra, có nghĩa là mạch so sánh trên sẽ cho ra 0 còn mạch so sách dưới sẽ cho ra 1, điều này sẽ đặt (Set) mạch flip-flop của chúng ta và kết quả đầu ra Q là 1 và not(Q) là 0. Sau đó tụ điện sẽ được sạc, và điện thế sẽ tăng.

![Simple Timer Behavior](SimpleTimerBehavior.gif "Simple Timer Behavior")

Vòng lặp này sẽ tiếp diễn liên tục, và kết quả sẽ cho ra một đèn LED (hay output của chúng ta) nhấp nháy. Bạn có thể thấy rằng, tốc độ sạc nhanh hay chậm của tụ điện phụ thuộc vào giá trị của hai điện trở, vì dòng điện chạy qua hai điện trở rồi mới sạc tụ điên. Vậy nếu điện trở có giá trị càng cao thì tốc độ sạc càng chậm và ngược lại.

Thêm một lưu ý nữa là, vì khi sạc dòng điện đi qua 2 điện trở nhưng khi xả điện thì dòng điện chỉ đi qua một điện trở ở pin 6 và pin 7. Vì vậy để thời gian tắt và bật của mạch được gần như tương đương nhau, chúng ta nên dùng một điện trở nhỏ (1K) và một điện trở rất lớn (1M) hơn ở pin 2 và pin 6. Lớn hơn gấp 1000 lần nên thời gian tắt bật khá ngang nhau.

Và để dễ dàng debug, chúng ta cần thay điện trở ở pin 2 và pin 6 thành một biến trở. Cụ thể ở đây dùng biến trở 1M. Và một điện trở nhỏ để làm giời hạn nhỏ của tốc độ.

Và thế là ta có một clock module có thể điều chỉnh tốc độ.

![Timer Behavior](TimerBehavior.gif "Timer Behavior")
