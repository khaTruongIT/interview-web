Web Fundamentals

- HTML
  - HTML5 vs HTML
    - HTML5 provide semantic markup
    - HTML5 provide new elements like video, audio, canvas, datalist, progress.
    - Enhance form, more attribute like placeholder, required, pattern
    - Provided storage like localStorage and sessionStorage.
    - Improve APIs like Geolocation API, Web Storage API.
  - Elements
    - Inside Head of HTML document: title, meta tags, script import external css/js/fonts files, favicon.
    - Meta tag:
      - charset: xác định kiểu mã hoá kí tự của trang web
      - content: chứa content của meta tag dùng cho name hoặc http-equiv
      - http-equiv: xác định kiểu nội dung và kiểu mã hoá kí tự của web
      - name: định danh 1 cái trường dữ liệu của meta data (viewport, keywords, description, generator)
    - Semantic & Non-semantic:
      - Non-semantic: Tag div, span, i,..
      - Semantic: Tag header (header of page include title, logo, navigation), Tag nav (for navigation links ), Tag article (dùng cho đoạn tài liệu như blog post, bài báo), Tag aside (dùng cho làm sidebar hay QC)
        => Semantic mang ngữ nghĩa với giúp structure tốt hơn, non-semantic chỉ để presentation chứ k mang ngữ nghĩa j nhất định -> nên dùng semantic để cải thiện accessibility, SEO, code dễ đọc
  - Hyperlinks
    - Link tới 1 elements khác: sử dụng id của elements và dùng thẻ a với href="#element-id"
    - Absolute link: link đầy đủ có cả https và domain, dùng để dẫn đến 1 trang web cụ thể nằm ngoài website hiện tại.
    - Relative link: thường là cái đường dẫn file HTML, khi muốn chuyển trang hoặc link tới resource trong chính trang của mình thì dùng thằng này.
    - Thuộc tính _target_: thường dùng để mở trang web trong 1 cửa sổ browser mới.
      - Set rel là noopener: để tránh việc cái trang web mới được mở bên cửa sổ mới có thể edit hoặc tác động đến trang chính của mình.
  - Multimedia
    - Format:
      - Common: JPEG/JPG, PNG, GIF, SVG
      - New: WEBP, AVIF
      - Width và height image kỹ thuật dùng sẽ tốt cho 2 cái:
        - Tối ưu hoá việc browser render cái hình, có height có width thì browser sẽ chừa chỗ cho cái hình vừa đủ, trước cả khi cái hình load, này giúp cho layout k bị thay đổi và tăng tính UX.
        - Page load performace: như nói trên chừa chỗ cho cái hình kể cả khi chưa render sẽ giúp page render nhanh hơn vì nó biết cái size r, nó sẽ đi render những cái khác.
      - Làm sao để đảm bảo render cái hình với size tối ưu:
        - Dùng CSS để sizing (max-width, max-height, width)
        - Với web hỗ trợ responsive thì dùng thêm media queries để cái hình responsive theo.
        - Dùng thẻ picture vs source để đáp ứng phù hợp với mấy cái mật độ của hình theo màn hình (thẻ này giống audio vs video, thêm nhiều resource, cái nào đáp ứng được điều kiện thì render)
      - Image lazy loading:
        - Loading image là kĩ thuật giúp cải thiện hiệu năng của web bằng việc hoãn lại cái việc load image đến khi nào cần hoặc là chỉ show lên trên màn hình của user. (Tốt cho page nào có nhiều hình)
        - Thẻ image có hỗ trợ attribute loading="lazy"
      - Mục đích của iframe: nhúng content từ trang web hay page khác
        - Communicate giữa content bên trong iframe với parent page (cùng domain), dùng post message, 1 bên bắn message 1 bên lắng nghe
- HTTP
  - Basic structure
    - Mô tả client-server model: đơn giản cái trang web trên browser là client còn backend sẽ là cục server, nếu cần dữ liệu từ phía server, client sẽ gọi request và backend sẽ xử lí và trả về response.
    - Vai trò của HTTP request method GET, POST, PUT, PATCH, DELETE
      - Get an toàn để cache vì nó k thay đổi state server hay dữ liệu trong dB
      - Mấy thằng còn lại thì có thay đổi, không cache trên browser được
    - HTTP response status code: chỉ ra rằng API có trả về kết quả thành công hay không.
      - 1xx (Informational): để chỉ ra cái progress hiện tại của request chứ không là kết quả cuối cùng.
        - Code: 100 Continue
      - 2xx (Success): status code trong range này chỉ ra server đã nhận được request, hiểu và đã xử lý thành công request.
        - Code: 200 OK
      - 3xx (Redirection): để chỉ rằng cái request trước đó cần action của client để complete, bình thường là cho những action redirect.
        - Code 304: Not Modified (cache của client vẫn còa n khả dụng server báo người dùng có thể dùng bản copy của cache)
      - 4xx (Client errors): chỉ ra có lỗi từ phía clients
        - Code: 404 Not found
        - Code: 401 Bad request (wrong or invalid parameters)
      - 5xx (Server errors): chỉ ra request gặp lỗi từ hệ thống server
        - Code: 500 Internal server error: server gặp lỗi khi đang xử lí request
    - So sánh giữa HTTP headers và request body:
      - Giống nhau:
        - Đều là thành phần có trong request và response
      - Khác nhau:
        - HTTP headers: kèm theo trong request gồm header metadata, instruction và context, lên server và nhận lại từ server, quản lý thông tin liên quan đến request và response.
        - Body: chứa dữ liệu thực tế của request, chẳng hạn nhưu form data hoặc media file
    - Common headers và mục đích:
      - Content-Type: định nghĩa media type của request và response body, examples "Content-Type: application/json" chỉ ra content ở format là JSON.
      - User-Agent: định danh client hay user đã gọi request, thông thường là thông tin web browser hoặc application, giúp server hiểu được loại client và dự theo đó để optimize response.
      - Content-Length: chỉ ra độ dài chính xác của request và response theo bytes, giúp nhận biết chính xác kích thước của của content.
      - Authorization: chứa credentials hoặc token yêu cầu cho việc authentication, dùng để authenticate client với server và grant access để bảo vệ resource.
  - State management & Cookie:
    - HTTP là stateless protocal vì:
      - Không có sự kết nối chắc chắn giữa client và server: sau khi request được handle và trả về response thì connection giữ client và server cũng đóng.
      - Mỗi request độc lập với nhau, các request tự quản lí và có những payload cần thiết khác nhau để server xử lí.
      - Không có client context: server không bảo trì hoặc quản lí bất cứ state nào của client và cái hành vi trong quá khứ của client, mỗi request là riêng biệt server không lưu trữ thông tin của request trước đó
    - Mục đích của HTTP cookie: lưu một phần nhỏ dữ liệu trả về từ server, lưu trên browser và có thể gửi lại về backend trong các request sau.
    - Một số công dụng: quản lý phiên làm việc của user, tracking hoặc cá nhân hoá.
    - Khác nhau giữa first-party cookie và third party cookie:
      - First-party là khởi tạo từ trang web mà người dùng đang truy cập, giúp tăng trải nghiệm của user với trang web, thường lưu trư cài đặt của user, lưu trư phiên làm việc hoặc track hành động của user trên trang.
      - Third-party được khởi tạo từ 1 domain ngoài trang web, thường là từ cái social media platforms hoăc các service khác được nhúng vào trong web.
    - Mục đich của Secure và HTTP Only
      - Secure: giúp force chỉ truyền cái cookie lên header nếu protocal đang dùng là HTTPS
      - HTTP-Only: giúp prevent JS có thể access vào cookie thông qua API.
  - Content-Types/Mime-types
    - Mine-type là format của 1 chuỗi byte (thường là file), và browser sẽ có những hành vi, action khác nhau dựa trên mine-type do máy chủ gửi khi browser gửi tài nguyên đi.
    - Làm sao để browser và client sử dụng header để thương lượng nội dụng trình diện?
      - Client sẽ gửi "Accept" trong header của request để chỉ ra loại dữ liệu được chấp nhận cho response.
      - Server sẽ thêm "Content-type" vài header của response chỉ ra loại dữ liệu được của gửi đi và đại diện
    - Vì sao HTTP1 là plaintext protocal vì sao lại gửi được binary data?
      - Vẫn gửi được vì browser đã mã hoá dữ liệu (context ở đây là file) thành dạng base64 (chẳng hạn) và gửi lên. Dữ liệu nhị phân được encoded thành chuỗi cái kí tự ASCII sử dụng base64 encoding, dữ liệu sau khi encode sẽ được chuỗi hoá mà kèm vào trong HTTP request body, server sẽ decode và nhận về dữ liệu nguyên thuỷ.
      - Method 2 là sử dụng Multipart/Form-Data: thường dùng upload file, cái file sẽ được chia làm nhiều part, mỗi part đều có content type và header, những part này sẽ được đóng gói trong multipart/form-data của HTTP request, cho phép dữ liệu nhị phân được gửi như 1 phần của http request body trong khi vẫn giữ được sự liên kết giữa các part
  - HTTP Version: (Good to know)
    - V2:
      - Sử dụng dữ liệu nhị phân thay vì plaintext để giao tiếp giữ client và server, giúp giảm chi phí và truyền giữ liệu nhanh và hiệu quả hơn
      - Multiplexing: cho phép cùng 1 lúc có nhiều response và request trong 1 kết nối TCP.
      - Header compressing: nén header giúp giảm size của header, giảm bandwidth sử dụng.
    - V3:
      - Sử dụng transport Protocal là QUIC (Quick UDP Internet connection).
      - Tự động mã hoá toàn bộ việc giao tiếp giữa client và server.
- CSS:
  - Selector:
    - là patter hoặc rule dùng để select chính xác HTML element trên web page mà mình muốn thêm style với CSS, giúp mình target và thêm style cho elements dựa theo các tiêu chuẩn như loại element, class, ID, attribute và relation giữa các elements.
    - Vì có nhiều selector type như đề cập ở trên, vì thế mà sử dụng thêm combinators để tối ưu hoá việc select elements
      - div p: select tất cả thẻ p mà nằm trong thẻ dev
      - div > p: select tất cả p là con của div
      - div + p: select thẻ p đầu tiên sau div
      - div ~ p: select tất cả thẻ p sau div
  - Property: là tên các thuộc tính cài đặt của CSS
  - CSS function: dùng để tính toán (calc()) hoặc các biểu thức phức tạp (rgba(), linear-gradient(), translate())
  - Common CSS page layout techniques
    - Float based
    - Flex
    - Grid
    - Media queries
  - Inheritance work trong CSS ntn?
    - Các thuộc tính được set ở element cha sẽ được tự động thừa kế ở element con ví dụ là màu
  - Ý nghĩa của độ cụ thể khi sử dụng CSS:
    - Xét về bố cục cây HTML có 3 loại css: inline > internal > external CSS
    - Xét về tổng thể thì
      - Inline có độ ưu tiên cao nhất
      - ID selectors có độ ưu tiên cao
      - Class, attributes và pseudo-classes có độ ưu tiên vừa
      - Element types và pseudo-elements có độ ưu tiên thấp nhất
- DNS:
  - DNS Record cung cấp thông tin của domain
  - Common DNS record type: A, AAAA, TXT, CNAME, MX
  - Structure của DNS dựa theo thứ bật như cây:
    - Root zone: single dot ('.')
    - Top-level domains: .net, .com, .org (also country top-level-domain: .uk, .vn)
    - Second-level domains: unique and choose by domain owner: google.com
    - Subdomains là level phụ được thêm vào trước SLD: blog.google.com
    - Full Quailified Domain name: www.blog.google.com
  - TTL on a DNS record: chỉ ra sau bao lâu thì record nên được cache lại trước khi nó bị refresh
  - DNS resolver: dùng để truy vấn DNS để lấy địa chỉ IP hoặc dữ liệu liên quan đến domain đưa trước, nó đóng vai trò như máy trung gian giữ client với cơ sở hạ tầng của DNS.
  - Authoritative nameserver: là bên chính thức giữ DNS records cho 1 domain cụ thể, nó cung cấp quyền cho các câu truy vấn DNS cho domain, đóng vai trò trong quá trình phân giải DNS
  - Root name-server có nhiệm vụ quản lý các record Top-level domain
- Web Performance
  - Function của CDN: là mạng lưới máy chủ phân tán, cho phép content thể được tải trên clients từ server gần với client nhất từ đó cải thiện hiệu suất trang web.
  - Code Minification: giúp loại bỏ phần code dư thừa từ resource để giảm tải kích thước từ đó giảm tải thời gian load
  - Async & defer attributes trong script tag ảnh hưởng performance ntn:
    - Async: giúp page tránh việc bị block trong khi script đang được tải về
    - Defer: giúp page tránh việc bị block bởi vì script đang được execute, defer sẽ trì hoạn việc execute script cho đến khi HTML được load xong
  - Code-spliting:
    - Là 1 kĩ thuật dùng trong web development để chia nhỏ file JS bundle, thành cái part dễ quản lí gọi là chunks. Mục tiêu là chỉ load phần code (chunks) cho 1 trang cụ thể hoặc 1 chức năng, từ đó giảm tời gian load cũng như cải thiện performance. Khi chia nhỏ code thành các part nhỏ hơn, nó sẽ cho phép thực hiện lazy loading
  - Ảnh hưởng của Cache-Control header on performance: có tác động đáng kể đến performance ví dụ từ caching rules và expiration time, mình có thể tối ưu hoá hiệu quả của cacher, giảm độ trễ bằng cách truy xuất tài nguyên từ bộ đệm, giảm thiểu mức sử dụng bằng thông, nhưng vẫn đảm bảo độ mới của nội dịng và giảm tải cho máy chủ. Những ảnh hưởng này sẽ giúp tải trang nhanh hơn, giảm độ trễ mạng và tăng trải nghiệm người dùng.
- APIs
  - Technologies utilise to make HTTP request: fetch, xhr APIs, jQuery Ajax.
  - Mô tả REST:
    - REST là style kiến trúc phổ biến đẩy xây dựng web application
    - Client-Server Architecture: REST chia ra client (UI, web/app) và server (nơi lưu trư và xử lí data), phân chia ra thì dễ quản lí, maintain cũng như scale mỗi thằng
    - Statelessness: REST thì stateless, server không quản lý bất cứ state nào của client, mỗi request từ client gửi lên server phải chưa đủ dữ liệu để server hiểu và xử lí.
    - Định danh resource: REST sử dụng URIs để định danh duy nhất 1 resource và sử dụng HTTP method để support quá trình xử lí, tương tác với resource.
  - Rate-limit:
    - Công dụng: thêm rate-limit sẽ giúp ngăn chặn việc 1 service bị quá tải.
    - Nên làm gì ở hướng client khi dính rate-limit:
      - Server có thể trả về status code 429 - Too many request, client nên nhận ra và có những action cần thiết.
      - Prevent user và tạo bộ đếm thời gian chẳng hạn, sau khi hết thì mới allow user thực hiện lại request.
      - Nên log lỗi và thông báo đến người dùng hoặc có những action nếu có những requirement liên quan đến nó.
  - Mô tả và đối chiếu các methods implement API authentication:
    - Basic Auth:
      - Đơn giản nhất, phía client sẽ gửi username & password trực tiếp trong request header.
      - Server sẽ grant access nếu mà thông tin gửi lên đúng.
      - Mặc dù username và password được encoded theo base64 nhưng mà vẫn rất risk vì dễ bị mã hoá ngược lại và credentials này mỗi request cần auth đều phải gửi lên lại.
    - Bearer Tokens:
      - Được sử dụng rộng rãi cho stateless authentication
      - Client sẽ lưu dưới storage token và gửi nó lên trong "Authorization" header API cần permission (prefix sẽ là Bearer)
      - Server sẽ validate và cho phép truy cập nếu token đúng.
      - Token này có thời hạn sống ngắn và cần phải renew 1 cái mới nếu hết hạn.
      - Token này có thể được dùng trong hệ thống hoặc các third-party provide authentication
    - Cookies:
      - Server set cookie session trong cookie sau khi đăng nhập thành công, mỗi lần client call request thì cookie sẽ tự thêm vào header, với mỗi request chung domain, server sẽ validate session trong cookie để authorize user.
      - Cookie có thể bị tấn công XSS và cần có biện pháp bảo mật hơn, 1 cách là enable Secure và HTTP Only
    - OAuth:
      - Là authentication và authorization framework.
      - Nó cho third-party access resource nhưng mà không share cái credentials của owner
      - Oauth support nhiều grant type như Authorization code, Implicitm Client credentials, and refresh token tuỳ theo yêu cầu hệ thống
- Security
  - HTTPS là gì?
    - HTTPS là phiên bản mã hoá HTTP, mục đích của HTTPS là đảm bảo những content được vận chuyển trong request hay response sẽ không thể bị đọc nếu bị chặn bởi hacker.
  -
- Front-end Development

  - Ưu và nhược của SPA & SSR:
    Server Side Rendering (SSR) và Client Side Rendering (CSR) là hai phương pháp khác nhau để tạo và hiển thị giao diện người dùng (UI) trong ứng dụng web. Dưới đây là sự so sánh giữa Server Side Rendering và Client Side Rendering:

  1.  **Server Side Rendering (SSR):**

  - SSR là quá trình tạo và hiển thị giao diện người dùng trên máy chủ trước khi trình duyệt của người dùng nhận được nội dung.
  - Khi một trang web sử dụng SSR, trình duyệt yêu cầu trang từ máy chủ, máy chủ xử lý yêu cầu và tạo ra trang hoàn chỉnh (bao gồm dữ liệu và giao diện) trước khi gửi trả về trình duyệt.
  - Vì trang web đã được tạo sẵn tại máy chủ, nên thời gian tải trang đầu tiên có thể lâu hơn so với CSR. Tuy nhiên, người dùng thường nhận được nội dung cơ bản ngay từ đầu.
  - SSR thích hợp cho các trang web có nội dung tĩnh hoặc ít thay đổi, hoặc khi cần tối ưu hóa SEO.

  2.  **Client Side Rendering (CSR):**

  - CSR là quá trình tạo và hiển thị giao diện người dùng trong trình duyệt của người dùng bằng cách sử dụng JavaScript sau khi trang web đã tải xong.
  - Khi một trang web sử dụng CSR, trình duyệt tải các tệp HTML, CSS và JavaScript cơ bản từ máy chủ, sau đó sử dụng JavaScript để tạo và điều khiển giao diện người dùng.
  - Với CSR, trang web có thể cảm thấy nhanh và tương tác, nhưng việc trang web cần phải tải và xử lý dữ liệu sau khi tải xong có thể dẫn đến một khoảng thời gian trống trước khi nội dung xuất hiện.
  - CSR thích hợp cho các ứng dụng web động, có nhiều tương tác và thay đổi dữ liệu thường xuyên.

    Tóm lại, sự lựa chọn giữa SSR và CSR phụ thuộc vào loại ứng dụng bạn đang phát triển và yêu cầu cụ thể của nó. SSR thường phù hợp cho việc tối ưu hóa SEO và cung cấp nội dung cơ bản ngay từ đầu, trong khi CSR thường phù hợp cho việc xây dựng các ứng dụng web động và tương tác cao.

    - Single Page Application:
      - Ưu:
        - Tăng trải nghiệm người dùng khi sử dụng, cho phép người dùng update content mà không phải reload lại cả page
        - Chuyển trang nhanh chóng hơn: sau khi init page được load, việc chuyển page sẽ nhanh hơn vì chỉ có data được fetch hoặc component được rerender lại.
        - Có nhiều UI framework, hỗ trợ nhiều tool mạnh mẽ để build trang web phức tạp và quản lý state.
      - Nhược:
        - Initial load time có thể lâu vì phải bao gồm cả assets và JS framework.
        - SEO không tốt.
        - Sẽ bị giới hạn vì hoạt động nhiều bên client-side, nếu máy user k đủ đám ứng sẽ dẫn đến low performance.
        - Phức tạp khi build và bảo trì 1 SPA, vì cần phải handle routing, state management, và xử lí bật đồng bộ khi làm việc với server
    - Server side rendering:
      - Ưu:
        - Cải thiện tốc độ initial.
        - SEO tốt.
        - Truy cập tốt cho mọi thiết bị.
      - Nhược:
        - Chuyển page chậm.
        - Làm tăng thời gian server load.
        - Hạn chế thao tác trên client-side.
        - Framework, thư viên còn hạn chế.
    - -> Chọn SPA khi cần tăng trải nghiệm ng dùng, real-time updates, UI đẹp :)), chọn SSR khi ưu tiên việc load ban đầu, SEO và khả năng truy cập, cân nhắc kết hợp cả 2 cũng được, SSR cho mấy trang crit còn SPA cho mấy trang user interactive nhiều.

  - JS module: là cơ chế để chia các ứng dụng JS thành các đoạn mã riêng biệt, có thể tái sử dụng và load độc lập
  - Vì sao JS, CSS, HTML trình duyệt tự hiểu được nma vẫn cần build tool, vì sao cái này cần thiết?:
    - Code Optimization & Transformation: build tool có thể tối ưu hoá code bằng cách nén và chuyển đổi, đồng thời cho phép viết code JS hiện đại sau đó chuyển đổi thành phiên bản tương thích với các trình duyệt cũ . Cải thiện thời gian và hiệu suất tải.
    - Assets Management & Transformation: FE build tool giúp quản lý và tối ưu nhiều loại tài nguyên như ảnh font chữ, stylesheeets. Có thể tự động nén ảnh và sinh ra bản tối ưu hơn cho kích thước của màn hình
    - Development Workflow Enhancements: build tools cung cấp những feature như hot reloading (browser tự động refresh khi có thay đổi), hot module replacement (chỉ update module thay vì reload lại cả page), error reporting để cải thiện quá trình code của developer.
    - Cross-Browser Compatibility: tự động add các prefix cần thiết cho CSS properties, đảm báo style correct khi dùng giữa các browser khác nhau.

  1.  `Những điểm khác nhau giữa NEXTJS và REACTJS là gì `\
      Next.js và React.js là hai công nghệ phổ biến trong việc phát triển ứng dụng web. Dưới đây là những điểm khác nhau chính giữa chúng:

      1. **Khung ứng dụng và tích hợp SSR (Server-Side Rendering):**

         - React.js: Là một thư viện JavaScript dùng để xây dựng giao diện người dùng. React.js không cung cấp cơ chế SSR tự động.
         - Next.js: Là một framework React, đi kèm với SSR (Server-Side Rendering) và cung cấp tích hợp sẵn cho việc SSR. Điều này giúp trang web được tải nhanh hơn bằng cách tạo các trang động trên máy chủ và trả về HTML hoàn chỉnh cho trình duyệt.

      2. **Routing (Định tuyến):**

         - React.js: Cần sử dụng thư viện bên ngoài như React Router để xử lý định tuyến.
         - Next.js: Cung cấp hệ thống định tuyến tích hợp sẵn. Bạn có thể tạo các trang React và tự động định tuyến mà không cần phải cấu hình nhiều.

      3. **Cấu hình và cài đặt ban đầu:**

         - React.js: Yêu cầu cấu hình ban đầu tương đối đơn giản, chỉ cần một số công cụ hỗ trợ như Babel và Webpack để bắt đầu xây dựng ứng dụng.
         - Next.js: Cung cấp môi trường phát triển đã được cấu hình sẵn, không cần bạn phải tùy chỉnh nhiều cho các tính năng căn bản như SSR và định tuyến.

      4. **Tối ưu hóa và Performance (Hiệu suất):**

         - React.js: Yêu cầu bạn tự quản lý và tối ưu hiệu suất ứng dụng của mình.
         - Next.js: Đã được tối ưu hóa sẵn cho hiệu suất tốt nhất. Các trang được tải nhanh và cơ chế SSR giúp tránh việc phải tải toàn bộ trang trước khi hiển thị cho người dùng.

      5. **Môi trường phát triển và triển khai:**
         - React.js: Đa phần sử dụng trong môi trường phát triển trình duyệt (client-side) và cần phải tích hợp thêm các công nghệ khác nhau để triển khai ứng dụng vào máy chủ (server).
         - Next.js: Được xây dựng sẵn với SSR, giúp dễ dàng triển khai ứng dụng lên máy chủ hoặc nền tảng dịch vụ đám mây.

      Tóm lại, Next.js là một framework xây dựng trên nền tảng React.js, bổ sung các tính năng quan trọng như SSR và định tuyến tích hợp sẵn để giúp bạn dễ dàng xây dựng các ứng dụng web với hiệu suất cao và trải nghiệm người dùng tốt hơn.

  2. ``Component life cycle trong react là gì ? ``

      Trong React, các component life cycle (vòng đời của component) là chuỗi các phương thức mà component của bạn sẽ thông qua trong quá trình khởi tạo, cập nhật và hủy bỏ. Các phương thức này cho phép bạn thực hiện các hành động cụ thể tại các giai đoạn khác nhau trong quá trình mà component được tạo ra, hiển thị và biến đổi.
      Dưới đây là các phương thức life cycle chính trong React và mô tả ngắn gọn về mỗi phương thức:

      1. **Mounting (Khởi tạo):**

         - `constructor()`: Được gọi đầu tiên khi component được khởi tạo. Bạn có thể thiết lập state và bind các phương thức ở đây.
         - `static getDerivedStateFromProps()`: Được gọi trước khi component được hiển thị lần đầu tiên và sau mỗi lần cập nhật props. Phương thức này được sử dụng để tính toán và trả về state mới dựa trên props mới.
         - `render()`: Phương thức này trả về JSX để hiển thị nội dung của component.

      2. **Updating (Cập nhật):**

         - `shouldComponentUpdate()`: Được gọi trước khi component được cập nhật. Bạn có thể kiểm tra xem liệu việc cập nhật có cần thiết hay không bằng cách so sánh props mới và props hiện tại, hoặc state mới và state hiện tại.
         - `getSnapshotBeforeUpdate()`: Được gọi trước khi các thay đổi được áp dụng vào DOM. Phương thức này cho phép bạn lấy thông tin từ DOM (ví dụ: vị trí cuộn) trước khi cập nhật để sau đó dùng trong `componentDidUpdate()`.
           - `componentDidUpdate()`: Được gọi sau khi component đã được cập nhật. Ở đây, bạn có thể thực hiện các thao tác sau khi cập nhật xảy ra, như làm sạch dữ liệu không cần thiết hoặc tương tác với DOM.

      3. **Unmounting (Hủy bỏ):**
         - `componentWillUnmount()`: Được gọi trước khi component bị hủy bỏ và bị gỡ khỏi DOM. Bạn nên dọn dẹp các tài nguyên không cần thiết ở đây, như huỷ các subscriptions, hủy các kết nối mạng, v.v.

      Ngoài ra, từ phiên bản React 16.3 trở đi, một số phương thức life cycle đã bị lược bỏ và thay thế bằng các phương thức mới để đảm bảo hiệu suất tốt hơn và hỗ trợ React Hooks. Ví dụ, `componentWillReceiveProps()` đã bị thay thế bằng `static getDerivedStateFromProps()`, và `componentWillUpdate()` bị thay thế bằng `getSnapshotBeforeUpdate()`.

Trong các phiên bản mới nhất của React, bạn cũng có thể sử dụng React Hooks để thay thế các phương thức life cycle và quản lý state một cách dễ dàng hơn.

3. `React hooks trong react js là gì `

   React Hooks là một tính năng được giới thiệu trong phiên bản React 16.8, cho phép bạn sử dụng các tính năng của React như state và lifecycle trong các thành phần hàm (functional components) thay vì phải sử dụng các thành phần lớp (class components). Điều này giúp viết mã ngắn gọn hơn, dễ đọc và dễ quản lý hơn.

   Các hooks được xây dựng sẵn trong React bao gồm:

   1. **useState**: Dùng để thêm state vào trong functional component. Hook này giúp bạn theo dõi và cập nhật trạng thái của component. Ví dụ:

   ```jsx
   import React, { useState } from "react";

   function Counter() {
     const [count, setCount] = useState(0);

     const increment = () => setCount(count + 1);
     const decrement = () => setCount(count - 1);

     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={increment}>Increment</button>
         <button onClick={decrement}>Decrement</button>
       </div>
     );
   }
   ```

   2. **useEffect**: Dùng để thực hiện các tác vụ liên quan đến side-effect, chẳng hạn như thực hiện API call, đăng ký sự kiện DOM, và làm sạch tài nguyên không cần thiết khi component bị hủy bỏ. Ví dụ:

   ```jsx
   import React, { useState, useEffect } from "react";

   function Example() {
     const [data, setData] = useState(null);

     useEffect(() => {
       fetch("https://api.example.com/data")
         .then((response) => response.json())
         .then((data) => setData(data))
         .catch((error) => console.error(error));
     }, []);

     return <div>{data ? <p>Data: {data}</p> : <p>Loading...</p>}</div>;
   }
   ```

   3. **useContext**: Dùng để truy cập context được tạo bởi `React.createContext` từ bất kỳ đâu trong component tree. Ví dụ:

   ```jsx
   import React, { useContext } from "react";
   import { MyContext } from "./MyContext";

   function MyComponent() {
     const data = useContext(MyContext);

     return (
       <div>
         <p>Data from Context: {data}</p>
       </div>
     );
   }
   ```

   4. **useReducer**: Dùng để quản lý state của component bằng cách sử dụng một reducer function, tương tự như Redux. Ví dụ:

   ```jsx
   import React, { useReducer } from "react";

   const initialState = { count: 0 };

   function reducer(state, action) {
     switch (action.type) {
       case "INCREMENT":
         return { count: state.count + 1 };
       case "DECREMENT":
         return { count: state.count - 1 };
       default:
         return state;
     }
   }

   function Counter() {
     const [state, dispatch] = useReducer(reducer, initialState);

     return (
       <div>
         <p>Count: {state.count}</p>
         <button onClick={() => dispatch({ type: "INCREMENT" })}>
           Increment
         </button>
         <button onClick={() => dispatch({ type: "DECREMENT" })}>
           Decrement
         </button>
       </div>
     );
   }
   ```

   Với sự hỗ trợ của React Hooks, bạn có thể viết các functional component với khả năng quản lý state và side-effect như class component mà không cần sử dụng class và các phương thức lifecycle truyền thống. Điều này giúp mã ngắn gọn và dễ đọc hơn, cũng như giúp bạn tận dụng các tính năng mới của React một cách hiệu quả.

4. `useEffect trong reactjs là gì ? Cách thức sử dụng useEffect trong reactjs ?`

   Trong React, `useEffect` là một trong những React Hook cơ bản, cho phép bạn thực hiện các side-effect trong functional components. Side-effect là những tác vụ không liên quan trực tiếp đến việc render giao diện, chẳng hạn như gọi API, đăng ký sự kiện DOM, hoặc làm sạch tài nguyên không cần thiết.

   Cách sử dụng `useEffect`:

   1. **Cài đặt `useEffect`**: Bạn có thể sử dụng `useEffect` bằng cách import nó từ thư viện React và gọi nó trong functional component. `useEffect` nhận vào một hàm callback làm tham số đầu tiên, và một mảng tham số thứ hai (tuỳ chọn) chứa các dependencies.

   ```jsx
   import React, { useEffect } from "react";

   function MyComponent() {
     useEffect(() => {
       // Thực hiện các tác vụ side-effect ở đây
       console.log("Component đã được render");

       // Return một hàm clean-up (tuỳ chọn)
       return () => {
         console.log("Component bị hủy bỏ");
       };
     }, []);

     return <div>My Component</div>;
   }
   ```

   2. **Dependency Array**: Tham số thứ hai của `useEffect` là một mảng chứa các dependencies (phụ thuộc). Nếu bạn muốn `useEffect` chỉ được gọi lại khi các giá trị trong mảng dependencies thay đổi, bạn nên cung cấp mảng dependencies này. Nếu mảng dependencies trống (không chứa bất kỳ giá trị nào), `useEffect` chỉ được gọi một lần sau khi component được khởi tạo.

   ```jsx
   import React, { useState, useEffect } from "react";

   function Counter() {
     const [count, setCount] = useState(0);

     useEffect(() => {
       console.log("Component đã render hoặc count thay đổi");
     }, [count]);

     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={() => setCount(count + 1)}>Increment</button>
         <button onClick={() => setCount(count - 1)}>Decrement</button>
       </div>
     );
   }
   ```

   Trong ví dụ trên, khi bạn nhấn vào nút "Increment" hoặc "Decrement", state `count` thay đổi, từ đó sẽ gọi lại hàm callback trong `useEffect`, và xuất hiện thông báo "Component đã render hoặc count thay đổi" trên console.

   3. **Clean-up function**: Bạn có thể sử dụng return của hàm callback trong `useEffect` để thực hiện các công việc dọn dẹp khi component bị hủy bỏ. Điều này giúp tránh rò rỉ bộ nhớ và quản lý tài nguyên một cách tốt hơn.

   ```jsx
   import React, { useEffect } from "react";

   function MyComponent() {
     useEffect(() => {
       console.log("Component đã được render");

       // Return một hàm clean-up
       return () => {
         console.log("Component bị hủy bỏ");
         // Thực hiện các tác vụ dọn dẹp (nếu cần)
       };
     }, []);

     return <div>My Component</div>;
   }
   ```

   Khi component bị hủy bỏ, `useEffect` sẽ gọi hàm clean-up trước khi nó bị hủy, cho phép bạn làm sạch dữ liệu và huỷ các subscriptions hoặc đăng ký sự kiện.

5. `Virtual dom trong reactjs là gì`

   Trong ReactJS, Virtual DOM (DOM ảo) là một khái niệm quan trọng và là một phần chính của cách React hoạt động. Virtual DOM là một biểu diễn ảo (bản sao) của cấu trúc DOM thực tế trên trình duyệt và được React sử dụng để quản lý sự thay đổi và cập nhật giao diện người dùng một cách hiệu quả.

   Khi bạn xây dựng một ứng dụng React, React sẽ sử dụng Virtual DOM để theo dõi trạng thái (state) của ứng dụng và xác định sự thay đổi nào cần được cập nhật trên giao diện người dùng. Quá trình này giúp tối ưu hóa hiệu suất bằng cách giảm số lượng lần thay đổi trực tiếp trên DOM thực tế.

   Cơ chế hoạt động của Virtual DOM như sau:

   1. Bắt đầu với trạng thái ban đầu: React sử dụng dữ liệu trạng thái hiện tại để xây dựng một Virtual DOM ban đầu.

   2. Render Virtual DOM: React sử dụng thông tin từ Virtual DOM để tạo ra một cấu trúc DOM ảo, mô tả cách giao diện người dùng sẽ được hiển thị.

   3. So sánh với DOM trước: Sau mỗi lần render, React so sánh Virtual DOM mới với Virtual DOM trước đó.

   4. Xác định sự thay đổi: React tìm ra sự khác biệt giữa Virtual DOM mới và Virtual DOM cũ. Điều này giúp xác định những phần tử nào thực sự cần được cập nhật lên DOM thực tế.

   5. Thực hiện cập nhật: React chỉ cập nhật các phần tử thay đổi mà không cần phải làm lại toàn bộ DOM. Điều này giúp giảm thiểu tải lên trình duyệt và cải thiện hiệu suất.

   Nhờ sử dụng Virtual DOM, React giúp tối ưu hóa quá trình cập nhật giao diện người dùng và cải thiện hiệu suất ứng dụng. Khi bạn cập nhật trạng thái của ứng dụng trong React, React sẽ xây dựng một Virtual DOM mới, so sánh với Virtual DOM cũ và chỉ cập nhật những phần thay đổi thực sự lên DOM thực tế. Điều này giúp giảm thiểu overhead và làm cho ứng dụng chạy nhanh hơn và mượt mà hơn.

6. `useState trong react là gì`

   Trong React, "useState" là một trong những Hook (cụ thể là State Hook) được cung cấp bởi thư viện React Hooks. Nó cho phép bạn sử dụng trạng thái (state) trong các thành phần hàm (functional components) của ứng dụng React. Trước khi có Hook, trạng thái chỉ có thể được sử dụng trong các thành phần dựa trên lớp (class components), nhưng giờ đây với Hook, bạn có thể sử dụng trạng thái trong cả hai loại thành phần (hàm và lớp).

   Để sử dụng useState trong một thành phần hàm, bạn cần import nó từ thư viện React và sau đó gọi nó trong cơ thể của thành phần. useState trả về một mảng với hai phần tử: giá trị trạng thái hiện tại và hàm để cập nhật trạng thái đó.

   Dưới đây là cách sử dụng useState trong một thành phần hàm:

   ```jsx
   import React, { useState } from "react";

   function ExampleComponent() {
     // Khai báo trạng thái (state) bằng cách sử dụng useState
     const [count, setCount] = useState(0);

     // Hàm xử lý sự kiện để tăng giá trị count lên 1
     const handleIncrement = () => {
       setCount(count + 1);
     };

     return (
       <div>
         <p>Giá trị count: {count}</p>
         <button onClick={handleIncrement}>Tăng</button>
       </div>
     );
   }

   export default ExampleComponent;
   ```

   Trong ví dụ trên, chúng ta sử dụng useState để khai báo một trạng thái có tên là "count" và khởi tạo giá trị ban đầu của nó là 0. useState trả về một mảng với hai phần tử: "count" là giá trị trạng thái hiện tại và "setCount" là hàm để cập nhật trạng thái đó. Chúng ta sử dụng setCount để tăng giá trị "count" lên 1 mỗi khi người dùng nhấn vào nút "Tăng".

   Khi người dùng nhấn nút, React sẽ tự động kích hoạt lại hàm ExampleComponent với giá trị trạng thái mới, và giao diện người dùng sẽ được cập nhật với giá trị "count" mới.

# Javascripts

## ES6 trong Javascript

ES6 (ECMAScript 6), còn được gọi là ECMAScript 2015, là một phiên bản tiêu chuẩn của ngôn ngữ JavaScript. Nó được phát hành vào năm 2015 và mang đến nhiều tính năng mới và cải tiến so với phiên bản trước đó của ECMAScript.

Dưới đây là một số tính năng quan trọng của ES6:

