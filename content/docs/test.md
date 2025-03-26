---
date: '2025-03-26T02:31:17+07:00'
draft: false
title: 'Test'
---

# 1. Xác suất

Xác suất là một đại lượng linh hoạt dùng để đo lường sự chắc chắn của một sự kiện. Khi nói đến xác suất, chúng ta nghĩ đến khả năng xảy ra. Lấy ví dụ trong tác vụ phân loại ảnh chó và mèo. Nếu bạn rất chắc chắn rằng bức ảnh đó là một con chó thì bạn sẽ đưa ra xác suất là một giá trị nào đó rất gần 1, chẳng hạn 0.95. Nhưng giả sử bức ảnh bị nhoè và chụp ở khoảng cách rất xa thì bạn không chắc chắn đó là một con chó. Do đó xác suất sẽ giúp bạn đưa ra một lựa chọn lưỡng lự hơn, đó là 0.5 (có thể là chó, mà cũng có thể là mèo).

Các sự kiện trong tự nhiên thì hoàn toàn không bao giờ chắc chắn. Chắc bạn còn nhớ trong bầu cử tổng thống Mỹ năm 2016 giữa ông Donald Trumph và bà Hillary Clinton. Trước khi bầu cử rất nhiều nhận định cho rằng bà Clinton sẽ thắng cử nhưng cuối cùng ông Trumph vẫn trở thành tổng thống. Chính vì thế các nhà khoa học sẽ gán cho các sự kiện không chắc chắn một xác suất để cho thấy sự tin cậy của quyết định.

Việc chúng ta dự báo xác suất có rất nhiều ý nghĩa trong thực tiễn. Các công ty thương mại điện tử muốn dự đoán khả năng khách hàng mua sản phẩm nào là cao nhất dựa trên xác suất. Từ đó họ tối ưu lại thiết kế hệ thống recommendation của mình để gợi ý cho khách hàng sao cho họ mua hàng nhiều nhất. Trong ngành bài bạc, các nhà cái muốn tìm cách chiến thắng người chơi dựa trên tính toán về khả năng chiến thắng/thất bại là bao nhiêu để tìm ra kỳ vọng về lợi nhuận. Các công ty bảo hiểm muốn tính toán khả năng xảy ra rủi ro đối với khách hàng của mình để đưa ra mức phí bảo hiểm phù hợp. Trong nông nghiệp chúng ta quan tâm nhiều hơn tới khả năng mưa, nắng, độ ẩm, gió, các cơn bão để tìm cách điều tiết mùa màng,.... Mục tiêu của các mô hình phân loại trong học máy đều là tìm ra một mô hình ước lượng xác suất tốt nhất để mang lại lợi ích cho tác vụ huấn luyện.

Chính vì vai trò quan trọng như vậy nên có rất nhiều ngành học đã ứng dụng xác suất như xác suất thống kê, định giá tài sản tài chính, định giá bảo hiểm,.... Không thể phủ nhận rằng đây là một mảng rất rộng và tất nhiên chương này tôi cũng không tìm cách bao quát toàn bộ kiến thức về xác suất mà chỉ giới thiệu đến các bạn những khái niệm nền tảng được ứng dụng nhiều trong học máy. Từ đó bạn đọc sẽ có thêm kiến thức để tự nghiên cứu và ứng dụng các mô hình trong thực tiễn.


+++ {"id": "QIZAiZvqYKwR"}

## 1.1. Không gian mẫu

Các xác suất chính là một độ đo được xác định trên một không gian mẫu. Không gian mẫu được ký hiệu là $S$ cho biết tất cả các khả năng có thể xảy ra của một sự kiện. Ví dụ khi chúng ta gieo một xúc sắc 6 mặt thì các mặt $\{1, 2, 3, 4, 5, 6\}$ chính là một không gian mẫu. Khi chúng ta tung đồng xu 2 mặt đồng chất thì các mặt $\{sap, ngua\}$ chính là một không gian mẫu.

Xác suất của một sự kiện $i$ bất kỳ nằm trong không gian mẫu được ký hiệu bằng $P(X=i)$ hoặc chúng ta có thể viết tắt $P(i)$.

