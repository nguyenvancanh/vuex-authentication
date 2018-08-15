# Vuex Authentication

Vuex là gì? Bạn có thể hiểu một cách nôm na là Vuex được xây dựng dựa trên ý tưởng của Flux, Redux và kiến trúc Elm, tuy nhiên nó không được tích hợp vào trong core của vuejs mà nó được phát triển thành một package riêng. Vuex sinh ra giúp chúng ta quản lý các components trong project một cách đơn giản và hiệu quả. Nếu bạn không xây dựng một ứng dụng đơn trang và có lượng dữ liệu lớn thì không cần thiết sử dụng đến nó. Nhưng khi bạn làm việc với dữ liệu lớn thì Vuex sẽ là một giải pháp hữu ích cho bạn. Một bài viết về Vuex tương đối cụ thể và dễ  hiểu. Bạn có thể tham khảo [tại đây](https://techblog.vn/tai-sao-dung-vuex). 

Trong bài này, tôi không tập trung vào giải thích các khái niệm cũng như cách sử dụng của **Vuex**. Vì vậy, trước khi đọc bài này, các bạn cũng cần nắm qua một chút kiến thức về Vuex nhé.

Trong bài này, chúng ta sẽ tập trung vào việc sử dụng Vuex để xây dựng một ứng dụng Authentication. Trước tiên, cần chuẩn bị môi trường để code đã. Chúng ta sẽ sử dụng **vue-cli** để tạo mới projects. Để cài được **vue-cli** tham khảo tại link [Vue-cli](https://cli.vuejs.org/guide/). Sau khi đã cài đặt thành công **vue-cli** chạy command sau để  tạo mới project. 

```
vue create vue-auth
```