1. Khai báo biến với `let` và `const`: ES6 giới thiệu hai từ khóa mới để khai báo biến. `let` cho phép bạn khai báo một biến có phạm vi chỉ trong block nơi nó được khai báo, trong khi `const` khai báo một hằng số không thể được gán lại giá trị sau khi khởi tạo.

2. Arrow functions: Arrow functions là một cú pháp viết ngắn gọn cho việc tạo hàm trong JavaScript. Chúng giúp rút gọn cú pháp và cung cấp quy tắc ràng buộc `this` rõ ràng.

3. Template literals: Template literals cho phép bạn tạo chuỗi với cú pháp dễ đọc hơn bằng cách sử dụng backticks để bao quanh chuỗi và chèn biểu thức vào bên trong chuỗi bằng cú pháp `${expression}`.

4. Default parameters: ES6 cho phép bạn định nghĩa giá trị mặc định cho các tham số của một hàm. Khi gọi hàm mà không truyền giá trị cho các tham số đó, giá trị mặc định sẽ được sử dụng.

5. Destructuring assignment: Destructuring assignment cho phép bạn trích xuất các giá trị từ một mảng hoặc đối tượng và gán chúng vào các biến riêng lẻ một cách dễ dàng.

6. Classes: ES6 giới thiệu cú pháp lớp để tạo đối tượng trong JavaScript. Lớp cung cấp một cách tiện lợi để định nghĩa các đối tượng và phương thức liên quan.

7. Modules: ES6 hỗ trợ modules, cho phép bạn tách các đoạn mã thành các tệp riêng biệt và import/export chúng giữa các tệp khác nhau. Điều này giúp quản lý mã nguồn dễ dàng hơn và khả năng tái sử dụng cao hơn.

## ES7

ES7 (ECMAScript 2016) là một phiên bản tiêu chuẩn của ngôn ngữ JavaScript, được phát hành vào năm 2016. ES7 không có nhiều thay đổi lớn so với ES6, nhưng nó đưa vào ngôn ngữ một số tính năng mới quan trọng. Dưới đây là một số tính năng chính của ES7:

1. `Array.prototype.includes()`: Phương thức `includes()` được thêm vào đối tượng `Array.prototype`, cho phép kiểm tra xem một mảng có chứa một phần tử cụ thể hay không. Phương thức trả về `true` nếu phần tử được tìm thấy và `false` nếu không tìm thấy.

2. `Exponentiation operator (**)`: Toán tử mũ (`**`) được thêm vào ngôn ngữ JavaScript để thực hiện phép tính lũy thừa. Ví dụ, `2 ** 3` sẽ trả về kết quả là 8.

3. `Object.values()` và `Object.entries()`: Hai phương thức `Object.values()` và `Object.entries()` được thêm vào đối tượng `Object`, giúp lấy các giá trị của thuộc tính và các cặp [key, value] của đối tượng một cách dễ dàng.

4. `Async functions`: ES7 giới thiệu từ khóa `async` và `await`, cho phép viết mã bất đồng bộ theo cách tuần tự và dễ đọc hơn. `async` được sử dụng để khai báo một hàm bất đồng bộ, trong khi `await` dùng để đợi kết quả của một biểu thức bất đồng bộ trước khi tiếp tục thực hiện.

Đây là một số tính năng chính của ES7. Các phiên bản tiếp theo như ES8, ES9 và ES10 đã đưa thêm nhiều tính năng mới và cải tiến khác cho ngôn ngữ JavaScript.

1.  `Explain Null and Undefined in JavaScript`  
    Trong nhiều ngôn ngữ lập trình, bao gồm JavaScript, "null" và "undefined" là hai giá trị đặc biệt được sử dụng để biểu thị sự thiếu vắng của dữ liệu hoặc trạng thái không xác định. Mặc dù chúng có thể có sự tương đồng, nhưng cũng có sự khác biệt quan trọng giữa chúng:

    1.  **Undefined (Không xác định):**

        - "Undefined" là giá trị mà một biến có thể có khi nó đã được khai báo, nhưng chưa được gán giá trị.
        - Một biến có thể trở thành "undefined" khi được khai báo nhưng không được gán giá trị hoặc khi truy cập vào một thuộc tính không tồn tại của một đối tượng.
        - Ví dụ:

          ```javascript
          let x;
          console.log(x); // undefined

          let obj = {};
          console.log(obj.property); // undefined
          ```

    2.  **Null (Trống):**

        - "Null" là giá trị biểu thị một biến đã được khởi tạo và gán giá trị là "null".
        - Điều này thường được sử dụng khi bạn muốn rõ ràng chỉ định rằng một biến không có giá trị hoặc chưa có dữ liệu.
        - "Null" thường được sử dụng trong các tình huống ngữ cảnh hợp lý, ví dụ như khi bạn muốn đặt một biến trạng thái của đối tượng thành "không có dữ liệu".
        - Ví dụ:

          ```javascript
          let y = null;
          console.log(y); // null

          let user = {
            name: null,
            age: 25,
          };
          console.log(user.name); // null
          ```

    Tóm lại, "undefined" thường xuất hiện khi một biến không có giá trị hoặc khi truy cập vào thuộc tính không tồn tại của đối tượng, trong khi "null" thường được sử dụng để biểu thị rõ ràng sự thiếu vắng của dữ liệu hoặc trạng thái không xác định.

2.  `What is strict mode`

    Strict Mode is a new feature in ECMAScript 5 that allows you to place a program, or a function, in a "strict" operating context. This strict context prevents certain actions from being taken and throws more exceptions.

3.  `Array method trong javascript`

    JavaScript cung cấp nhiều phương thức có sẵn để làm việc với mảng. Dưới đây là một số array method thông dụng và cách sử dụng chúng:

    1.  **Array.prototype.forEach()**: Dùng để lặp qua từng phần tử của mảng và thực hiện một hành động nào đó trên từng phần tử.

    ```javascript
    const numbers = [1, 2, 3, 4];

    numbers.forEach((number) => {
      console.log(number);
    });
    ```

    2.  **Array.prototype.map()**: Dùng để tạo một mảng mới bằng cách ánh xạ (mapping) qua từng phần tử của mảng gốc.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const doubledNumbers = numbers.map((number) => {
      return number * 2;
    });

    console.log(doubledNumbers); // Output: [2, 4, 6, 8]
    ```

    3.  **Array.prototype.filter()**: Dùng để tạo một mảng mới chỉ chứa các phần tử thỏa mãn điều kiện trong hàm callback.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const evenNumbers = numbers.filter((number) => {
      return number % 2 === 0;
    });

    console.log(evenNumbers); // Output: [2, 4]
    ```

    4.  **Array.prototype.reduce()**: Dùng để tích hợp các phần tử của mảng lại thành một giá trị duy nhất.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const sum = numbers.reduce((accumulator, currentValue) => {
      return accumulator + currentValue;
    }, 0);

    console.log(sum); // Output: 10
    ```

    5.  **Array.prototype.find()**: Dùng để tìm phần tử đầu tiên trong mảng thỏa mãn điều kiện trong hàm callback.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const foundNumber = numbers.find((number) => {
      return number > 2;
    });

    console.log(foundNumber); // Output: 3
    ```

    6.  **Array.prototype.findIndex()**: Tương tự như `find()`, nhưng trả về chỉ số của phần tử thỏa mãn điều kiện.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const foundIndex = numbers.findIndex((number) => {
      return number > 2;
    });

    console.log(foundIndex); // Output: 2 (Chỉ số của số 3)
    ```

    7.  **Array.prototype.some()**: Kiểm tra xem có ít nhất một phần tử trong mảng thỏa mãn điều kiện trong hàm callback hay không.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const hasEvenNumber = numbers.some((number) => {
      return number % 2 === 0;
    });

    console.log(hasEvenNumber); // Output: true
    ```

    8.  **Array.prototype.every()**: Kiểm tra xem tất cả các phần tử trong mảng có thỏa mãn điều kiện trong hàm callback hay không.

    ```javascript
    const numbers = [1, 2, 3, 4];

    const allEvenNumbers = numbers.every((number) => {
      return number % 2 === 0;
    });

    console.log(allEvenNumbers); // Output: false
    ```

    Đây chỉ là một số ví dụ về array method trong JavaScript. Có nhiều array method khác nữa, hãy tìm hiểu thêm để tận dụng tối đa các tính năng mạnh mẽ của mảng trong JavaScript.

4.  `String method trong javascript ? `

    JavaScript cung cấp nhiều phương thức (method) để làm việc với chuỗi (string). Dưới đây là một số string method phổ biến và cách sử dụng chúng:

    1.  **String.prototype.length**: Trả về độ dài của chuỗi.

    ```javascript
    const myString = "Hello, world!";
    const length = myString.length;
    console.log(length); // Output: 13
    ```

    2.  **String.prototype.indexOf()**: Tìm vị trí đầu tiên của một chuỗi con trong chuỗi ban đầu. Trả về chỉ số của ký tự đầu tiên nếu tìm thấy, hoặc -1 nếu không tìm thấy.

    ```javascript
    const myString = "Hello, world!";
    const index = myString.indexOf("world");
    console.log(index); // Output: 7
    ```

    3.  **String.prototype.lastIndexOf()**: Tìm vị trí cuối cùng của một chuỗi con trong chuỗi ban đầu. Trả về chỉ số của ký tự đầu tiên nếu tìm thấy, hoặc -1 nếu không tìm thấy.

    ```javascript
    const myString = "Hello, world!";
    const lastIndex = myString.lastIndexOf("o");
    console.log(lastIndex); // Output: 8
    ```

    4.  **String.prototype.slice()**: Trích xuất một phần của chuỗi dựa trên chỉ số bắt đầu và kết thúc.

    ```javascript
    const myString = "Hello, world!";
    const extractedString = myString.slice(0, 5);
    console.log(extractedString); // Output: "Hello"
    ```

    5.  **String.prototype.substring()**: Tương tự như `slice()`, nhưng không cho phép chỉ số âm.

    ```javascript
    const myString = "Hello, world!";
    const extractedString = myString.substring(0, 5);
    console.log(extractedString); // Output: "Hello"
    ```

    6.  **String.prototype.substr()**: Trích xuất một phần của chuỗi dựa trên chỉ số bắt đầu và độ dài của chuỗi con.

    ```javascript
    const myString = "Hello, world!";
    const extractedString = myString.substr(0, 5);
    console.log(extractedString); // Output: "Hello"
    ```

    7.  **String.prototype.replace()**: Thay thế một chuỗi con bằng một chuỗi khác trong chuỗi ban đầu.

    ```javascript
    const myString = "Hello, world!";
    const replacedString = myString.replace("world", "universe");
    console.log(replacedString); // Output: "Hello, universe!"
    ```

    8.  **String.prototype.toUpperCase()**: Chuyển đổi chuỗi thành dạng chữ in hoa.

    ```javascript
    const myString = "Hello, world!";
    const upperCaseString = myString.toUpperCase();
    console.log(upperCaseString); // Output: "HELLO, WORLD!"
    ```

    9.  **String.prototype.toLowerCase()**: Chuyển đổi chuỗi thành dạng chữ thường.

    ```javascript
    const myString = "Hello, world!";
    const lowerCaseString = myString.toLowerCase();
    console.log(lowerCaseString); // Output: "hello, world!"
    ```

    10. **String.prototype.trim()**: Loại bỏ khoảng trắng (hoặc các ký tự khác nếu được chỉ định) từ hai đầu chuỗi.

    ```javascript
    const myString = "   Hello, world!   ";
    const trimmedString = myString.trim();
    console.log(trimmedString); // Output: "Hello, world!"
    ```

    11. **charAt**: Trả về ký tự trong chuỗi

    ```javascript
    const str = "Hello, World!";
    console.log(str.charAt(0)); // Output: "H"
    ```

    Đây là một số string method trong JavaScript. Có nhiều method khác nữa, hãy tìm hiểu thêm để sử dụng chúng trong công việc của bạn.

5.  `Object method trong javascript ?`

    JavaScript cung cấp một số phương thức (method) có sẵn cho đối tượng (object). Dưới đây là một số object method phổ biến và cách sử dụng chúng:

    1.  **Object.keys()**: Trả về một mảng chứa tất cả các khóa (keys) của đối tượng.

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
      occupation: "Engineer",
    };

    const keys = Object.keys(myObject);
    console.log(keys); // Output: ["name", "age", "occupation"]
    ```

    2.  **Object.values()**: Trả về một mảng chứa tất cả các giá trị (values) của đối tượng.

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
      occupation: "Engineer",
    };

    const values = Object.values(myObject);
    console.log(values); // Output: ["John", 30, "Engineer"]
    ```

    3.  **Object.entries()**: Trả về một mảng chứa các cặp [key, value] của đối tượng.

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
      occupation: "Engineer",
    };

    const entries = Object.entries(myObject);
    console.log(entries);
    // Output:
    // [["name", "John"], ["age", 30], ["occupation", "Engineer"]]
    ```

    4.  **Object.assign()**: Kết hợp các đối tượng thành một đối tượng mới hoặc cập nhật các thuộc tính của đối tượng đích với các thuộc tính từ các đối tượng nguồn.

    ```javascript
    const obj1 = { a: 1, b: 2 };
    const obj2 = { c: 3, d: 4 };

    const combinedObject = Object.assign({}, obj1, obj2);
    console.log(combinedObject);
    // Output: { a: 1, b: 2, c: 3, d: 4 }
    ```

    5.  **Object.create()**: Tạo một đối tượng mới với nguyên mẫu đã cho.

    ```javascript
    const personPrototype = {
      introduce() {
        console.log(
          `Hi, my name is ${this.name} and I am ${this.age} years old.`
        );
      },
    };

    const john = Object.create(personPrototype);
    john.name = "John";
    john.age = 30;

    john.introduce(); // Output: "Hi, my name is John and I am 30 years old."
    ```

    6.  **Object.hasOwnProperty()**: Kiểm tra xem một thuộc tính có tồn tại trong đối tượng không (không kiểm tra thuộc tính kế thừa).

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
    };

    console.log(myObject.hasOwnProperty("name")); // Output: true
    console.log(myObject.hasOwnProperty("occupation")); // Output: false
    ```

    7.  **Object.freeze()**: Đóng băng đối tượng, ngăn không cho thay đổi các thuộc tính của nó.

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
    };

    Object.freeze(myObject);
    myObject.age = 40;
    console.log(myObject); // Output: { name: "John", age: 30 }
    ```

    8.  **Object.seal()**: Seals (niêm phong) đối tượng, cho phép chỉnh sửa các thuộc tính hiện có của nó, nhưng không thể thêm hoặc xóa thuộc tính.

    ```javascript
    const myObject = {
      name: "John",
      age: 30,
    };

    Object.seal(myObject);
    myObject.age = 40; // Có thể chỉnh sửa giá trị của thuộc tính age
    myObject.occupation = "Engineer"; // Không thể thêm thuộc tính mới
    delete myObject.name; // Không thể xóa thuộc tính
    console.log(myObject); // Output: { name: "John", age: 40 }
    ```

    Đây là một số object method trong JavaScript. Hãy tìm hiểu thêm để tận dụng các phương thức mạnh mẽ này khi làm việc với đối tượng trong JavaScript.

6.  `Phân biệt local storage, session storage, cookie `

    Dưới đây là sự phân biệt giữa Session Storage, Local Storage và Cookies, cùng với cách sử dụng chúng trong JavaScript:

    1.  **Session Storage:**

        - **Phạm vi:** Dữ liệu chỉ tồn tại trong suốt phiên làm việc của trang.
        - **Kích thước lưu trữ:** Thường giới hạn khoảng 5-10 MB tuỳ thuộc vào trình duyệt.
        - **Sử dụng:** Session Storage thích hợp để lưu trữ dữ liệu tạm thời trong suốt quá trình người dùng truy cập trang web. Dữ liệu sẽ bị xóa khi trình duyệt đóng tab hoặc cửa sổ.

        ```javascript
        // Lưu trữ dữ liệu vào Session Storage
        sessionStorage.setItem("key", "value");

        // Lấy dữ liệu từ Session Storage
        const data = sessionStorage.getItem("key");
        ```

    2.  **Local Storage:**

        - **Phạm vi:** Dữ liệu lưu trữ tồn tại vĩnh viễn trên thiết bị của người dùng, thậm chí sau khi trình duyệt đóng và mở lại.
        - **Kích thước lưu trữ:** Thường giới hạn khoảng 5-10 MB tuỳ thuộc vào trình duyệt.
        - **Sử dụng:** Local Storage thích hợp để lưu trữ dữ liệu lâu dài hoặc vĩnh viễn mà bạn muốn giữ nguyên kể cả khi người dùng tắt trình duyệt và quay lại sau này.

        ```javascript
        // Lưu trữ dữ liệu vào Local Storage
        localStorage.setItem("key", "value");

        // Lấy dữ liệu từ Local Storage
        const data = localStorage.getItem("key");
        ```

    3.  **Cookies:**

        - **Phạm vi:** Dữ liệu lưu trữ trên thiết bị của người dùng và có thể được đặt với thời hạn hết hạn. Cookies tồn tại sau khi trình duyệt đóng và mở lại, tùy thuộc vào thời hạn mà bạn đặt.
        - **Kích thước lưu trữ:** Thường giới hạn khoảng 4 KB.
        - **Sử dụng:** Cookies thường được sử dụng để lưu trữ thông tin như thông tin đăng nhập, giỏ hàng, cài đặt ngôn ngữ, v.v. Cookies sẽ được gửi cùng với mọi yêu cầu HTTP đến máy chủ, điều này làm cho chúng hữu ích cho việc lưu trữ dữ liệu có thể truy cập từ cả phía máy chủ và phía máy khách.

        ```javascript
        // Đặt một cookie với thời hạn hết hạn (tính bằng ngày)
        document.cookie =
          "key=value; expires=Thu, 18 Jul 2024 12:00:00 UTC; path=/";

        // Lấy giá trị của cookie bằng tên
        function getCookie(name) {
          const value = `; ${document.cookie}`;
          const parts = value.split(`; ${name}=`);
          if (parts.length === 2) return parts.pop().split(";").shift();
        }
        const data = getCookie("key");
        ```

    Tùy theo mục đích và tính chất của dữ liệu mà bạn muốn lưu trữ, bạn có thể lựa chọn Session Storage, Local Storage hoặc Cookies để quản lý dữ liệu trong ứng dụng JavaScript của bạn.

7.  `OOP trong JAVASCRIPT `

    1.  Đối tượng (Object): Đối tượng là một thực thể có các thuộc tính (properties) và hành vi (methods). Trong JavaScript, một đối tượng có thể là một đối tượng dựng sẵn như `Date`, `Array`, `Math`, hoặc một đối tượng tự định nghĩa.

    2.  Lớp (Class): Lớp là một mô tả chung của một đối tượng, bao gồm các thuộc tính và phương thức mà đối tượng sẽ có. Trong JavaScript, lớp được mô phỏng bằng cách sử dụng các hàm tạo (constructor function) hoặc cú pháp `class` (ES6).

    3.  Tính đa hình (Polymorphism): Tính đa hình cho phép một đối tượng thực hiện một hành động theo nhiều cách khác nhau. Điều này giúp tăng tính linh hoạt và tái sử dụng mã.

    4.  Kế thừa (Inheritance): Kế thừa cho phép một lớp con (subclass) kế thừa các thuộc tính và phương thức từ một lớp cha (superclass). Lớp con có thể mở rộng hoặc ghi đè các tính năng của lớp cha.

    5.  Đóng gói (Encapsulation): Đóng gói cho phép che dấu thông tin bên trong một đối tượng, chỉ hiển thị những phương thức cần thiết cho việc tương tác với đối tượng đó.

    Dưới đây là cách sử dụng OOP trong JavaScript:

    1.  Sử dụng Hàm Tạo (Constructor Functions):

    ```javascript
    // Định nghĩa lớp
    function Person(name, age) {
      this.name = name;
      this.age = age;
    }

    // Thêm phương thức cho lớp
    Person.prototype.sayHello = function () {
      console.log(
        `Hello, my name is ${this.name} and I am ${this.age} years old.`
      );
    };

    // Tạo đối tượng từ lớp
    const person1 = new Person("Alice", 30);
    const person2 = new Person("Bob", 25);

    person1.sayHello(); // Hello, my name is Alice and I am 30 years old.
    person2.sayHello(); // Hello, my name is Bob and I am 25 years old.
    ```

    2.  Sử dụng Cú pháp `class` (ES6):

    ```javascript
    // Định nghĩa lớp bằng cú pháp class
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }

      // Phương thức của lớp
      sayHello() {
        console.log(
          `Hello, my name is ${this.name} and I am ${this.age} years old.`
        );
      }
    }

    // Tạo đối tượng từ lớp
    const person1 = new Person("Alice", 30);
    const person2 = new Person("Bob", 25);

    person1.sayHello(); // Hello, my name is Alice and I am 30 years old.
    person2.sayHello(); // Hello, my name is Bob and I am 25 years old.
    ```

    Đây chỉ là một phần nhỏ về cách sử dụng OOP trong JavaScript. Có rất nhiều khái niệm và cú pháp khác để khám phá trong lập trình hướng đối tượng, như kế thừa, đóng gói, tính đa hình và ghi đè phương thức.

8.`REPEAT trong javascript ?`

Trong JavaScript (cũng áp dụng cho TypeScript), phương thức `repeat()` được sử dụng để tạo ra một chuỗi mới bằng cách lặp lại chuỗi gốc một số lần nhất định.

Cú pháp:

```javascript
string.repeat(count);
```

Trong đó:

- `string`: Chuỗi gốc bạn muốn lặp lại.
- `count`: Số lần lặp lại chuỗi gốc. Phải là một số nguyên không âm.

Ví dụ:

```javascript
const str = "Hello, ";
const repeatedStr = str.repeat(3);

console.log(repeatedStr);
// Output: "Hello, Hello, Hello, "
```

Trong ví dụ trên, chuỗi gốc là "Hello, " và chúng ta sử dụng phương thức `repeat(3)` để lặp lại chuỗi này 3 lần, tạo thành chuỗi mới "Hello, Hello, Hello, ".

Lưu ý rằng `count` phải là một số nguyên không âm. Nếu `count` không phải số hoặc là một số âm, hoặc không phải số nguyên, phương thức `repeat()` sẽ trả về một chuỗi trống ("").

9. `STACK TRONG JAVASCRIPT `

   Trong ngôn ngữ JavaScript, bạn có thể biểu diễn cấu trúc dữ liệu stack bằng cách sử dụng một mảng và triển khai các phương thức cơ bản để thêm và loại bỏ các phần tử khỏi stack. Dưới đây là một ví dụ về cách triển khai stack:

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // Thêm một phần tử vào đỉnh của stack
  push(element) {
    this.items.push(element);
  }

  // Lấy và loại bỏ phần tử ở đỉnh của stack
  pop() {
    if (this.isEmpty()) {
      return "Stack is empty";
    }
    return this.items.pop();
  }

  // Lấy phần tử ở đỉnh của stack (không loại bỏ)
  peek() {
    if (this.isEmpty()) {
      return "Stack is empty";
    }
    return this.items[this.items.length - 1];
  }

  // Kiểm tra xem stack có trống không
  isEmpty() {
    return this.items.length === 0;
  }

  // Lấy số lượng phần tử trong stack
  size() {
    return this.items.length;
  }

  // Xóa tất cả các phần tử trong stack
  clear() {
    this.items = [];
  }
}

// Sử dụng stack
const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);

console.log(stack.peek()); // Output: 3

console.log(stack.pop()); // Output: 3

console.log(stack.size()); // Output: 2

console.log(stack.isEmpty()); // Output: false

stack.clear();
console.log(stack.isEmpty()); // Output: true
```

Trong ví dụ trên, chúng ta đã triển khai các phương thức cơ bản cho stack, bao gồm `push` để thêm phần tử vào đỉnh của stack, `pop` để lấy và loại bỏ phần tử khỏi đỉnh của stack, `peek` để xem phần tử ở đỉnh mà không loại bỏ nó, `isEmpty` để kiểm tra xem stack có trống không, `size` để lấy số lượng phần tử trong stack, và `clear` để xóa tất cả các phần tử trong stack.

10. `QUEUE trong javascript`

    Trong ngôn ngữ JavaScript, bạn có thể biểu diễn cấu trúc dữ liệu queue bằng cách sử dụng một mảng và triển khai các phương thức cơ bản để thêm và loại bỏ các phần tử khỏi queue theo nguyên tắc "First-In-First-Out" (FIFO). Dưới đây là một ví dụ về cách triển khai queue:

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // Thêm một phần tử vào cuối queue
  enqueue(element) {
    this.items.push(element);
  }

  // Lấy và loại bỏ phần tử ở đầu queue
  dequeue() {
    if (this.isEmpty()) {
      return "Queue is empty";
    }
    return this.items.shift();
  }

  // Lấy phần tử ở đầu queue (không loại bỏ)
  front() {
    if (this.isEmpty()) {
      return "Queue is empty";
    }
    return this.items[0];
  }

  // Kiểm tra xem queue có trống không
  isEmpty() {
    return this.items.length === 0;
  }

  // Lấy số lượng phần tử trong queue
  size() {
    return this.items.length;
  }

  // Xóa tất cả các phần tử trong queue
  clear() {
    this.items = [];
  }
}

// Sử dụng queue
const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);

console.log(queue.front()); // Output: 1

console.log(queue.dequeue()); // Output: 1

console.log(queue.size()); // Output: 2

console.log(queue.isEmpty()); // Output: false

queue.clear();
console.log(queue.isEmpty()); // Output: true
```

Trong ví dụ trên, chúng ta đã triển khai các phương thức cơ bản cho queue, bao gồm `enqueue` để thêm phần tử vào cuối queue, `dequeue` để lấy và loại bỏ phần tử khỏi đầu queue, `front` để xem phần tử ở đầu mà không loại bỏ nó, `isEmpty` để kiểm tra xem queue có trống không, `size` để lấy số lượng phần tử trong queue, và `clear` để xóa tất cả các phần tử trong queue.

11. `Tìm ước chung lớn nhất, bội chung nhỏ nhất trong javascript `

    Để tìm ước chung lớn nhất (Greatest Common Divisor - GCD) và bội chung nhỏ nhất (Least Common Multiple - LCM) của hai số a và b bằng JavaScript, bạn có thể sử dụng thuật toán Euclid để tìm GCD và sử dụng công thức tính LCM dựa trên GCD. Dưới đây là một ví dụ về cách làm điều này:

```javascript
// Hàm tính ước chung lớn nhất (GCD) bằng thuật toán Euclid
function gcd(a, b) {
  if (b === 0) {
    return a;
  } else {
    return gcd(b, a % b);
  }
}

// Hàm tính bội chung nhỏ nhất (LCM) dựa trên GCD
function lcm(a, b) {
  return (a * b) / gcd(a, b);
}

// Đầu vào
const a = 24;
const b = 36;

// Tính và in kết quả
const greatestCommonDivisor = gcd(a, b);
const leastCommonMultiple = lcm(a, b);

console.log("Ước chung lớn nhất (GCD): " + greatestCommonDivisor);
console.log("Bội chung nhỏ nhất (LCM): " + leastCommonMultiple);
```

Kết quả khi chạy đoạn mã trên sẽ là:

```
Ước chung lớn nhất (GCD): 12
Bội chung nhỏ nhất (LCM): 72
```

Trong ví dụ trên, chúng ta đã triển khai hai hàm là `gcd` để tính ước chung lớn nhất và `lcm` để tính bội chung nhỏ nhất. Hàm `gcd` sử dụng thuật toán Euclid để tìm ước chung lớn nhất của hai số. Sau đó, chúng ta sử dụng kết quả GCD để tính LCM bằng công thức `LCM(a, b) = (a * b) / GCD(a, b)`.

12. `Cây nhị phân trong javascript`

    Cây nhị phân là một cấu trúc dữ liệu phổ biến trong lập trình, nó bao gồm một tập hợp các node, mỗi node chứa một giá trị và có tối đa hai con trỏ con trỏ tới hai node con, gọi là node trái và node phải. Dưới đây là một triển khai cơ bản của cây nhị phân bằng JavaScript:

Đầu tiên, chúng ta sẽ tạo lớp Node để đại diện cho mỗi node trong cây:

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
```

Sau đó, chúng ta sẽ tạo lớp BinarySearchTree để đại diện cho cây nhị phân:

```javascript
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  // Thêm một giá trị vào cây
  insert(value) {
    const newNode = new Node(value);

    if (!this.root) {
      this.root = newNode;
    } else {
      this.insertNode(this.root, newNode);
    }
  }

  // Hỗ trợ hàm cho phương thức insert
  insertNode(node, newNode) {
    if (newNode.value < node.value) {
      if (!node.left) {
        node.left = newNode;
      } else {
        this.insertNode(node.left, newNode);
      }
    } else {
      if (!node.right) {
        node.right = newNode;
      } else {
        this.insertNode(node.right, newNode);
      }
    }
  }

  // Tìm giá trị trong cây
  search(value) {
    return this.searchNode(this.root, value);
  }

  // Hỗ trợ hàm cho phương thức search
  searchNode(node, value) {
    if (!node) {
      return false;
    }

    if (node.value === value) {
      return true;
    } else if (value < node.value) {
      return this.searchNode(node.left, value);
    } else {
      return this.searchNode(node.right, value);
    }
  }

  // Duyệt cây theo thứ tự trung tố (In-order)
  inOrderTraversal() {
    return this.inOrderTraversalNode(this.root);
  }

  // Hỗ trợ hàm cho phương thức inOrderTraversal
  inOrderTraversalNode(node) {
    if (!node) {
      return [];
    }

    const result = [];
    result.push(...this.inOrderTraversalNode(node.left));
    result.push(node.value);
    result.push(...this.inOrderTraversalNode(node.right));

    return result;
  }
}
```

Giờ ta đã có cây nhị phân hoạt động trong JavaScript. Dưới đây là cách sử dụng nó:

```javascript
const bst = new BinarySearchTree();

bst.insert(15);
bst.insert(10);
bst.insert(25);
bst.insert(5);
bst.insert(12);
bst.insert(22);
bst.insert(30);

console.log(bst.search(12)); // Output: true
console.log(bst.search(20)); // Output: false

console.log(bst.inOrderTraversal()); // Output: [5, 10, 12, 15, 22, 25, 30]
```

Trong ví dụ trên, chúng ta đã tạo một cây nhị phân và thêm các giá trị vào cây bằng phương thức `insert`. Sau đó, chúng ta kiểm tra sự tồn tại của một giá trị bằng phương thức `search`, và cuối cùng, chúng ta duyệt cây theo thứ tự trung tố bằng phương thức `inOrderTraversal`.

13. `Graph trong javascript`

    Trong JavaScript, bạn có thể triển khai cấu trúc dữ liệu đồ thị (Graph) bằng nhiều cách. Một trong những cách phổ biến là sử dụng danh sách kề (Adjacency List) để lưu trữ các đỉnh và cạnh của đồ thị. Dưới đây là một ví dụ về cách triển khai đồ thị bằng danh sách kề:

```javascript
class Graph {
  constructor() {
    this.nodes = new Map();
  }

  // Thêm một đỉnh mới vào đồ thị
  addNode(node) {
    this.nodes.set(node, []);
  }

  // Thêm một cạnh nối hai đỉnh trong đồ thị (hướng không quan trọng)
  addEdge(node1, node2) {
    if (!this.nodes.has(node1) || !this.nodes.has(node2)) {
      throw new Error("Both nodes must exist in the graph.");
    }

    this.nodes.get(node1).push(node2);
    this.nodes.get(node2).push(node1); // Nếu là đồ thị có hướng, hãy bỏ dòng này
  }

  // Lấy danh sách các đỉnh kề của một đỉnh
  getNeighbors(node) {
    if (!this.nodes.has(node)) {
      throw new Error("Node does not exist in the graph.");
    }

    return this.nodes.get(node);
  }

  // Kiểm tra xem hai đỉnh có kề nhau hay không
  hasEdge(node1, node2) {
    if (!this.nodes.has(node1) || !this.nodes.has(node2)) {
      throw new Error("Both nodes must exist in the graph.");
    }

    return this.nodes.get(node1).includes(node2);
  }

  // Lấy tất cả các đỉnh của đồ thị
  getAllNodes() {
    return Array.from(this.nodes.keys());
  }
}

// Sử dụng đồ thị
const graph = new Graph();

graph.addNode("A");
graph.addNode("B");
graph.addNode("C");
graph.addNode("D");

graph.addEdge("A", "B");
graph.addEdge("B", "C");
graph.addEdge("C", "D");
graph.addEdge("D", "A");

console.log(graph.getNeighbors("A")); // Output: ['B', 'D']
console.log(graph.hasEdge("B", "C")); // Output: true
console.log(graph.getAllNodes()); // Output: ['A', 'B', 'C', 'D']
```

Trong ví dụ trên, chúng ta đã triển khai một lớp `Graph` để đại diện cho đồ thị. Chúng ta sử dụng một `Map` để lưu trữ danh sách kề của mỗi đỉnh trong đồ thị. Phương thức `addNode` được sử dụng để thêm một đỉnh mới vào đồ thị, `addEdge` để thêm một cạnh nối hai đỉnh, `getNeighbors` để lấy danh sách các đỉnh kề của một đỉnh, `hasEdge` để kiểm tra xem hai đỉnh có kề nhau hay không, và `getAllNodes` để lấy tất cả các đỉnh của đồ thị.

14. `Linked list trong javascript ?`

    Trong JavaScript, bạn có thể triển khai cấu trúc dữ liệu danh sách liên kết (linked list) bằng cách sử dụng các đối tượng và tham chiếu. Dưới đây là một ví dụ về cách triển khai danh sách liên kết đơn giản:

Đầu tiên, chúng ta sẽ tạo lớp Node để đại diện cho mỗi phần tử trong danh sách:

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

Sau đó, chúng ta sẽ tạo lớp LinkedList để đại diện cho danh sách liên kết:

```javascript
class LinkedList {
  constructor() {
    this.head = null;
  }

  // Thêm một phần tử vào đầu danh sách
  prepend(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }

  // Thêm một phần tử vào cuối danh sách
  append(data) {
    const newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
      return;
    }

    let current = this.head;
    while (current.next) {
      current = current.next;
    }

    current.next = newNode;
  }

  // Tìm một phần tử trong danh sách
  find(data) {
    let current = this.head;
    while (current) {
      if (current.data === data) {
        return current;
      }
      current = current.next;
    }
    return null;
  }

  // Xóa một phần tử khỏi danh sách
  delete(data) {
    if (!this.head) {
      return;
    }

    if (this.head.data === data) {
      this.head = this.head.next;
      return;
    }

    let current = this.head;
    while (current.next) {
      if (current.next.data === data) {
        current.next = current.next.next;
        return;
      }
      current = current.next;
    }
  }

  // Lấy tất cả các phần tử trong danh sách và trả về dưới dạng mảng
  toArray() {
    const result = [];
    let current = this.head;
    while (current) {
      result.push(current.data);
      current = current.next;
    }
    return result;
  }
}
```

Giờ ta đã có danh sách liên kết hoạt động trong JavaScript. Dưới đây là cách sử dụng nó:

```javascript
const linkedList = new LinkedList();

linkedList.append(1);
linkedList.append(2);
linkedList.prepend(0);
linkedList.append(3);

console.log(linkedList.toArray()); // Output: [0, 1, 2, 3]

linkedList.delete(1);
console.log(linkedList.toArray()); // Output: [0, 2, 3]

console.log(linkedList.find(2)); // Output: Node { data: 2, next: Node {...} }
```

Trong ví dụ trên, chúng ta đã tạo một danh sách liên kết và thêm các phần tử vào danh sách bằng phương thức `append` và `prepend`. Sau đó, chúng ta kiểm tra việc xóa một phần tử bằng phương thức `delete` và tìm một phần tử bằng phương thức `find`. Cuối cùng, chúng ta lấy tất cả các phần tử trong danh sách và in ra bằng phương thức `toArray`.

14. `BFS và DFS trong javascript`

    BFS (Breadth-First Search) và DFS (Depth-First Search) là hai thuật toán duyệt đồ thị phổ biến được sử dụng để tìm kiếm và truy cập các đỉnh trong đồ thị. Dưới đây là một ví dụ về cách triển khai BFS và DFS trong JavaScript:

Đầu tiên, chúng ta sẽ triển khai cấu trúc đồ thị bằng danh sách kề (Adjacency List):

```javascript
class Graph {
  constructor() {
    this.nodes = new Map();
  }

  addNode(node) {
    this.nodes.set(node, []);
  }

  addEdge(node1, node2) {
    if (!this.nodes.has(node1) || !this.nodes.has(node2)) {
      throw new Error("Both nodes must exist in the graph.");
    }

    this.nodes.get(node1).push(node2);
    this.nodes.get(node2).push(node1); // Nếu là đồ thị có hướng, hãy bỏ dòng này
  }

  getNeighbors(node) {
    if (!this.nodes.has(node)) {
      throw new Error("Node does not exist in the graph.");
    }

    return this.nodes.get(node);
  }
}
```

Tiếp theo, chúng ta sẽ triển khai BFS và DFS:

```javascript
// Breadth-First Search (BFS)
function bfs(graph, startNode) {
  const visited = new Set();
  const queue = [startNode];

  while (queue.length > 0) {
    const currentNode = queue.shift();
    if (!visited.has(currentNode)) {
      visited.add(currentNode);
      console.log(currentNode);

      const neighbors = graph.getNeighbors(currentNode);
      for (const neighbor of neighbors) {
        if (!visited.has(neighbor)) {
          queue.push(neighbor);
        }
      }
    }
  }
}

// Depth-First Search (DFS)
function dfs(graph, startNode) {
  const visited = new Set();

  function traverse(node) {
    visited.add(node);
    console.log(node);

    const neighbors = graph.getNeighbors(node);
    for (const neighbor of neighbors) {
      if (!visited.has(neighbor)) {
        traverse(neighbor);
      }
    }
  }

  traverse(startNode);
}
```

