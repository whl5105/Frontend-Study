# SSR(Server-side Rendering)

SSR은 서버에서 페이지를 렌더링하는 방식으로, Next.js와 PHP, ASP 등이 이에 속합니다.

## SSR 동작 방식

<p align="center">
<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblthJT%2FbtrD3SXvNIt%2F57pMtTxLInoP2Kecr5xHV0%2Fimg.png">
</p>

1. 클라이언트가 특정 페이지를 요청한다.

2. 서버에서는 해당 페이지에 필요한 데이터를 포함한 HTML 파일을 클라이언트에 전달한다.

3. 클라이언트에서는 해당 HTML 파일을 파싱하면서 필요한 정적 리소스(CSS, 이미지 등)와 자바스크립트 파일을 다운로드하며, 페이지를 렌더링한다. 이 때 사용자는 렌더링된 페이지를 볼 수는 있지만 아직 클릭 등의 인터렉션은 할 수 없다.

4. 클라이언트에서 다운로드한 자바스크립트 파일을 실행한다.

5. 페이지 인터렉션이 가능해진다.

## SSR의 특징

1. 최초 페이지 로딩 시간이 짧음  
    요청한 페이지에 필요한 리소스만 다운로드하여 페이지를 생성하므로 렌더링에 필요한 시간이 짧다.

   다만 빈 HTML 문서를 전달하는 CSR 방식과는 달리 SSR에서는 페이지를 생성하는 시간이 필요하므로 TTFB는 CSR 방식보다 오래 걸린다.

> TTFB(Time to First Byte)란?
>
> 클라이언트(브라우저)가 서버에서 보낸 첫 번째 바이트가 수신하는 데까지 걸리는 시간
> = HTTP 요청에 걸리는 시간 + 서버의 요청 처리 시간 + 서버에서 클라이언트까지의 응답 시간

2. 자바스크립트 실행이 완료될 때까지 인터렉션 불가
   SSR 방식은 사용자가 더 빨리 페이지를 조회할 수는 있지만 자바스크립트 실행이 완료될 때까지는 클릭 등 페이지 내에서의 상호 작용이 불가능하다.

> 만약 인터렉션 가능 시점 이전에 버튼 클릭 등의 작업이 발생했다면, 인터렉션 가능 시점까지 해당 동작의 수행은 보류된다.

3. 페이지 이동에 걸리는 시간이 CSR 방식보다 길다  
   페이지를 이동할 때마다 해당 페이지에 필요한 리소스를 다운로드하고 페이지를 다시 생성해야 하므로 CSR 방식에 비해 페이지 이동에 걸리는 시간은 더 길다.

4. 검색엔진 최적화(SEO)에 적합  
   서버에서 페이지를 생성하므로 검색엔진에서는 빈 HTML 문서가 아닌 완성된 HTML 문서를 수집할 수 있으므로 검색엔진 최적화에 용이하다.

# CSR(Client-side Rendering)

CSR는 클라이언트(브라우저)에서 페이지를 렌더링하는 방식으로, React와 Vue, Angular 등이 이에 속한다.

## CSR 동작 방식

<p align="center">
<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkJGNN%2FbtrD8NOfWcQ%2FX39awzv7UVQuKIZkPpmDYk%2Fimg.png">
</p>

1. 클라이언트가 특정 페이지를 요청한다.

2. 서버에서는 빈 HTML 문서를 클라이언트에 전달한다.

3. 클라이언트가 HTML 문서에 포함된 정적 리소스(CSS, 이미지 등), 번들 자바스크립트 파일을 다운로드한다.

4. 클라이언트에서 번들 자바스크립트 파일을 실행한다. 자바스크립트에 의해 페이지가 렌더링되며, 이 때 사용자는 렌더링된 페이지를 볼 수 있다. 아직 API에서 데이터를 받아오지 않았기 때문에 로딩(빈 화면) 혹은 임시 데이터가 표출된다.

5. 페이지 렌더링이 완료된 후, (useEffect 내의) API 요청 코드가 실행된다.

6. API에서 받아온 데이터로 state를 업데이트하고 페이지를 리렌더링한다.

7. 페이지 인터렉션이 가능해진다.

## CSR의 특징

1. 최초 페이지 로딩 시간이 SSR보다 오래 걸림  
   브라우저에 HTML 파일이 전송되기까지의 시간(TTFB)은 짧지만, 렌더링에 필요한 리소스와 번들 자바스크립트 파일을 다운로드 한 후 화면을 그리는 데 걸리는 시간이 길기 때문에 전체적인 렌더링 완료 시간은 오래 걸리게 된다.

> 특히 번들 자바스크립트 파일의 용량이 클 수록 다운로드에 많은 시간이 소요되므로 정적 리소스(이미지, 폰트 등) 및 용량이 적은 라이브러리 사용, 코드 스플리팅 등을 적용하여 번들 파일을 용량을 줄이는 것이 좋다.

2. 페이지 이동에 걸리는 시간은 짧음  
   페이지 렌더링에 필요한 정적 리소스와 번들 자바스크립트 파일은 최초 페이지 접근 시에만 다운로드하고, 이동할 페이지에 필요한 부분만 추가로 요청하므로 페이지 이동에 걸리는 시간은 짧다.

3. 데이터 응답을 받아올 때까지 빈 화면(혹은 로딩) 표출  
   CSR 방식은 번들 자바스크립트 실행이 완료된 후, API 응답을 받아오기 전까지는 빈 화면(혹은 별도로 설정한 로딩 화면)이 표출된다.

> API에서 데이터를 받아온 후 화면 리렌더링이 완료되면 즉시 화면에서 인터렉션이 가능하다.
>
> 화면은 보이지만 인터렉션이 되지 않는 경우보다는 아예 화면이 렌더링되지 않는 편이 사용자에게는 더 직관적일 수 있다.