Chúng ta cũng có thể sử dụng ký hiệu $P(1 \leq X \leq 4)$ để chỉ ra xác suất rơi vào các khả năng $\{1, 2, 3, 4\}$. Ký hiệu $X$ ở trên được gọi là biến ngẫu nhiên.





+++ {"id": "p7ZyghaJZFrw"}

## 1.2. Biến ngẫu nhiên

Biến ngẫu nhiên (_random variable_, _aleatory variable_ hoặc _stochastic  variable_) là một khái niệm xuất phát từ bộ môn xác suất thống kê, biến ngẫu nhiên là biến mà có giá trị phụ thuộc vào một sự kiện ngẫu nhiên. Ví dụ như kết quả của tung đồng xu hai mặt đồng chất, kết quả gieo xúc sắc 6 mặt hay kết quả hai số cuối của giải đặc biệt xskt MB mà bạn xem hàng ngày là một biến ngẫu nhiên. Biến ngẫu nhiên có thể liên tục hoặc rời rạc tuỳ theo đại lượng mà nó biểu diễn. 

Trong trường hợp tung xúc sắc 6 mặt thì biến ngẫu nhiên chính là một trong các khả năng $\{1, 2, 3, 4, 5, 6\}$. Đây là biến rời rạc vì tập hợp của chúng có số lượng quan sát cố định. Nếu chúng ta đo lường cân nặng của một người thì giá trị đó là một biến ngẫu nhiên liên tục. Lý do nó liên tục là vì cân nặng có thể là một số hữu tỷ bất kỳ, ví dụ như 55.0293102311 mà không nhất thiết phải là một số nguyên. Bởi vì chắc chắn rằng cân nặng giữa 2 người bất kỳ trên trái đất là khác nhau. Khi chúng ta nói hai người có cân nặng bằng nhau là ta đang giả định rằng cân nặng của họ cùng nằm trên một khoảng rất nhỏ ví dụ như từ $52-53$.

Biến ngẫu nhiên liên tục và rời rạc có sự khác biệt nhau về tính liên tục nên trong công thức tính toán xác suất chúng ta thường sử dụng tổng cho biến rời rạc và tích phân cho biến ngẫu nhiên. Tiếp theo ta sẽ cùng tìm hiểu các đặc trưng của biến cho hai trường hợp biến ngẫu nhiên liên tục và rời rạc như bên dưới.

## 1.3. Đặc trưng của biến

### 1.3.1 Kì vọng

Trong một biến ngẫu nhiên có rất nhiều các quan sát thì chúng ta không biết chọn ra giá trị nào làm đại diện cho biến. Đại diện của biến phải là giá trị có thể giúp đánh giá được khái quát độ lớn của biến đó về mặt giá trị. Kỳ vọng là một giá trị đáp ứng được điều này vì nó cho biết về trung bình thì biến có độ lớn là bao nhiêu. Giá trị của kỳ vọng được tính theo hai trường hợp:

* Nếu $\text{x}$ là biến ngẫu nhiên rời rạc.

$$\text{E(x)} = \sum_{i=1}^{n} x_i p(x_i)$$

Trong đó $p(x_i)$ là xác suất xảy ra biến cố $x = x_i$. Khi khả năng xảy ra của các biến cố ngẫu nhiên $x_i$ là như nhau thì giá trị của kỳ vọng: 

$$\text{E(x)} = \bar{\text{x}} = \frac{\sum_{i=1}^{n}x_i}{n}$$

* Nếu $\text{x}$ là một đại lượng ngẫu nhiên liên tục:

$$\text{E(x) }= \bar{\text{x}} = \int xp(x) dx$$

Một số tính chất của kì vọng:

$$\begin{eqnarray}\text{E(ax)} & = & a\text{E(x)} \\
\text{E(ax+by)} & = & a\text{E(x)} + b\text{E(y)} \\
\text{E(xy)} & = & \text{E(x)}\text{E(y)}, ~ \text{if} ~ \text{x, y} ~ \text{independent}
\end{eqnarray}$$