Giờ ta đã có BFS và DFS hoạt động trong JavaScript. Dưới đây là cách sử dụng nó:

```javascript
const graph = new Graph();

graph.addNode("A");
graph.addNode("B");
graph.addNode("C");
graph.addNode("D");
graph.addNode("E");

graph.addEdge("A", "B");
graph.addEdge("A", "C");
graph.addEdge("B", "D");
graph.addEdge("C", "E");

console.log("BFS:");
bfs(graph, "A");

console.log("DFS:");
dfs(graph, "A");
```

Trong ví dụ trên, chúng ta đã tạo một đồ thị và triển khai BFS và DFS để duyệt đồ thị và in các đỉnh theo thứ tự tương ứng.

15. `Async, sync, setTimeout trong javascript`

    Trong JavaScript, các khái niệm "async", "sync", "setTimeout", và "setInterval" liên quan đến cách mã chương trình được thực thi và xử lý các tác vụ không đồng bộ (asynchronous tasks) và đồng bộ (synchronous tasks). Đây là các khái niệm quan trọng khi làm việc với JavaScript, đặc biệt là trong ngữ cảnh của trình duyệt (browser) hoặc Node.js.

    "async" và "sync":

    - "async" (asynchronous): Là một cách để đánh dấu một hàm (function) là một hàm bất đồng bộ. Hàm bất đồng bộ là hàm sẽ không chờ đến khi các tác vụ không đồng bộ hoàn thành mà tiếp tục thực thi các tác vụ khác. Thay vào đó, nó sẽ trả về một Promise (một giá trị có thể hoàn thành trong tương lai) và tiếp tục thực thi các câu lệnh tiếp theo trong hàm gọi.

    - "sync" (synchronous): Đối lập với bất đồng bộ, hàm đồng bộ thực hiện các tác vụ tuần tự, chờ đến khi một tác vụ hoàn thành trước khi thực hiện tác vụ tiếp theo.

    Ví dụ:

    a) Hàm bất đồng bộ (async function):

    ```javascript
    async function fetchData() {
      const response = await fetch("https://api.example.com/data"); // Chờ response từ API
      const data = await response.json(); // Chờ chuyển đổi dữ liệu thành JSON
      return data;
    }

    fetchData().then((data) => {
      console.log(data); // In dữ liệu nhận được từ API sau khi hoàn thành
    });
    ```

    b) Hàm đồng bộ (synchronous function):

    ```javascript
    function addNumbers(a, b) {
      return a + b; // Trả về kết quả trực tiếp mà không cần đợi
    }

    const sum = addNumbers(5, 3);
    console.log(sum); // In kết quả tổng (8) ngay lập tức
    ```

    2.  "setTimeout" và "setInterval":

    - "setTimeout": Hàm này được sử dụng để lên lịch thực thi một hàm hoặc các câu lệnh sau một khoảng thời gian đã cho. Sau khi thời gian đã định trôi qua, hàm hoặc câu lệnh sẽ được thực thi một lần duy nhất.

    - "setInterval": Tương tự như "setTimeout", hàm này cũng lên lịch thực thi một hàm hoặc câu lệnh sau một khoảng thời gian đã cho. Tuy nhiên, khác với "setTimeout", "setInterval" sẽ tiếp tục lặp lại việc thực thi hàm hoặc câu lệnh với khoảng thời gian cố định giữa các lần thực thi.

    Ví dụ:

    a) Sử dụng "setTimeout" để thực thi một hàm sau 1 giây:

    ```javascript
    function sayHello() {
      console.log("Hello!");
    }

    setTimeout(sayHello, 1000); // In "Hello!" sau 1 giây
    ```

    b) Sử dụng "setInterval" để lặp lại việc in dòng chữ "Hello!" sau mỗi 2 giây:

    ```javascript
    function sayHello() {
      console.log("Hello!");
    }

    setInterval(sayHello, 2000); // In "Hello!" sau mỗi 2 giây
    ```

    Chú ý: Khi sử dụng "setInterval", bạn cần đặc biệt lưu ý để dừng nó khi không cần thiết nữa, bằng cách sử dụng "clearInterval" để hủy lịch trình đã đặt trước đó.

16. `Hash table trong javascript`

    Để cài đặt một bảng băm (hash table) trong JavaScript, bạn có thể sử dụng đối tượng (object) hoặc một lớp tự định nghĩa. Dưới đây, tôi sẽ hướng dẫn bạn cách triển khai cả hai cách.

    **1. Sử dụng đối tượng (object) trong JavaScript:**

    Trong JavaScript, đối tượng là một cấu trúc dữ liệu có thể sử dụng như một bảng băm. Chúng ta có thể sử dụng các cặp key-value trong đối tượng để đại diện cho các phần tử trong bảng băm.

    ```javascript
    // Khởi tạo bảng băm bằng đối tượng
    const hashTable = {};

    // Thêm phần tử vào bảng băm
    hashTable["key1"] = "value1";
    hashTable["key2"] = "value2";

    // Truy xuất phần tử từ bảng băm
    console.log(hashTable["key1"]); // Output: "value1"
    console.log(hashTable["key2"]); // Output: "value2"

    // Kiểm tra xem một key có tồn tại trong bảng băm hay không
    if ("key1" in hashTable) {
      console.log("Key1 exists!");
    } else {
      console.log("Key1 does not exist!");
    }

    // Xóa phần tử từ bảng băm
    delete hashTable["key2"];
    console.log(hashTable); // Output: { "key1": "value1" }
    ```

    **2. Sử dụng lớp tự định nghĩa (ES6 class) trong JavaScript:**

    Bạn cũng có thể triển khai bảng băm bằng cách sử dụng một lớp tự định nghĩa. Lớp này sẽ chứa các phương thức để thêm, lấy và xóa các phần tử trong bảng băm.

    ```javascript
    class HashTable {
      constructor() {
        this.table = {};
      }

      // Thêm phần tử vào bảng băm
      add(key, value) {
        this.table[key] = value;
      }

      // Lấy phần tử từ bảng băm
      get(key) {
        return this.table[key];
      }

      // Kiểm tra sự tồn tại của một key trong bảng băm
      has(key) {
        return key in this.table;
      }

      // Xóa phần tử từ bảng băm
      remove(key) {
        delete this.table[key];
      }
    }

    // Sử dụng lớp HashTable
    const hashTable = new HashTable();
    hashTable.add("key1", "value1");
    hashTable.add("key2", "value2");

    console.log(hashTable.get("key1")); // Output: "value1"
    console.log(hashTable.get("key2")); // Output: "value2"

    if (hashTable.has("key1")) {
      console.log("Key1 exists!");
    } else {
      console.log("Key1 does not exist!");
    }

    hashTable.remove("key2");
    console.log(hashTable); // Output: { "key1": "value1" }
    ```

    Lưu ý rằng trong thực tế, khi triển khai một bảng băm phức tạp hơn, bạn nên xem xét các vấn đề như xử lý va chạm (collision handling), việc cải thiện hiệu suất, và các thuật toán hàm băm tốt hơn để giảm thiểu xung đột. Tuy nhiên, ví dụ trên cung cấp một cách đơn giản để bắt đầu làm việc với bảng băm trong JavaScript.

17. `Set trong javascript`

    Trong JavaScript, Set là một cấu trúc dữ liệu mà nó giữ các giá trị không trùng lặp, tức là mỗi giá trị trong Set chỉ xuất hiện một lần. Set giữ các giá trị theo thứ tự thêm vào, không có thứ tự sắp xếp cụ thể.

    Để tạo một Set mới, bạn có thể sử dụng từ khoá `new` kèm theo lớp Set như sau:

    ```javascript
    // Tạo một Set mới rỗng
    const mySet = new Set();

    // Tạo Set từ một mảng
    const myArray = [1, 2, 3, 2, 1];
    const mySetFromArr = new Set(myArray);
    console.log(mySetFromArr); // Output: Set { 1, 2, 3 }

    // Thêm giá trị vào Set
    mySet.add(1);
    mySet.add(2);
    mySet.add(3);
    mySet.add(2); // Giá trị 2 đã tồn tại, không thêm vào lại
    console.log(mySet); // Output: Set { 1, 2, 3 }

    // Kiểm tra sự tồn tại của một giá trị trong Set
    console.log(mySet.has(2)); // Output: true
    console.log(mySet.has(4)); // Output: false

    // Xóa giá trị từ Set
    mySet.delete(3);
    console.log(mySet); // Output: Set { 1, 2 }

    // Lấy số lượng các phần tử trong Set
    console.log(mySet.size); // Output: 2

    // Xóa tất cả các phần tử trong Set
    mySet.clear();
    console.log(mySet); // Output: Set {}
    ```

    Set hữu ích khi bạn muốn lưu trữ các giá trị duy nhất và không cần quan tâm đến thứ tự của chúng. Bạn có thể sử dụng Set để loại bỏ các giá trị trùng lặp từ một mảng, thực hiện các phép toán tập hợp như hợp, giao, hiệu, và thực hiện các tác vụ khác liên quan đến các tập hợp duy nhất trong JavaScript.

18. `Map trong javascript`

    Trong JavaScript, "Map" là một loại cấu trúc dữ liệu hữu ích để lưu trữ các cặp key-value (khóa-giá trị) và cho phép bạn thực hiện các thao tác thêm, xóa, tìm kiếm và truy xuất giá trị dựa vào khóa. Một điểm mạnh của Map là nó cho phép sử dụng bất kỳ kiểu dữ liệu nào làm khóa, bao gồm cả đối tượng và hàm.

    Để sử dụng Map trong JavaScript, bạn có thể sử dụng cú pháp sau:

    ```javascript
    const map = new Map();
    ```

    Dưới đây là một số phương thức cơ bản của Map:

    1.  `set(key, value)`: Thêm một cặp khóa-giá trị vào Map.

    ```javascript
    map.set("name", "John");
    map.set(1, "One");
    ```

    2.  `get(key)`: Trả về giá trị tương ứng với khóa được chỉ định, nếu không tồn tại trả về undefined.

    ```javascript
    const nameValue = map.get("name"); // 'John'
    const oneValue = map.get(1); // 'One'
    const nonExistentValue = map.get("nonExistentKey"); // undefined
    ```

    3.  `has(key)`: Kiểm tra xem khóa có tồn tại trong Map hay không.

    ```javascript
    const hasName = map.has("name"); // true
    const hasNonExistentKey = map.has("nonExistentKey"); // false
    ```

    4.  `delete(key)`: Xóa cặp khóa-giá trị với khóa được chỉ định khỏi Map.

    ```javascript
    map.delete("name");
    ```

    5.  `size`: Trả về số lượng cặp khóa-giá trị trong Map.

    ```javascript
    const size = map.size; // 1
    ```

    6.  `clear()`: Xóa tất cả các cặp khóa-giá trị trong Map.

    ```javascript
    map.clear();
    ```

    Map cũng hỗ trợ việc duyệt qua các cặp khóa-giá trị thông qua các phương thức `forEach`, `keys`, `values`, và `entries`.

    ```javascript
    map.set("name", "John");
    map.set("age", 30);

    // Duyệt qua các cặp khóa-giá trị
    map.forEach((value, key) => {
      console.log(`${key}: ${value}`);
    });

    // Duyệt qua các khóa
    for (const key of map.keys()) {
      console.log(key);
    }

    // Duyệt qua các giá trị
    for (const value of map.values()) {
      console.log(value);
    }

    // Duyệt qua các cặp khóa-giá trị sử dụng destructuring
    for (const [key, value] of map.entries()) {
      console.log(`${key}: ${value}`);
    }
    ```

    Map là một cấu trúc dữ liệu mạnh mẽ và linh hoạt trong JavaScript, và nó rất hữu ích khi bạn cần lưu trữ dữ liệu theo kiểu key-value.

19. `Hoisting trong javascript là gì ?`

    Hoisting là một cơ chế JavaScript trong đó các biến, khai báo hàm và lớp được di chuyển lên đầu phạm vi của chúng trước khi thực thi mã. Hãy nhớ rằng JavaScript chỉ nâng các khai báo, không khởi tạo. Hãy lấy một ví dụ đơn giản về cẩu biến

    EX:

    ```typescript
    console.log(message); //output : undefined
    var message = "The variable Has been hoisted";

    var message;
    console.log(message);
    message = "The variable Has been hoisted";

    message("Good morning"); //Good morning
    function message(name) {
      console.log(name);
    }
    ```

20. `Closure trong javascript là gì`

    Closure trong JavaScript là một khái niệm quan trọng, đề cập đến khả năng của một hàm có thể truy cập và sử dụng các biến được định nghĩa trong phạm vi của hàm cha của nó, ngay cả khi hàm cha đã thực thi xong và đã ra khỏi ngữ cảnh.

    Một ví dụ cơ bản về closure trong JavaScript như sau:

    ```javascript
    function outerFunction() {
      var outerVariable = "I am from outer";

      function innerFunction() {
        console.log(outerVariable);
      }

      return innerFunction;
    }

    var closureFunc = outerFunction();
    closureFunc(); // Kết quả: "I am from outer"
    ```

    Trong ví dụ trên, chúng ta có một hàm `outerFunction` chứa một biến cục bộ là `outerVariable` và một hàm con là `innerFunction`. Hàm `innerFunction` có thể truy cập vào biến `outerVariable`, mặc dù hàm `outerFunction` đã thực thi xong. Khi gọi `outerFunction`, nó trả về `innerFunction`, và sau đó khi gọi `closureFunc`, nó vẫn có thể truy cập và hiển thị giá trị của `outerVariable`. Đây chính là closure.

    Với closure, ta có thể tạo ra các biến ẩn (private variables), quản lý trạng thái, triển khai các pattern như module pattern để kiểm soát phạm vi và tránh xung đột biến toàn cục, v.v.

21. `Modules là gì và tại sao cần phải có modules `

    Trong ngữ cảnh lập trình, modules (còn gọi là module) là một cách tổ chức mã nguồn thành các phần riêng biệt và độc lập, giúp tách biệt các chức năng khác nhau và quản lý phạm vi (scope) của biến và hàm trong một cách có tổ chức. Modules giúp giảm thiểu xung đột tên biến, tạo ra các biến "private", và tạo ra cơ chế tái sử dụng mã nguồn.

    Các lý do cần phải sử dụng modules trong lập trình bao gồm:

    1.  **Tách biệt chức năng:** Modules cho phép bạn tách biệt các chức năng khác nhau của ứng dụng vào các phần riêng biệt. Điều này giúp mã nguồn dễ đọc, dễ hiểu và dễ bảo trì hơn.

    2.  **Quản lý phạm vi (scope):** Các biến và hàm trong một module thường chỉ có phạm vi trong module đó, tránh việc xung đột tên biến với các phần khác trong ứng dụng.

    3.  **Bảo mật và ẩn thông tin:** Các biến và hàm được định nghĩa trong module có thể được bảo vệ và không thể truy cập từ bên ngoài module, tạo ra các biến "private" và giúp ẩn thông tin quan trọng.

    4.  **Tái sử dụng:** Các modules có thể được sử dụng lại trong nhiều dự án khác nhau, giúp tiết kiệm thời gian và công sức trong việc phát triển.

    5.  **Quản lý dependencies:** Modules giúp quản lý các phụ thuộc (dependencies) của ứng dụng một cách có tổ chức, giúp kiểm soát và cập nhật các thư viện và thành phần dễ dàng hơn.

    6.  **Hiệu suất tải trang:** Modules cho phép tải lần đầu chỉ những phần cần thiết của ứng dụng, giúp tối ưu hóa hiệu suất tải trang.

    Trong JavaScript, trước khi có hỗ trợ chính thức cho ES6 Modules (EcmaScript 2015), các nhà phát triển đã sử dụng các kỹ thuật như IIFE (Immediately Invoked Function Expression) và CommonJS để tạo ra modules. Tuy nhiên, với sự phát triển của ngôn ngữ, ES6 Modules đã trở thành một phần quan trọng của ngôn ngữ và giúp quản lý modules một cách rõ ràng hơn và hiệu quả hơn.

22. `Scope trong javascript là gì ?`

    Trong lập trình JavaScript, scope (phạm vi) là vùng mà các biến và hàm có thể được truy cập và sử dụng. Scope xác định phạm vi của biến, quyết định biến nào có thể được truy cập từ đâu và trong thời gian nào. JavaScript sử dụng các khối mã như hàm và khối if để tạo ra các phạm vi khác nhau.

    Có hai loại scope chính trong JavaScript:

    1.  **Global Scope (Phạm vi toàn cục):** Biến được khai báo ở ngoài bất kỳ hàm nào hoặc khối mã nào sẽ nằm trong phạm vi toàn cục. Điều này có nghĩa là biến có thể được truy cập từ bất kỳ đâu trong mã JavaScript, bất kể nằm trong hàm hay ngoài hàm.

    ```javascript
    var globalVariable = "I am a global variable";

    function someFunction() {
      console.log(globalVariable); // Có thể truy cập globalVariable ở đây
    }

    someFunction();
    console.log(globalVariable); // Có thể truy cập globalVariable ở đây
    ```

    2.  **Local Scope (Phạm vi cục bộ):** Biến được khai báo trong một hàm hoặc khối mã cụ thể chỉ có thể được truy cập từ bên trong phạm vi của nó. Điều này giúp giới hạn tác động của biến chỉ trong phạm vi nhất định và tránh xung đột với các biến khác nằm trong các phạm vi khác.

    ```javascript
    function someFunction() {
      var localVariable = "I am a local variable";
      console.log(localVariable); // Có thể truy cập localVariable ở đây
    }

    someFunction();
    console.log(localVariable); // Lỗi: Không thể truy cập localVariable ở đây
    ```

    Khi truy cập biến, JavaScript sẽ tìm kiếm biến đó từ trong phạm vi gần nhất trước khi tiến xa ra các phạm vi khác. Điều này được gọi là "scope chain" (chuỗi phạm vi). Nếu biến không được tìm thấy trong phạm vi hiện tại hoặc các phạm vi cha, JavaScript sẽ tạo biến mới trong phạm vi toàn cục (nếu chế độ "strict mode" không được sử dụng) hoặc sẽ ném ra lỗi (nếu chế độ "strict mode" được sử dụng).

23. `Nan là gì`

    Hàm isNaN() được sử dụng để xác định xem một giá trị có phải là số không hợp lệ (Không phải là số) hay không. tức là, Hàm này trả về true nếu giá trị bằng NaN. Nếu không, nó trả về false.

    ```javascript
    isNaN("Hello"); //true
    isNaN("100"); //false
    ```

24. `Global varaiables là gì`

    Biến toàn cục là những biến có sẵn trong suốt chiều dài của mã mà không có bất kỳ phạm vi nào. Từ khóa var dùng để khai báo biến cục bộ nhưng nếu bạn bỏ nó đi thì nó sẽ trở thành biến toàn cục

    ```typescript
    msg = "Hello"; // var is missing, it becomes global variable
    ```

25. `Phân biệt let,const,var`

    Trong JavaScript, `var`, `let`, và `const` là ba từ khóa được sử dụng để khai báo biến. Mỗi loại biến này có cách hoạt động và phạm vi sử dụng khác nhau trong quá trình thực thi mã.

    1.  **var:**
        Trước khi có `let` và `const`, `var` là từ khóa chính để khai báo biến trong JavaScript. Biến được khai báo bằng `var` có phạm vi (scope) là hàm (function scope) hoặc toàn cục (global scope), tùy thuộc vào nơi chúng được khai báo.

    Ví dụ:

    ```javascript
    function example() {
      var x = 10;
      if (true) {
        var y = 20;
        console.log(x); // 10
      }
      console.log(y); // 20
    }

    console.log(x); // Lỗi: x is not defined
    ```

    2.  **let:**
        `let` được giới thiệu trong ES6 để giải quyết một số vấn đề với cách `var` hoạt động. Biến khai báo bằng `let` có phạm vi là khối (block scope), nghĩa là chúng chỉ có thể truy cập được trong khối mà chúng được khai báo.

    Ví dụ:

    ```javascript
    function example() {
      let x = 10;
      if (true) {
        let y = 20;
        console.log(x); // 10
      }
      console.log(y); // Lỗi: y is not defined
    }

    console.log(x); // Lỗi: x is not defined
    ```

    3.  **const:**
        `const` cũng được giới thiệu trong ES6 và tương tự như `let`, ngoại trừ biến được khai báo bằng `const` không thể thay đổi giá trị sau khi được gán một lần. Biến khai báo bằng `const` cũng có phạm vi là khối.

    Ví dụ:

    ```javascript
    function example() {
      const x = 10;
      if (true) {
        const y = 20;
        console.log(x); // 10
      }
      console.log(y); // Lỗi: y is not defined
    }

    console.log(x); // Lỗi: x is not defined
    ```

    Tóm lại:

    - `var` có phạm vi là hàm hoặc toàn cục.
    - `let` và `const` có phạm vi là khối.
    - `let` cho phép thay đổi giá trị sau khi được gán.
    - `const` yêu cầu giữ nguyên giá trị sau khi được gán.

    Lựa chọn giữa `let` và `const` phụ thuộc vào việc bạn có muốn biến thay đổi giá trị sau khi gán hay không. Sử dụng `const` khi bạn biết biến không nên thay đổi giá trị và `let` khi bạn cần thay đổi giá trị.

26.`Phân biệt null và undefined`

Trong nhiều ngôn ngữ lập trình, bao gồm JavaScript, "null" và "undefined" là hai giá trị đặc biệt được sử dụng để biểu thị sự thiếu vắng của dữ liệu hoặc trạng thái không xác định. Mặc dù chúng có thể có sự tương đồng, nhưng cũng có sự khác biệt quan trọng giữa chúng:

1. **Undefined (Không xác định):**

   - "Undefined" là giá trị mà một biến có thể có khi nó đã được khai báo, nhưng chưa được gán giá trị.
   - Một biến có thể trở thành "undefined" khi được khai báo nhưng không được gán giá trị hoặc khi truy cập vào một thuộc tính không tồn tại của một đối tượng.
   - Ví dụ:

     ```javascript
     let x;
     console.log(x); // undefined

     let obj = {};
     console.log(obj.property); // undefined
     ```

2. **Null (Trống):**

   - "Null" là giá trị biểu thị một biến đã được khởi tạo và gán giá trị là "null".
   - Điều này thường được sử dụng khi bạn muốn rõ ràng chỉ định rằng một biến không có giá trị hoặc chưa có dữ liệu.
   - "Null" thường được sử dụng trong các tình huống ngữ cảnh hợp lý, ví dụ như khi bạn muốn đặt một biến trạng thái của đối tượng thành "không có dữ liệu".
   - Ví dụ:

     ```javascript
     let y = null;
     console.log(y); // null

     let user = {
       name: null,
       age: 25,
     };
     console.log(user.name); // null
     ```

Tóm lại, "undefined" thường xuất hiện khi một biến không có giá trị hoặc khi truy cập vào thuộc tính không tồn tại của đối tượng, trong khi "null" thường được sử dụng để biểu thị rõ ràng sự thiếu vắng của dữ liệu hoặc trạng thái không xác định.

# Typescript

Typescript compiles to Javascript và nó có thể execute bởi bất kỳ Javascript engine nào

Lợi ích của Typescript

- Hỗ trợ static typing, optionally strongly typed
- Type inference
- Access to ES6 và ES7 features

1. `Phân biệt interface và type trong typescript`

   Trong TypeScript, interface và type đều được sử dụng để định nghĩa kiểu dữ liệu. Dưới đây là những điểm khác biệt chính giữa interface và type trong TypeScript:

   1. Syntax: Interface được khai báo bằng từ khóa `interface`, trong khi type được khai báo bằng từ khóa `type`.

   2. Object Shape vs. Type Alias: Interface chủ yếu được sử dụng để định nghĩa hình dạng của một đối tượng, bao gồm các thuộc tính và phương thức. Ngoài ra, interface cũng có thể được sử dụng để định nghĩa kiểu của hàm. Trong khi đó, type (còn được gọi là type alias) có thể biểu diễn nhiều kiểu dữ liệu khác nhau, bao gồm kiểu đối tượng, kiểu hợp (union type), kiểu giao (intersection type), và nhiều hơn nữa. Type linh hoạt hơn trong việc định nghĩa các kiểu dữ liệu tùy chỉnh hơn chỉ là hình dạng của đối tượng.

   3. Extensibility: Interface có thể được mở rộng từ các interface khác bằng cách sử dụng từ khóa `extends`, cho phép tạo ra các cấu trúc kế thừa. Điều này có nghĩa là một interface có thể kế thừa các thuộc tính và phương thức từ một interface khác. Type alias không hỗ trợ kế thừa hoặc mở rộng.

   4. Declaration Merging: Interface trong TypeScript hỗ trợ gộp khai báo (declaration merging), điều này có nghĩa là bạn có thể khai báo một interface nhiều lần và TypeScript sẽ tự động gộp các khai báo lại với nhau. Điều này cho phép bạn dần dần thêm các thuộc tính hoặc phương thức vào interface đã tồn tại. Type alias không hỗ trợ gộp khai báo.

   5. Implementability: Interface có thể được triển khai (implement) bởi các lớp (classes) hoặc các đối tượng (objects). Khi một lớp hoặc đối tượng triển khai một interface, nó phải tuân thủ cấu trúc và hành vi được định nghĩa bởi interface đó. Type alias, tuy nhiên, không thể được triển khai trực tiếp bởi các lớp hoặc đối tượng.

   6. Đọc và tài liệu: Interface thường được ưa chuộng khi tập trung vào việc cung cấp tài liệu rõ ràng và mô tả cho hình dạng dự kiến của các đối tượng, vì chúng dễ hiểu trong việc mô tả mục đích và cách sử dụng. Type alias thích hợp hơn để định nghĩa các kiểu dữ liệu phức tạp hoặc có thể tái sử dụng hơn, vượt qua khái niệm chỉ là hình dạng của đối tượng.

      Nhìn chung, nếu bạn cần định nghĩa hình dạng của một đối tượng, bao gồm các thuộc tính và phương thức, và có thể mô tả hành vi dự kiến, interface là lựa chọn tốt. Nếu bạn cần tính linh hoạt hơn, chẳng hạn như tạo kiểu hợp (union type) hoặc định nghĩa các kiểu dữ liệu phức tạp, type alias là lựa chọn phù hợp hơn. Tuy nhiên, interface và type alias thường có thể được sử dụng thay thế cho nhau, và việc chọn giữa chúng phụ thuộc vào yêu cầu cụ thể và thiết kế của dự án TypeScript của bạn.

2. `Khi nhấn lệnh yarn build thì chương trình sẽ làm gì trong một ứng dụng nodejs typescipt `

   Khi bạn chạy lệnh `yarn build` trong một ứng dụng Node.js TypeScript, thường sẽ có một quy trình build được thực hiện để biên dịch và tạo ra phiên bản sản phẩm của ứng dụng. Dưới đây là các bước phổ biến trong quá trình build một ứng dụng Node.js TypeScript:

   1. Kiểm tra cú pháp và kiểm tra kiểu (Linting & Type Checking): Đầu tiên, mã nguồn TypeScript của bạn thường sẽ được kiểm tra cú pháp (linting) để đảm bảo tuân thủ quy tắc viết mã. Sau đó, TypeScript Compiler (tsc) sẽ kiểm tra kiểu (type checking) để phát hiện và báo lỗi các sai sót liên quan đến kiểu dữ liệu.

   2. Biên dịch TypeScript thành JavaScript: Sau khi kiểm tra cú pháp và kiểu, mã nguồn TypeScript sẽ được biên dịch thành mã JavaScript. Quá trình này thường bao gồm sử dụng TypeScript Compiler (tsc) để chuyển đổi mã nguồn TypeScript thành JavaScript tương ứng. Tùy thuộc vào cấu hình của dự án, bạn có thể cấu hình tsc để tạo ra các phiên bản JavaScript tương thích với phiên bản ECMAScript cụ thể hoặc các phiên bản cũ hơn.

   3. Xử lý tệp tin tĩnh và tài nguyên: Quá trình build cũng có thể bao gồm xử lý các tệp tin tĩnh và tài nguyên, chẳng hạn như hình ảnh, tệp CSS, tệp HTML, và các tệp tin khác. Các tệp tin này có thể được sao chép hoặc di chuyển vào thư mục đích trong cấu trúc thư mục đích của phiên bản sản phẩm.

   4. Tối ưu và nén tệp tin: Trong quá trình build, bạn có thể áp dụng các quy tắc tối ưu và nén tệp tin để giảm kích thước và cải thiện hiệu suất của ứng dụng. Điều này có thể bao gồm việc loại bỏ các mã không sử dụng, nén và tối ưu hóa tệp tin CSS, tệp tin JavaScript và các tệp tin tĩnh khác.

   5. Tạo phiên bản sản phẩm (distribution): Cuối cùng, quá trình build có thể tạo ra phiên bản sản phẩm (distribution) của ứng dụng Node.js TypeScript. Điều này thường bao gồm việc sao chép các tệp tin biên dịch và tệp tin tĩnh khác vào một thư mục hoặc cấu trúc thư mục đích chuẩn để triển khai ứng dụng.

   Các bước và công đoạn trong quá trình build có thể thay đổi tùy thuộc vào cấu hình và yêu cầu của dự án cụ thể.

3. `Phân biệt yarn build và yarn run build`

   Trong `yarn`, có sự khác biệt giữa lệnh `yarn build` và `yarn run build`. Dưới đây là sự phân biệt giữa hai lệnh này:

   1. `yarn build`: Khi bạn chạy lệnh `yarn build`, `yarn` sẽ tìm kiếm một script có tên `build` trong phần `"scripts"` của file `package.json`. Nếu script này được tìm thấy, `yarn` sẽ thực thi nó. Nếu không có script `build`, lệnh `yarn build` sẽ không có hiệu lực. Ví dụ: `"scripts": { "build": "tsc" }`. Trong ví dụ này, khi chạy `yarn build`, `tsc` (TypeScript Compiler) sẽ được thực thi.

   2. `yarn run build`: Khi bạn chạy lệnh `yarn run build`, `yarn` sẽ chạy một script cụ thể được chỉ định, thường là script có tên `build`. Script này không cần phải được khai báo trong phần `"scripts"` của file `package.json`. Ví dụ: `yarn run build`. Trong ví dụ này, `yarn` sẽ tìm và thực thi script `build` mà không cần phải khai báo trong `package.json`.

   Tóm lại, `yarn build` thực thi script có tên `build` trong phần `"scripts"` của `package.json`, trong khi `yarn run build` thực thi một script có tên `build` mà không cần phải khai báo trong `package.json`.

4. Phân biệt file `.d.ts` và `.ts`

   Trong TypeScript, có hai loại tệp tin phổ biến có phần mở rộng `.d.ts` và `.ts`. Dưới đây là sự phân biệt giữa hai loại tệp tin này:

   1. Tệp tin `.d.ts` (Declaration File):

      - Tệp tin `.d.ts` được sử dụng để định nghĩa các khai báo kiểu (type declarations) cho các thư viện JavaScript không có sẵn kiểu dữ liệu TypeScript.
      - Nó cung cấp thông tin về kiểu dữ liệu, giao diện, lớp, hằng số, và các phần tử khác của các thư viện JavaScript để TypeScript hiểu được cách sử dụng chúng và kiểm tra kiểu dữ liệu chính xác.
      - Tệp tin `.d.ts` không chứa mã thực thi JavaScript. Nó chỉ chứa thông tin kiểu dữ liệu để TypeScript sử dụng trong quá trình phân tích và kiểm tra mã nguồn TypeScript.
      - Các tệp tin `.d.ts` thường được tạo ra tự động bởi trình biên dịch TypeScript hoặc các công cụ khác như `dts-gen`.

   2. Tệp tin `.ts` (TypeScript File):
      - Tệp tin `.ts` chứa mã nguồn TypeScript, bao gồm khai báo biến, hàm, lớp, giao diện, kiểu dữ liệu và mã thực thi.
      - TypeScript Compiler (tsc) sẽ biên dịch các tệp tin `.ts` thành mã JavaScript tương ứng.
      - Mã TypeScript trong các tệp tin `.ts` có thể sử dụng các tính năng của TypeScript như kiểu dữ liệu tĩnh, hỗ trợ kiểm tra kiểu dữ liệu tại thời gian biên dịch, kế thừa, giao diện, và các tính năng nâng cao khác của ngôn ngữ TypeScript.

   Tóm lại, tệp tin `.d.ts` được sử dụng để cung cấp khai báo kiểu cho các thư viện JavaScript, trong khi tệp tin `.ts` chứa mã nguồn TypeScript cho dự án của bạn.

5. `Generic trong typescrcipt là gì ?`

   Trong TypeScript, generics là một tính năng cho phép bạn định nghĩa các loại (types) hoặc hàm mà làm việc với một loạt các kiểu dữ liệu thay thế. Generics cho phép bạn tạo các thành phần động và linh hoạt, tức là bạn có thể sử dụng cùng một mã để xử lý nhiều kiểu dữ liệu khác nhau mà không cần viết lại mã cho từng kiểu riêng biệt.

   Để định nghĩa generics trong TypeScript, bạn sử dụng các tham số kiểu (type parameter) để biểu thị kiểu dữ liệu đó sẽ được xác định sau khi generics được sử dụng. Cú pháp chung của generics trong TypeScript là:

   ```typescript
   function functionName<T>(param: T): T {
     // code implementation here
   }
   ```

   Trong đó, `T` là tham số kiểu (type parameter) và có thể là bất kỳ tên nào bạn muốn, nhưng thường là `T` để biểu thị "type". Khi bạn gọi hàm `functionName` và cung cấp kiểu dữ liệu cụ thể, TypeScript sẽ thay thế `T` bằng kiểu dữ liệu mà bạn đã cung cấp.

   Ví dụ, ta có thể viết một hàm sử dụng generics để hoán đổi giá trị của hai biến:

   ```typescript
   function swap<T>(a: T, b: T): void {
     let temp: T = a;
     a = b;
     b = temp;
   }

   // Sử dụng generics để hoán đổi số nguyên
   let num1: number = 5;
   let num2: number = 10;
   swap<number>(num1, num2);
   console.log(num1, num2); // Output: 10, 5

   // Sử dụng generics để hoán đổi chuỗi
   let str1: string = "hello";
   let str2: string = "world";
   swap<string>(str1, str2);
   console.log(str1, str2); // Output: "world", "hello"
   ```

   Như bạn có thể thấy, generics cho phép hàm `swap` hoạt động với nhiều kiểu dữ liệu khác nhau, mà không cần viết lại mã cho từng kiểu cụ thể. Điều này giúp tăng tính linh hoạt và tái sử dụng trong mã TypeScript.

6. `OOP trong typescript`

   Trong TypeScript, cũng giống như trong JavaScript, bạn có thể sử dụng lập trình hướng đối tượng để tạo các lớp, đối tượng, kế thừa, tính đa hình và đóng gói. Tuy nhiên, TypeScript hỗ trợ mạnh mẽ hơn với tính năng kiểu tĩnh, giúp bạn có thể xác định kiểu dữ liệu của các thuộc tính và phương thức của lớp.

   Dưới đây là một ví dụ về cách sử dụng OOP trong TypeScript:

   ```typescript
   // Định nghĩa lớp
   class Person {
     // Thuộc tính với kiểu dữ liệu được xác định
     name: string;
     age: number;

     // Constructor
     constructor(name: string, age: number) {
       this.name = name;
       this.age = age;
     }

     // Phương thức của lớp
     sayHello(): void {
       console.log(
         `Hello, my name is ${this.name} and I am ${this.age} years old.`
       );
     }
   }

   // Kế thừa lớp
   class Student extends Person {
     // Thuộc tính riêng của lớp con
     studentId: string;

     // Constructor của lớp con
     constructor(name: string, age: number, studentId: string) {
       // Gọi constructor của lớp cha bằng từ khóa "super"
       super(name, age);
       this.studentId = studentId;
     }

     // Ghi đè phương thức của lớp cha
     sayHello(): void {
       console.log(
         `Hello, my name is ${this.name}, I am ${this.age} years old, and my student ID is ${this.studentId}.`
       );
     }
   }

   // Tạo đối tượng từ lớp
   const person1 = new Person("Alice", 30);
   const student1 = new Student("Bob", 25, "12345");

   person1.sayHello(); // Hello, my name is Alice and I am 30 years old.
   student1.sayHello(); // Hello, my name is Bob, I am 25 years old, and my student ID is 12345.
   ```

   Trong TypeScript, bạn có thể xác định các kiểu dữ liệu cho các thuộc tính và tham số của hàm tạo (constructor) để đảm bảo tính chính xác và an toàn của mã. Ngoài ra, bạn cũng có thể sử dụng tính năng kế thừa và ghi đè phương thức như trong ví dụ trên. TypeScript sẽ kiểm tra kiểu dữ liệu và đảm bảo rằng bạn không thực hiện các thao tác không hợp lệ với đối tượng của lớp.

7. `Partial trong typescript là gì`

   Trong TypeScript, "Partial" là một loại kiểu dữ liệu được tích hợp sẵn trong ngôn ngữ. Nó cho phép bạn tạo ra một phiên bản mới của một kiểu dữ liệu, nhưng với tất cả các thuộc tính của nó đều trở thành tùy chọn (optional). Điều này hữu ích khi bạn muốn chỉ thay đổi một số thuộc tính của một đối tượng mà không cần phải chỉ định tất cả các thuộc tính bắt buộc.

   Cú pháp của "Partial" trong TypeScript như sau:

   ```typescript
   type Partial<T> = {
     [P in keyof T]?: T[P];
   };
   ```

   Trong đó:

   - "T" là kiểu dữ liệu đang có.
   - "keyof T" là một phép toán kiểu dữ liệu, nó tạo ra một liệt kê (union) các tên thuộc tính trong kiểu "T".
   - "[P in keyof T]" là một index signature, cho phép bạn duyệt qua tất cả các thuộc tính của "T".
   - "?: T[P]" là tạo ra các thuộc tính tùy chọn bằng cách thêm "?" vào trước mỗi thuộc tính, điều này đồng nghĩa với việc làm cho các thuộc tính đó trở thành tùy chọn (optional).

   Ví dụ:

   ```typescript
   interface Person {
     name: string;
     age: number;
     email: string;
   }

   // Tạo một kiểu mới với tất cả các thuộc tính của Person đều trở thành optional
   type PartialPerson = Partial<Person>;

   const partialPerson: PartialPerson = {
     name: "John", // Được phép chỉ cung cấp một phần các thuộc tính
   };
   ```

   Trong ví dụ trên, kiểu "PartialPerson" sẽ có cùng cấu trúc với kiểu "Person", nhưng tất cả các thuộc tính của nó đều trở thành tùy chọn. Điều này cho phép bạn chỉ cần cung cấp một phần các thuộc tính khi khởi tạo đối tượng, thay vì phải cung cấp tất cả các thuộc tính bắt buộc của "Person".

8. `Typescript là gì ? Tại sao chúng ta nên sử dụng typescript`

   TypeScript là một ngôn ngữ lập trình mã nguồn mở được phát triển và duy trì bởi Microsoft. Nó là một siêu cú pháp (superset) của JavaScript, điều đó có nghĩa là TypeScript mở rộng các tính năng của JavaScript bằng cách thêm các khái niệm và công cụ mới để làm cho việc lập trình trở nên dễ dàng hơn và an toàn hơn.

   Một số đặc điểm chính của TypeScript bao gồm:

   1. Kiểu dữ liệu tĩnh: TypeScript hỗ trợ kiểu dữ liệu tĩnh (static typing), cho phép bạn xác định kiểu dữ liệu của biến, tham số và giá trị trả về của hàm trong quá trình phát triển. Việc này giúp tăng tính chính xác và hiểu rõ hơn về mã nguồn, đồng thời giúp phát hiện lỗi phát sinh trước khi chương trình được chạy.

   2. Tính đa hình (Polymorphism): TypeScript hỗ trợ tính đa hình, cho phép bạn tạo các lớp con (subclasses) kế thừa từ các lớp cha (superclasses) và ghi đè các phương thức hoặc thuộc tính của lớp cha. Điều này giúp tái sử dụng mã nguồn, dễ dàng mở rộng và bảo trì ứng dụng.

   3. Quản lý kiểu dữ liệu: TypeScript cung cấp các kiểu dữ liệu gốc như số, chuỗi, mảng, v.v. và cho phép bạn xây dựng kiểu dữ liệu tùy chỉnh của riêng mình. Điều này giúp giảm thiểu lỗi liên quan đến kiểu dữ liệu và cung cấp thông tin phong phú hơn về các đối tượng trong chương trình.

   4. Hỗ trợ ES6+: TypeScript hỗ trợ toàn bộ các tính năng của ECMAScript 6 (ES6) và phiên bản sau này, bao gồm khái niệm khai báo biến "let" và "const", hàm mũi tên, module, lớp, promise, async/await, v.v. Điều này giúp bạn viết mã hiện đại và dễ đọc hơn.

   Tại sao nên dùng TypeScript?

   1. Tăng tính bảo mật và ổn định: Kiểu dữ liệu tĩnh giúp phát hiện các lỗi kiểu dữ liệu trong quá trình phát triển, giúp bạn tránh một số lỗi thường gặp khi chạy mã JavaScript.

   2. Tăng hiệu suất và hiệu quả: TypeScript giúp viết mã dễ dàng hơn và cung cấp thông tin phong phú hơn về mã nguồn, điều này giúp tăng hiệu suất và hiệu quả trong việc phát triển và bảo trì ứng dụng.

   3. Hỗ trợ cộng đồng lớn: TypeScript có một cộng đồng phong phú và lớn, với nhiều thư viện và công cụ hữu ích cho việc phát triển ứng dụng.

   4. Hỗ trợ tích hợp tốt: TypeScript tích hợp tốt với các công cụ phổ biến khác như Babel, Webpack, ESLint, v.v., giúp bạn dễ dàng tích hợp vào quy trình phát triển hiện có.

   Tóm lại, TypeScript là một công cụ mạnh mẽ và hiệu quả để phát triển ứng dụng web và Node.js, giúp tăng tính chính xác và an toàn trong việc lập trình và mang lại nhiều lợi ích cho các dự án phát triển phức tạp.

9. `Phân biệt never, unknown và any trong typescript`

   "never", "unknown", và "any" là các kiểu dữ liệu đặc biệt trong TypeScript, và chúng có mục đích sử dụng khác nhau. Dưới đây là sự so sánh giữa chúng:

   1. "never":

   - "never" là một kiểu dữ liệu đại diện cho các giá trị không bao giờ xảy ra.
   - Khi một hàm không bao giờ trả về (không có lệnh "return" hoặc luôn throw exception), kiểu trả về của hàm đó sẽ là "never".
   - Nó được sử dụng khi hàm không thể kết thúc hoặc khi phải tung ra một ngoại lệ (exception) và dừng toàn bộ chương trình.
   - Cũng được sử dụng khi union type chứa các kiểu không thể giao dịch với nhau (ví dụ: number và string).

   Ví dụ:

   ```typescript
   function throwError(message: string): never {
     throw new Error(message);
   }

   function infiniteLoop(): never {
     while (true) {
       // Vòng lặp vô hạn, hàm không bao giờ kết thúc
     }
   }
   ```

   2. "unknown":

   - "unknown" là một kiểu dữ liệu mới được giới thiệu trong TypeScript 3.0.
   - Đây là kiểu dữ liệu an toàn hơn "any", nhưng ít linh hoạt hơn. Đối với "unknown", bạn phải xác định kiểu dữ liệu trước khi sử dụng nó.
   - Khác với "any", bạn không thể gọi bất kỳ phương thức nào, hoặc truy cập bất kỳ thuộc tính nào của giá trị "unknown" mà không kiểm tra kiểu dữ liệu trước.

   Ví dụ:

   ```typescript
   let value: unknown;

   value = 5; // Gán giá trị kiểu number cho value

   // Kiểm tra kiểu dữ liệu trước khi sử dụng
   if (typeof value === "number") {
     const result = value * 2;
     console.log(result); // In ra 10
   }
   ```

   3. "any":

   - "any" là kiểu dữ liệu linh hoạt nhất trong TypeScript.
   - Khi một biến có kiểu dữ liệu là "any", bạn có thể thực hiện bất kỳ hoạt động nào trên nó mà không cần kiểm tra kiểu dữ liệu.
   - Điều này giúp giảm tính an toàn trong việc phát hiện lỗi và hiểu rõ hơn về mã nguồn.

   Ví dụ:

   ```typescript
   let data: any;

   data = 10; // Gán giá trị kiểu number cho data
   const result = data * 2; // Không cần kiểm tra kiểu dữ liệu

   console.log(result); // In ra 20
   ```

   Tóm lại:

   - "never" là kiểu dữ liệu cho các giá trị không bao giờ xảy ra.
   - "unknown" là kiểu dữ liệu an toàn hơn "any", bạn phải kiểm tra kiểu trước khi sử dụng.
   - "any" là kiểu dữ liệu linh hoạt nhất, không kiểm tra kiểu dữ liệu và giảm tính an toàn trong việc phát hiện lỗi.

10. `Phân biệt type và interface trong typescript`

    Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

    Trong TypeScript, "interface" và "type" đều được sử dụng để định nghĩa các kiểu dữ liệu tùy chỉnh, nhưng chúng có một số điểm khác nhau và giống nhau. Dưới đây là phân biệt và ví dụ chi tiết cho mỗi loại:

    **1. Interface:**

    - "interface" là một cách để định nghĩa kiểu dữ liệu tùy chỉnh cho các đối tượng (objects).
    - Nó cho phép bạn xác định cụ thể các thuộc tính (properties) và phương thức (methods) mà các đối tượng của kiểu dữ liệu đó phải có.
    - Các interface có thể mở rộng (extend) nhau để tạo ra các kiểu dữ liệu phức tạp hơn.
    - Interface cũng hỗ trợ kế thừa đa hình (polymorphism), cho phép một đối tượng có thể có nhiều loại dữ liệu.

    Ví dụ:

    ```typescript
    interface Person {
      name: string;
      age: number;
    }

    interface Employee extends Person {
      jobTitle: string;
    }

    const john: Employee = {
      name: "John",
      age: 30,
      jobTitle: "Software Engineer",
    };
    ```

    **2. Type:**

    - "type" cũng là một cách để định nghĩa kiểu dữ liệu tùy chỉnh, tuy nhiên nó linh hoạt hơn interface về mặt khai báo.
    - Nó cho phép bạn định nghĩa các kiểu union, intersection và các kiểu dữ liệu phức tạp khác mà không cần phải chỉ định các thuộc tính hay phương thức cụ thể.
    - "type" cũng có thể sử dụng cho các kiểu dữ liệu nguyên thủy như string, number, boolean, v.v.

    Ví dụ:

    ```typescript
    type Person = {
      name: string;
      age: number;
    };

    type Employee = Person & {
      jobTitle: string;
    };

    const jane: Employee = {
      name: "Jane",
      age: 25,
      jobTitle: "Project Manager",
    };
    ```

    **Giống nhau:**

    - Cả "interface" và "type" đều có thể được sử dụng để định nghĩa các kiểu dữ liệu tùy chỉnh.
    - Cả hai đều hỗ trợ các kiểu dữ liệu phức tạp như union và intersection.
    - Cả hai đều cho phép bạn tái sử dụng kiểu dữ liệu đã định nghĩa trong nhiều đối tượng.

    **Khác nhau:**

    - "interface" chỉ hỗ trợ định nghĩa kiểu dữ liệu cho các đối tượng, trong khi "type" có thể được sử dụng cho nhiều mục đích khác nhau, bao gồm cả đối tượng, union types, intersection types, v.v.
    - Khi sử dụng "interface", bạn không thể sử dụng các tính năng như union types, intersection types, và mapped types, trong khi "type" hỗ trợ tất cả các tính năng này.
    - "interface" thường được sử dụng trong các trường hợp đơn giản hơn, trong khi "type" thường được sử dụng trong các trường hợp phức tạp hơn và cần linh hoạt cao hơn trong định nghĩa kiểu dữ liệu.

    Tóm lại, cả "interface" và "type" đều hỗ trợ định nghĩa kiểu dữ liệu tùy chỉnh trong TypeScript, nhưng có một số sự khác biệt trong cách sử dụng và tính linh hoạt. Lựa chọn giữa "interface" và "type" phụ thuộc vào yêu cầu cụ thể của bạn và mức độ phức tạp của kiểu dữ liệu bạn muốn định nghĩa.

11. `Phân biệt require và import trong nodejs`

    "Sự khác biệt giữa "require" và "import" liên quan đến cách Node.js và các phiên bản ECMAScript (ES) xử lý cú pháp và tải module trong mã nguồn.

    **1. require:**

    - "require" là một cú pháp được sử dụng trong Node.js để tải các module và sử dụng chúng trong mã nguồn.
    - "require" không phải là một tính năng của JavaScript chuẩn, mà là một tính năng đặc biệt của Node.js.

    Ví dụ:

    ```javascript
    const express = require("express");
    const fs = require("fs");
    ```

    **2. import:**

    - "import" là một tính năng thuộc chuẩn ECMAScript, được giới thiệu trong ES6 (ES2015).
    - "import" được sử dụng trong các phiên bản JavaScript hiện đại và trong các trình duyệt hỗ trợ ES6 trở lên để tải các module và sử dụng chúng trong mã nguồn.

    Ví dụ:

    ```javascript
    import express from "express";
    import fs from "fs";
    ```

    **Sự khác biệt chính:**

    - "require" là cú pháp sử dụng trong Node.js để tải module, trong khi "import" là cú pháp thuộc chuẩn ECMAScript để tải module.
    - "require" sử dụng cú pháp CommonJS trong Node.js và không yêu cầu trình duyệt hỗ trợ ES6, trong khi "import" yêu cầu trình duyệt hỗ trợ ES6 hoặc phải được biên dịch thành ES5 bằng trình biên dịch như Babel để hoạt động.
    - Khi sử dụng "import", bạn cần thêm thuộc tính "type=module" vào file HTML để cho phép trình duyệt nhận diện cú pháp import.

    ```html
    <script type="module" src="main.js"></script>
    ```

    **Lưu ý:**

    - Nếu bạn sử dụng Node.js và muốn sử dụng "import" thay vì "require", bạn cần sử dụng flag `--experimental-modules` khi chạy Node.js. Tuy nhiên, trong nhiều trường hợp, người ta vẫn ưa thích sử dụng "require" trong Node.js để tránh vấn đề tương thích và không cần thiết phải cấu hình thêm.

12. `Phân biệt promise và callback`

    "Sự khác biệt giữa callback và Promise trong Node.js" liên quan đến cách xử lý các hoạt động bất đồng bộ (asynchronous operations) trong mã nguồn.

    **1. Callback:**

    - Callback là một hàm được truyền làm đối số cho một hàm khác, và được gọi lại sau khi hoạt động bất đồng bộ hoàn thành.
    - Callback được sử dụng phổ biến trong Node.js trước khi Promise được giới thiệu và thường được sử dụng trong các phiên bản JavaScript cũ hơn.
    - Mô hình callback có thể gây ra tình trạng "callback hell" khi có quá nhiều hoạt động bất đồng bộ liên tiếp, khiến mã trở nên khó đọc và khó bảo trì.

    Ví dụ sử dụng callback trong Node.js:

    ```javascript
    const fs = require("fs");

    fs.readFile("file.txt", "utf8", (err, data) => {
      if (err) {
        console.error("Error reading file:", err);
      } else {
        console.log("File content:", data);
      }
    });
    ```

    **2. Promise:**

    - Promise là một cơ chế hỗ trợ xử lý các hoạt động bất đồng bộ trong JavaScript.
    - Promise giúp tránh tình trạng "callback hell" bằng cách cho phép xử lý các hoạt động bất đồng bộ một cách tuần tự và dễ đọc hơn.
    - Promise hỗ trợ xử lý kết quả thành công (resolve) và kết quả thất bại (reject), cho phép bạn dễ dàng xử lý lỗi.

    Ví dụ sử dụng Promise trong Node.js:

    ```javascript
    const fs = require("fs");

    const readFilePromise = (filename) => {
      return new Promise((resolve, reject) => {
        fs.readFile(filename, "utf8", (err, data) => {
          if (err) {
            reject(err);
          } else {
            resolve(data);
          }
        });
      });
    };

    readFilePromise("file.txt")
      .then((data) => {
        console.log("File content:", data);
      })
      .catch((err) => {
        console.error("Error reading file:", err);
      });
    ```

    **Sự khác biệt chính:**

    - Callback là một cơ chế cũ và sử dụng phổ biến trước khi Promise được giới thiệu.
    - Promise là một cơ chế mới và cải tiến để xử lý hoạt động bất đồng bộ và tránh tình trạng callback hell.
    - Promise cho phép bạn xử lý các kết quả thành công và thất bại một cách dễ dàng và tuần tự hơn.

    Khi làm việc với Node.js và các hoạt động bất đồng bộ, việc sử dụng Promise là một lựa chọn tốt để làm mã nguồn của bạn dễ đọc và dễ quản lý hơn.

13. `Mapped type trong typescript`

    Trong TypeScript, "Mapped type" là một tính năng mạnh mẽ cho phép bạn tạo ra các loại mới dựa trên một loại đã tồn tại. Điều này cho phép bạn tạo ra các loại mới với các thuộc tính được thay đổi hoặc tùy chỉnh từ loại gốc mà không cần phải viết lại mã lặp đi lặp lại.

    Để sử dụng Mapped type, bạn sử dụng cú pháp `{ [P in K]: T }`, trong đó:

    - `[P in K]` là phần dựng loại, cho phép bạn duyệt qua tất cả các thuộc tính trong loại K (thường là một chuỗi đại diện cho tên thuộc tính).
    - `T` là loại dữ liệu mới bạn muốn sử dụng cho các thuộc tính.

    Ví dụ, giả sử bạn có một interface "Person" như sau:

    ```typescript
    interface Person {
      name: string;
      age: number;
      email: string;
    }
    ```

    Bạn muốn tạo một phiên bản của "Person" nhưng loại "age" và "email" sẽ trở thành tùy chọn. Bạn có thể sử dụng Mapped type để làm điều này:

    ```typescript
    type PartialPerson = { [P in "name" | "age" | "email"]?: Person[P] };
    ```

    Trong ví dụ trên, "PartialPerson" sẽ có cùng các thuộc tính như "Person", nhưng tất cả các thuộc tính đều trở thành tùy chọn (thêm "?" trước mỗi thuộc tính).

    Bây giờ, bạn có thể sử dụng "PartialPerson" như sau:

    ```typescript
    const person: PartialPerson = { name: "John" };
    ```

    Lưu ý rằng, bạn có thể sử dụng Mapped type không chỉ với các union types (như trong ví dụ trên), mà cũng với các loại động được xác định bởi keyof và các thuộc tính của loại gốc. Điều này cho phép bạn tạo các loại mới dựa trên bất kỳ loại nào và sử dụng lại các loại phức tạp mà không cần phải viết lại mã. Mapped type là một công cụ mạnh mẽ trong TypeScript giúp tăng tính tái sử dụng mã và tăng cường tính linh hoạt của mã TypeScript.

# Test

- UnitTest: Bảo vệ code khi sửa code trong tương lai, tránh lỗi của quá khứ', mục tiêu của unit test là cô lập một phần code và xác minh tính chính xác của đoạn code đó

# Back end

1. `Microservice và Monolithic khác nhau ở chỗ nào? Ưu nhược điểm mỗi thứ so với nhau`

   - Monolithic: Trong kiến trúc Monolithic, toàn bộ ứng dụng được xây dựng và triển khai như một đơn vị duy nhất. Tất cả các thành phần của ứng dụng chia sẻ cùng một cơ sở dữ liệu và quy trình thực thi. Ưu điểm của Monolithic là dễ triển khai và quản lý đơn giản, phù hợp cho các ứng dụng nhỏ và đơn giản. Nhược điểm là khả năng mở rộng hạn chế, việc thay đổi và bảo trì khó khăn, và khi một thành phần gặp vấn đề, toàn bộ hệ thống có thể bị ảnh hưởng.

   - Microservice: Trong kiến trúc Microservice, ứng dụng được chia thành các thành phần nhỏ gọn và độc lập, được gọi là microservice, mỗi service có thể triển khai và quản lý riêng biệt. Các microservice giao tiếp thông qua các giao thức như HTTP hoặc message queue. Ưu điểm của Microservice là khả năng mở rộng linh hoạt, dễ dàng thay đổi và triển khai các thành phần riêng lẻ, khả năng phân tán phát triển và tối ưu hóa hiệu suất. Nhược điểm là phức tạp hóa quản lý, khó khăn trong việc điều phối các service và tăng khả năng lỗi do mạng hoặc sự phụ thuộc giữa các service.

2. ` Clean architecture là gì ? ví dụ về clean architecture`

   Clean Architecture là một kiến trúc phần mềm đề xuất bởi Robert C. Martin (còn được gọi là Uncle Bob). Nó tách biệt các thành phần của một ứng dụng thành các lớp độc lập và định nghĩa rõ ràng các quy tắc và giới hạn giữa chúng. Mục tiêu chính của Clean Architecture là tạo ra một hệ thống dễ bảo trì, dễ mở rộng và độc lập với các công nghệ cụ thể.

   Clean Architecture tuân thủ nguyên tắc SOLID (Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, Dependency Inversion), và cung cấp một cách tiếp cận tổ chức mã nguồn tập trung vào sự phân chia rõ ràng giữa các thành phần, giúp giảm sự phụ thuộc giữa chúng và dễ dàng thay đổi hoặc thay thế một thành phần mà không ảnh hưởng đến các thành phần khác.

   Một ví dụ về ứng dụng sử dụng Clean Architecture là ứng dụng Android chứa các thành phần sau:

   1. Domain Layer (Lớp Miền): Đây là lớp chứa luật kinh doanh, giao diện và logic của ứng dụng. Nó không phụ thuộc vào bất kỳ thư viện hay framework nào khác và định nghĩa các use case cốt lõi của ứng dụng. Ví dụ: quản lý người dùng, xử lý dữ liệu, các luật tính toán.

   2. Data Layer (Lớp Dữ liệu): Lớp này làm nhiệm vụ truy cập và lưu trữ dữ liệu. Nó chịu trách nhiệm tương tác với cơ sở dữ liệu, API hoặc các nguồn dữ liệu khác. Lớp Dữ liệu cung cấp giao diện cho Lớp Miền để truy xuất và cập nhật dữ liệu.

   3. Presentation Layer (Lớp Trình bày): Lớp này xử lý việc hiển thị dữ liệu và tương tác người dùng. Nó làm việc với các thành phần giao diện người dùng như Activities, Fragments, Views và gọi các use case trong Lớp Miền để lấy và xử lý dữ liệu.

   4. Frameworks & Drivers (Các Framework và Trình điều khiển): Lớp này bao gồm các framework và thư viện bên ngoài như Android Framework, thư viện Retrofit, Dagger, Room, để hỗ trợ triển khai và kết nối các thành phần khác nhau của ứng dụng.

- Clean Architecture giúp tách biệt các thành phần của ứng dụng và tạo ra một sự phụ thuộc lỏng lẻo giữa chúng. Điều này giúp cho việc kiểm thử, bảo trì, và mở rộng ứng dụng trở nên dễ dàng hơn

  Nguyên tắc `SOLID` là một tập hợp các nguyên tắc lập trình hướng đối tượng được định hình bởi Robert C. Martin, còn được gọi là Uncle Bob, nhằm tăng tính bảo maintainability, mở rộng và tái sử dụng của mã nguồn. SOLID là một từ viết tắt đại diện cho năm nguyên tắc cơ bản sau đây:

  1.  Nguyên tắc đơn trách nhiệm (Single Responsibility Principle - SRP): Theo nguyên tắc này, một lớp hoặc module chỉ nên có một trách nhiệm duy nhất. Nếu một đối tượng hoặc lớp có quá nhiều trách nhiệm, việc bảo trì và sửa đổi sẽ trở nên khó khăn và dễ gây lỗi.

  2.  Nguyên tắc mở/đóng (Open/Closed Principle - OCP): Nguyên tắc này đề xuất rằng mã nguồn cần phải mở cho việc mở rộng (có thể thêm tính năng mới) nhưng đóng cho việc sửa đổi mã nguồn gốc. Điều này đảm bảo rằng khi thay đổi hoặc mở rộng chức năng, chúng ta không cần chỉnh sửa mã nguồn hiện tại mà chỉ cần viết mã mới.

  3.  Nguyên tắc thay thế Liskov (Liskov Substitution Principle - LSP): Nguyên tắc này đề cập đến tính đúng đắn trong việc kế thừa của đối tượng. Tức là, đối tượng con của một lớp nên có thể thay thế cho đối tượng của lớp cha mà không làm thay đổi tính đúng đắn của chương trình.

  4.  Nguyên tắc phân tách giao diện (Interface Segregation Principle - ISP): Nguyên tắc này khuyến khích chia các giao diện lớn thành các giao diện nhỏ, cụ thể và đồng nhất để các lớp chỉ triển khai các giao diện cần thiết cho họ. Điều này giúp tránh việc các lớp phải triển khai các phương thức không liên quan đến mục đích của chúng.

  5.  Nguyên tắc độc lập với kiểu (Dependency Inversion Principle - DIP): Nguyên tắc này tập trung vào việc giảm sự phụ thuộc trực tiếp giữa các lớp và module. Thay vào đó, các module nên phụ thuộc vào một giao diện chung thay vì một lớp cụ thể. Điều này giúp giảm thiểu tác động khi thay đổi mã nguồn và tăng tính linh hoạt trong hệ thống.

3. `Phân biệt middleware và interceptor trong nestjs`

- NestJS Middleware và Interceptor trong NestJS là các cơ chế được cung cấp bởi framework NestJS để xử lý yêu cầu trước và sau khi chúng đi qua các endpoint. Tuy nhiên, có một số khác biệt:
- Middleware: Là một hàm trung gian được gọi trước hoặc sau khi đi qua một endpoint. Middleware có thể thay đổi yêu cầu (request) hoặc phản hồi (response), và có khả năng chuyển quyền điều khiển cho middleware tiếp theo trong chuỗi middleware.
- Interceptor: Là một lớp hoạt động như một bộ lọc cho yêu cầu và phản hồi. Nó có thể thực hiện các thao tác trước và sau khi xử lý yêu cầu. Interceptor không thay đổi yêu cầu hoặc phản hồi, nhưng có thể thực hiện các hành động bổ sung như ghi log, xử lý lỗi, thêm thông tin, vv.

4. `Trong Nestjs, decorator là gì`

- Trong NestJS, Decorator là một tính năng của TypeScript cho phép bạn thêm metadata và mở rộng hoặc thay đổi hành vi của các class, phương thức, thuộc tính và tham số.
  Một decorator hoạt động bằng cách áp dụng một hàm hoặc một class decorator lên một class, phương thức hoặc thuộc tính cụ thể. Decorator được áp dụng bằng cách đặt nó trước đối tượng mà bạn muốn thay đổi hoặc mở rộng. Decorator có thể thay đổi các thuộc tính, thêm chức năng hoặc thực hiện các logic bổ sung trước hoặc sau khi đối tượng được khởi tạo hoặc gọi.
  8a. Một decorator phổ biến trong NestJS là `@Injectable()`. Decorator này được sử dụng để đánh dấu một class là một provider có thể được inject vào các class khác thông qua dependency injection của NestJS. Ví dụ:
  `typescript
			@Injectable()
			export class UserService {
				// ...
			}
	`
  Trong ví dụ trên, `@Injectable()` được áp dụng lên class `UserService` để đánh dấu nó là một provider có thể được inject vào các thành phần khác trong ứng dụng NestJS.

5. `Sequence trong nodejs là gì ?`

   Trong Node.js, "sequence" là một thuật ngữ được sử dụng để chỉ một chuỗi các hàm hoặc middleware được thực thi theo một thứ tự nhất định.

   Trong ngữ cảnh của Node.js và Express.js, một sequence thường được thực hiện như một chuỗi các middleware. Middleware là các hàm được gọi liên tiếp trong quá trình xử lý yêu cầu từ client và trước khi gửi phản hồi trả về client. Mỗi middleware có khả năng kiểm tra và thay đổi yêu cầu và phản hồi.

   Sequence (hay middleware sequence) cho phép bạn xác định các middleware và quy định thứ tự chúng được gọi trong quá trình xử lý yêu cầu. Thông thường, khi một yêu cầu được nhận, các middleware sẽ được gọi lần lượt từ đầu đến cuối của sequence. Mỗi middleware có thể thực hiện một số công việc nhất định, chẳng hạn như xác thực, ghi log, xử lý dữ liệu, và gọi middleware tiếp theo trong sequence bằng cách gọi hàm `next()`.

   Ví dụ, dưới đây là một ví dụ đơn giản về cách sử dụng sequence (middleware sequence) trong Node.js và Express.js:

   ```javascript
   const express = require("express");
   const app = express();

   // Middleware 1
   app.use((req, res, next) => {
     console.log("Middleware 1");
     next(); // Gọi middleware tiếp theo trong sequence
   });

   // Middleware 2
   app.use((req, res, next) => {
     console.log("Middleware 2");
     next(); // Gọi middleware tiếp theo trong sequence
   });

   // Route handler
   app.get("/", (req, res) => {
     res.send("Hello, World!");
   });

   app.listen(3000, () => {
     console.log("Server is running on port 3000");
   });
   ```

   Trong ví dụ trên, có hai middleware được đăng ký trong sequence của ứng dụng Express. Khi một yêu cầu GET đến đường dẫn "/" được nhận, trình tự của các middleware sẽ được theo đúng thứ tự: Middleware 1 sẽ được gọi trước, sau đó là Middleware 2 và cuối cùng là Route handler để xử lý yêu cầu và gửi phản hồi trả về client.

   Sequence (middleware sequence) là một khái niệm cơ bản và quan trọng trong Node.js và Express.js, cho phép bạn kiểm soát và mở rộng quy trình xử lý yêu cầu trong ứng dụng web.

6.`TypeOrm là gì ? `

TypeORM là một thư viện ORM (Object-Relational Mapping) được phát triển cho Node.js và TypeScript. Nó cung cấp một cách thuận tiện để tương tác với cơ sở dữ liệu SQL mà không cần viết trực tiếp các truy vấn SQL.

Với TypeORM, bạn có thể định nghĩa các mô hình dữ liệu (entities) dưới dạng các lớp TypeScript, và TypeORM sẽ tự động tạo và quản lý cấu trúc bảng trong cơ sở dữ liệu tương ứng. Nó cung cấp các khái niệm như migrations (di chuyển cấu trúc cơ sở dữ liệu), associations (quan hệ giữa các bảng), lazy loading (tải dữ liệu theo yêu cầu), và nhiều tính năng khác để hỗ trợ quản lý cơ sở dữ liệu.

Một số tính năng và lợi ích chính của TypeORM bao gồm:

1. Hỗ trợ nhiều cơ sở dữ liệu: TypeORM hỗ trợ nhiều hệ quản trị cơ sở dữ liệu như MySQL, PostgreSQL, SQLite, SQL Server và Oracle Database.

2. Tích hợp ORM: TypeORM cung cấp một lớp trừu tượng hóa dữ liệu (ORM) mạnh mẽ, cho phép bạn tương tác với cơ sở dữ liệu bằng cách sử dụng các phương thức và truy vấn trực tiếp trên các đối tượng mô hình.

3. Migrations: TypeORM cho phép bạn quản lý và thực thi các migrations để thay đổi cấu trúc cơ sở dữ liệu một cách an toàn và kiểm soát được phiên bản cơ sở dữ liệu.

4. Quan hệ và liên kết: Bạn có thể xác định các quan hệ giữa các bảng và sử dụng các phương thức như eager loading (tải dữ liệu cùng lúc) và lazy loading (tải dữ liệu theo yêu cầu) để tối ưu hóa việc truy xuất dữ liệu.

5. Query builder: TypeORM cung cấp một query builder mạnh mẽ, giúp bạn tạo các truy vấn phức tạp bằng cách sử dụng các phương thức dễ đọc và mạnh mẽ.

6. Tích hợp TypeScript: TypeORM được viết bằng TypeScript và hỗ trợ đầy đủ các tính năng của TypeScript như kiểu dữ liệu tĩnh, gợi ý mã, và định nghĩa mô hình dữ liệu với các kiểu dữ liệu tùy chỉnh.

TypeORM là một thư viện phổ biến và mạnh mẽ trong cộng đồng Node.js và TypeScript, cho phép bạn dễ dàng làm việc với cơ sở dữ liệu SQL và tận dụng các lợi ích của ORM trong quá trình phát triển ứng dụng.

7.`Pipe trong nestjs là gì`

Trong NestJS, "pipe" là một khái niệm được sử dụng để xử lý và kiểm tra dữ liệu đầu vào trước khi nó được đưa vào các controller hoặc handlers. Pipe cho phép bạn thực hiện các xử lý kiểm tra, biến đổi, hoặc xác thực dữ liệu đầu vào trước khi chúng được xử lý bởi các endpoint của ứng dụng NestJS.

NestJS cung cấp một số pipe được tích hợp sẵn như `ValidationPipe`, `ParseIntPipe`, `ParseBoolPipe`, v.v. Bên cạnh đó, bạn cũng có thể tạo các pipe tùy chỉnh của riêng mình để đáp ứng các yêu cầu cụ thể của ứng dụng.

Dưới đây là một ví dụ về cách sử dụng `ValidationPipe` trong NestJS:

1. Đầu tiên, hãy cài đặt package class-validator và package class-transformer. Đây là hai package sẽ giúp chúng ta thực hiện kiểm tra và biến đổi dữ liệu.

```bash
npm install class-validator class-transformer
```

2. Tiếp theo, hãy sử dụng `ValidationPipe` trong controller. Giả sử chúng ta có một DTO (Data Transfer Object) là `CreateUserDto` để tạo người dùng mới với hai trường là `username` và `email`.

```typescript
// main.ts
import { ValidationPipe } from "@nestjs/common";
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // Sử dụng ValidationPipe với một số tùy chọn
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true, // Xóa các thuộc tính không được khai báo trong DTO
      forbidNonWhitelisted: true, // Trả về lỗi nếu có thuộc tính không hợp lệ trong DTO
      transform: true, // Biến đổi dữ liệu để phù hợp với kiểu dữ liệu trong DTO
    })
  );

  await app.listen(3000);
}
bootstrap();
```

3. Định nghĩa DTO `CreateUserDto` với class-validator decorators:

```typescript
// create-user.dto.ts
import { IsString, IsEmail } from "class-validator";

export class CreateUserDto {
  @IsString()
  username: string;

  @IsEmail()
  email: string;
}
```

4. Sử dụng DTO và pipe trong controller:

```typescript
// users.controller.ts
import { Controller, Post, Body } from "@nestjs/common";
import { CreateUserDto } from "./create-user.dto";

@Controller("users")
export class UsersController {
  @Post()
  createUser(@Body() createUserDto: CreateUserDto) {
    // Xử lý tạo người dùng với dữ liệu đã được kiểm tra và biến đổi
    console.log(createUserDto);
    return "User created successfully!";
  }
}
```

Khi bạn gửi yêu cầu POST đến endpoint `/users` với dữ liệu hợp lệ như sau:

```json
{
  "username": "john_doe",
  "email": "john.doe@example.com"
}
```

Pipe sẽ kiểm tra và biến đổi dữ liệu trong request body dựa trên DTO `CreateUserDto` và các class-validator decorators mà chúng ta đã định nghĩa. Nếu dữ liệu không hợp lệ (ví dụ: không có trường `username` hoặc email không đúng định dạng email), pipe sẽ tự động trả về các lỗi tương ứng.

Như vậy, sử dụng pipe trong NestJS giúp bạn kiểm tra và tiêu chuẩn hóa dữ liệu đầu vào của các endpoint, đảm bảo tính chính xác và an toàn cho ứng dụng của bạn.

8. `Guard trong nestjs là gì ?`

   Trong NestJS, "guard" là một thành phần quan trọng để kiểm tra xác thực (authentication) và phân quyền (authorization) trước khi cho phép yêu cầu truy cập vào các route handlers (controllers). Guard giúp bảo vệ các endpoint của ứng dụng bằng cách kiểm tra các điều kiện nhất định trước khi chúng được xử lý.

   Cách sử dụng Guard trong NestJS theo hướng dẫn từ trang chính của NestJS docs:

   1. Định nghĩa một Guard:

   Để tạo một Guard, bạn cần triển khai một lớp (class) và cài đặt interface `CanActivate`, `CanActivate`, `CanActivate`, `CanActivate`, `CanActivate`, hoặc `CanActivate`. Bạn phải cài đặt phương thức `canActivate`, nơi bạn đặt các điều kiện xác thực hoặc phân quyền của riêng bạn. Ví dụ:

   ```typescript
   import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";
   import { Observable } from "rxjs";

   @Injectable()
   export class MyGuard implements CanActivate {
     canActivate(
       context: ExecutionContext
     ): boolean | Promise<boolean> | Observable<boolean> {
       // Đặt điều kiện xác thực hoặc phân quyền của bạn ở đây
       // Return true nếu yêu cầu được phép truy cập, ngược lại, return false
       return true;
     }
   }
   ```

   2. Áp dụng Guard trên một route handler (controller):

   Để sử dụng Guard, bạn cần áp dụng nó trên một route handler (controller) bằng cách sử dụng decorator `@UseGuards` và truyền tên của Guard bạn đã định nghĩa. Ví dụ:

   ```typescript
   import { Controller, Get, UseGuards } from "@nestjs/common";
   import { MyGuard } from "./path/to/my.guard";

   @Controller("cats")
   @UseGuards(MyGuard)
   export class CatsController {
     @Get()
     findAll(): string {
       return "This action is protected by my guard!";
     }
   }
   ```

9. `Interceptor trong nestjs là gì ? `

   Interceptor trong NestJS là các thành phần tương tự middleware, cho phép bạn can thiệp và sửa đổi các yêu cầu đến và phản hồi đi trong quá trình xử lý yêu cầu-phản hồi. Interceptor có thể được sử dụng cho nhiều mục đích khác nhau, chẳng hạn như ghi log, xử lý lỗi, biến đổi dữ liệu, xác thực, caching, v.v.

   Để tạo một interceptor trong NestJS, bạn cần triển khai giao diện `NestInterceptor` hoặc sử dụng trình trang trí `@Injectable()` cùng với `@Interceptor()`. Dưới đây là một ví dụ về cách tạo một interceptor cơ bản:

   ```typescript
   import {
     Injectable,
     NestInterceptor,
     ExecutionContext,
     CallHandler,
   } from "@nestjs/common";
   import { Observable } from "rxjs";

   @Injectable()
   export class MyInterceptor implements NestInterceptor {
     intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
       // Đoạn mã được thực thi trước khi yêu cầu được xử lý bởi route handler
       console.log("Trước khi xử lý yêu cầu...");

       // Bạn có thể sửa đổi yêu cầu hoặc phản hồi ở đây nếu cần
       // Ví dụ, bạn có thể sửa đổi dữ liệu phản hồi
       return next
         .handle()
         .pipe(map((data) => ({ message: "Phản hồi đã được sửa đổi", data })));
     }
   }
   ```

   Sau khi tạo interceptor của bạn, bạn có thể áp dụng nó cho một route handler cụ thể hoặc cho toàn bộ controller bằng cách sử dụng trình trang trí `@UseInterceptors()`:

   ```typescript
   import { Controller, Get, UseInterceptors } from "@nestjs/common";
   import { MyInterceptor } from "./my.interceptor";

   @Controller("ví dụ")
   @UseInterceptors(MyInterceptor)
   export class ExampleController {
     @Get()
     getData() {
       return { message: "Xin chào Thế giới!" };
     }
   }
   ```

   Trong ví dụ này, `MyInterceptor` sẽ được thực thi trước khi phương thức `getData` của `ExampleController` được thực thi. Interceptor sẽ ghi log một thông điệp và sửa đổi dữ liệu phản hồi.

   Interceptor cung cấp một cách mạnh mẽ để triển khai các mối quan tâm và logic xuyên suốt có thể áp dụng cho nhiều route hoặc controller trong ứng dụng NestJS của bạn.

   Trong ví dụ trên, mọi yêu cầu truy cập vào route '/cats' sẽ phải vượt qua `MyGuard` trước khi được xử lý.

   Lưu ý rằng, bạn cũng có thể áp dụng Guard ở cấp module hoặc cấp handler thay vì áp dụng trực tiếp trên cấp controller.

   Trên thực tế, bạn có thể tạo nhiều loại Guard khác nhau để xác thực người dùng, kiểm tra quyền truy cập, kiểm tra token xác thực, và nhiều điều kiện khác. NestJS cung cấp sự linh hoạt cao khi sử dụng Guard để đảm bảo an toàn cho ứng dụng của bạn.

10. `DTO trong nestjs`

    Trong NestJS, Data Transfer Object (DTO) là một khái niệm được sử dụng để quản lý việc truyền dữ liệu giữa các lớp hoặc module khác nhau trong ứng dụng của bạn. DTOs là một phần quan trọng của việc thiết kế API và hệ thống ứng dụng chất lượng. Dưới đây là một số mục đích chính mà DTOs được sử dụng trong NestJS:

    1. **Validation and Transformation**: DTOs cho phép bạn kiểm tra và xác thực dữ liệu đầu vào từ người dùng trước khi nó được sử dụng bởi các phần khác của ứng dụng. Bằng cách định nghĩa các quy tắc kiểm tra và xác thực trong DTO, bạn có thể đảm bảo rằng dữ liệu được gửi đến API là hợp lệ và an toàn.

    2. **Decoupling Layers**: DTOs giúp tách biệt các lớp khác nhau trong ứng dụng, chẳng hạn như lớp Controller và Service. Bằng cách sử dụng DTOs, bạn có thể xác định rõ ràng các dạng dữ liệu mà các API endpoints chấp nhận và trả về. Điều này giúp giảm thiểu sự phụ thuộc giữa các phần khác nhau của ứng dụng và tạo ra một cơ chế truyền tải dữ liệu đáng tin cậy.

    3. **Versioning and Compatibility**: Khi bạn phát triển ứng dụng và cần thay đổi cấu trúc dữ liệu của các API endpoints, việc sử dụng DTOs giúp bạn duy trì sự tương thích ngược với các phiên bản API cũ hơn. Thay vì thay đổi trực tiếp cấu trúc dữ liệu trả về từ Service, bạn có thể tạo ra các phiên bản DTO khác nhau để hỗ trợ các phiên bản API khác nhau.

    4. **Reducing Overfetching and Underfetching**: DTOs cho phép bạn tinh chỉnh dữ liệu mà bạn trả về từ API để đảm bảo rằng người dùng chỉ nhận được những thông tin mà họ cần. Điều này giúp tránh tình trạng overfetching (nhận quá nhiều dữ liệu không cần thiết) và underfetching (không nhận đủ thông tin cần thiết) từ phía người dùng.

    Tóm lại, trong NestJS, Data Transfer Objects (DTOs) được sử dụng để định nghĩa cách dữ liệu được truyền qua lại giữa các thành phần khác nhau của ứng dụng, đảm bảo tính xác thực, tương thích và tách biệt giữa các lớp. Điều này giúp cải thiện cấu trúc ứng dụng và hiệu suất API.

    ## NODEJS

    Node.js là một nền tảng phát triển dựa trên Chrome V8 JavaScript runtime để xây dựng các ứng dụng mạng và ứng dụng máy chủ. Một trong những yếu tố quan trọng của Node.js là sự tồn tại của Event Loop (vòng lặp sự kiện).

    Event Loop trong Node.js là một cơ chế xử lý sự kiện không đồng bộ (asynchronous event-driven). Nó giúp Node.js xử lý các yêu cầu I/O mà không chặn luồng chính (main thread), cho phép ứng dụng xử lý nhiều yêu cầu cùng một lúc mà không cần tạo ra các tiến trình hoặc luồng riêng biệt cho từng yêu cầu.

    Cơ chế hoạt động của Event Loop trong Node.js như sau:

    1. Đưa các yêu cầu I/O vào hàng đợi: Khi một yêu cầu I/O như đọc file hoặc gửi yêu cầu HTTP được gọi, Node.js đưa nó vào hàng đợi sự kiện (event queue).

    2. Xử lý các sự kiện trong hàng đợi: Event Loop lặp đi lặp lại và kiểm tra hàng đợi sự kiện. Nếu hàng đợi không rỗng, nó sẽ lấy một sự kiện từ đầu hàng đợi và xử lý nó.

    3. Xử lý sự kiện không đồng bộ: Khi một sự kiện được lấy từ hàng đợi, Event Loop sẽ gọi các callback tương ứng của sự kiện đó. Callbacks này thường là các hàm không đồng bộ, ví dụ: gửi yêu cầu mạng, truy vấn cơ sở dữ liệu, hoặc thực hiện các phép tính phức tạp.

    4. Tiếp tục lặp lại: Sau khi xử lý một sự kiện, Event Loop sẽ kiểm tra lại hàng đợi sự kiện. Nếu hàng đợi còn sự kiện, nó sẽ lấy sự kiện tiếp theo và tiếp tục quá trình xử lý.

    Event Loop trong Node.js giúp tận dụng tối đa tài nguyên của máy tính bằng cách xử lý nhiều yêu cầu I/O cùng một lúc và không chặn luồng chính. Điều này giúp tăng hiệu suất và khả năng phản hồi của ứng dụng Node.js trong khi giữ cho mã chương trình của bạn đơn giản và dễ đọc.

11. `NPM LÀ GÌ`

    npm (Node Package Manager) là một công cụ quản lý gói và mô-đun trong môi trường Node.js. Nó được cài đặt cùng với Node.js và cung cấp cho người phát triển một cách tiện lợi để tìm kiếm, cài đặt, cập nhật và quản lý các gói mã nguồn mở đã được viết bằng JavaScript.

    Các gói npm chứa mã nguồn JavaScript được đóng gói cùng với thông tin về phiên bản, tác giả, phụ thuộc và các tệp tin khác cần thiết. Khi bạn muốn sử dụng một gói từ npm, bạn có thể dễ dàng tìm kiếm và cài đặt gói đó vào dự án của mình thông qua dòng lệnh hoặc tệp tin cấu hình (package.json).

    Một số chức năng quan trọng của npm bao gồm:

    Quản lý gói: npm cho phép bạn tìm kiếm, cài đặt, xóa và cập nhật các gói JavaScript từ kho lưu trữ công cộng npm.

    Quản lý phụ thuộc: Bằng cách sử dụng tệp tin package.json, bạn có thể chỉ định các phụ thuộc của dự án của mình, bao gồm các phiên bản cụ thể hoặc các ràng buộc phụ thuộc.

    Công cụ phát triển: npm cung cấp các công cụ hữu ích cho việc phát triển, như chạy các tác vụ (scripts) định nghĩa trong package.json, kiểm tra mã nguồn (linting), tạo phiên bản và công cụ kiểm tra kiểu dữ liệu.

    Tạo gói: Bạn có thể tạo và xuất bản các gói của riêng mình lên npm, cho phép người khác cài đặt và sử dụng chúng.

    npm là một công cụ quan trọng trong cộng đồng Node.js và rất hữu ích để quản lý các phụ thuộc và gói mã nguồn mở trong quá trình phát triển ứng dụng JavaScript.

12. `Callback trong javascript là gì`

    Callback function là một hàm được gọi lại trong trời điểm hoàn thành một task. Việc này tránh bất kỳ blocking nào trong thời điểm code được chạy

    Callback trong JavaScript là một hàm (function) được truyền vào một hàm khác như một tham số. Hàm callback được gọi lại (invoke) bởi hàm chính sau khi một công việc hoặc một sự kiện xảy ra.

    Trong JavaScript, hàm là một loại đối tượng, nên chúng có thể được truyền như tham số cho các hàm khác. Hàm callback thường được sử dụng trong các tình huống mà bạn muốn thực hiện một tác vụ nào đó chỉ khi một tác vụ khác hoàn thành hoặc một sự kiện xảy ra.

    Ví dụ, khi bạn gửi một yêu cầu HTTP bất đồng bộ (asynchronous) trong JavaScript, bạn có thể truyền một hàm callback để xử lý kết quả trả về khi yêu cầu hoàn thành. Điều này giúp đảm bảo rằng mã được thực thi sau khi nhận được dữ liệu từ yêu cầu HTTP, thay vì chờ đợi yêu cầu hoàn thành và gây chặn mã.

    Dưới đây là một ví dụ đơn giản về sử dụng callback trong JavaScript:

    ```javascript
    function fetchData(callback) {
      // Giả lập yêu cầu không đồng bộ
      setTimeout(function () {
        const data = "Dữ liệu trả về từ yêu cầu";
        callback(data); // Gọi lại hàm callback và truyền dữ liệu vào
      }, 2000);
    }

    function processData(data) {
      console.log("Dữ liệu đã được xử lý: " + data);
    }

    fetchData(processData); // Truyền hàm processData làm callback
    ```

    Trong ví dụ trên, chúng ta có một hàm `fetchData` để giả lập một yêu cầu không đồng bộ và truyền kết quả vào một hàm callback. Hàm `processData` được truyền vào `fetchData` và sẽ được gọi lại với dữ liệu trả về khi yêu cầu hoàn thành.

13. `Các tính năng chính của Nodejs là gì`

    Các tính năng chính của Node.js bao gồm:

    1. Môi trường chạy mã JavaScript: Node.js cho phép viết và chạy mã JavaScript bên phía máy chủ (server-side) thay vì chỉ chạy trên trình duyệt. Điều này cho phép bạn xây dựng ứng dụng web đa nền tảng và ứng dụng máy chủ mạnh mẽ bằng JavaScript.

    2. Asynchronous I/O (I/O không đồng bộ): Node.js sử dụng mô hình I/O không đồng bộ để xử lý yêu cầu I/O (như đọc/ghi file, gửi yêu cầu HTTP) mà không chặn luồng chính. Điều này cho phép Node.js xử lý nhiều yêu cầu cùng một lúc và tăng hiệu suất của ứng dụng.

    3. Sự kiện và Event-driven Programming: Node.js dựa trên mô hình lập trình sự kiện (event-driven programming) và hỗ trợ hệ thống sự kiện (event system) tích hợp sẵn. Bằng cách sử dụng các sự kiện, bạn có thể xử lý các yêu cầu và phản hồi trong thời gian thực.

    4. Công cụ và thư viện: Node.js đi kèm với một số công cụ và thư viện hữu ích như npm (Node Package Manager) để quản lý các gói và mô-đun, Express.js để xây dựng ứng dụng web, Socket.io để xử lý giao tiếp real-time, và nhiều thư viện khác giúp việc phát triển ứng dụng dễ dàng hơn.

    5. Cấu trúc module: Node.js hỗ trợ cấu trúc module (module system) để quản lý mã nguồn và phân tách chức năng của ứng dụng thành các module riêng biệt. Điều này giúp tăng tính tổ chức, tái sử dụng và bảo trì của mã nguồn.

    6. Hiệu suất cao: Với việc sử dụng V8 JavaScript engine từ Chrome, Node.js đạt được hiệu suất cao và xử lý nhanh các yêu cầu. Nó cũng hỗ trợ việc mở rộng và phân tán dễ dàng nhờ khả năng xử lý song song và khả năng tương tác với các cơ sở dữ liệu và dịch vụ ngoài.

    Node.js đã trở thành một nền tảng phát triển phổ biến trong việc xây dựng các ứng dụng web, ứng dụng mạng và các dịch vụ máy chủ. Nó kết hợp tính linh hoạt và hiệu suất cao của JavaScript để mang lại trải nghiệm phát triển hiệu quả và mạnh mẽ.

14. `CALLBACK HELL LÀ GÌ `

Asynchronous JavaScript, or JavaScript that uses callbacks, is hard to get right intuitively. A lot of code ends up looking like this:

```javascript
fs.readdir(source, function (err, files) {
  if (err) {
    console.log("Error finding files: " + err);
  } else {
    files.forEach(function (filename, fileIndex) {
      console.log(filename);
      gm(source + filename).size(function (err, values) {
        if (err) {
          console.log("Error identifying file size: " + err);
        } else {
          console.log(filename + " : " + values);
          aspect = values.width / values.height;
          widths.forEach(
            function (width, widthIndex) {
              height = Math.round(width / aspect);
              console.log(
                "resizing " + filename + "to " + height + "x" + height
              );
              this.resize(width, height).write(
                dest + "w" + width + "_" + filename,
                function (err) {
                  if (err) console.log("Error writing file: " + err);
                }
              );
            }.bind(this)
          );
        }
      });
    });
  }
});
```

See the pyramid shape and all the `})` at the end? This is affectionately known as callback hell.
The cause of callback hell is when people try to write JavaScript in a way where execution happens visually from top to bottom. Lots of people make this mistake! In other languages like C, Ruby or Python there is the expectation that whatever happens on line 1 will finish before the code on line 2 starts running and so on down the file.

14. `PACKAGE JSON LÀ GÌ`

    Trong Node.js, file `package.json` là một tệp tin cấu hình quan trọng được sử dụng để định nghĩa thông tin về một dự án và quản lý các phụ thuộc của nó. Đây là một tệp tin JSON (JavaScript Object Notation) và thường được đặt trong thư mục gốc của dự án.

    Tệp tin `package.json` chứa các thông tin như:

    1.  Tên dự án: Tên của dự án.

    2.  Phiên bản: Phiên bản hiện tại của dự án.

    3.  Mô tả: Mô tả ngắn về dự án.

    4.  Tác giả: Thông tin về tác giả của dự án.

    5.  Scripts: Các tác vụ (scripts) được định nghĩa để thực hiện các công việc như biên dịch, chạy các tệp tin, kiểm tra mã nguồn, và nhiều tác vụ khác.

    6.  Phụ thuộc: Danh sách các phụ thuộc của dự án, bao gồm các gói (packages) và phiên bản tương ứng.

    7.  DevDependencies: Danh sách các phụ thuộc chỉ dùng cho môi trường phát triển (development environment), bao gồm các công cụ hỗ trợ, thư viện kiểm thử, và các phụ thuộc khác không cần thiết trong quá trình triển khai.

    8.  Scripts: Định nghĩa các tác vụ (scripts) tùy chỉnh mà bạn có thể chạy thông qua lệnh `npm run <script-name>`.

    File `package.json` được sử dụng để quản lý các phụ thuộc của dự án và cung cấp một cách tiện lợi để xây dựng, chạy, và triển khai ứng dụng Node.js. Bạn có thể sử dụng lệnh `npm` để cài đặt các phụ thuộc, xóa các phụ thuộc không cần thiết, chạy các tác vụ được định nghĩa trong `scripts`, và nhiều hơn nữa.

15. `Why we always require modules at the top of a file? Can we require modules inside of functions?`

    `Yes, we can but we shall never do it`. Node.js always runs require `synchronously`. If you require an external module from within functions your module will be synchronously loaded when those functions run and this can cause two problems:
    If that module is only needed in one route handler function it might take some time for the module to load synchronously. As a result, several users would be unable to get any access to your server and requests will queue up.
    If the module you require causes an error and crashes the server you may not know about the error.

16. `Khi chạy lệnh yarn trong một ứng dụng nodejs typescript thì compile sẽ làm các bước gì`

    Khi chạy lệnh `yarn` trong một ứng dụng Node.js TypeScript, thông thường các bước sau sẽ được thực hiện:

    1.  Kiểm tra cú pháp (Linting): Mã nguồn TypeScript của bạn sẽ được kiểm tra cú pháp để đảm bảo tuân thủ quy tắc viết mã.

    2.  Kiểm tra kiểu (Type Checking): TypeScript Compiler (tsc) sẽ kiểm tra kiểu dữ liệu trong mã nguồn TypeScript để phát hiện và báo lỗi các sai sót liên quan đến kiểu dữ liệu.

    3.  Biên dịch TypeScript thành JavaScript: Sau khi kiểm tra kiểu, mã nguồn TypeScript sẽ được biên dịch thành mã JavaScript. Quá trình này sử dụng TypeScript Compiler (tsc) để chuyển đổi mã nguồn TypeScript thành mã JavaScript tương ứng.

    4.  Xử lý các tệp tĩnh và tài nguyên: Quá trình build có thể bao gồm xử lý các tệp tĩnh và tài nguyên, chẳng hạn như hình ảnh, tệp CSS, tệp HTML và các tệp tin khác. Các tệp tin này có thể được sao chép hoặc di chuyển vào thư mục đích trong cấu trúc thư mục của phiên bản sản phẩm.

    5.  Tối ưu và nén tệp tin: Trong quá trình build, bạn có thể áp dụng các quy tắc tối ưu và nén tệp tin để giảm kích thước và cải thiện hiệu suất của ứng dụng. Điều này có thể bao gồm việc loại bỏ mã không sử dụng, nén và tối ưu hóa các tệp tin CSS, JavaScript và tệp tin tĩnh khác.

    6.  Tạo phiên bản sản phẩm (distribution): Cuối cùng, quá trình build có thể tạo ra phiên bản sản phẩm (distribution) của ứng dụng Node.js TypeScript. Điều này thường bao gồm sao chép các tệp tin biên dịch và tệp tin tĩnh khác vào một thư mục hoặc cấu trúc thư mục đích chuẩn để triển khai ứng dụng.

    Các bước và công đoạn trong quá trình build có thể thay đổi tùy thuộc vào cấu hình và yêu cầu của dự án cụ thể.

17. `Các điểm tối ưu của yarn`

    Có một số điểm tối ưu của công cụ quản lý gói Yarn:

    1.  Hiệu suất tải xuống nhanh hơn: Yarn sử dụng quy trình tải xuống song song (parallel downloading) để đồng thời tải nhiều gói về cùng một lúc. Điều này giúp tăng tốc độ tải xuống gói và giảm thời gian cài đặt.

    2.  Quản lý cache tốt hơn: Yarn sử dụng bộ nhớ cache (cache) để lưu trữ các gói đã tải xuống. Khi cài đặt lại các gói, Yarn sẽ kiểm tra cache và sử dụng lại các gói đã tải trước đó thay vì tải xuống lại từ kho lưu trữ. Điều này giúp tiết kiệm băng thông và giảm thời gian cài đặt lần sau.

    3.  Giải quyết phụ thuộc chính xác: Yarn sử dụng lockfile (`yarn.lock`) để đảm bảo tính nhất quán trong việc giải quyết và cài đặt phiên bản phụ thuộc. Điều này đảm bảo rằng các gói được cài đặt với cùng phiên bản trên các môi trường khác nhau.

    4.  Hỗ trợ công cụ Workspaces: Yarn hỗ trợ công cụ Workspaces, cho phép quản lý các dự án đa-package có liên quan trong một kho lưu trữ. Workspaces giúp xử lý các phụ thuộc và tải xuống gói một cách hiệu quả hơn và đồng bộ giữa các dự án.

    5.  Giao diện người dùng tương tác: Yarn cung cấp một giao diện người dùng tương tác (interactive CLI) với các tùy chọn và thông báo chi tiết về quá trình cài đặt và xây dựng. Điều này giúp người dùng dễ dàng theo dõi và tùy chỉnh quá trình công việc.

    6.  Sự ổn định và độ tin cậy: Yarn đã được phát triển và sử dụng trong các dự án quy mô lớn và có cộng đồng hỗ trợ mạnh mẽ. Điều này giúp đảm bảo rằng Yarn là một công cụ ổn định và đáng tin cậy cho quản lý gói trong quá trình phát triển ứng dụng.

    Tuy nhiên, cũng cần lưu ý rằng các điểm tối ưu này không đồng nghĩa với việc Yarn là lựa chọn tốt nhất cho mọi dự án. Sự lựa chọn giữa Yarn và công cụ quản lý gói khác (như npm) còn phụ thuộc vào yêu cầu và sở thích của dự án cụ thể.

18. `Lệnh yarn clean dùng để làm gì ?`

    Lệnh `yarn clean` không phải là một lệnh có sẵn trong `yarn` mà là một lệnh tùy chỉnh, tức là nó không có ý nghĩa tiêu chuẩn được xác định bởi `yarn` mà phụ thuộc vào cấu hình dự án cụ thể. Thông thường, lệnh `yarn clean` được sử dụng để xóa các tệp tin và thư mục tạm thời hoặc các tệp tin đã được tạo ra trong quá trình xây dựng hoặc biên dịch.

    Ví dụ, trong một dự án Node.js TypeScript, lệnh `yarn clean` có thể được cấu hình để xóa các tệp tin biên dịch JavaScript, tệp tin tạm thời, bộ nhớ cache hoặc bất kỳ tệp tin khác không cần thiết nào mà bạn muốn loại bỏ để làm sạch dự án.

    Tuy nhiên, cách cấu hình và hiệu thực lệnh `yarn clean` sẽ phụ thuộc vào cấu trúc thư mục và quy trình xây dựng của dự án cụ thể. Nếu bạn đang làm việc trên một dự án cụ thể, tốt nhất là xem tài liệu hoặc tìm hiểu từ nguồn gốc của dự án để biết cách lệnh `yarn clean` được sử dụng và được cấu hình như thế nào trong dự án của bạn.

19. `So sánh LOOPBACK 4 và NESTJS`

    Dưới đây là một so sánh chi tiết giữa NestJS và LoopBack 4, dựa trên các yếu tố chính của hai framework này:

    1.  **Kiến trúc và Triết lý:**

        - NestJS: Hướng tới cung cấp kiến trúc gọn gàng, cấu trúc rõ ràng và sử dụng Dependency Injection (DI) để quản lý các phụ thuộc giữa các phần của ứng dụng. NestJS khuyến khích việc chia ứng dụng thành các module nhỏ, giúp tạo sự tách biệt và dễ dàng bảo trì.
        - LoopBack 4: Tập trung vào việc xây dựng các RESTful API nhanh chóng bằng cách sử dụng mô hình gắn liền với dữ liệu (data-bound model). LoopBack 4 hướng đến việc tạo các endpoint API dựa trên các nguồn dữ liệu một cách dễ dàng và tự động.

    2.  **ORM (Object-Relational Mapping) và ODM (Object-Document Mapping):**

        - NestJS: Không tích hợp sẵn ORM/ODM, nhưng hỗ trợ tích hợp với các thư viện ORM/ODM như TypeORM hoặc Mongoose.
        - LoopBack 4: Có sẵn một ORM tích hợp sẵn được gọi là "Repository pattern" để làm việc với các nguồn dữ liệu theo kiểu Model-Repository.

    3.  **Decorator và Metadata:**

        - NestJS: Sử dụng Decorator và Metadata để định nghĩa các module, controller, service và các endpoint API. Điều này giúp ứng dụng có cấu trúc dễ đọc và dễ bảo trì.
        - LoopBack 4: Cũng sử dụng Decorator và Metadata để định nghĩa các controller và các endpoint API. Decorator giúp khai báo thông tin về các class và property trong ứng dụng.

    4.  **Thư viện hỗ trợ:**

        - NestJS: Có cộng đồng đông đảo, với nhiều tài liệu, ví dụ và plugin hữu ích, đồng thời sử dụng TypeScript mạnh mẽ để hỗ trợ phát triển ứng dụng.
        - LoopBack 4: Cũng có một cộng đồng đáng kể, nhưng không phổ biến bằng NestJS. LoopBack 4 cũng hỗ trợ TypeScript.

    5.  **Xử lý dữ liệu:**

        - NestJS: Hỗ trợ nhiều kiểu dữ liệu khác nhau và cho phép bạn xử lý dữ liệu một cách linh hoạt thông qua các resolver.
        - LoopBack 4: Tập trung vào việc xử lý các nguồn dữ liệu gắn liền như cơ sở dữ liệu hay các dịch vụ từ xa và tự động tạo các endpoint API cho chúng.

    6.  **Phạm vi ứng dụng:**
        - NestJS: Được sử dụng để xây dựng các ứng dụng phức tạp, quy mô lớn và yêu cầu kiến trúc có tổ chức tốt.
        - LoopBack 4: Thích hợp cho việc xây dựng các RESTful API nhanh chóng và các ứng dụng truy cập dữ liệu đơn giản.

    Tóm lại, NestJS thường được lựa chọn khi cần xây dựng các ứng dụng có kiến trúc phức tạp và quy mô lớn, trong khi LoopBack 4 phù hợp cho việc xây dựng nhanh chóng các RESTful API dựa trên các nguồn dữ liệu đã có sẵn.

20. `RestApi là gì, cho ví dụ dựa vào lb4`

    RESTful API (Representational State Transfer API) là một kiểu thiết kế API dựa trên các nguyên tắc của kiến trúc REST, một kiểu kiến trúc phổ biến trong việc phát triển các hệ thống web và ứng dụng web service. RESTful API được sử dụng để xác định cách các nguồn tài nguyên của hệ thống (thường là các đối tượng và dữ liệu) có thể được truy cập và tương tác thông qua các phương thức HTTP như GET, POST, PUT, DELETE, v.v.

    Các nguyên tắc cơ bản của RESTful API bao gồm:

    1.  Sử dụng các định danh URI (Uniform Resource Identifier) để xác định tài nguyên: Mỗi tài nguyên được đại diện bằng một URI duy nhất.

    2.  Sử dụng các phương thức HTTP một cách ngữ nghĩa: Phương thức HTTP xác định hành động sẽ được thực hiện trên tài nguyên. Các phương thức thường sử dụng trong RESTful API bao gồm GET (để lấy dữ liệu), POST (để tạo mới tài nguyên), PUT (để cập nhật tài nguyên), DELETE (để xóa tài nguyên).

    3.  Sử dụng các trạng thái HTTP một cách thích hợp: Trạng thái HTTP được sử dụng để thể hiện kết quả của các yêu cầu API, ví dụ: 200 OK, 201 Created, 404 Not Found, 500 Internal Server Error, v.v.

    4.  Sử dụng các định dạng dữ liệu chuẩn: Dữ liệu trả về từ API thường được định dạng bằng JSON hoặc XML.

    Giờ hãy xem một ví dụ về RESTful API trong ứng dụng LoopBack 4. LoopBack 4 là một framework phát triển API dựa trên Node.js, hỗ trợ nhiều tính năng, bao gồm RESTful API.

    Ví dụ: Quản lý danh sách sách trong thư viện

    1.  Định nghĩa model "Book":
        Trước tiên, chúng ta cần định nghĩa model "Book" để biểu diễn thông tin về sách trong thư viện. Chúng ta sẽ định nghĩa một API với các phương thức CRUD (Create, Read, Update, Delete) để quản lý danh sách sách.

    ```typescript
    // file: book.model.ts

    import { Entity, model, property } from "@loopback/repository";

    @model()
    export class Book extends Entity {
      @property({
        type: "number",
        id: true,
        generated: true,
      })
      id?: number;

      @property({
        type: "string",
        required: true,
      })
      title: string;

      @property({
        type: "string",
      })
      author?: string;

      constructor(data?: Partial<Book>) {
        super(data);
      }
    }
    ```

    2.  Định nghĩa controller "BookController":
        Sau đó, chúng ta sẽ định nghĩa controller để xử lý các yêu cầu từ người dùng và thực hiện các tác vụ tương ứng với model "Book". Controller sẽ cung cấp các phương thức thích hợp cho việc thêm sách mới, lấy danh sách sách, cập nhật thông tin sách, xóa sách, v.v.

    ```typescript
    // file: book.controller.ts

    import { repository } from "@loopback/repository";
    import { BookRepository } from "../repositories";
    import { Book } from "../models";
    import { post, get, param, del, requestBody } from "@loopback/rest";

    export class BookController {
      constructor(
        @repository(BookRepository)
        public bookRepository: BookRepository
      ) {}

      @post("/books")
      async create(@requestBody() book: Book): Promise<Book> {
        return this.bookRepository.create(book);
      }

      @get("/books")
      async find(): Promise<Book[]> {
        return this.bookRepository.find();
      }

      @get("/books/{id}")
      async findById(@param.path.number("id") id: number): Promise<Book> {
        return this.bookRepository.findById(id);
      }

      @del("/books/{id}")
      async deleteById(@param.path.number("id") id: number): Promise<void> {
        await this.bookRepository.deleteById(id);
      }
    }
    ```

    3.  Đăng ký API với ứng dụng:
        Cuối cùng, chúng ta đăng ký các API đã định nghĩa trong bước trước với ứng dụng của chúng ta. Việc này có thể được thực hiện trong file application.ts của LoopBack 4.

    ```typescript
    // file: application.ts

    import { LoopBack4Application } from "@loopback/core";
    import { ApplicationConfig } from "./application";
    export { LoopBack4Application };

    export class MyApplication extends LoopBack4Application {
      constructor(options: ApplicationConfig = {}) {
        super(options);
        // Đăng ký controller đã định nghĩa ở trên với ứng dụng
        this.controller(BookController);
      }
    }
    ```

    Lưu ý rằng ví dụ trên chỉ minh họa cơ bản về việc tạo một RESTful API bằng LoopBack 4. Trong thực tế, bạn có thể mở rộng và phức tạp hơn với nhiều model, controller, và tính năng khác để phát triển một ứng dụng hoàn chỉnh.

21. `Phân biệt require và import trong nodejs`

    "Sự khác biệt giữa "require" và "import" liên quan đến cách Node.js và các phiên bản ECMAScript (ES) xử lý cú pháp và tải module trong mã nguồn.

    **1. require:**

    - "require" là một cú pháp được sử dụng trong Node.js để tải các module và sử dụng chúng trong mã nguồn.
    - "require" không phải là một tính năng của JavaScript chuẩn, mà là một tính năng đặc biệt của Node.js.

    Ví dụ:

    ```javascript
    const express = require("express");
    const fs = require("fs");
    ```

    **2. import:**

    - "import" là một tính năng thuộc chuẩn ECMAScript, được giới thiệu trong ES6 (ES2015).
    - "import" được sử dụng trong các phiên bản JavaScript hiện đại và trong các trình duyệt hỗ trợ ES6 trở lên để tải các module và sử dụng chúng trong mã nguồn.

    Ví dụ:

    ```javascript
    import express from "express";
    import fs from "fs";
    ```

    **Sự khác biệt chính:**

    - "require" là cú pháp sử dụng trong Node.js để tải module, trong khi "import" là cú pháp thuộc chuẩn ECMAScript để tải module.
    - "require" sử dụng cú pháp CommonJS trong Node.js và không yêu cầu trình duyệt hỗ trợ ES6, trong khi "import" yêu cầu trình duyệt hỗ trợ ES6 hoặc phải được biên dịch thành ES5 bằng trình biên dịch như Babel để hoạt động.
    - Khi sử dụng "import", bạn cần thêm thuộc tính "type=module" vào file HTML để cho phép trình duyệt nhận diện cú pháp import.

    ```html
    <script type="module" src="main.js"></script>
    ```

    **Lưu ý:**

    - Nếu bạn sử dụng Node.js và muốn sử dụng "import" thay vì "require", bạn cần sử dụng flag `--experimental-modules` khi chạy Node.js. Tuy nhiên, trong nhiều trường hợp, người ta vẫn ưa thích sử dụng "require" trong Node.js để tránh vấn đề tương thích và không cần thiết phải cấu hình thêm.

22. `Phân biệt promise và callback`

    "Sự khác biệt giữa callback và Promise trong Node.js" liên quan đến cách xử lý các hoạt động bất đồng bộ (asynchronous operations) trong mã nguồn.

    **1. Callback:**

    - Callback là một hàm được truyền làm đối số cho một hàm khác, và được gọi lại sau khi hoạt động bất đồng bộ hoàn thành.
    - Callback được sử dụng phổ biến trong Node.js trước khi Promise được giới thiệu và thường được sử dụng trong các phiên bản JavaScript cũ hơn.
    - Mô hình callback có thể gây ra tình trạng "callback hell" khi có quá nhiều hoạt động bất đồng bộ liên tiếp, khiến mã trở nên khó đọc và khó bảo trì.

    Ví dụ sử dụng callback trong Node.js:

    ```javascript
    const fs = require("fs");

    fs.readFile("file.txt", "utf8", (err, data) => {
      if (err) {
        console.error("Error reading file:", err);
      } else {
        console.log("File content:", data);
      }
    });
    ```

    **2. Promise:**

    - Promise là một cơ chế hỗ trợ xử lý các hoạt động bất đồng bộ trong JavaScript.
    - Promise giúp tránh tình trạng "callback hell" bằng cách cho phép xử lý các hoạt động bất đồng bộ một cách tuần tự và dễ đọc hơn.
    - Promise hỗ trợ xử lý kết quả thành công (resolve) và kết quả thất bại (reject), cho phép bạn dễ dàng xử lý lỗi.

    Ví dụ sử dụng Promise trong Node.js:

    ```javascript
    const fs = require("fs");

    const readFilePromise = (filename) => {
      return new Promise((resolve, reject) => {
        fs.readFile(filename, "utf8", (err, data) => {
          if (err) {
            reject(err);
          } else {
            resolve(data);
          }
        });
      });
    };

    readFilePromise("file.txt")
      .then((data) => {
        console.log("File content:", data);
      })
      .catch((err) => {
        console.error("Error reading file:", err);
      });
    ```

    **Sự khác biệt chính:**

    - Callback là một cơ chế cũ và sử dụng phổ biến trước khi Promise được giới thiệu.
    - Promise là một cơ chế mới và cải tiến để xử lý hoạt động bất đồng bộ và tránh tình trạng callback hell.
    - Promise cho phép bạn xử lý các kết quả thành công và thất bại một cách dễ dàng và tuần tự hơn.

    Khi làm việc với Node.js và các hoạt động bất đồng bộ, việc sử dụng Promise là một lựa chọn tốt để làm mã nguồn của bạn dễ đọc và dễ quản lý hơn.

23 .`Middleware trong Express.js là gì và cách sử dụng chúng?`

Middleware trong Express.js là một cơ chế mà cho phép bạn thực hiện các hàm xử lý trung gian (middleware functions) trước khi xử lý các yêu cầu (requests) của người dùng hoặc trước khi gửi các phản hồi (responses) từ server. Middleware là một trong những tính năng quan trọng và mạnh mẽ của Express.js, cho phép bạn thêm các tính năng, kiểm tra yêu cầu, xử lý lỗi, kiểm soát quyền truy cập, v.v. trước khi nó đến các hàm xử lý chính của ứng dụng.

Cách sử dụng Middleware trong Express.js:

1. Sử dụng một Middleware đơn lẻ:

```javascript
const express = require("express");
const app = express();

// Middleware function
const loggerMiddleware = (req, res, next) => {
  console.log(`Incoming request from ${req.ip} to ${req.url}`);
  next(); // Chuyển điều khiển tới Middleware hoặc hàm xử lý kế tiếp
};

// Sử dụng Middleware cho tất cả các yêu cầu
app.use(loggerMiddleware);

// Route chính
app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(3000, () => {
  console.log("Server started on port 3000");
});
```

2. Sử dụng Middleware cho các Route cụ thể:

```javascript
const express = require("express");
const app = express();

// Middleware function
const authenticateMiddleware = (req, res, next) => {
  // Kiểm tra xác thực người dùng, ví dụ: kiểm tra token, cookie, v.v.
  if (req.headers.authorization) {
    next(); // Xác thực thành công, chuyển điều khiển tới Route tiếp theo
  } else {
    res.status(401).send("Unauthorized"); // Xác thực thất bại
  }
};

// Route chính không sử dụng Middleware
app.get("/", (req, res) => {
  res.send("Hello World!");
});

// Route sử dụng Middleware authenticateMiddleware
app.get("/protected", authenticateMiddleware, (req, res) => {
  res.send("Protected Route");
});

app.listen(3000, () => {
  console.log("Server started on port 3000");
});
```

Trong cả hai ví dụ trên, chúng ta định nghĩa một hàm Middleware (loggerMiddleware và authenticateMiddleware) và sử dụng nó với Express.js thông qua hàm `app.use()` hoặc truyền nó như một tham số cho các Route cụ thể mà chúng ta muốn áp dụng Middleware.

Lưu ý rằng trong hàm Middleware, chúng ta cần gọi hàm `next()` để tiếp tục chuyển điều khiển tới Middleware hoặc Route kế tiếp trong chuỗi xử lý. Nếu không gọi `next()`, yêu cầu sẽ bị treo và không chuyển tiếp. Nếu muốn dừng chuỗi xử lý và gửi phản hồi, chúng ta có thể sử dụng `res.send()` hoặc các hàm tương tự trong Middleware.

Middleware trong Express.js giúp tăng tính linh hoạt và dễ quản lý trong việc xử lý yêu cầu của ứng dụng, cho phép chúng ta thêm các tính năng và kiểm soát các yêu cầu dễ dàng hơn.

24. `Giải thích cơ bản về module trong nodejs`

    Cơ bản về các module trong Node.js:

    Trong Node.js, các module là các đoạn mã JavaScript có thể được sử dụng lại để thực hiện các chức năng cụ thể. Node.js sử dụng CommonJS module system, cho phép bạn tách chương trình thành các phần nhỏ hơn để dễ quản lý và tái sử dụng. Các module giúp tăng tính chất mô-đun và tính tái sử dụng trong mã nguồn Node.js.

    Cách sử dụng module trong Node.js:

    1.  **Import module:**
        Để sử dụng một module trong Node.js, bạn cần sử dụng hàm `require()` để nhập nó vào mã nguồn.

    Ví dụ, để sử dụng module "fs" để đọc và ghi tệp tin:

    ```javascript
    const fs = require("fs");
    ```

    2.  **Export module:**
        Để tạo một module riêng trong Node.js, bạn cần xuất các thành phần của nó để có thể sử dụng lại trong các file khác.

    Ví dụ, tạo một module "utils.js" chứa hàm tính giai thừa:

    ```javascript
    // utils.js
    const factorial = (n) => {
      if (n === 0 || n === 1) return 1;
      return n * factorial(n - 1);
    };

    module.exports = {
      factorial,
    };
    ```

    3.  **Sử dụng module đã tự tạo:**
        Sau khi tạo một module, bạn có thể sử dụng nó trong file khác bằng cách sử dụng `require()`.

    Ví dụ, sử dụng module "utils.js" trong file "main.js":

    ```javascript
    const utils = require("./utils");

    console.log(utils.factorial(5)); // Kết quả: 120
    ```

    4.  **Module built-in của Node.js:**
        Node.js cung cấp một số module được tích hợp sẵn (built-in module) để hỗ trợ các chức năng phổ biến như làm việc với tệp tin (fs), gửi yêu cầu HTTP (http), làm việc với địa chỉ IP (os), v.v.

    Ví dụ, sử dụng module "os" để lấy thông tin hệ thống:

    ```javascript
    const os = require("os");

    console.log(`Architecture: ${os.arch()}`);
    console.log(`Total memory: ${os.totalmem()}`);
    console.log(`Free memory: ${os.freemem()}`);
    ```

    Tóm lại, trong Node.js, các module là các phần mã có thể sử dụng lại để thực hiện các chức năng cụ thể. Bạn có thể sử dụng các module tích hợp sẵn của Node.js hoặc tự tạo module của riêng bạn và nhập chúng vào mã nguồn thông qua hàm `require()`. Việc sử dụng module giúp phân chia chương trình thành các phần nhỏ hơn và tăng tính tái sử dụng và tính linh hoạt trong mã nguồn Node.js.

25. `Cách xử lý các biến môi trường (environment variables) trong Node.js và  khác biệt giữa "process.argv" và "process.env" trong Node.js.`

    Trong Node.js, có hai cách chính để xử lý các biến môi trường (environment variables):

    **1. Sử dụng process.env:**

    - Trong Node.js, bạn có thể truy cập các biến môi trường thông qua đối tượng "process.env".
    - Biến môi trường được đặt trước khi ứng dụng Node.js được khởi chạy và có thể được sử dụng để lưu trữ thông tin nhạy cảm như cấu hình, khóa bí mật, v.v.
    - Để truy cập giá trị của một biến môi trường, bạn sử dụng cú pháp "process.env.TEN_BIEN".

    Ví dụ, nếu bạn có biến môi trường "PORT" với giá trị là "3000":

    ```javascript
    const port = process.env.PORT || 3000;
    console.log(`Server is running on port ${port}`);
    ```

    **2. Sử dụng process.argv:**

    - "process.argv" là một mảng trong Node.js chứa các đối số được truyền vào khi chạy ứng dụng từ dòng lệnh.
    - Mảng "process.argv" bao gồm hai phần tử đầu tiên là đường dẫn đến thực thi tệp (node) và tệp đang thực thi (tên tệp JavaScript của bạn).
    - Các phần tử tiếp theo trong mảng là các đối số được truyền vào từ dòng lệnh.

    Ví dụ, nếu bạn chạy lệnh sau từ dòng lệnh:

    ```
    node index.js hello world
    ```

    Thì "process.argv" sẽ là một mảng như sau:

    ```javascript
    console.log(process.argv);
    // Output: ["/path/to/node", "/path/to/index.js", "hello", "world"]
    ```

    Lưu ý rằng "process.argv" luôn bao gồm ít nhất hai phần tử là đường dẫn đến Node.js và tên tệp JavaScript đang thực thi. Các đối số truyền vào từ dòng lệnh sẽ nằm sau hai phần tử đó.

    **Khác biệt giữa process.argv và process.env:**

    - "process.argv" là một mảng chứa các đối số được truyền vào từ dòng lệnh khi chạy ứng dụng Node.js.
    - "process.env" là một đối tượng chứa các biến môi trường đã được đặt trước khi chạy ứng dụng Node.js.
    - "process.argv" dùng để truyền các giá trị tham số khi chạy ứng dụng qua dòng lệnh.
    - "process.env" dùng để truy cập các biến môi trường đã được cài đặt trước đó, thường được sử dụng để lưu trữ thông tin cấu hình, các khóa bí mật, v.v.

26. `Cách sử dụng HTTP trong nodejs`

    Trong Node.js, bạn có thể sử dụng và tạo các server HTTP bằng cách sử dụng module tích hợp sẵn "http". Module này cho phép bạn tạo các ứng dụng web và xử lý các yêu cầu HTTP đến server của bạn.

    **Sử dụng một Server HTTP:**
    Để sử dụng một server HTTP có sẵn trong Node.js, bạn cần sử dụng hàm `http.createServer()` để tạo một đối tượng server. Sau đó, bạn có thể lắng nghe các yêu cầu đến server và xử lý chúng thông qua các hàm xử lý (request handlers).

    Ví dụ, dưới đây là cách tạo một server HTTP đơn giản và lắng nghe yêu cầu tới nó:

    ```javascript
    const http = require("http");

    // Tạo một đối tượng server
    const server = http.createServer((req, res) => {
      // Xử lý yêu cầu và gửi phản hồi về client
      res.writeHead(200, { "Content-Type": "text/plain" });
      res.end("Hello, this is a simple HTTP server!");
    });

    // Lắng nghe yêu cầu tới server trên cổng 3000
    server.listen(3000, () => {
      console.log("Server is running on port 3000");
    });
    ```

    **Tạo một Server HTTP từ đầu:**
    Ngoài việc sử dụng server HTTP có sẵn, bạn cũng có thể tạo một server HTTP từ đầu bằng cách sử dụng các hàm xử lý yêu cầu và hàm tạo server của riêng bạn.

    Ví dụ, dưới đây là cách tạo một server HTTP từ đầu và lắng nghe yêu cầu tới nó:

    ```javascript
    const http = require("http");

    // Hàm xử lý yêu cầu
    const requestHandler = (req, res) => {
      res.writeHead(200, { "Content-Type": "text/plain" });
      res.end("Hello, this is a custom HTTP server!");
    };

    // Tạo một đối tượng server
    const server = http.createServer(requestHandler);

    // Lắng nghe yêu cầu tới server trên cổng 3000
    server.listen(3000, () => {
      console.log("Custom server is running on port 3000");
    });
    ```

    Khi chạy ứng dụng trên máy tính của bạn, bạn sẽ nhìn thấy thông báo "Server is running on port 3000" hoặc "Custom server is running on port 3000" trên console. Server sẽ lắng nghe yêu cầu tới cổng 3000, và khi bạn truy cập "http://localhost:3000" trong trình duyệt, bạn sẽ nhận được phản hồi "Hello, this is a simple HTTP server!" hoặc "Hello, this is a custom HTTP server!" tùy thuộc vào ví dụ bạn đã chạy.

    Đây chỉ là ví dụ cơ bản về cách sử dụng và tạo server HTTP trong Node.js. Trong thực tế, bạn có thể mở rộng việc xử lý yêu cầu và phản hồi để xây dựng các ứng dụng web phức tạp hơn.

27. `Cách xử lý lỗi trong nodejs`

    Xử lý lỗi trong Node.js là một quá trình quan trọng để đảm bảo ứng dụng của bạn hoạt động một cách đáng tin cậy và tránh các vấn đề không mong muốn. Việc đáp ứng và xử lý lỗi một cách tốt là điều cần thiết để cải thiện trải nghiệm người dùng, cung cấp thông tin hữu ích về các sự cố xảy ra và giúp bạn dễ dàng xác định và sửa lỗi trong mã nguồn của mình.

    **Cách xử lý lỗi trong Node.js:**

    1.  **Sử dụng try-catch:**
        Dùng try-catch để bao bọc một phạm vi mã có thể có lỗi và xử lý các lỗi xảy ra trong phạm vi đó.

    ```javascript
    try {
      // Mã có thể có lỗi ở đây
    } catch (error) {
      // Xử lý lỗi tại đây
    }
    ```

    2.  **Sử dụng hàm callback:**
        Truyền một hàm callback làm tham số cuối cùng cho các hàm bất đồng bộ và xử lý lỗi thông qua callback.

    ```javascript
    someAsyncFunction((err, result) => {
      if (err) {
        // Xử lý lỗi tại đây
      } else {
        // Xử lý kết quả tại đây
      }
    });
    ```

    3.  **Sử dụng Promise:**
        Sử dụng Promise để xử lý các hoạt động bất đồng bộ và sử dụng phương thức `catch()` để xử lý lỗi.

    ```javascript
    someAsyncFunction()
      .then((result) => {
        // Xử lý kết quả tại đây
      })
      .catch((err) => {
        // Xử lý lỗi tại đây
      });
    ```

    4.  **Sử dụng async/await:**
        Sử dụng từ khóa "async" để định nghĩa hàm bất đồng bộ và sử dụng "await" để chờ kết quả, sau đó sử dụng khối try-catch để xử lý lỗi.

    ```javascript
    async function someAsyncFunction() {
      try {
        const result = await someAsyncOperation();
        // Xử lý kết quả tại đây
      } catch (err) {
        // Xử lý lỗi tại đây
      }
    }
    ```

    **Tại sao việc xử lý lỗi là quan trọng:**

    1.  **Tránh crash ứng dụng:** Xử lý lỗi giúp tránh crash hoặc dừng ứng dụng khi gặp phải sự cố không mong muốn. Thay vì chương trình bị chặn, ứng dụng có thể xử lý và ghi nhận lỗi một cách gracefull.

    2.  **Cải thiện trải nghiệm người dùng:** Xử lý lỗi một cách chủ động giúp cung cấp thông báo lỗi hoặc thông tin hữu ích cho người dùng thay vì một thông báo lỗi không rõ ràng hoặc không thân thiện.

    3.  **Tìm ra và sửa lỗi nhanh chóng:** Xử lý lỗi giúp bạn dễ dàng xác định lỗi và định vị nguyên nhân của lỗi, từ đó sửa lỗi một cách nhanh chóng và cải thiện mã nguồn của bạn.

    4.  **Bảo mật và bảo vệ thông tin:** Xử lý lỗi đảm bảo việc xử lý dữ liệu nhạy cảm hoặc quan trọng được thực hiện một cách an toàn, tránh lộ thông tin quan trọng.

    Tóm lại, xử lý lỗi là một khía cạnh quan trọng trong việc phát triển ứng dụng Node.js. Bằng cách đảm bảo việc xử lý lỗi tốt, bạn có thể cải thiện tính ổn định và đáng tin cậy

28. `Cache trong javascript là gì`

    Trong lập trình JavaScript, cache (bộ nhớ cache) là một cơ chế lưu trữ tạm thời dữ liệu để giảm thiểu thời gian truy cập và tải dữ liệu từ nguồn gốc. Cơ chế cache giúp cải thiện hiệu suất và giảm tải cho máy chủ bằng cách lưu trữ phiên bản của các tài nguyên trên trình duyệt hoặc máy tính của người dùng.

    Có hai loại chính của cache trong JavaScript:

    1.  Cache trình duyệt (Browser cache): Trình duyệt lưu trữ tạm thời các tệp tài nguyên như hình ảnh, CSS, JavaScript, v.v. từ các trang web mà bạn đã truy cập. Khi bạn truy cập lại trang web đó, trình duyệt sẽ sử dụng bản sao được lưu trữ trong cache thay vì tải lại từ máy chủ. Điều này giúp giảm thời gian tải trang và tiết kiệm lưu lượng mạng. Để quản lý cache trình duyệt, bạn có thể sử dụng HTTP Cache-Control headers hoặc các công cụ lập trình viên, chẳng hạn như Service Workers để điều khiển cách cache được quản lý.

    2.  Cache dữ liệu trong ứng dụng JavaScript: Trong các ứng dụng web hoặc ứng dụng đơn trang (SPA), bạn có thể sử dụng cache để lưu trữ kết quả phức tạp tính toán, dữ liệu từ máy chủ, hoặc bất kỳ dữ liệu nào mà bạn muốn lưu trữ tạm thời để tránh tính toán lặp lại hoặc tải dữ liệu lần nữa từ máy chủ. Điều này có thể giúp cải thiện hiệu suất ứng dụng và trải nghiệm người dùng. Bạn có thể sử dụng các cơ chế cache như LocalStorage, SessionStorage, IndexedDB hoặc các thư viện bên thứ ba để quản lý cache dữ liệu trong ứng dụng JavaScript của mình.

    Cần lưu ý rằng việc sử dụng cache cần được thực hiện cẩn thận để đảm bảo rằng dữ liệu được cập nhật đúng mức và không bị lỗi vì việc lưu trữ tạm thời. Việc quản lý cache đòi hỏi một cân nhắc cẩn thận giữa hiệu suất và độ chính xác của dữ liệu trong ứng dụng của bạn.

29. `Bodyparser trong nodejs`

    Trong Node.js, "body-parser" là một middleware được sử dụng để xử lý dữ liệu gửi từ client đến server qua phương thức POST, PUT, PATCH và các phương thức khác có thể chứa dữ liệu trong phần thân (body) của yêu cầu HTTP.

    Khi bạn gửi dữ liệu từ client đến server thông qua phương thức POST hoặc PUT, dữ liệu đó thường được đính kèm trong phần thân của yêu cầu HTTP. Để truy cập và xử lý dữ liệu này trong Node.js, bạn cần sử dụng "body-parser" để giải mã dữ liệu từ phần thân yêu cầu thành các đối tượng JavaScript có thể truy cập và sử dụng dễ dàng.

    Để sử dụng "body-parser" trong ứng dụng Node.js của bạn, bạn cần thực hiện các bước sau:

    1.  Cài đặt gói "body-parser" thông qua npm (Node.js Package Manager):

        ```
        npm install body-parser
        ```

    2.  Sử dụng "body-parser" như một middleware trong mã Express.js của bạn:

        ```javascript
        const express = require("express");
        const bodyParser = require("body-parser");

        const app = express();

        // Sử dụng middleware bodyParser để xử lý dữ liệu từ phần thân yêu cầu
        app.use(bodyParser.urlencoded({ extended: false }));
        app.use(bodyParser.json());

        // Các route và xử lý yêu cầu khác ở đây...

        const port = 3000;
        app.listen(port, () => {
          console.log(`Server is running on port ${port}`);
        });
        ```

    Sau khi cài đặt và sử dụng "body-parser", bạn có thể truy cập dữ liệu gửi từ client thông qua các thuộc tính như `req.body` trong mã route của bạn:

    ```javascript
    app.post("/api/data", (req, res) => {
      const data = req.body; // Truy cập dữ liệu từ phần thân yêu cầu
      console.log(data);
      // Xử lý và trả về phản hồi
    });
    ```

    Lưu ý rằng cần chắc chắn sử dụng "body-parser" trước khi định nghĩa các route mà bạn muốn xử lý dữ liệu từ phần thân yêu cầu.

30. `Cors trong nodejs`

    CORS (Cross-Origin Resource Sharing) là một cơ chế bảo mật trong trình duyệt web, cho phép các trang web từ một nguồn gốc (origin) có thể yêu cầu tài nguyên từ một nguồn gốc khác. Một nguồn gốc là một tập hợp gồm ba yếu tố: giao thức (http, https), tên miền và cổng. Nếu hai trang web có cùng giao thức, tên miền và cổng, chúng được coi là cùng một nguồn gốc (same-origin). CORS giúp ngăn chặn các cuộc yêu cầu không an toàn từ các nguồn gốc khác nhau, nhưng vẫn cho phép các trang web tương tác với nhau một cách an toàn.

    Khi sử dụng Express.js (một framework Node.js phổ biến) để xây dựng ứng dụng web, bạn cần xử lý các yêu cầu CORS nếu ứng dụng của bạn chạy trên một máy chủ (origin) khác với máy chủ chứa tài nguyên mà bạn muốn yêu cầu. Điều này phổ biến khi bạn phát triển các ứng dụng đơn trang (SPA) sử dụng JavaScript để gọi API từ một máy chủ khác.

    Để hỗ trợ CORS trong Express.js, bạn cần thêm middleware có thể xử lý các yêu cầu CORS. Một trong những cách thông thường để làm điều này là sử dụng middleware "cors" của Express.js.

    Để cài đặt middleware cors, bạn cần thực hiện các bước sau:

    1.  Cài đặt gói cors thông qua npm (Node.js Package Manager):

        ```
        npm install cors
        ```

    2.  Sử dụng middleware cors trong mã Express.js của bạn:

        ```javascript
        const express = require("express");
        const cors = require("cors");

        const app = express();

        // Sử dụng middleware cors cho tất cả các yêu cầu đến máy chủ
        app.use(cors());

        // Hoặc có thể chỉ áp dụng cho các route cụ thể
        // app.get('/api/data', cors(), (req, res) => {
        //   // Xử lý yêu cầu và trả về dữ liệu
        // });

        // Các route và xử lý yêu cầu khác ở đây...

        const port = 3000;
        app.listen(port, () => {
          console.log(`Server is running on port ${port}`);
        });
        ```

    Middleware cors sẽ thêm các tiêu đề cần thiết vào các yêu cầu và phản hồi để cho phép hoặc từ chối các yêu cầu từ các nguồn gốc khác nhau. Nó giúp xác định quyền truy cập trên máy chủ và đảm bảo rằng các yêu cầu từ các nguồn không được phép sẽ bị chặn để tránh các vấn đề bảo mật.

31. `Các moudle thường hay sử dụng trong nodejs là gì ?`

    Có rất nhiều module và thư viện được sử dụng trong Node.js để giúp phát triển ứng dụng dễ dàng hơn và mở rộng khả năng của chúng. Dưới đây là một số module phổ biến mà bạn có thể sử dụng trong dự án Node.js:

    1.  **Express:** Một framework web cho Node.js giúp xây dựng các ứng dụng web và API dễ dàng bằng cách cung cấp các tính năng quản lý định tuyến, middleware, và xử lý yêu cầu.

    2.  **Mongoose:** Thư viện hỗ trợ tương tác với cơ sở dữ liệu MongoDB, cung cấp các công cụ để định nghĩa các kiểu dữ liệu, tạo các mô hình và thực hiện các truy vấn dữ liệu.

    3.  **Axios:** Thư viện HTTP client cho Node.js, giúp thực hiện các yêu cầu HTTP đến các API hoặc máy chủ khác.

    4.  **Socket.io:** Thư viện cho phép giao tiếp realtime thông qua WebSocket, hữu ích cho việc xây dựng các ứng dụng chat, game thời gian thực và các ứng dụng realtime khác.

    5.  **Lodash:** Thư viện utility cung cấp nhiều hàm hỗ trợ xử lý mảng, đối tượng, chuỗi, và các tác vụ khác.

    6.  **jsonwebtoken:** Cho phép tạo và xác minh các JSON Web Tokens (JWT), thường được sử dụng để xác thực người dùng trong các ứng dụng web.

    7.  **dotenv:** Cho phép bạn quản lý các biến môi trường trong các tệp `.env` và dễ dàng sử dụng chúng trong ứng dụng của bạn.

    8.  **Multer:** Thư viện giúp xử lý việc tải lên (upload) và lưu trữ tệp tin từ yêu cầu HTTP, thường được sử dụng để xử lý tải lên hình ảnh và tệp đính kèm.

    9.  **Joi:** Thư viện để xác thực và kiểm tra dữ liệu đầu vào, thường được sử dụng trong API để đảm bảo dữ liệu đầu vào hợp lệ.

    10. **Passport:** Thư viện hỗ trợ xác thực người dùng trong ứng dụng, cung cấp các chiến lược xác thực khác nhau như Local, OAuth, JWT, và nhiều chiến lược khác.

    11. **Sequelize:** Thư viện ORM (Object-Relational Mapping) giúp tương tác với cơ sở dữ liệu quan hệ như MySQL, PostgreSQL, SQLite, v.v.

    12. **Nodemailer:** Cho phép gửi email từ ứng dụng Node.js.

    13. **Redis:** Thư viện để tương tác với cơ sở dữ liệu in-memory Redis, thường được sử dụng cho việc lưu trữ bộ nhớ tạm thời và caching.

    14. **Winston:** Thư viện logging mạnh mẽ giúp quản lý và ghi lại thông tin từ ứng dụng.

    Đây chỉ là một số ví dụ về các module phổ biến được sử dụng trong Node.js. Tùy theo yêu cầu cụ thể của dự án, bạn có thể sử dụng nhiều thư viện và module khác nữa.

32. `Middleware function trong nodejs là gì ?`

    Trong Node.js, middleware là các chương trình con (functions) hoặc các plugins được thực thi trong quá trình xử lý của một ứng dụng web. Chúng được gọi liên tiếp theo một thứ tự nhất định, giúp thực hiện các nhiệm vụ như xử lý yêu cầu (request), kiểm tra dữ liệu, thực hiện xác thực, logging, và nhiều chức năng khác mà không phải là chức năng chính của ứng dụng.

    Middleware cho phép bạn tách biệt các phần khác nhau của logic ứng dụng thành các lớp riêng biệt, làm cho mã nguồn dễ đọc, dễ bảo trì và dễ mở rộng.

    Trong Node.js, các framework như Express cung cấp hỗ trợ middleware mạnh mẽ. Ví dụ, để sử dụng middleware trong Express, bạn có thể sử dụng phương thức `.use()`:

    ```javascript
    const express = require("express");
    const app = express();

    // Middleware example
    app.use((req, res, next) => {
      console.log("This is a middleware function.");
      next(); // Chuyển quyền kiểm soát cho middleware tiếp theo
    });

    // Route handler
    app.get("/", (req, res) => {
      res.send("Hello, World!");
    });

    app.listen(3000, () => {
      console.log("Server is running on port 3000");
    });
    ```

    Trong ví dụ trên, middleware function sẽ được gọi mỗi khi có một yêu cầu tới ứng dụng. Sau khi middleware đã hoàn thành công việc của nó, `next()` được gọi để chuyển quyền kiểm soát sang middleware tiếp theo hoặc đến route handler.

    Có thể có nhiều middleware được áp dụng trong cùng một ứng dụng Express, và chúng sẽ được thực thi theo thứ tự bạn khai báo. Middleware có thể thực hiện các nhiệm vụ như kiểm tra xác thực, xử lý dữ liệu đầu vào, bắt lỗi, cài đặt headers, và nhiều chức năng khác tùy theo mục đích của bạn.

33. `Giải thích cách sử dụng next trong nodejs`

    Trong Node.js và các framework như Express, `next` là một tham số được truyền vào trong các middleware functions và route handlers để chuyển quyền kiểm soát từ một middleware hoặc route handler sang middleware hoặc route handler tiếp theo trong chuỗi xử lý.

    Khi một middleware function hoặc route handler hoàn thành công việc của mình và sẵn sàng để chuyển quyền kiểm soát cho middleware tiếp theo, bạn gọi hàm `next()` để thực hiện việc chuyển này. Nếu không gọi `next()`, quyền kiểm soát sẽ không chuyển tiếp và các middleware hoặc route handler tiếp theo sẽ không được thực thi.

    Dưới đây là một ví dụ minh họa cách sử dụng `next` trong Express middleware và route handlers:

    ```javascript
    const express = require("express");
    const app = express();

    // Middleware example
    app.use((req, res, next) => {
      console.log("This is the first middleware.");
      next(); // Chuyển quyền kiểm soát cho middleware tiếp theo
    });

    app.use((req, res, next) => {
      console.log("This is the second middleware.");
      next(); // Chuyển quyền kiểm soát cho route handler
    });

    // Route handler
    app.get("/", (req, res, next) => {
      console.log("This is the route handler.");
      res.send("Hello, World!");
    });

    app.listen(3000, () => {
      console.log("Server is running on port 3000");
    });
    ```

    Trong ví dụ này, khi một yêu cầu đến, quá trình xử lý sẽ được thực hiện theo thứ tự sau:

    1.  Đầu tiên, middleware thứ nhất được gọi và sau khi hoàn thành, nó gọi `next()`.
    2.  Middleware thứ hai được gọi và sau khi hoàn thành, nó gọi `next()`.
    3.  Route handler được gọi và sau khi hoàn thành, yêu cầu được xử lý hoàn toàn.

    Lưu ý rằng việc sử dụng `next()` để chuyển quyền kiểm soát là quan trọng để đảm bảo các middleware và route handler tiếp theo trong chuỗi xử lý cũng được thực thi. Nếu bạn không gọi `next()` trong middleware, hoặc bạn quên gọi nó, quá trình xử lý sẽ bị block và không thể tiếp tục sang các bước tiếp theo.

34. `Tại sao lại chia cấu trúc express app và server`

    Trong Node.js và framework Express, việc chia thành cấu trúc `app` và `server` có thể xuất phát từ việc quản lý mã nguồn và tách biệt các chức năng khác nhau trong ứng dụng. Dưới đây là một số lý do bạn có thể muốn chia cấu trúc như vậy:

    1.  **Tách biệt logic ứng dụng và logic server:** Trong ứng dụng Express, `app` thường chứa tất cả các định nghĩa route handlers, middleware và cấu hình khác của ứng dụng. Trong khi đó, `server` chứa mã để khởi động và lắng nghe máy chủ (server). Việc này giúp bạn tách biệt logic của ứng dụng (như xử lý yêu cầu, xử lý dữ liệu) và logic của máy chủ (như cài đặt port, lắng nghe kết nối).

    2.  **Dễ quản lý khi phát triển:** Chia thành `app` và `server` giúp bạn dễ dàng quản lý mã nguồn và logic của ứng dụng. Khi bạn cần thay đổi cấu hình server, bạn chỉ cần chỉnh sửa trong file `server.js` hoặc tệp tương tự. Khi bạn cần thay đổi logic xử lý ứng dụng, bạn chỉ cần thay đổi trong file `app.js` hoặc tệp tương tự.

    3.  **Dễ dàng kiểm soát và kiểm tra:** Tách biệt `app` và `server` giúp bạn kiểm soát và kiểm tra các khía cạnh khác nhau của ứng dụng một cách riêng biệt. Bạn có thể kiểm tra các route handlers và middleware trong `app` mà không cần phải lo lắng về cấu hình máy chủ. Ngược lại, bạn có thể kiểm tra cấu hình máy chủ mà không cần phải xem xét logic của ứng dụng.

    Dưới đây là ví dụ cách chia thành `app` và `server` trong một ứng dụng Express:

    Trong file `app.js` (hoặc tương tự):

    ```javascript
    const express = require("express");
    const app = express();

    // Định nghĩa route handlers và middleware ở đây

    module.exports = app; // Xuất app để sử dụng ở các file khác
    ```

    Trong file `server.js` (hoặc tương tự):

    ```javascript
    const app = require("./app"); // Import app từ file app.js
    const port = process.env.PORT || 3000;

    app.listen(port, () => {
      console.log(`Server is running on port ${port}`);
    });
    ```

    Tóm lại, việc chia thành `app` và `server` giúp bạn tách biệt logic ứng dụng và logic máy chủ, dễ quản lý khi phát triển, và dễ dàng kiểm soát và kiểm tra từng khía cạnh của ứng dụng.

35. `npm shrinkwrap là gì? cách sử dụng`

    `npm shrinkwrap` là một công cụ trong Node Package Manager (npm) cho phép bạn kiểm soát và bảo đảm rằng các phiên bản của các gói npm được sử dụng trong dự án của bạn được giữ cố định. Khi bạn chạy `npm shrinkwrap`, npm sẽ tạo ra một tệp có tên `npm-shrinkwrap.json` (hoặc `npm-shrinkwrap.yaml` đối với các dự án sử dụng Yarn) để lưu trữ thông tin về phiên bản chính xác của các gói, bao gồm cả phiên bản con (sub-dependencies) của chúng.

    Việc sử dụng `npm shrinkwrap` giúp đảm bảo rằng mọi người trong dự án sẽ sử dụng cùng một phiên bản của các gói npm, ngay cả khi bạn thêm hoặc cập nhật các gói mới vào dự án. Điều này ngăn ngừa các tình huống không mong muốn xảy ra khi phiên bản của một gói thay đổi và gây ra sự không tương thích hoặc lỗi trong dự án của bạn.

    Cách sử dụng `npm shrinkwrap`:

    1.  **Cài đặt các gói trong dự án của bạn:**
        Đảm bảo rằng bạn đã cài đặt tất cả các gói cần thiết cho dự án của mình bằng cách chạy lệnh sau:

        ```
        npm install
        ```

    2.  **Chạy `npm shrinkwrap`:**
        Sau khi đã cài đặt các gói, bạn có thể chạy lệnh sau để tạo tệp `npm-shrinkwrap.json`:

        ```
        npm shrinkwrap
        ```

    3.  **Lưu tệp `npm-shrinkwrap.json` vào kho dự án:**
        Tệp `npm-shrinkwrap.json` sẽ được tạo ra trong thư mục gốc của dự án. Bạn cần đảm bảo tệp này được lưu vào kho dự án (repository) cùng với mã nguồn để đảm bảo rằng mọi người khác trong dự án cũng sẽ sử dụng cùng một phiên bản gói.

    4.  **Commit và push thay đổi:**
        Sau khi đã thêm tệp `npm-shrinkwrap.json` vào kho dự án, bạn cần commit và push thay đổi lên repository để các thành viên khác trong dự án có thể sử dụng tệp này.

    Khi ai đó khác trong dự án chạy `npm install`, npm sẽ sử dụng thông tin trong `npm-shrinkwrap.json` để cài đặt các phiên bản gói chính xác như đã định nghĩa. Điều này giúp đảm bảo tính nhất quán về phiên bản gói giữa các máy tính và môi trường phát triển.

36. `Cookie-parser dùng để làm gì trong nodejs ?`

	Trong Node.js, "cookie parser" là một middleware được sử dụng để xử lý và phân tích cú pháp của các header "Cookie" trong yêu cầu HTTP. Các header Cookie chứa thông tin về các cookies được gửi từ trình duyệt của người dùng đến máy chủ. Middleware này giúp bạn dễ dàng truy cập và làm việc với dữ liệu cookie trong ứng dụng của bạn.

	Cookie parser có thể thực hiện các nhiệm vụ sau:

	1. **Phân tích cú pháp cookie:** Cookie parser giúp bạn trích xuất dữ liệu từ header "Cookie" của yêu cầu HTTP và chuyển chúng thành một đối tượng dễ quản lý. Điều này giúp bạn truy cập và sử dụng dữ liệu cookie dễ dàng hơn.

	2. **Giữ session và xác thực người dùng:** Cookie thường được sử dụng để duy trì thông tin phiên làm việc (session) của người dùng. Cookie parser cho phép bạn lưu trữ các thông tin như ID phiên, thông tin đăng nhập, quyền hạn, vv. và sau đó kiểm tra và xác thực người dùng dựa trên các thông tin này.

	3. **Lưu trữ thông tin tùy chỉnh:** Bạn có thể sử dụng cookie để lưu trữ thông tin tùy chỉnh cho từng người dùng, ví dụ như cài đặt ứng dụng, ngôn ngữ, giao diện người dùng, vv.

	4. **Theo dõi hoạt động người dùng:** Cookie có thể được sử dụng để theo dõi hoạt động của người dùng trên trang web, như xem trang, sản phẩm yêu thích, giỏ hàng, vv.

	Dưới đây là ví dụ cách sử dụng cookie parser trong một ứng dụng Node.js (sử dụng Express framework):

	```javascript
	const express = require('express');
	const cookieParser = require('cookie-parser');

	const app = express();

	// Sử dụng cookie parser middleware
	app.use(cookieParser());

	// Route để đặt cookie và đọc cookie
	app.get('/set-cookie', (req, res) => {
		res.cookie('username', 'john_doe', { maxAge: 900000, httpOnly: true });
		res.send('Cookie đã được đặt.');
	});

	app.get('/get-cookie', (req, res) => {
		const username = req.cookies.username;
		res.send(`Tên người dùng từ cookie: ${username}`);
	});

	app.listen(3000, () => {
		console.log('Server đang lắng nghe tại cổng 3000...');
	});
	```

	Lưu ý rằng, việc sử dụng cookies cần được thực hiện cẩn thận để đảm bảo an toàn và bảo mật cho người dùng của bạn.

37. `Các phương thức kết nối trong mô hình microservices nestjs`

	Trong mô hình microservices với NestJS, các dịch vụ được xây dựng và triển khai độc lập nhau và cần phải có khả năng giao tiếp. NestJS hỗ trợ nhiều phương thức để thiết lập kết nối giữa các dịch vụ microservices. Dưới đây là một số phương thức phổ biến:

	1. **Transporter-based (giao tiếp dựa trên Transporter):**
		NestJS hỗ trợ nhiều loại transporter như AMQP (RabbitMQ), MQTT, Redis, NATS, Kafka, và một số loại khác. Đây là các cơ chế giao tiếp bất đồng bộ dựa trên hàng đợi hoặc kênh.

		Ví dụ sử dụng Redis transporter:
		```typescript
		const app = await NestFactory.createMicroservice<MicroserviceOptions>(AppModule, {
			transport: Transport.REDIS,
			options: {
				url: 'redis://localhost:6379',
			},
		});
		```

	2. **HTTP-based (giao tiếp dựa trên HTTP):**
		Microservices có thể giao tiếp thông qua các API HTTP. NestJS cung cấp `HttpService` để thực hiện cuộc gọi HTTP tới các dịch vụ khác.

		Ví dụ sử dụng `HttpService`:
		```typescript
		@Injectable()
		export class AppService {
			constructor(private httpService: HttpService) {}

			async fetchDataFromOtherService(): Promise<any> {
				const response = await this.httpService.get('http://other-service/api/data').toPromise();
				return response.data;
			}
		}
		```

	3. **gRPC-based (giao tiếp dựa trên gRPC):**
		gRPC là một giao thức giao tiếp mạnh mẽ, phù hợp cho việc gọi từ xa. NestJS hỗ trợ giao tiếp dựa trên gRPC thông qua decorators và module riêng.

		Ví dụ sử dụng gRPC:
		```typescript
		@GrpcService()
		export class MathService {
			@GrpcMethod('Add')
			add(data: any): any {
				const { a, b } = data;
				return { result: a + b };
			}
		}
		```

	Nhớ rằng, phương thức giao tiếp cụ thể bạn chọn sẽ phụ thuộc vào yêu cầu của ứng dụng và sự tương thích với hệ thống hiện tại. NestJS cho phép bạn lựa chọn phương thức giao tiếp tốt nhất cho từng trường hợp sử dụng và kết hợp chúng trong cùng một ứng dụng.

38. `gRPC là gì ? cho ví dụ sử dụng gRPC trong nestjs`

	gRPC (g stands for "Google") là một giao thức giao tiếp từ xa (remote procedure call protocol) được phát triển ban đầu bởi Google. Nó cho phép các ứng dụng chạy trên các máy tính khác nhau có thể giao tiếp và gọi hàm từ xa như gọi hàm cục bộ, mà không cần phải quan tâm đến việc truyền dữ liệu qua mạng như thế nào.

	Một số đặc điểm của gRPC:

	- Sử dụng giao thức HTTP/2 cho việc truyền tải dữ liệu, tối ưu hóa hiệu suất và tiết kiệm tài nguyên.
	- Hỗ trợ nhiều ngôn ngữ lập trình, cho phép bạn tạo các dịch vụ từ xa và khách hàng trên các ngôn ngữ khác nhau.
	- Định nghĩa giao diện dịch vụ bằng Protobuf (Protocol Buffers), giúp đảm bảo sự chính xác và khả năng cập nhật trong tương lai.

	Dưới đây là một ví dụ cơ bản về cách sử dụng gRPC trong NestJS:

	1. **Cài đặt các thư viện cần thiết:**
		Cài đặt các thư viện `@nestjs/microservices` và `@nestjs/microservices/protos` để hỗ trợ gRPC trong NestJS.

	2. **Định nghĩa giao diện dịch vụ bằng Protobuf:**
		Đầu tiên, bạn cần định nghĩa giao diện dịch vụ bằng Protobuf. Ví dụ, tạo file `math.proto` như sau:

		```protobuf
		syntax = "proto3";

		service MathService {
			rpc Add (AddRequest) returns (AddResponse);
		}

		message AddRequest {
			int32 a = 1;
			int32 b = 2;
		}

		message AddResponse {
			int32 result = 1;
		}
		```

	3. **Tạo dịch vụ gRPC trong NestJS:**
		Tạo một module dịch vụ gRPC bằng cách sử dụng `@nestjs/microservices` và `@nestjs/microservices/protos`:

		```typescript
		import { Module } from '@nestjs/common';
		import { ClientsModule, Transport } from '@nestjs/microservices';
		import { join } from 'path';

		@Module({
			imports: [
				ClientsModule.register([
					{
						name: 'MATH_SERVICE',
						transport: Transport.GRPC,
						options: {
							url: 'localhost:50051',
							package: 'math',
							protoPath: join(__dirname, 'math.proto'),
						},
					},
				]),
			],
		})
		export class MathModule {}
		```

	4. **Sử dụng dịch vụ gRPC trong NestJS Controller:**
		Sử dụng dịch vụ gRPC đã đăng ký trong controller:

		```typescript
		import { Controller, Logger } from '@nestjs/common';
		import { GrpcMethod } from '@nestjs/microservices';
		import { Observable } from 'rxjs';
		import { MathService } from './math.interface';

		@Controller()
		export class AppController {
			private logger = new Logger('AppController');

			constructor(private readonly mathService: MathService) {}

			@GrpcMethod('MathService', 'Add')
			accumulate(data: { a: number; b: number }): { result: number } {
				this.logger.log(`Adding ${data.a} and ${data.b}`);
				return { result: data.a + data.b };
			}
		}
		```

	5. **Khởi động ứng dụng NestJS:**
		Khởi động ứng dụng NestJS với module `MathModule`.

	Ví dụ trên là một ví dụ cơ bản về cách sử dụng gRPC trong NestJS. Giao thức gRPC có nhiều tính năng mạnh mẽ khác như xác thực, mã hóa, streaming, và nhiều loại tương tác khác.

39. `Setup một project nodejs đơn giản với chủ đề ecommerce`

	Dưới đây là một hướng dẫn cơ bản về cách tạo một dự án Node.js đơn giản về thương mại điện tử (ecommerce):

	**Bước 1: Chuẩn bị môi trường**
	1. Đảm bảo bạn đã cài đặt Node.js và npm (Node Package Manager) trên máy tính của bạn.

	**Bước 2: Tạo thư mục dự án và khởi tạo dự án**
	1. Tạo một thư mục mới cho dự án của bạn:
		```
		mkdir ecommerce-project
		cd ecommerce-project
		```

	2. Khởi tạo dự án Node.js bằng lệnh sau và làm theo hướng dẫn trên màn hình:
		```
		npm init
		```

	**Bước 3: Cài đặt các gói cần thiết**
	1. Cài đặt Express để xây dựng web server:
		```
		npm install express
		```

	2. Cài đặt EJS (Embedded JavaScript) để làm việc với giao diện người dùng:
		```
		npm install ejs
		```

	**Bước 4: Tạo cấu trúc dự án**
	1. Tạo thư mục `views` trong thư mục dự án để chứa các tệp giao diện người dùng.

	2. Tạo một tệp `index.ejs` trong thư mục `views` để hiển thị trang chính của trang web.

	**Bước 5: Tạo server**
	1. Tạo tệp `app.js` (hoặc `index.js`) trong thư mục gốc của dự án và tạo server Express:

		```javascript
		const express = require('express');
		const app = express();

		app.set('view engine', 'ejs'); // Sử dụng EJS làm engine view
		app.use(express.static('public')); // Sử dụng các tệp tĩnh trong thư mục public

		app.get('/', (req, res) => {
			res.render('index'); // Hiển thị giao diện người dùng index.ejs
		});

		const PORT = process.env.PORT || 3000;
		app.listen(PORT, () => {
			console.log(`Server đang chạy tại cổng ${PORT}`);
		});
		```

	**Bước 6: Tạo tệp giao diện người dùng**
	1. Trong tệp `views/index.ejs`, bạn có thể thêm mã HTML để hiển thị giao diện người dùng của trang chính.

	**Bước 7: Chạy dự án**
	1. Sử dụng lệnh sau để chạy dự án:
		```
		node app.js
		```

	**Bước 8: Truy cập trang web**
	1. Mở trình duyệt và truy cập `http://localhost:3000` để xem trang web của bạn.

	Lưu ý rằng đây chỉ là một hướng dẫn cơ bản về cách tạo dự án Node.js về thương mại điện tử. Một ứng dụng thương mại điện tử thực sự sẽ phức tạp hơn với các chức năng như đăng ký, đăng nhập, xem sản phẩm, thêm vào giỏ hàng, thanh toán, vv. Bạn có thể mở rộng dự án này bằng cách thêm các chức năng và tính năng phức tạp hơn.

## LOOPBACK

LoopBack là một framework phát triển ứng dụng web và API được xây dựng trên Node.js. Dựa vào trang web mà bạn đã cung cấp, sau đây là một số đặc điểm chính của LoopBack:

1. Mô hình lập trình hướng cơ sở dữ liệu (DBMS-agnostic): LoopBack hỗ trợ nhiều loại cơ sở dữ liệu như MongoDB, PostgreSQL, MySQL và các cơ sở dữ liệu khác. Nó cho phép bạn xác định các mô hình dữ liệu và tự động tạo các API RESTful cho các mô hình đó.

2. Tích hợp dữ liệu linh hoạt: LoopBack giúp bạn tạo ra các kết nối và tương tác với các nguồn dữ liệu khác nhau, bao gồm cơ sở dữ liệu, dịch vụ RESTful, SOAP, các trang web HTML và hơn thế nữa.

3. Tạo API nhanh chóng: Với LoopBack, bạn có thể nhanh chóng tạo ra các API RESTful cho các mô hình dữ liệu mà bạn đã xác định. Framework này cung cấp các phương pháp CRUD (Create, Read, Update, Delete) tiêu chuẩn, cho phép bạn dễ dàng tạo, đọc, cập nhật và xóa dữ liệu.

4. Tích hợp bảo mật: LoopBack cung cấp các tính năng bảo mật như xác thực người dùng, quản lý quyền truy cập và mã hóa dữ liệu. Bạn có thể dễ dàng xác định các quyền và phân quyền cho từng tài nguyên trong ứng dụng của mình.

5. Hỗ trợ phát triển đa nền tảng: LoopBack hỗ trợ việc phát triển ứng dụng web và API trên nhiều nền tảng, bao gồm cả di động. Bạn có thể xây dựng ứng dụng dành cho các thiết bị di động sử dụng React Native hoặc NativeScript và tận dụng các tính năng của LoopBack.

6. Thư viện mở rộng và tiện ích: LoopBack cung cấp nhiều thư viện mở rộng và tiện ích để giúp bạn phát triển ứng dụng một cách hiệu quả. Các module mở rộng cung cấp các tính năng như gửi email, xử lý ảnh, giao diện người dùng, và nhiều hơn nữa.

Tóm lại, LoopBack là một framework mạnh mẽ cho phát triển ứng dụng web và API, với khả năng tích hợp dữ liệu linh hoạt, tạo API nhanh chóng và hỗ trợ bảo mật. Nó cũng cho phép phát triển trên nhiều nền tảng và cung cấp nhiều tiện ích và thư viện mở rộng để tăng cường khả năng phát triển của bạn.

### INTERCEPTOR

Trong LoopBack 4, Interceptor là một khái niệm quan trọng để kiểm soát và thay đổi luồng xử lý của các yêu cầu và phản hồi trong ứng dụng. Interceptor cho phép bạn thực hiện các hành động trước và sau khi yêu cầu được xử lý bởi các thành phần khác trong ứng dụng.

Interceptor có thể được sử dụng để thực hiện các tác vụ như:

1. Xác thực: Kiểm tra xem người dùng đã được xác thực hay chưa trước khi cho phép truy cập vào tài nguyên.

2. Ghi log: Ghi lại các thông tin quan trọng về yêu cầu và phản hồi để phân tích và theo dõi hoạt động của ứng dụng.

3. Ghi lại thời gian: Đo và ghi lại thời gian xử lý yêu cầu để xác định hiệu suất và tối ưu hóa ứng dụng.

4. Thêm thông tin phụ: Thêm thông tin bổ sung vào yêu cầu hoặc phản hồi, chẳng hạn như thông tin ngôn ngữ, thông tin phiên bản, v.v.

5. Kiểm tra lỗi: Xử lý các lỗi xảy ra trong quá trình xử lý yêu cầu và phản hồi.

Để triển khai một Interceptor trong LoopBack 4, bạn cần thực hiện các bước sau:

1. Định nghĩa một lớp mới mở rộng từ `Interceptor` và triển khai các phương thức cần thiết, chẳng hạn `intercept()`.

2. Trong phương thức `intercept()`, bạn có thể thực hiện các hành động của Interceptor, chẳng hạn như kiểm tra, ghi log, thay đổi yêu cầu và phản hồi, và gọi `next()` để chuyển giao quyền kiểm soát cho Interceptor tiếp theo hoặc thành phần cuối cùng trong chuỗi Interceptor.

3. Đăng ký Interceptor trong ứng dụng bằng cách thêm nó vào phương thức `component()` trong file `application.ts`. Ví dụ:

```typescript
import { Interceptor } from "@loopback/core";

export class MyInterceptor implements Interceptor {
  async intercept(
    invocationCtx: InvocationContext,
    next: Next
  ): Promise<ValueOrPromise<InvocationResult>> {
    // Thực hiện các hành động của Interceptor ở đây

    // Gọi next() để chuyển giao quyền kiểm soát cho Interceptor tiếp theo hoặc thành phần cuối cùng
    return await next();
  }
}
```

```typescript
import { MyInterceptor } from "./my-interceptor";

export class MyApplication extends Application {
  constructor(options: ApplicationConfig = {}) {
    super(options);

    // Đăng ký Interceptor trong ứng dụng
    this.component(MyInterceptor);
  }
}
```

Lưu ý rằng Interceptor trong LoopBack 4 được thực hiện theo kiểu "Chuỗi Interceptor" (Interceptor Chain), trong đó mỗi Interceptor có thể được đăng ký và chạy tuần tự theo thứ tự xác định.

# Database

## SQL

### SQL (Structured Query Language) là một ngôn ngữ lập trình dùng để truy vấn và quản lý cơ sở dữ liệu quan hệ (Relational Database Management System - RDBMS). SQL được thiết kế để thao tác dữ liệu trong các hệ thống quản lý cơ sở dữ liệu quan hệ như MySQL, Oracle, SQL Server, PostgreSQL, và SQLite.

Tại sao phải sử dụng ngôn ngữ SQL:

1. Dễ học và sử dụng: SQL có cú pháp đơn giản, dễ hiểu và rất giống với ngôn ngữ tự nhiên, do đó, việc học và sử dụng SQL trở nên dễ dàng cho người mới bắt đầu.

2. Đa nền tảng: SQL có thể chạy trên nhiều hệ thống quản lý cơ sở dữ liệu khác nhau, cho phép bạn chuyển đổi giữa các hệ thống mà không cần thay đổi nhiều mã nguồn.

3. Quản lý cơ sở dữ liệu quan hệ: SQL hỗ trợ tạo, cập nhật, xóa và truy vấn dữ liệu trong cơ sở dữ liệu quan hệ, giúp bạn quản lý mối quan hệ giữa các bảng và cột dễ dàng.

4. Hiệu suất tốt: SQL được tối ưu hóa để thực thi các truy vấn dữ liệu một cách hiệu quả và nhanh chóng.

Đặc điểm và thế mạnh của SQL:

- Đơn giản và dễ hiểu: SQL sử dụng cú pháp đơn giản, cho phép người dùng truy vấn dữ liệu và thực hiện các thao tác cơ bản một cách dễ dàng.
- Tính tương thích: SQL tương thích với nhiều hệ thống quản lý cơ sở dữ liệu, cho phép truy cập và thao tác dữ liệu trên nhiều hệ thống khác nhau.
- Mạnh mẽ và linh hoạt: SQL cung cấp các câu lệnh mạnh mẽ để truy vấn, tìm kiếm, sắp xếp, lọc và thao tác dữ liệu trong cơ sở dữ liệu.
- Hỗ trợ giao dịch: SQL hỗ trợ giao dịch ACID (Atomicity, Consistency, Isolation, Durability), đảm bảo tính toàn vẹn và nhất quán của dữ liệu trong quá trình thực hiện các thao tác.

Điểm yếu của SQL:

- Không phù hợp cho cơ sở dữ liệu phi quan hệ: SQL chủ yếu được sử dụng cho cơ sở dữ liệu quan hệ, vì vậy không phù hợp cho các cơ sở dữ liệu phi quan hệ như MongoDB (NoSQL) hoặc các hệ thống lưu trữ khác.
- Khó thay đổi cấu trúc: Khi cấu trúc cơ sở dữ liệu thay đổi, việc sửa đổi các truy vấn SQL có thể gặp khó khăn và đòi hỏi sự thay đổi trong mã nguồn.
- Hiệu suất có thể bị ảnh hưởng: SQL có thể gặp vấn đề hiệu suất khi xử lý các tác vụ phức tạp hoặc với cơ sở dữ liệu lớn. Việc tối ưu truy vấn SQL là một thách thức đối với các cơ sở dữ liệu lớn và có tải cao.

Các cách tối ưu sql trong hệ thống lớn
Để tối ưu SQL trong một hệ thống cơ sở dữ liệu lớn, có thể áp dụng các kỹ thuật và phương pháp sau:

1. Chỉ lấy ra những dữ liệu cần thiết: Sử dụng câu truy vấn SELECT để chỉ lấy ra các cột và hàng dữ liệu cần thiết thay vì lấy toàn bộ dữ liệu. Điều này giúp giảm tải cho cơ sở dữ liệu và tăng tốc độ truy vấn.

2. Tối ưu hóa câu truy vấn: Xem xét cấu trúc câu truy vấn và sử dụng các chỉ dẫn, chỉ mục (index) và câu lệnh JOIN để cải thiện hiệu suất. Đảm bảo rằng các bảng được thiết kế chính xác và các chỉ mục được tạo cho các cột mà thường xuyên được sử dụng trong câu truy vấn.

3. Sử dụng câu lệnh EXPLAIN: Sử dụng câu lệnh EXPLAIN để kiểm tra kế hoạch truy vấn của cơ sở dữ liệu và xác định các vấn đề hiệu suất. Điều này giúp tìm ra các truy vấn chậm chạp hoặc không hiệu quả và tối ưu hóa chúng.

4. Cải thiện chỉ mục: Sử dụng chỉ mục (index) cho các cột thường xuyên được sử dụng trong câu truy vấn để giảm thời gian truy xuất dữ liệu. Xác định những cột quan trọng và tạo chỉ mục cho chúng.

5. Điều chỉnh cấu hình hệ thống: Xem xét và điều chỉnh cấu hình hệ thống cơ sở dữ liệu và máy chủ database để tối ưu hiệu suất. Điều này có thể bao gồm cấu hình bộ đệm (buffer cache), kích thước bộ đệm, số lượng kết nối đồng thời và các thiết lập khác.

6. Partitioning (Phân vùng): Sử dụng kỹ thuật phân vùng để chia dữ liệu thành các phân đoạn nhỏ hơn, tách biệt theo tiêu chí nhất định. Điều này giúp tăng tốc độ truy vấn và quản lý dữ liệu hiệu quả hơn.

7. Caching (Bộ nhớ cache): Sử dụng bộ nhớ cache để lưu trữ các kết quả truy vấn phổ biến. Việc này giúp giảm tải cho cơ sở dữ liệu và cung cấp thời gian truy vấn nhanh hơn.

8. Vertical và horizontal scaling: Xem xét sử dụng các phương pháp scale cơ sở dữ liệu, bao gồm scaling theo chiều dọc (vertical scaling) và scaling theo chiều ngang (horizontal scaling), để tăng khả năng chịu tải và hiệu suất của hệ thống.

- Cần lưu ý rằng tối ưu SQL là một quá trình liên tục và đòi hỏi sự phân tích kỹ lưỡng, theo dõi hiệu suất và tinh chỉnh liên tục để đạt được kết quả tối ưu nhất cho hệ thống cơ sở dữ liệu lớn.

Đánh chỉ mục index

Đánh chỉ mục (indexing) là một cách tối ưu hóa truy vấn SQL bằng cách tạo ra một cấu trúc dữ liệu phụ để tăng tốc độ truy xuất dữ liệu từ cơ sở dữ liệu. Dưới đây là các cách đánh chỉ mục trong SQL:

1. Đánh chỉ mục cột đơn (Single-column indexing):

   - Non-unique index: Đánh chỉ mục không duy nhất trên một cột dùng để tìm kiếm và sắp xếp dữ liệu. Ví dụ: `CREATE INDEX idx_column_name ON table_name (column_name);`
   - Unique index: Đánh chỉ mục duy nhất trên một cột đảm bảo rằng không có giá trị trùng lặp trong cột đó. Ví dụ: `CREATE UNIQUE INDEX idx_column_name ON table_name (column_name);`

2. Đánh chỉ mục cột kết hợp (Composite indexing):

   - Non-unique composite index: Đánh chỉ mục không duy nhất trên một nhóm cột kết hợp. Ví dụ: `CREATE INDEX idx_column1_column2 ON table_name (column1, column2);`
   - Unique composite index: Đánh chỉ mục duy nhất trên một nhóm cột kết hợp đảm bảo rằng không có giá trị trùng lặp trong nhóm cột đó. Ví dụ: `CREATE UNIQUE INDEX idx_column1_column2 ON table_name (column1, column2);`

3. Đánh chỉ mục trên biểu thức (Expression indexing): Đánh chỉ mục trên một biểu thức hoặc hàm của cột để tối ưu hóa truy vấn. Ví dụ: `CREATE INDEX idx_expression ON table_name (LOWER(column_name));`

4. Đánh chỉ mục trên kiểu dữ liệu không gian (Spatial indexing): Đánh chỉ mục trên các kiểu dữ liệu không gian (GIS) để tối ưu hóa các truy vấn không gian. Ví dụ: `CREATE SPATIAL INDEX idx_spatial ON table_name (column_name);`

5. Đánh chỉ mục full-text (Full-text indexing): Đánh chỉ mục trên cột chứa dữ liệu văn bản để tối ưu truy vấn full-text search. Ví dụ: `CREATE FULLTEXT INDEX idx_fulltext ON table_name (column_name);`

6. Xóa chỉ mục (Drop index): Để xóa chỉ mục không cần thiết, sử dụng câu lệnh `DROP INDEX`. Ví dụ: `DROP INDEX idx_column_name ON table_name;`

- Lưu ý rằng việc đánh chỉ mục cần được thực hiện một cách cân nhắc, tùy thuộc vào các yêu cầu và mẫu truy vấn của hệ thống. Đánh quá nhiều chỉ mục có thể làm tăng kích thước cơ sở dữ liệu và làm chậm quá trình cập nhật dữ liệu.

Thuật toán đánh index trong sql là gì

- Bản chất của quá trình index là việc chuyển đổi một hoặc nhiều column sang table mới (DB system sẽ quản lý table này) với các tính chất
  - Table index được sắp xếp theo thứ tự, giá trị của column là giá trị của một hoặc nhiều column được đánh index
  - Tìm kiếm nhanh hơn với một vài điều kiện trên column được đánh index
  - Mỗi index được ánh xạ sang một hoặc nhiều row trong table chính
  - Có thể index được nhiều cột cùng lúc
- Thay vì scanning trên table chính, ta sẽ scanning trên table index

  - DB engine sẽ kiểm tra column với Where condition được đánh index hay không, nếu có nó chỉ lấy column được index để thực hiện trên việc scan trên index table thay vì scan trên table chính, giảm tải lượng data phải read từ disk
  - Table index được sắp xếp nên việc scan đơn giản hơn. Thay vì scan toàn bộ --> sử dụng cấu truc binary tree để scan. Phổ biến nhất là dùng BTREE index B-Tree LÀ Balanced Tree

- Trong hệ thống quản lý cơ sở dữ liệu (DBMS), thuật toán phổ biến được sử dụng để đánh chỉ mục trong SQL là thuật toán B-tree (Balanced Tree). B-tree là một cấu trúc dữ liệu cây cân bằng được sử dụng để lưu trữ và tìm kiếm dữ liệu theo thứ tự.

- Thuật toán B-tree xây dựng một cây có nhiều cấp (levels) từ các nút (nodes) chứa khóa (keys) được sắp xếp theo thứ tự tăng dần. Mỗi nút trong B-tree có thể chứa nhiều khóa và các con trỏ đến các nút con. Điều này cho phép tìm kiếm hiệu quả dữ liệu bằng cách sử dụng phép tìm kiếm nhị phân (binary search) trên cây.

- Khi tạo chỉ mục B-tree trên một cột trong SQL, hệ thống quản lý cơ sở dữ liệu sẽ sắp xếp các giá trị trong cột theo thứ tự tăng dần và xây dựng cây B-tree dựa trên các khóa đó. Quá trình này thường được thực hiện tự động bởi hệ thống, không yêu cầu sự can thiệp từ người dùng.

- Với cây B-tree, việc tìm kiếm, chèn và xóa dữ liệu có thể được thực hiện trong thời gian O(log n), với n là số lượng khóa trong cây. Điều này giúp cải thiện hiệu suất truy vấn trong SQL khi sử dụng chỉ mục.

- Ngoài thuật toán B-tree, còn có các thuật toán khác được sử dụng trong việc đánh chỉ mục như thuật toán Hash Indexing, R-tree (dùng trong các truy vấn không gian) và Full-text Indexing (dùng trong truy vấn văn bản). Mỗi thuật toán có ưu điểm và hạn chế riêng, và lựa chọn thuật toán đánh chỉ mục phụ thuộc vào yêu cầu và đặc điểm của ứng dụng cụ thể.

- Order By được sử dụng trong sql để sắp xếp dữ liệu trả về bởi một câu truy vấn theo thứ tự tăng hoặc giảm dần (mặc định là giảm dần). ASC là tăng dần, DESC là giảm dần

  ```
  SELECT column1, column2, ...
  FROM table_name
  ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;
  ```

- Group By, được sử dụng trong câu SQL để tổ chức dữ liệu có thuộc tính giống nhau.**Group by đặt sau mệnh đề where, Group by đặt trước order by**. Chúng ta thường sử dụng mệnh để để phối hợp vs các phép toán như SUM, MAX, AVG, MIN, COUNT. Điều quan trọng cần nhớ là thuộc tính trong mệnh đề này phải đi cùng với Select. Mệnh đề group by luôn đi cùng với select. Truy vấn cho mệnh đề group by trả về một hàng duy nhất cho mỗi đối tượng được nhóm.

GROUP BY

- Nó được sử dụng để nhóm các hàng có cùng giá trị.
- Nó có thể được cho phép trong câu lệnh CREATE VIEW.
- Nó kiểm soát việc trình bày các hàng.
- Thuộc tính không được dưới hàm tổng hợp trong câu lệnh GROUP BY.
- Nó luôn được sử dụng trước mệnh đề ORDER BY trong câu lệnh SELECT.
- Bắt buộc phải sử dụng các hàm tổng hợp trong GROUP BY.
- Ở đây, việc phân nhóm được thực hiện dựa trên sự giống nhau giữa các giá trị thuộc tính của hàng.

ORDER BY

- Nó sắp xếp tập kết quả theo thứ tự tăng dần hoặc giảm dần.
- Nó không được phép trong câu lệnh CREATE VIEW
- Nó kiểm soát việc trình bày các cột.
- Thuộc tính có thể nằm dưới hàm tổng hợp trong câu lệnh ORDER BY.
- Nó luôn được sử dụng sau mệnh đề GROUP BY trong câu lệnh SELECT.
- Không bắt buộc phải sử dụng các hàm tổng hợp trong ORDER BY.
- Ở đây, tập hợp kết quả được sắp xếp dựa trên các giá trị thuộc tính của cột, theo thứ tự tăng dần hoặc giảm dần.

1. `FOREIGN KEY TRONG SQL LA GI `

   Trong SQL, FOREIGN KEY (tạm dịch là "khóa ngoại") là một ràng buộc dữ liệu được sử dụng để liên kết hai bảng trong cơ sở dữ liệu. Nó xác định một quan hệ giữa hai bảng thông qua một trường hoặc một tập hợp các trường trong bảng.

   Khi tạo một khóa ngoại, bạn định nghĩa rõ ràng rằng các giá trị trong trường hoặc tập hợp trường trong bảng hiện tại là liên kết với các giá trị trong trường hoặc tập hợp trường của bảng khác. Điều này giúp xây dựng mối quan hệ giữa hai bảng, cho phép bạn thực hiện các thao tác liên quan đến dữ liệu từ các bảng khác nhau.

   Cú pháp tạo FOREIGN KEY trong SQL thường có dạng như sau:

   ```sql
   CREATE TABLE table_name (
   		column1 data_type,
   		column2 data_type,
   		...,
   		FOREIGN KEY (column1, column2, ...) REFERENCES other_table (other_column1, other_column2, ...)
   );
   ```

   Trong đó:

   - `table_name`: Tên bảng hiện tại.
   - `column1, column2, ...`: Các trường trong bảng hiện tại được sử dụng làm khóa ngoại.
   - `other_table`: Tên bảng mà trường khóa ngoại tham chiếu đến.
   - `other_column1, other_column2, ...`: Các trường trong bảng tham chiếu được kết nối với các trường trong bảng hiện tại.

   Một khi bạn đã định nghĩa khóa ngoại, việc thực hiện các thao tác JOIN hoặc truy vấn dữ liệu từ nhiều bảng liên quan sẽ trở nên dễ dàng và hiệu quả hơn. Khóa ngoại đóng vai trò quan trọng trong việc duy trì tính toàn vẹn và hợp lý của dữ liệu trong cơ sở dữ liệu.

2 `Bình thường hóa trong sql là gì`

Bình thường hóa (Normalization) trong SQL là quá trình thiết kế cơ sở dữ liệu để giảm thiểu sự trùng lặp thông tin và đảm bảo tính toàn vẹn dữ liệu. Mục tiêu của bình thường hóa là tạo ra cấu trúc cơ sở dữ liệu tối ưu, giúp truy xuất và cập nhật dữ liệu dễ dàng và hiệu quả hơn.

Quá trình bình thường hóa thường được thực hiện thông qua các bước sau:

1. Bình thường hóa cấp 1 (1st Normal Form - 1NF): Đảm bảo mỗi ô dữ liệu trong bảng chỉ chứa một giá trị đơn. Bảng không chứa các trường lặp lại hoặc giá trị đa giá trị (multivalued attributes).

2. Bình thường hóa cấp 2 (2nd Normal Form - 2NF): Bảng đã đạt 1NF và không có các thuộc tính phụ thuộc hàm trong phần còn lại của khóa chính. Trong trường hợp bảng có nhiều trường khóa, thì mỗi thuộc tính phải phụ thuộc vào toàn bộ khóa chính, không chỉ một phần của nó.

3. Bình thường hóa cấp 3 (3rd Normal Form - 3NF): Bảng đã đạt 2NF và không có các phụ thuộc trực tiếp giữa các thuộc tính non-key (không phải là khóa chính). Mỗi thuộc tính non-key phụ thuộc duy nhất vào khóa chính.

Ngoài ra, còn có các cấp bình thường hóa cao hơn như bình thường hóa cấp 4 (4th Normal Form - 4NF) và bình thường hóa cấp 5 (5th Normal Form - 5NF) tùy thuộc vào độ phức tạp và yêu cầu của cơ sở dữ liệu.

Bình thường hóa giúp loại bỏ sự trùng lặp và đảm bảo tính toàn vẹn của dữ liệu, tăng cường hiệu suất và sự linh hoạt của cơ sở dữ liệu. Tuy nhiên, việc bình thường hóa cũng có thể làm tăng độ phức tạp trong việc truy xuất dữ liệu từ nhiều bảng liên quan, do đó, việc thiết kế cơ sở dữ liệu cần cân nhắc giữa hiệu quả và phức tạp trong môi trường ứng dụng cụ thể.

3 `Sự khác biệt giữa Ngôn ngữ định nghĩa dữ liệu (DDL) và Ngôn ngữ thao tác dữ liệu (DML) là gì?`

Sự khác biệt giữa Ngôn ngữ định nghĩa dữ liệu (DDL - Data Definition Language) và Ngôn ngữ thao tác dữ liệu (DML - Data Manipulation Language) trong SQL là như sau:

1. Ngôn ngữ định nghĩa dữ liệu (DDL - Data Definition Language):

   - Mục đích: DDL được sử dụng để định nghĩa và quản lý cấu trúc cơ sở dữ liệu.
   - Các câu lệnh: DDL bao gồm các câu lệnh để tạo, sửa đổi hoặc xóa các đối tượng cơ sở dữ liệu như bảng, chỉ mục, khóa ngoại, quyền truy cập, chế độ xem, v.v.
   - Ví dụ: Một số câu lệnh DDL phổ biến như `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `GRANT`, `REVOKE`, v.v.

2. Ngôn ngữ thao tác dữ liệu (DML - Data Manipulation Language):
   - Mục đích: DML được sử dụng để thao tác và quản lý dữ liệu trong các bảng và cơ sở dữ liệu.
   - Các câu lệnh: DML bao gồm các câu lệnh để truy xuất, chèn, cập nhật và xóa dữ liệu từ bảng trong cơ sở dữ liệu.
   - Ví dụ: Một số câu lệnh DML phổ biến như `SELECT`, `INSERT`, `UPDATE`, `DELETE`, v.v.

Ví dụ minh họa sự khác biệt giữa DDL và DML:

1. Sử dụng DDL để tạo bảng trong cơ sở dữ liệu:

```sql
-- DDL
CREATE TABLE Customers (
    ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT
);
```

2. Sử dụng DML để chèn dữ liệu vào bảng đã tạo:

```sql
-- DML
INSERT INTO Customers (ID, Name, Age) VALUES (1, 'John', 30);
INSERT INTO Customers (ID, Name, Age) VALUES (2, 'Alice', 25);
```

3. Sử dụng DML để truy xuất dữ liệu từ bảng:

```sql
-- DML
SELECT * FROM Customers WHERE Age > 25;
```

Tóm lại, DDL được sử dụng để định nghĩa cấu trúc dữ liệu trong cơ sở dữ liệu, trong khi DML được sử dụng để thao tác và quản lý dữ liệu trong các bảng.

3. `Sự khác biệt giữa truncate và delete trong sql`

   Truncate và Delete là hai câu lệnh trong SQL được sử dụng để xóa dữ liệu từ bảng, nhưng chúng có một số sự khác biệt quan trọng:

   1. TRUNCATE:
      - TRUNCATE là một câu lệnh DDL (Data Definition Language).
      - TRUNCATE được sử dụng để xóa toàn bộ nội dung của bảng.
      - TRUNCATE làm việc nhanh hơn DELETE vì nó không ghi lại từng hàng xóa vào log, mà chỉ ghi lại thông tin không gian được giải phóng trong bảng.
      - TRUNCATE không hỗ trợ điều kiện WHERE và không thể hoàn tác (non-rollbackable).
      - Khi sử dụng TRUNCATE, không có trigger (cơ chế kích hoạt) nào được kích hoạt.

   Ví dụ TRUNCATE:

   ```sql
   TRUNCATE TABLE table_name;
   ```

   2. DELETE:
      - DELETE là một câu lệnh DML (Data Manipulation Language).
      - DELETE được sử dụng để xóa dữ liệu từ bảng dựa trên điều kiện cho trước.
      - DELETE ghi lại mỗi hành động xóa trong log, cho phép hoàn tác bằng cơ chế Rollback.
      - DELETE có thể sử dụng điều kiện WHERE để chỉ xóa các hàng thỏa mãn điều kiện cụ thể.
      - Khi sử dụng DELETE, các trigger có thể được kích hoạt nếu được định nghĩa cho bảng.

   Ví dụ DELETE:

   ```sql
   DELETE FROM table_name WHERE condition;
   ```

   Tóm lại:

   - TRUNCATE dùng để xóa toàn bộ dữ liệu của bảng một cách nhanh chóng, không hỗ trợ điều kiện WHERE và không thể hoàn tác.
   - DELETE dùng để xóa các hàng dữ liệu dựa trên điều kiện cho trước, hỗ trợ WHERE và có thể hoàn tác nếu được sử dụng cùng với Rollback.

4. `Phân biệt JOIN và UNION trong sql ?`

   Join và Union là hai câu lệnh khác nhau trong SQL được sử dụng để kết hợp dữ liệu từ nhiều bảng hoặc truy vấn khác nhau. Dưới đây là sự phân biệt giữa chúng:

   1. JOIN:

      - JOIN là một câu lệnh DML (Data Manipulation Language).
      - JOIN được sử dụng để kết hợp các hàng từ nhiều bảng dựa trên một điều kiện liên kết giữa các bảng.
      - JOIN có thể được sử dụng để lấy thông tin từ các bảng có liên quan với nhau thông qua các khóa ngoại và khóa chính.
      - Các loại JOIN phổ biến bao gồm INNER JOIN (kết hợp các hàng có giá trị liên kết trong cả hai bảng), LEFT JOIN (kết hợp tất cả các hàng từ bảng bên trái và các hàng liên kết từ bảng bên phải), RIGHT JOIN (kết hợp tất cả các hàng từ bảng bên phải và các hàng liên kết từ bảng bên trái) và FULL JOIN (kết hợp tất cả các hàng từ cả hai bảng).
      - Cú pháp JOIN thường bao gồm: `SELECT * FROM table1 JOIN table2 ON table1.column = table2.column;`

   2. UNION:
      - UNION là một câu lệnh DML (Data Manipulation Language).
      - UNION được sử dụng để kết hợp các kết quả của hai hoặc nhiều truy vấn SELECT có cấu trúc giống nhau và trả về kết quả duy nhất.
      - Các truy vấn được kết hợp bằng UNION phải có cùng số lượng cột và kiểu dữ liệu tương ứng.
      - UNION loại bỏ các bản sao dữ liệu và chỉ trả về kết quả duy nhất.
      - Cú pháp UNION thường bao gồm: `SELECT column1, column2 FROM table1 UNION SELECT column1, column2 FROM table2;`

   Tóm lại:

   - JOIN được sử dụng để kết hợp các hàng từ nhiều bảng dựa trên điều kiện liên kết.
   - UNION được sử dụng để kết hợp các kết quả của các truy vấn SELECT có cấu trúc giống nhau và trả về kết quả duy nhất.

5. `Phân biệt inner join, outer join, full outer join, left join, right join tron sql`

   Các loại JOIN trong SQL, bao gồm INNER JOIN, OUTER JOIN (bao gồm LEFT JOIN và RIGHT JOIN), và FULL OUTER JOIN, cho phép kết hợp dữ liệu từ nhiều bảng dựa trên điều kiện liên kết giữa chúng. Dưới đây là sự khác biệt giữa các loại JOIN:

   1. INNER JOIN:

      - INNER JOIN (kết hợp nội) trả về các hàng chỉ khi có sự khớp giữa hai bảng dựa trên điều kiện liên kết.
      - Các hàng không có sự khớp trong cả hai bảng sẽ không được bao gồm trong kết quả.
      - Cú pháp INNER JOIN:
        ```sql
        SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;
        ```

   2. OUTER JOIN:
      - OUTER JOIN (kết hợp ngoại) là một nhóm chung cho các loại JOIN bao gồm LEFT JOIN và RIGHT JOIN.
      - OUTER JOIN trả về các hàng từ một bảng (LEFT JOIN hoặc RIGHT JOIN) và các hàng liên kết từ bảng kia. Nếu không có sự khớp, các giá trị NULL được điền vào cho các cột từ bảng không có sự khớp.
   3. LEFT JOIN (kết hợp trái):

      - LEFT JOIN trả về tất cả các hàng từ bảng bên trái và các hàng liên kết từ bảng bên phải.
      - Nếu không có sự khớp từ bảng bên phải, các giá trị NULL được điền vào cho các cột từ bảng bên phải.
      - Cú pháp LEFT JOIN:
        ```sql
        SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;
        ```

   4. RIGHT JOIN (kết hợp phải):

      - RIGHT JOIN trả về tất cả các hàng từ bảng bên phải và các hàng liên kết từ bảng bên trái.
      - Nếu không có sự khớp từ bảng bên trái, các giá trị NULL được điền vào cho các cột từ bảng bên trái.
      - Cú pháp RIGHT JOIN:
        ```sql
        SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;
        ```

   5. FULL OUTER JOIN (kết hợp đầy đủ):
      - FULL OUTER JOIN trả về tất cả các hàng từ cả hai bảng, bao gồm cả các hàng không có sự khớp.
      - Nếu không có sự khớp từ bảng nào đó, các giá trị NULL được điền vào cho các cột từ bảng đó.
      - Cú pháp FULL OUTER JOIN:
        ```sql
        SELECT * FROM table1 FULL OUTER JOIN table2 ON table1.column = table2.column;
        ```

   Tóm lại:

   - INNER JOIN trả về các hàng chỉ khi có sự khớp trong cả hai bảng.
   - OUTER JOIN trả về các hàng từ một bảng và các hàng liên kết từ bảng kia, bao gồm LEFT JOIN và RIGHT JOIN.
   - LEFT JOIN trả về tất cả các hàng từ bảng bên trái và các hàng liên kết từ bảng bên phải.
   - RIGHT JOIN trả về tất cả các hàng từ bảng bên phải và các hàng liên kết từ bảng bên trái.
   - FULL OUTER JOIN trả về tất cả các hàng từ cả hai bảng, bao gồm cả các hàng không có sự khớp.

6. `Phân biệt WHERE clause và HAVING clause ?`

   Sự khác biệt chính giữa WHERE clause và HAVING clause trong SQL là cách chúng được sử dụng để lọc dữ liệu trong câu truy vấn:

   1. WHERE clause:
      - WHERE clause được sử dụng trong câu truy vấn SELECT, UPDATE hoặc DELETE để lọc các hàng dữ liệu dựa trên điều kiện cho trước.
      - WHERE clause áp dụng cho từng hàng dữ liệu riêng lẻ, và chỉ cho phép điều kiện dựa trên các cột trong bảng nguồn dữ liệu.
      - Nếu hàng không đáp ứng điều kiện được chỉ định trong WHERE clause, nó sẽ không được bao gồm trong kết quả truy vấn.

   Ví dụ sử dụng WHERE clause:

   ```sql
   SELECT * FROM employees WHERE department = 'HR';
   ```

   2. HAVING clause:
      - HAVING clause được sử dụng trong câu truy vấn SELECT với GROUP BY để lọc các kết quả của các nhóm (group) dữ liệu dựa trên điều kiện cho trước.
      - HAVING clause áp dụng cho mỗi nhóm dữ liệu, và cho phép điều kiện dựa trên các cột được tính toán từ kết quả của GROUP BY (chẳng hạn như SUM, COUNT, AVG, v.v.).
      - HAVING clause không áp dụng cho từng hàng dữ liệu riêng lẻ như WHERE clause, mà nó chỉ áp dụng cho các nhóm dữ liệu đã được nhóm lại bởi GROUP BY.

   Ví dụ sử dụng HAVING clause:

   ```sql
   SELECT department, COUNT(*) AS employee_count FROM employees GROUP BY department HAVING COUNT(*) > 10;
   ```

   Tóm lại:

   - WHERE clause dùng để lọc các hàng dữ liệu theo điều kiện dựa trên các cột trong bảng nguồn.
   - HAVING clause dùng để lọc các kết quả của các nhóm dữ liệu dựa trên điều kiện dựa trên các cột được tính toán từ kết quả của GROUP BY.

7. `Phân biệt Union và Union All`

   Union và Union All là hai câu lệnh trong SQL được sử dụng để kết hợp kết quả của các truy vấn SELECT khác nhau thành một kết quả duy nhất. Dưới đây là sự khác biệt giữa chúng:

   1. UNION:
      - UNION được sử dụng để kết hợp các kết quả của hai hoặc nhiều truy vấn SELECT có cấu trúc giống nhau và trả về kết quả duy nhất.
      - Các truy vấn kết hợp bằng UNION phải có cùng số lượng cột và kiểu dữ liệu tương ứng.
      - UNION loại bỏ các bản sao dữ liệu trong các kết quả kết hợp, chỉ trả về một bản ghi cho mỗi bản sao dữ liệu.
      - Các truy vấn trong UNION phải có cấu trúc giống nhau (cùng số lượng cột và kiểu dữ liệu tương ứng).

   Ví dụ UNION:

   ```sql
   SELECT column1, column2 FROM table1
   UNION
   SELECT column1, column2 FROM table2;
   ```

   2. UNION ALL:
      - UNION ALL cũng được sử dụng để kết hợp các kết quả của hai hoặc nhiều truy vấn SELECT có cấu trúc giống nhau.
      - Tuy nhiên, UNION ALL không loại bỏ các bản sao dữ liệu, nó trả về tất cả các bản ghi từ tất cả các truy vấn kết hợp mà không xử lý bản sao dữ liệu.
      - UNION ALL nhanh hơn UNION, vì không phải loại bỏ các bản sao dữ liệu trong quá trình kết hợp kết quả.

   Ví dụ UNION ALL:

   ```sql
   SELECT column1, column2 FROM table1
   UNION ALL
   SELECT column1, column2 FROM table2;
   ```

   Tóm lại:

   - UNION được sử dụng để kết hợp các kết quả của các truy vấn SELECT có cấu trúc giống nhau và loại bỏ các bản sao dữ liệu.
   - UNION ALL được sử dụng để kết hợp các kết quả của các truy vấn SELECT có cấu trúc giống nhau và giữ lại tất cả các bản sao dữ liệu.

8. `Phân biệt fetch và limit`

   Trong ngữ cảnh của PostgreSQL, "FETCH" và "LIMIT" là hai từ khóa có liên quan đến truy vấn dữ liệu. Chúng có chức năng tương tự nhau nhưng có một số điểm khác biệt quan trọng.

   1. **LIMIT:**
      LIMIT là một mệnh đề trong SQL (Structured Query Language) được sử dụng để giới hạn số lượng hàng trả về từ kết quả truy vấn. Điều này rất hữu ích khi bạn muốn truy vấn dữ liệu từ một bảng nhưng chỉ cần một số lượng hạn chế các hàng.

   Ví dụ:

   ```sql
   SELECT * FROM employees LIMIT 10;
   ```

   Lệnh trên sẽ trả về tối đa 10 hàng từ bảng "employees".

   2. **FETCH:**
      FETCH cũng liên quan đến giới hạn số lượng hàng trả về từ một kết quả truy vấn, tuy nhiên, FETCH thường được sử dụng khi bạn muốn điều khiển việc lấy hàng dựa trên số lượng và vị trí. Nó được thường được sử dụng trong kết hợp với lệnh ORDER BY để xác định thứ tự của các hàng được trả về.

   Ví dụ:

   ```sql
   SELECT * FROM employees ORDER BY last_name FETCH FIRST 10 ROWS ONLY;
   ```

   Lệnh trên sẽ trả về 10 hàng đầu tiên từ bảng "employees" sau khi đã sắp xếp chúng theo trường "last_name".

   Tóm lại, cả LIMIT và FETCH đều liên quan đến việc giới hạn số lượng hàng trả về từ một kết quả truy vấn, nhưng FETCH thường được sử dụng để điều khiển việc lấy hàng dựa trên vị trí và thứ tự. Trong khi LIMIT thường được sử dụng để đơn giản hóa việc trả về một số lượng hạn chế các hàng từ kết quả truy vấn.

## NOSQL

NoSQL (Not Only SQL) là một thuật ngữ dùng để chỉ các hệ thống quản lý cơ sở dữ liệu không phụ thuộc vào mô hình quan hệ (relational model) như các hệ thống SQL truyền thống. NoSQL là một loại cơ sở dữ liệu phi quan hệ (non-relational database) được thiết kế để đáp ứng các yêu cầu đặc biệt như khả năng mở rộng, xử lý dữ liệu phi cấu trúc, hiệu suất cao và độ tin cậy.

Có một số trường hợp khi nên sử dụng NoSQL:

1. Dữ liệu phi cấu trúc: Khi dữ liệu của bạn có cấu trúc phức tạp hoặc không đồng nhất, NoSQL cho phép lưu trữ dữ liệu phi cấu trúc một cách linh hoạt mà không yêu cầu một mô hình quan hệ cố định.

2. Khả năng mở rộng: Khi bạn cần mở rộng hệ thống cơ sở dữ liệu một cách dễ dàng và linh hoạt, NoSQL cung cấp khả năng mở rộng ngang (horizontal scalability) bằng cách phân tán dữ liệu trên nhiều máy chủ.

3. Tốc độ và hiệu suất: Khi ứng dụng của bạn đòi hỏi xử lý dữ liệu với tốc độ cao và hiệu suất tối ưu, NoSQL có thể cung cấp khả năng xử lý song song và truy vấn nhanh hơn so với các hệ thống SQL truyền thống.

4. Dữ liệu có quy mô lớn: Khi bạn có một lượng dữ liệu lớn và cần lưu trữ và truy xuất nhanh chóng, NoSQL có thể hỗ trợ việc xử lý các tải công việc lớn và có khả năng mở rộng theo quy mô.

5. Kịch bản sử dụng đa dạng: Khi ứng dụng của bạn có nhiều kịch bản sử dụng khác nhau và yêu cầu linh hoạt trong việc lưu trữ và truy xuất dữ liệu, NoSQL có thể phù hợp với các mô hình dữ liệu khác nhau như tài liệu (document), cột (column), key-value, đồ thời gian (time-series), v.v.

Tuy nhiên, cần lưu ý rằng việc chọn sử dụng NoSQL hay SQL phụ thuộc vào yêu cầu cụ thể của ứng dụng, cấu trúc dữ liệu, quy mô và tính chất

của dữ liệu. Một số ứng dụng có thể sử dụng cả hai loại cơ sở dữ liệu để tận dụng lợi ích của cả hai hệ thống.

# REDIS

Redis là một hệ thống cơ sở dữ liệu in-memory (dữ liệu lưu trữ trong bộ nhớ RAM) mã nguồn mở. Tên gốc của Redis là "Remote Dictionary Server" (Redis) vì nó được thiết kế để lưu trữ và truy xuất dữ liệu từ một cấu trúc dữ liệu key-value (từ điển) được lưu trữ trên một máy chủ từ xa.

Redis hỗ trợ nhiều kiểu dữ liệu, bao gồm chuỗi (strings), danh sách (lists), bảng băm (hashes), tập hợp (sets) và dãy có thứ tự (sorted sets). Ngoài ra, Redis còn cung cấp các chức năng mạnh mẽ như đăng ký thông báo (pub/sub), xác thực, khóa và hạn chế truy cập dữ liệu.

Redis thường được sử dụng làm một cơ sở dữ liệu tạm thời hoặc bộ nhớ đệm (cache) cho ứng dụng web và hệ thống phân tán, nhờ khả năng truy xuất dữ liệu cực kỳ nhanh từ bộ nhớ RAM. Nó có hiệu suất cao và hỗ trợ khả năng mở rộng đơn giản bằng cách sử dụng nhiều máy chủ Redis thành một cụm.

Redis cũng có khả năng bảo đảm tính toàn vẹn dữ liệu và khôi phục sau sự cố thông qua việc sao lưu dữ liệu trên đĩa và cung cấp cơ chế replikasi để sao chép dữ liệu sang các máy chủ khác. Điều này đảm bảo rằng dữ liệu không bị mất khi xảy ra sự cố và hệ thống vẫn có thể hoạt động liên tục.

Tóm lại, Redis là một hệ thống cơ sở dữ liệu in-memory mạnh mẽ và linh hoạt, thường được sử dụng để lưu trữ và truy xuất dữ liệu tạm thời một cách nhanh chóng và tin cậy.

# GRAPHQL

1. `GRAPHQL là gì ?`

   GraphQL là một ngôn ngữ truy vấn dữ liệu và một lớp trung gian để truy cập dữ liệu cho ứng dụng web và di động. Nó đã được phát triển bởi Facebook và được công bố công khai vào năm 2015. GraphQL giúp cho việc truy vấn và cập nhật dữ liệu trở nên dễ dàng và hiệu quả hơn so với các giao thức truy vấn truyền thống như REST.

   Một số khái niệm cơ bản trong GraphQL:

   1. **Schema (Kiểu dữ liệu)**: Schema là phần quan trọng nhất của GraphQL. Nó xác định cách dữ liệu sẽ được truy vấn và cập nhật. Mỗi schema bao gồm các kiểu dữ liệu, các trường có thể truy vấn và các mối quan hệ giữa chúng.

   2. **Query (Truy vấn)**: Truy vấn là một phương thức để đọc dữ liệu từ GraphQL server. Truy vấn được viết bằng ngôn ngữ GraphQL và có thể chỉ định chính xác các trường dữ liệu mà bạn muốn trả về từ server.

   3. **Mutation (Điều chỉnh)**: Mutation cũng là một phương thức để thay đổi dữ liệu trên server. Bạn có thể sử dụng mutation để thêm, sửa đổi hoặc xóa dữ liệu.

   4. **Subscription (Đăng ký)**: Subscription cho phép bạn theo dõi các thay đổi dữ liệu thời gian thực. Khi dữ liệu thay đổi, server sẽ thông báo cho client thông qua kết nối websocket hoặc một cơ chế theo dõi khác.

   5. **Resolver (Trình giải mã)**: Resolver là một hàm hoặc phương thức trên server mà xử lý truy vấn và trả về kết quả. Mỗi trường trong schema có một resolver tương ứng.

   6. **Fragment**: Fragment là một cách để tái sử dụng các phần truy vấn GraphQL. Bạn có thể định nghĩa một fragment và sau đó sử dụng nó trong nhiều truy vấn hoặc mutation khác nhau.

   GraphQL cho phép bạn yêu cầu chính xác dữ liệu bạn cần, giúp tối ưu hóa hiệu suất ứng dụng và tránh over-fetching (lấy nhiều dữ liệu hơn cần thiết) và under-fetching (lấy ít dữ liệu hơn cần thiết). Điều này làm cho GraphQL trở thành một lựa chọn hấp dẫn cho việc phát triển ứng dụng hiện đại.

# LY THUYET CO BAN

1. `Giái thích mô hình TCP/IP`

   Mô hình TCP/IP (Transmission Control Protocol/Internet Protocol) là một mô hình tham chiếu dùng để mô tả cách các thiết bị trong mạng giao tiếp với nhau trên Internet. Mô hình này được chia thành các lớp, mỗi lớp có một nhiệm vụ cụ thể trong quá trình truyền thông. Mô hình TCP/IP gồm 4 lớp chính:

   1. **Application Layer (Lớp ứng dụng):** Lớp này chứa các ứng dụng và dịch vụ mà người dùng tương tác trực tiếp. Điều này bao gồm các giao thức như HTTP, FTP, SMTP, POP3, Telnet, và nhiều giao thức khác. Nhiệm vụ chính của lớp này là quản lý giao tiếp giữa người dùng và các ứng dụng trên Internet.

   2. **Transport Layer (Lớp vận chuyển):** Lớp này xử lý việc truyền tải dữ liệu từ một điểm đến điểm khác. Giao thức TCP (Transmission Control Protocol) hoạt động ở lớp này để cung cấp truyền tải đáng tin cậy, đảm bảo dữ liệu không bị mất hoặc lỗi. Giao thức UDP (User Datagram Protocol) cũng là một phần của lớp này, nhưng nó không đảm bảo tính tin cậy như TCP.

   3. **Internet Layer (Lớp Internet):** Lớp này quản lý việc định tuyến (routing) dữ liệu qua các mạng và định nghĩa địa chỉ IP để xác định các thiết bị trong mạng. Giao thức IP (Internet Protocol) là trung tâm của lớp này, và nó quản lý việc gửi và nhận các gói dữ liệu giữa các thiết bị trong mạng.

   4. **Link Layer (Lớp liên kết):** Lớp này quản lý giao tiếp trực tiếp với phần vật lý của mạng. Nó xác định cách dữ liệu được đóng gói và truyền qua phương tiện truyền thông như Ethernet, Wi-Fi, hay các phương tiện khác. Giao thức ARP (Address Resolution Protocol) cũng hoạt động ở lớp này để ánh xạ địa chỉ IP thành địa chỉ vật lý (MAC address).

   Mỗi lớp trong mô hình TCP/IP có nhiệm vụ cụ thể và tương tác với các lớp khác để cung cấp quá trình truyền thông toàn diện. Tổng cộng, mô hình TCP/IP giúp các thiết bị trong mạng Internet có thể giao tiếp và truyền tải dữ liệu một cách hiệu quả.

2. `Phân biệt các loại vùng nhớ và cho ví dụ bằng typescript`

   Dưới đây là phân biệt các loại vùng nhớ lập trình và ví dụ sử dụng TypeScript để minh họa:

   1. **Stack Memory (Bộ nhớ ngăn xếp):** Sử dụng để lưu trữ các biến cục bộ, tham số hàm và giá trị trả về của hàm. Thường có vòng đời ngắn hơn, do bộ nhớ được tự động giải phóng khi một hàm kết thúc.

   ```typescript
   function exampleStackMemory(x: number): number {
     const localVar = x + 10;
     return localVar;
   }

   const result = exampleStackMemory(5);
   console.log(result); // Kết quả là 15
   // localVar đã bị giải phóng sau khi hàm kết thúc
   ```

   2. **Heap Memory (Bộ nhớ heap):** Sử dụng để cấp phát và giải phóng bộ nhớ động, thường cần người lập trình quản lý. Dữ liệu trong heap có thể được truy cập từ nhiều phạm vi khác nhau.

   ```typescript
   class Person {
     constructor(public name: string) {}
   }

   const person1 = new Person("Alice"); // Đối tượng person1 nằm trong heap
   const person2 = person1; // person2 tham chiếu đến cùng một đối tượng trong heap
   person1.name = "Bob";

   console.log(person2.name); // Kết quả là "Bob"
   ```

   3. **Data Memory (Bộ nhớ dữ liệu):** Sử dụng để lưu trữ dữ liệu tĩnh, biến toàn cục và hằng số. Dữ liệu trong bộ nhớ này không thay đổi trong quá trình chạy chương trình.

   ```typescript
   const globalVariable = "I am a global variable"; // Lưu trong bộ nhớ dữ liệu

   function accessGlobalVariable(): void {
     console.log(globalVariable);
   }

   accessGlobalVariable(); // Kết quả là "I am a global variable"
   ```

   4. **Code Memory (Bộ nhớ mã nguồn):** Chứa mã máy của chương trình được lưu trữ trong bộ nhớ.

   ```typescript
   function add(a: number, b: number): number {
     return a + b;
   }

   console.log(add(3, 5)); // Kết quả là 8
   // Mã máy của hàm add được lưu trong bộ nhớ mã nguồn
   ```

   5. **Memory-Mapped I/O (I/O được ánh xạ vào bộ nhớ):** Không phải loại vùng nhớ trong lập trình thông thường, nhưng ví dụ có thể là sử dụng các thư viện cho việc tương tác với các thiết bị ngoại vi như cổng COM hoặc GPIO thông qua cách ánh xạ địa chỉ I/O vào bộ nhớ.

   ```typescript
   // Ví dụ về cách sử dụng thư viện để tương tác với GPIO qua ánh xạ vào bộ nhớ
   // (Đây chỉ là một giả định và không hoạt động trong thực tế)
   const GPIO_ADDRESS = 0x1234; // Địa chỉ I/O được ánh xạ vào bộ nhớ

   function writeToGPIO(value: number): void {
     // Ghi giá trị vào địa chỉ I/O ánh xạ vào bộ nhớ
     memoryWrite(GPIO_ADDRESS, value);
   }

   writeToGPIO(1); // Ghi giá trị 1 vào địa chỉ GPIO
   ```

   Vui lòng lưu ý rằng các ví dụ trên là giả định và dựa trên nguyên tắc. Trong thực tế, các cách thức giao tiếp và quản lý bộ nhớ có thể phức tạp hơn và phụ thuộc vào ngôn ngữ lập trình và hệ điều hành được sử dụng.

3. `Phân biệt biến tham chiếu và tham trị trong lập trình`

   Trong lập trình, biến tham chiếu và tham trị đều liên quan đến cách tham số hoặc giá trị được truyền vào hàm hoặc phương thức. Sự khác biệt giữa chúng nằm ở cách chúng xử lý dữ liệu.

   **Biến tham trị (Pass by Value):**

   - Khi bạn truyền một biến tham trị vào một hàm hoặc phương thức, một bản sao của giá trị của biến được tạo ra.
   - Bất kỳ thay đổi nào đối với tham số trong hàm không ảnh hưởng đến giá trị ban đầu của biến bên ngoài hàm.
   - Tham trị thường được sử dụng cho các kiểu dữ liệu nguyên thủy (primitive data types) như số nguyên, số thực, ký tự, boolean, v.v.

   **Biến tham chiếu (Pass by Reference):**

   - Khi bạn truyền một biến tham chiếu vào một hàm hoặc phương thức, thực tế bạn đang truyền tham chiếu đến vùng nhớ của biến.
   - Bất kỳ thay đổi nào đối với tham số trong hàm cũng ảnh hưởng trực tiếp đến biến ban đầu ngoài hàm.
   - Tham chiếu thường được sử dụng cho các kiểu dữ liệu không nguyên thủy (reference data types) như mảng, danh sách liên kết, đối tượng.

   Dưới đây là ví dụ để minh họa:

   ```java
   // Pass by Value
   public void modifyValue(int x) {
   		x = x + 10;
   		System.out.println("Inside function: " + x);
   }

   public static void main(String[] args) {
   		int value = 5;
   		modifyValue(value);
   		System.out.println("Outside function: " + value);
   }

   // Output:
   // Inside function: 15
   // Outside function: 5

   // Pass by Reference
   public void modifyArray(int[] arr) {
   		arr[0] = arr[0] + 10;
   		System.out.println("Inside function: " + arr[0]);
   }

   public static void main(String[] args) {
   		int[] array = {5};
   		modifyArray(array);
   		System.out.println("Outside function: " + array[0]);
   }

   // Output:
   // Inside function: 15
   // Outside function: 15
   ```

   Như ví dụ trên, biến `value` trong hàm `modifyValue` không ảnh hưởng đến biến `value` trong `main`, trong khi mảng `array` trong hàm `modifyArray` ảnh hưởng đến mảng `array` trong `main`.

4. `Con trỏ là gì ? Cho ví dụ về con trỏ`

   Trong lập trình, con trỏ là một biến đặc biệt mà chứa địa chỉ của một vùng nhớ trong bộ nhớ máy tính. Con trỏ cho phép bạn truy cập và thay đổi dữ liệu tại vùng nhớ đó thông qua địa chỉ. Con trỏ thường được sử dụng trong ngôn ngữ lập trình như C và C++.

   Dưới đây là một ví dụ về việc sử dụng con trỏ trong ngôn ngữ C++:

   ```cpp
   #include <iostream>

   int main() {
   		int num = 42;
   		int* ptr; // Khai báo một con trỏ kiểu int

   		ptr = &num; // Gán địa chỉ của biến num cho con trỏ

   		std::cout << "Value of num: " << num << std::endl;
   		std::cout << "Address of num: " << &num << std::endl;
   		std::cout << "Value pointed by ptr: " << *ptr << std::endl; // Sử dụng * để truy cập giá trị theo địa chỉ
   		std::cout << "Address stored in ptr: " << ptr << std::endl;

   		*ptr = 99; // Thay đổi giá trị tại địa chỉ mà con trỏ trỏ đến

   		std::cout << "Value of num after modification: " << num << std::endl;

   		return 0;
   }
   ```

   Kết quả:

   ```
   Value of num: 42
   Address of num: 0x7ffdcb5b6d3c
   Value pointed by ptr: 42
   Address stored in ptr: 0x7ffdcb5b6d3c
   Value of num after modification: 99
   ```

   Trong ví dụ trên, biến `num` chứa giá trị 42. Con trỏ `ptr` trỏ tới địa chỉ của `num`, và khi chúng ta sử dụng `*ptr`, nó truy cập và trả về giá trị tại địa chỉ mà con trỏ trỏ đến.

   Vui lòng lưu ý rằng việc sử dụng con trỏ đòi hỏi sự cẩn trọng và quản lý bộ nhớ thủ công để tránh rò rỉ bộ nhớ hoặc xung đột bộ nhớ.

   # DOCKER

   1. `Docker là gì ?`

   Docker là một nền tảng ảo hóa cấp phối (containerization platform), cho phép bạn đóng gói ứng dụng và tất cả các phụ thuộc của nó - bao gồm mã nguồn, thư viện, biến môi trường và tệp cấu hình - vào một gói duy nhất gọi là container. Container là một hình thức tiêu chuẩn hóa cho việc đóng gói phần mềm, giúp đảm bảo rằng ứng dụng của bạn có thể chạy một cách đáng tin cậy và nhất quán trên môi trường khác nhau.

   Một số điểm chính về Docker bao gồm:

   1. **Portability (Khả năng di động):** Containers cho phép bạn đóng gói tất cả các yếu tố cần thiết để chạy ứng dụng vào một gói duy nhất. Điều này giúp đảm bảo rằng ứng dụng của bạn sẽ hoạt động giống nhau trên mọi nền tảng mà Docker hỗ trợ.

   2. **Isolation (Cách ly):** Mỗi container hoạt động như một môi trường độc lập, cách ly khỏi các container khác và hệ thống host. Điều này giúp ngăn chặn các xung đột và ảnh hưởng tới nhau.

   3. **Tích hợp và triển khai dễ dàng:** Các container có thể được đóng gói và chia sẻ dễ dàng thông qua các hệ thống quản lý phiên bản như Docker Hub. Điều này giúp tăng tốc quá trình triển khai và đảm bảo sự nhất quán giữa môi trường phát triển và môi trường sản xuất.

   4. **Hiệu suất:** So với máy ảo truyền thống, container thường có hiệu suất tốt hơn, vì chúng chia sẻ hạ tầng hệ thống của máy chủ host và sử dụng tài nguyên hệ thống hiệu quả hơn.

   5. **Quản lý tài nguyên:** Docker cung cấp các công cụ để quản lý tài nguyên của các container, cho phép bạn xác định và kiểm soát việc sử dụng CPU, bộ nhớ và các tài nguyên khác.

   Docker đã đạt được sự phổ biến rộng rãi trong việc triển khai ứng dụng và dịch vụ, từ các dự án nhỏ đến các hệ thống quy mô lớn, do tính đơn giản, khả năng di động và khả năng cách ly môi trường của nó.

   2. `Setup docker cho một ứng dụng nodejs express postgres redis cơ bản`

      Dưới đây là hướng dẫn cơ bản để bạn thiết lập một ứng dụng Node.js Express với PostgreSQL và Redis sử dụng Docker.

      **Bước 1: Tạo dự án Node.js Express:**

      1. Tạo thư mục cho dự án của bạn và di chuyển vào thư mục đó.
      2. Khởi tạo dự án Node.js bằng cách chạy lệnh: `npm init -y`.
      3. Cài đặt các module cần thiết bằng lệnh: `npm install express pg redis`.

      **Bước 2: Tạo file `Dockerfile` cho ứng dụng:**
      Tạo một file có tên `Dockerfile` trong thư mục gốc của dự án với nội dung sau:

      ```Dockerfile
      # Sử dụng image base của Node.js
      FROM node:14

      # Thiết lập thư mục làm việc trong container
      WORKDIR /app

      # Sao chép package.json và package-lock.json vào thư mục /app
      COPY package*.json ./

      # Cài đặt các dependencies
      RUN npm install

      # Sao chép tất cả mã nguồn ứng dụng vào thư mục /app
      COPY . .

      # Expose port của ứng dụng
      EXPOSE 3000

      # Khởi chạy ứng dụng khi container được chạy
      CMD ["node", "app.js"]
      ```

      **Bước 3: Tạo file `docker-compose.yml`:**
      Tạo một file có tên `docker-compose.yml` trong thư mục gốc của dự án với nội dung sau:

      ```yaml
      version: "3"
      services:
      	app:
      		build:
      			context: .
      			dockerfile: Dockerfile
      		ports:
      			- "3000:3000"
      		links:
      			- postgres
      			- redis

      	postgres:
      		image: postgres
      		environment:
      			POSTGRES_DB: mydb
      			POSTGRES_USER: myuser
      			POSTGRES_PASSWORD: mypassword

      	redis:
      		image: redis
      ```

      **Bước 4: Khởi chạy ứng dụng bằng Docker Compose:**
      Mở terminal và di chuyển vào thư mục của dự án, sau đó chạy lệnh sau để khởi chạy các dịch vụ:

      ```
      docker-compose up
      ```

      Docker Compose sẽ tải về và thiết lập các images cần thiết, sau đó khởi động các containers cho ứng dụng Node.js, PostgreSQL và Redis.

      Ứng dụng Node.js sẽ chạy trên `http://localhost:3000`, PostgreSQL sẽ sẵn sàng để kết nối trên `localhost` cổng `5432`, và Redis sẽ sẵn sàng trên `localhost` cổng `6379`.

      Lưu ý rằng đây chỉ là một hướng dẫn cơ bản để bắt đầu với Docker và Docker Compose. Trong thực tế, bạn có thể cần cấu hình thêm cho các dịch vụ như biến môi trường, mạng, quản lý dữ liệu lưu trữ, và nhiều thứ khác.

	3.`Image trong docker là gì ?`

	Trong Docker, "image" là một gói đóng gói chứa mọi thứ cần thiết để chạy một ứng dụng, bao gồm mã nguồn, các thư viện, biến môi trường, tệp cấu hình và các tài nguyên khác cần thiết. Images được sử dụng để tạo các container, là các phiên bản thực tế của ứng dụng chạy trong môi trường cô lập.

	Một image Docker có thể được coi như một bản "template" hoặc "nguyên mẫu" cho một container. Bạn có thể tạo nhiều container từ một image cụ thể, và mỗi container sẽ chia sẻ cùng một cấu trúc cơ bản từ image nhưng có thể có các biến môi trường, dữ liệu, và trạng thái riêng biệt.

	Dưới đây là một số khái niệm quan trọng liên quan đến image trong Docker:

	- **Docker Hub:** Nơi lưu trữ và chia sẻ images. Docker Hub là một dịch vụ trực tuyến cho phép bạn tìm kiếm, chia sẻ và lấy images từ cộng đồng hoặc từ dịch vụ lưu trữ riêng.

	- **Dockerfile:** Một tệp văn bản chứa các chỉ thị để xây dựng một image Docker. Dockerfile mô tả cách thức sắp xếp và cấu hình ứng dụng và môi trường trong image.

	- **Layer:** Mỗi thay đổi được thực hiện trong Dockerfile hoặc trên image sẽ tạo ra một layer mới trong image. Các layer là các phần nhỏ có thể được chia sẻ giữa các image khác nhau, làm cho việc chia sẻ và quản lý images hiệu quả hơn.

	- **Base Image:** Đây là image cơ bản mà bạn dựa trên để xây dựng image của mình. Base image có thể là các hệ điều hành như Ubuntu, CentOS, hoặc image đã được tạo sẵn từ Docker Hub.

	- **Registry:** Nơi lưu trữ các images. Docker Hub là một registry. Bạn cũng có thể tạo và quản lý các registry riêng nếu muốn.

	Để tạo một image Docker, bạn thường viết một Dockerfile định nghĩa cách cài đặt và cấu hình ứng dụng của bạn. Sau đó, bạn có thể sử dụng lệnh `docker build` để xây dựng image từ Dockerfile, và lệnh `docker run` để chạy container từ image đã tạo.

	4. `Container trong docker là gì`

		Trong Docker, "container" là một phiên bản thực tế của một image Docker. Nó là một môi trường cô lập chứa tất cả những gì cần thiết để chạy một ứng dụng cụ thể, bao gồm mã nguồn, thư viện, biến môi trường, tệp cấu hình và các tài nguyên khác.

		Các điểm quan trọng về container trong Docker:

		1. **Cô lập:** Mỗi container được cô lập với các container khác và môi trường chủ nhân (host). Điều này đảm bảo rằng các ứng dụng trong các container không ảnh hưởng lẫn nhau và không ảnh hưởng tới hệ thống host.

		2. **Portability (Khả chuyển):** Containers là di động và khả chuyển. Một ứng dụng container có thể chạy trên bất kỳ máy tính hoặc môi trường nào mà Docker có sẵn mà không cần thay đổi.

		3. **Lightweight (Nhẹ):** Containers sử dụng chia sẻ kernel với hệ điều hành host, làm cho chúng nhẹ hơn và tiết kiệm tài nguyên hơn so với máy ảo truyền thống.

		4. **Tích hợp và triển khai dễ dàng:** Containers có thể được đóng gói, triển khai và quản lý dễ dàng. Docker cung cấp các công cụ và lệnh để tạo, lưu trữ, và chia sẻ images, tạo và chạy containers, cũng như quản lý vòng đời của chúng.

		5. **Scalability (Khả năng mở rộng):** Containers cho phép bạn mở rộng dễ dàng các ứng dụng của mình bằng cách tạo nhiều bản sao của một container cùng một image.

		6. **Snapshot (Ảnh chụp):** Bạn có thể tạo snapshot của một container tại một thời điểm cụ thể để làm việc và kiểm tra. Snapshot này có thể được chia sẻ, sao lưu và khôi phục.

		Để chạy một container từ một image Docker, bạn sử dụng lệnh `docker run` và chỉ định image cần chạy. Ví dụ:

		```bash
		docker run -d -p 8080:80 nginx
		```

		Trong ví dụ này, lệnh trên sẽ chạy một container từ image "nginx" và ánh xạ cổng 80 của container với cổng 8080 của máy host. Container này sẽ chạy web server Nginx.

	5. `Dockerfile trong nodejs là gì?`

		Trong Docker, `Dockerfile` là một tệp văn bản chứa các chỉ thị và hướng dẫn để xây dựng một image Docker. Dockerfile mô tả cách thức cài đặt và cấu hình ứng dụng cùng với môi trường mà ứng dụng sẽ chạy trong image.

	Một Dockerfile đơn giản thường bao gồm các bước sau:

	1. **Chọn một base image:** Đầu tiên, bạn phải chọn một base image từ Docker Hub hoặc một registry khác. Base image chứa hệ điều hành cơ bản và các công cụ cần thiết để chạy ứng dụng của bạn.

	2. **Cài đặt các phụ thuộc:** Sử dụng các chỉ thị như `RUN` để cài đặt các phần mềm, thư viện, và các phụ thuộc cần thiết cho ứng dụng của bạn.

	3. **Cấu hình môi trường:** Sử dụng chỉ thị `ENV` để định nghĩa các biến môi trường mà ứng dụng của bạn cần để hoạt động.

	4. **Mở cổng:** Sử dụng chỉ thị `EXPOSE` để định nghĩa các cổng mà ứng dụng của bạn sẽ lắng nghe trên container.

	5. **Khởi chạy ứng dụng:** Sử dụng chỉ thị `CMD` hoặc `ENTRYPOINT` để chỉ định lệnh mà container sẽ thực thi khi được khởi chạy.

	Ví dụ về một Dockerfile đơn giản để tạo một image cho một ứng dụng Node.js:

	```Dockerfile
	# Sử dụng Node.js làm base image
	FROM node:14

	# Thiết lập thư mục làm việc trong container
	WORKDIR /app

	# Sao chép file package.json và package-lock.json vào thư mục làm việc
	COPY package*.json ./

	# Cài đặt các phụ thuộc của ứng dụng
	RUN npm install

	# Sao chép mã nguồn ứng dụng vào thư mục làm việc
	COPY . .

	# Mở cổng 3000
	EXPOSE 3000

	# Khởi chạy ứng dụng khi container được chạy
	CMD ["node", "app.js"]
	```

	Sau khi bạn đã tạo Dockerfile, bạn có thể sử dụng lệnh `docker build` để xây dựng image từ Dockerfile:

	```bash
	docker build -t my-node-app .
	```

	Sau khi xây dựng thành công, bạn có thể chạy container từ image bằng cách sử dụng lệnh `docker run`:

	```bash
	docker run -p 3000:3000 my-node-app
	```

	Điều này sẽ tạo ra một container chạy ứng dụng Node.js và ánh xạ cổng 3000 của container với cổng 3000 của máy host.

# REGEX

1. `Kiến thức cơ bản về regex`

   Regex (Regular Expressions) là một công cụ mạnh trong lập trình để tìm kiếm và xử lý các chuỗi văn bản dựa trên các mẫu cụ thể. Regex cho phép bạn thực hiện các tác vụ như kiểm tra sự tồn tại của một mẫu, tìm kiếm các chuỗi khớp với một mẫu, thay thế các khớp bằng một chuỗi khác, và nhiều tác vụ khác.

   Dưới đây là một số khái niệm cơ bản về regex:

   1. **Ký tự đặc biệt:**

      - `.`: Khớp bất kỳ ký tự nào ngoại trừ newline.
      - `^`: Bắt đầu chuỗi hoặc dòng (nếu được sử dụng với cờ `m`).
      - `$`: Kết thúc chuỗi hoặc dòng (nếu được sử dụng với cờ `m`).

   2. **Ký tự đại diện:**

      - `[abc]`: Khớp bất kỳ ký tự 'a', 'b', hoặc 'c'.
      - `[a-z]`: Khớp bất kỳ ký tự từ 'a' đến 'z'.
      - `[A-Z]`: Khớp bất kỳ ký tự từ 'A' đến 'Z'.
      - `[0-9]`: Khớp bất kỳ chữ số nào.

   3. **Quantifiers (lượng từ):**

      - `*`: Khớp 0 hoặc nhiều lần.
      - `+`: Khớp 1 hoặc nhiều lần.
      - `?`: Khớp 0 hoặc 1 lần.
      - `{n}`: Khớp chính xác n lần.
      - `{n,}`: Khớp ít nhất n lần.
      - `{n,m}`: Khớp từ n đến m lần.

   4. **Ký tự đặc biệt trong mẫu:**

      - `\`: Dùng để escape các ký tự đặc biệt (ví dụ: `\\`, `\.`).
      - `|`: OR logic (ví dụ: `apple|banana` khớp "apple" hoặc "banana").

   5. **Nhóm và phân nhóm:**

      - `(abc)`: Tạo một nhóm các ký tự 'abc'.
      - `(a|b)`: Tạo một nhóm OR giữa 'a' và 'b'.

   6. **Anchors (gắn kết):**

      - `\b`: Word boundary (ranh giới từ).
      - `\B`: Not a word boundary (không phải ranh giới từ).
      - `^`: Bắt đầu chuỗi hoặc dòng.
      - `$`: Kết thúc chuỗi hoặc dòng.

   7. **Modifiers (cờ):**
      - `g`: Tìm kiếm toàn bộ chuỗi (global).
      - `i`: Không phân biệt chữ hoa chữ thường (case-insensitive).
      - `m`: Cho phép tìm kiếm trên nhiều dòng (multiline).

   Regex có thể khá phức tạp khi bạn học các khái niệm nâng cao hơn như lookaheads, lookbehinds, và các biểu thức chính quy phức tạp hơn. Việc thường xuyên thực hành và sử dụng các công cụ kiểm tra regex trực tuyến sẽ giúp bạn làm quen và nắm vững kiến thức về regex.

2. `Ví dụ về việc sử dụng regex`

   Regular expressions (regex) là một công cụ mạnh trong JavaScript (cũng như nhiều ngôn ngữ lập trình khác) cho việc tìm kiếm và xử lý các chuỗi văn bản dựa trên các mẫu cụ thể. Dưới đây là một số ví dụ về regex cơ bản trong JavaScript:

	3. **Kiểm tra một chuỗi có khớp với một mẫu nào đó:**

	```javascript
	const pattern = /hello/;
	const text = "Hello, world!";
	const isMatch = pattern.test(text);
	console.log(isMatch); // true
	```

	2. **Tìm kiếm tất cả các sự khớp trong một chuỗi:**

	```javascript
	const pattern = /a/g; // 'g' ở đây nghĩa là tìm kiếm toàn bộ chuỗi
	const text = "abcadeaf";
	const matches = text.match(pattern);
	console.log(matches); // ['a', 'a', 'a']
	```

	3. **Tìm kiếm một mẫu cụ thể và lấy thông tin về sự khớp:**

	```javascript
	const pattern = /(\d{2})-(\d{2})-(\d{4})/;
	const text = "Ngày sinh: 15-08-1990";
	const result = text.match(pattern);
	console.log(result); // ['15-08-1990', '15', '08', '1990']
	```

	4. **Thay thế các khớp trong chuỗi:**

	```javascript
	const pattern = /apple/g;
	const text = "An apple, an apple tree, and an apple pie.";
	const replacedText = text.replace(pattern, "banana");
	console.log(replacedText);
	// "An banana, an banana tree, and an banana pie."
	```

	5. **Tìm kiếm một mẫu và trả về chỉ mục đầu tiên của sự khớp:**

	```javascript
	const pattern = /world/;
	const text = "Hello, world!";
	const index = text.search(pattern);
	console.log(index); // 7
	```

	6. **Sử dụng ký tự đại diện và tập hợp ký tự:**

	```javascript
	const pattern = /[aeiou]/g;
	const text = "Hello, world!";
	const vowels = text.match(pattern);
	console.log(vowels); // ['e', 'o', 'o']
	```

	Đây chỉ là những ví dụ cơ bản. Regular expressions rất mạnh mẽ và có nhiều tính năng phức tạp khác nhau như quantifiers, anchors, groups, lookaheads, và nhiều khái niệm khác. Bạn có thể tìm hiểu thêm trong tài liệu chính thức của JavaScript hoặc các nguồn học khác về regex.
